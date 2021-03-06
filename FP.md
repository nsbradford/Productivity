# Functional Programming is Easy, Practical, and Fun.

Many newcomers to Functional Programming (FP) are turned away by feelings that it is overly complicated and academic but not practical. This goal of this doc is to show that FP is easy, practical and fun by motivating a few simple problems and how they tie well to FP concepts. In particular, we'll cover:

* Data vs Functional extensibility
* ad-hoc polymorphism with typeclasses
* Independent computations with Applicatives
* Dependent computations with Monads (yes, we're going to explain Monads and it'll be super easy!)
* Folding and Reducing
* Inversions with Traverse
* Teasers: Purely functional State and DSLs
* Further reading and acknowledgements

Although we'll be using Scala in these examples, we'll mostly gloss over the implementation details because they're just there to make these abstractions a bit more concrete. Once you're able to name the FP solutions to solve these various types of problems, it's easy to just look up the docs for the specific thing you need referenced - you want to memorize the interface, not the implementation.

## OO vs. FP Design
### What is FP?
At the highest level: what does functional programming offer? **Referential transparency**, the idea that expressions can always be substituted for values (no side effects; "pure"), is a big part of it because the lack of mutable state means that you can more easily reason about and **compose** (think function composition) large programs. But the key second-order effect of this design choice is...

### Extending Data vs. Functionality
...Object-Oriented architectures tend to make Data extension easy, while Functional architectures tend to make Functionality extension easy. 

Consider the our example before (of `Animal` is a `Cat` or `Dog`). In an OO design, the key principle is that *objects encapsulate their behavior*, and the program can be modelled as *message passing between objects*. Everything related to `Dog`s, all functionality, all state, are going into the `Dog` class, which makes lots of intuitive sense.

```scala
abstract class Animal{
  def noise: String
}
class Dog extends Animal {
  override def noise: String = "Woof"
}
class Cat extends Animal {
  override def noise: String = "Meow"
}
```

By contrast, in FP you think of *functions operating on data*. The `Dog` class will be *very* light (perhaps modelled with an [algebraic data type](https://en.wikipedia.org/wiki/Algebraic_data_type), but we won't get into that), with the functionality decoupled, and polymorphism (different behavior for different types) achieve with [pattern matching](https://docs.scala-lang.org/tour/pattern-matching.html):

```scala
abstract class Animal
case class Dog() extends Animal
case class Cat() extends Animal

object AnimalFunctions {
  def noise(animal: Animal): String = Animal match {
    case Dog => "Woof"
    case Cat => "Meow"
  }
}
```

Now, back to adding data vs functionality. 

Imagine you want to add a new function `foo` to `Animal`. With FP it's simple, you just add `foo` with your other functions, no need to edit your data model *no matter how much functionality you add*. With OO, it's a bit annoying because you need to edit every node in the `Animal` inheritance tree. (The OO [visitor pattern](https://en.wikipedia.org/wiki/Visitor_pattern) is an attempt to solve this problem.)

Imagine you want to add a new `Animal`: a `Shark`. In the OO world, you just add a new `Shark` class, no need to edit any of the other classes. In the FP world, it's a bit annoying because you have to edit every function's pattern matching to include the new data type.

These aren't absolutes - multi-paradigm languages (such as Scala) allow you to blur the lines in your modelling decisions. But in summary, the FP modelling style will make it easy to have a lot of varied functionality around a stable set of data models, while the OO modelling style. In my experience, developers tend to change functions more often than the data model.

## FP Tools and Abstractions (intro)
The FP world has a rich ecosystem of tools and abstractions, many of which are not confined to Functional programs. Most examples will assume you've imported Cats:

```scala
import cats._
import cats.data._
import cats.implicits._
```

### Ad-hoc polymorphism with Typeclasses
You're probably familiar with [polymorphism](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)) through subtyping, which is fairly intuitive. For example, a class `Animal` can have subclasses `Cat` and `Dog`. If `Animal` has a function `noise()`, you know both `Cat` and `Dog` "inherit" the `noise()` method, but can have different implementations.

```scala
abstract class Animal{
  def noise(): String
}
class Dog extends Animal {...}
class Cat extends Animal {...}

def foo(animal: Animal): String = animal.noise() // cat or dog? who knows!

```

Now let's say you want to **add new functionality** in a very general way; for example, you want `JsonWritable` for all types that can be written to JSON. But here's the catch - there are lots of types you want to write to JSON that you don't control, such as classes in 3rd-party libraries, or just normal typical primitivies - you can't edit the definition of `Int` or `String` to `extend JsonWritable`. 

If only there was a way to **decouple the model from the functionality**. Enter typeclasses, where instead of inheriting functionality, you provide "evidence" so the compiler can "prove" things are `JsonWritable` (later we'll see that this is very powerful, and allows you to auto-generate proofs on the fly):

```scala
trait JsonWritable[T]{ // think of "trait" like "interface"
  def toJson: JsonBlob
}

// we won't get too deep into implicits for now, but imagine it's an extra scope 
// you can place "evidence" for the compiler.
implicit object JsonWritableString extends JsonWritable[String]{
  override def toJson: JsonBlob = {...}
}

// boilerplate implicit class adds extra methods to `String`
// without editing String source definition
implicit class RichString(s: String){
  def toJson(implicit ev: JsonWritable[String]): JsonBlob
}

// phew! now onto using what we've built...

// this is a shorthand way to tell the compiler to look for "evidence" that T is JsonWritable.
def writeToDb[T : JsonWritable](writable: T, db: SomeDatabase): Unit = {
  db.serializeJson(writable.toJson) //
}

writeToDb("hello world") // compiles fine
writeToDb(123) // compiler error: can't prove 123 is JsonWritable

```

Now, let's introduce you to some of our favorite typeclasses...

### Functors
A functor is anything you can `map()` over; think collections such as `List`, `Option`, etc. This is the foundation of our cool control-flow typeclasses.

```scala
trait Functor[F[_]] {
  def map[A, B](fa: F[A])(f: A => B): F[B]
}

def stringifyAnyInternal[F[_] : Functor](xs: F[Double]): F[String] = xs.map(_.toString)
```

See, that wasn't so hard, was it? Everyone loves a good `map`.

### Independent Computations with Applicatives
Ever have independent computations in `F[_]` you want to express succinctly, making their independence clear?
```scala
val result: Option[Int] =
 for {
   a <- Some(1)
   b <- Some(2)
   c <- Some(3)
  } yield a + b + c
```

If `F[_]` is an `Applicative`, a slightly weaked `Monad` (every `Monad` is an `Applicative`, but not the other way around), you can do just that:

```scala
trait Applicative[F[_]] extends Functor[F] { // for reference (simplified)
  def pure[A](a: A): F[A]
  def product[A, B](fa: F[A], fb: F[B]): F[(A, B)]
}

val result: Option[Int] = (Some(1), Some(2), Some(3)).mapN(_ + _ + _)
```

The intuition is this: `product()` allows you to **combine values in a context**, and if you can combine 2, you can combine arbitrarily many (Cats has lots of boilerplate auto-generated for you, which you see above in `mapN()`). This allows you to model independent computation, particularly useful if you want to, say, accumulate results from all the independent failures, i.e. [cats.Validated](https://typelevel.org/cats/datatypes/validated.html).

### Dependent Computations with Monads

Here it is: the part where I explain `Monad`. In a concrete sense, a `Monad` is simply this: anything which you can `flatMap` over (and satisfies a couple basic laws, e.g. you can derive the `map` and `product` from `Functor` and `Applicative`):

```scala
trait Monad[F[_]] extends Applicative[F[_]]{
  def flatMap[A, B](value: F[A])(func: A => F[B]): F[B]

  def pure[A](value: A): F[A]
  
  override final def map[A, B](value: F[A])(func: A => B): F[B] =
    flatMap(value)(a => pure(func(a)))
  override final def product[A, B](fa: Calc[A], fb: Calc[B]): Calc[(A, B)] =
    fa.flatMap{ a => fb.map{ b => (a, b) } }
}

def stringifyAnyInternal[F[_] : Monad](xs: F[Double]): F[String] = xs.map(_.toString)
```

The most intuitive way I can find is by thinking of *computation graphs*; and a `Monad` as *representing a computation context*.

Let's first consider `Functor`, which can express a single *statically defined* graph using `map()`. But you can't combine contexts, and you can't dynamically change the path based on values from a previous step.
```scala 
List(1,2,3).map(_ + 1).map(_ * 2)
```
(insert link)

Now we have `Applicative`, which can *combine contexts*, but still is static:
```scala
( 
  (Some(1), Some(2)).mapN(_ + _), 
  Some(1) 
).mapN(_ + _)
```
(insert link)

Finally we have `Monad`, which allows you to dynamically choose your path chaining *additional computations in that context*:
```scala
 // TODO tbh i'm still working on this example and my diagram sorry guys

def foo(x: Int): Future[String] = x match {
  case 0 => Future.success("nothing")
  case y => Future(readFromDbId(y))
}
List(Future(1)).flatMap(foo)

```
(insert link)

### Folding and Reducing
#### Monoid
Ever find yourself wanting to express values that can "combine" - String concatenation, List concatenation, Integer addition, time series sums? Enter `Monoid`:

```scala
trait Monoid[A] {
  def combine(x: A, y: A): A
  def empty: A
}

val map1 = Map("a" -> 1, "b" -> 2)
val map2 = Map("b" -> 3, "d" -> 4)

map1 |+| map2 // uses `combine` on the values of the map
// res3: Map[String,Int] = Map(b -> 5, d -> 4, a -> 1)
```

#### Fold
Ever find yourself doing a fold over  Cats has lots of helpers to make that easier, including the simple `fold[A : Monoid](fa : F[A]): A` which cuts out your boilerplate if the values are a `Monoid`:

```scala
List("a", "b", "c").fold // equivalent to Foldable[List].fold(List("a", "b", "c"))
// res0: String = abc
```

### Inversions with Traverse
Ever want to "invert" a collection and find yourself writing a long, annoying `fold` of some kind?
```scala
val numbers: List[Try[Int]] = List(Try(1), Try(2), Try(3))
val numbers2: Try[List[Int]] = ???
```

If you have a collection `F[G[A]]`, where `F[_]` is a `Traverse` and `G[_]` is an `Applicative`, you can invert the collections in one line!

```scala
trait Traverse[F[_]] { // definition for reference
  def sequence[G[_]: Applicative, B](inputs: F[G[B]]): G[F[B]]
}

val numbers: List[Try[Int]] = List(Try(1), Try(2), Try(3))
val numbers2: Try[List[Int]] = numbers.sequence // equivalent to Traverse[List].sequence(numbers)
```

### Teaser: Purely functional State and DSLs
I won't get into this. Just a teaser!

### Further Reading and Acknoweledgements

#### Read more
* [Functional Programming and Scala](https://docs.google.com/document/d/1-nUJLUGAYSW4vYvX2crEJ3f_QHSvuwcYporOPyCsEAw/edit#)
* [FP vs OO](https://docs.google.com/document/d/1OvToSVJdEz5YoEfPbquUSfYHVQkYyBpWWS1siTl_g8g/edit#heading=h.76z3gytmdt8l)

#### Ack
* Monads are hard because: https://www.johndcook.com/blog/2014/03/03/monads-are-hard-because/
* Monad Tutorial Fallacy: https://byorgey.wordpress.com/2009/01/12/abstraction-intuition-and-the-monad-tutorial-fallacy/
* Scala with Cats: https://underscore.io/books/scala-with-cats/
* Uncle Bob: https://blog.cleancoder.com/uncle-bob/2018/04/13/FPvsOO.html

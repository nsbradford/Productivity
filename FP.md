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

## OO vs. FP: Extending Data vs. Functionality
At the highest level: what does functional programming offer?

## Ad-hoc polymorphism with Typeclasses
You're probably familiar with [polymorphism](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)) through subtyping, which is fairly intuitive. For example, a class `Animal` can have subclasses `Cat` and `Dog`. If `Animal` has a function `eat()`, you know both `Cat` and `Dog` "inherit" the `eat()` method, but can have different implementations.

```scala
trait Animal{ // think of "trait" like "interface"
  def eat(): Unit // "Unit" is the type of "()" in Scala, which is analagous to "void" in Java.
}
class Dog extends Animal {...}
class Cat extends Animal {...}

def foo(animal: Animal): Unit = animal.eat() // cat or dog? who knows!

```

Now let's say you want to **add new functionality** in a very general way; for example, you want `JsonWritable` for all types that can be written to JSON. But here's the catch - there are lots of types you want to write to JSON that you don't control, such as classes in 3rd-party libraries, or just normal typical primitivies - you can't edit the definition of `Int` or `String` to `extend JsonWritable`. 

If only there was a way to **decouple the model from the functionality**. Enter typeclasses, where instead of inheriting functionality, you provide "evidence" so the compiler can "prove" things are `JsonWritable` (later we'll see that this is very powerful, and allows you to auto-generate proofs on the fly):

```scala
// TODO(nick.bradford) use simalacrum here to eliminate some boilerplate?
trait JsonWritable[T]{
  def toJson: JsonBlob
}

// we won't get too deep into implicits for now, but imagine it's an extra scope 
// you can place "evidence" for the compiler.
implicit object JsonWritableString extends JsonWritable[String]{
  override def toJson: JsonBlob = {...}
}

// this is a shorthand way to tell the compiler to look for "evidence" that T is JsonWritable.
def writeToDb[T : JsonWritable](writable: T, db: SomeDatabase): Unit = {
    
}

writeToDb("hello world") // compiles fine
writeToDb(123) // compiler error: can't prove 123 is JsonWritable

```





### Functors

## Independent Computations with Applicatives

## Dependent Computations with Monads

## Folding and Reducing

### Monoid

### Fold

## Inversions with Traverse

## Teaser: Purely functional State and DSLs

## Further Reading and Acknoweledgements

* Scala with Cats: https://underscore.io/books/scala-with-cats/
* Uncle Bob: https://blog.cleancoder.com/uncle-bob/2018/04/13/FPvsOO.html

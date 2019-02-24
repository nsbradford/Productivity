# Productivity

By [Nicholas S. Bradford](http://nicholasbradford.io)

* **A collection of ideas regarding productivity**, varying in level from abstract to detailed, and varying in supporting evidence from personal intuition to scientific study.
* This document is continuously updating.

## Contents

* [General Thoughts](#general-thoughts)
* [Goals](#goals)
* [Focus](#focus)
* [Organization](#organization)
* [Prioritization/Time Management](#prioritizationtime-management)
* [Health](#health)
* [Learning](#learning)
* [Finances](#finances)
* [Professional/Career](#professionalcareer)
* [Meetings](#meetings)
* [Misc processes/tools](#misc-processestools)
* [Other](#other)

## General Thoughts
* **Motivation** is at the root of productivity, and it comes from 1) having strongly defined goals, and 2) knowing the consequences if your worst flaws are left unchecked.
* **Habits** are compoundable programs for self-automation. Habits and routine are positive.
* **You’ll have to bargain with yourself** if you want any chance of following your plans.
* **Favor assertiveness over open-mindedness** lest you die of analysis paralysis. 
  * “The most impressive people I know have strong beliefs about the world, which is rare in the general population. If you find yourself always agreeing with whomever you last spoke with, that’s bad.” ([Sam Altman’s blog](http://blog.samaltman.com/productivity))
  * “What important thing do you believe that most people disagree with you on?” - Peter Thiel interview question.
  * “The consensus is built into the price.” - Ray Dalio on markets.
* **Write what you learn down as [principles](https://www.principles.com/)** which you can share and discuss with other people; they can in turn rip you apart and spur you to improve (i.e. this page).

## Goals
* “Productivity in the wrong direction isn’t worth anything at all.” ([Sam Altman’s blog](http://blog.samaltman.com/productivity))
* **Your most fundamental goal** is the answer to “Who do I want to become?”
* **Journal** with an either daily or weekly frequency to force synthesis and track your progress against your goals.
* **Perform personal yearly reviews** against your goals, and use the opportunity to learn from your failures and plan better for next year.

## Focus
* **Distraction is the enemy of the creator/engineer**: see Maker's Schedule, Manager's Schedule ([Paul Graham's Blog](http://www.paulgraham.com/makersschedule.html)). Make sure to defend your time and regularly engage in long periods of [Deep Work](http://calnewport.com/books/deep-work/) ([book summary](https://paulminors.com/deep-work-cal-newport-book-summary-pdf/)). There are a few specific implementations such as the [Pomodoro Technique](https://en.wikipedia.org/wiki/Pomodoro_Technique), in which you use a [timer](https://tomato-timer.com/) to set a distraction-free block for 25-55 minutes followed by a 5-10 minute break/reward.
  * Apparently [Pinterest](https://medium.com/@Pinterest_Engineering/three-day-no-meeting-schedule-for-engineers-fca9f857a567) has tried this with great success.

## Organization
* **A good test of your organization** is “can I find anything in 30 seconds?”
* I’ve used a **Recursive Goal Queue** happily since 2014: Organize yourself by highest-level goals (e.g. Work, Education, Finances, Friends, Philanthropy...). Then create two lists: a "TO-DO" a priority-queue backlog for each category that can grow arbitrarily large, and an "Agenda" which contains the top items in each category. Add to the TO-DO at will. Read over the Agenda every day to focus what you need to do; whenever you complete something, pop an item from that category's TO-DO queue and add it to the Agenda. Starter template [here](https://docs.google.com/document/d/1oCi1DPtzGXrCs-bocLy1y1qiuINj1DtqEbB_mcFgb00/edit?usp=sharing).
* In general, try a Kanban Board tool such as Trello for any number of different types of to-do lists. The [Getting Things Done](https://gettingthingsdone.com/) methodology (see [blog](https://hamberg.no/gtd/) and [TED Talk](https://www.youtube.com/watch?v=CHxhjDPKfbY)) requires a fair amount of overhead but scales well. Simply setting 1-3 Big Goals for the day can give you focus and a proper sense of accomplishment (see [The Productivity Project](https://alifeofproductivity.com/book/)). A written to-do list for each day is easy to maintain. Make sure that even while in flow you are linking every task back to your high-level goal.
* **Music Playlist Organization**: This I'm less certain about, but have had a fairly stable routine for ~3 years: Have a small set of "Core" genre playlists (Rock, Pop, Rap, Classical, Jazz...) which are MECE (mutually exclusive collectively exhaustive), and a large set of "Duplicate" playlists by application (Workout, Fancy Dinner, Chill Pregame, Party...).
  * **New Music**: new songs I find go in a central "New" playlist which is what I primarily listen to. After getting bored of a song, I decide to either remove it from the library, or to add it to a Core playlist and one or more Duplicate playlists.
  * I use Spotify Premium for its discovery features and integrations.
* **Filesystem organization**
  * (Turns out that this is extremely similar to Stephen Wolfram's system - see [Leading the Productive Life](https://blog.stephenwolfram.com/2019/02/seeking-the-productive-life-some-details-of-my-personal-infrastructure/))
  * **Put everything in the Cloud** (Google Drive or similar) and enjoy instant access to everything, everywhere - surprisingly handy. Keep everything digital instead of physical.
  * **Securely encrypt sensitive files**; macOS makes this easy with encrypted Sparse Bundled Disk Images that you can create with Disk Utility.
  * **Keep the major directories very general** and only have a few, maybe 3-6, at each level - this makes it much easier to figure out where you categorized things.
  * **Directory structure**: here's the general structure I use. Note that I use "Archive" folders in various places to separate things that I'm not actively working on 
```
   ~/Documents
      /dev
        /localdev
        /GitHub
   ~/GoogleDrive
      /GDriveDocs
      /GDriveDocsShared
      /Documents
        /Important (encrypt)
          /Health
          /Housing
          /Finances
          /Travel
        /Learning
        /Pictures and Video
          /2018
        /Projects
        /Work
```

## Prioritization/Time Management
* **Mental bandwidth should be your limiting factor**, not the number of hours in a day. If not, you need to refine your focus/time management.
* Take advantage of your Circadian rhythm and schedule high-cognition tasks for the morning, boring admin/email/meetings for afternoon, and creativity/brainstorming for the evening (Source: ?)
  * Note that there are definitely biological “early birds” and “night owls”. (Source: ?)
* Two schools of thought: **Frog eating**, in which you get the most unpleasant task done first thing in the day, and **momentum building**, in which you first get a few quick wins. I strongly prefer building momentum both for the confidence boost and feeling of decluttering. 
* Set up a schedule for the day that aligns with your goals. Don’t forget to give yourself breaks, as these keep it sustainable
* **Use a personal time-tracking app** (such as RescueTime) and see how the “8 hours I spent coding” was really spent.
* If you can't figure out where all your time is going, try using a "Mosaic Calendar" to keep track (literally labelling + color-coding blocks of time throughout the day)

## Health
* We often forget one of the largest long-term factors in productivity is our basic health - exercise, sleep, and nutrition (see [80,000 Hours](https://80000hours.org/career-guide/how-to-be-successful/#top) for a comprehensive breakdown). Keeping good posture ([Mayo Clinic](https://www.mayoclinic.org/healthy-lifestyle/adult-health/in-depth/office-ergonomics/art-20046169)) and body language not only has health benefits, but also measurably increases your confidence ([TED Talk](https://www.youtube.com/watch?v=Ks-_Mh1QhMc)).
* **Sleep**: 
  * The scary part is that chronic sleep deprivation (i.e. consistently getting only ~6 hours/night) will measurably impair you cognitively, but after you “adjust to less sleep” you just won’t notice that you’re under-performing! While the “right” amount probably varies wildly, for most people it’s 7-8 hours. (Source: ?)
  * It’s important to wake up at a consistent time, so avoid oversleeping on weekends. Caffeine might not feel like it’s affecting you, and alcohol might feel like it actually helps you sleep, but both will actually reduce your sleep quality (Source: ?). Try a light-based alarm for a smoother morning, and melatonin (not daily) to reset yourself to a healthy bedtime.
* **Diet and Nutrition**: mostly hard to find “general” rules; e.g. the apparent conflict between the “intermittent fasting” crowd and the “breakfast is the most important meal” crowd, which I’ll try to resolve with the edict “if you feel hungry, eat breakfast”. Coffee is associated with mild health benefits ([Healthcare Triage](https://www.youtube.com/watch?v=ly1NjibK79U&frags=pl%2Cwn)), but tea does basically nothing. Weirdly, consuming 1-2 alcohol drinks a day is actually associated with overall health benefits (some claim only red wine, but that’s confounded with income level?) - unsurprisingly, more than that is very detrimental ([Healthcare Triage](https://www.youtube.com/watch?v=gIEJvsDakj4&t=258s)). 
* **Exercise**: 30 minutes of light cardio or weight training 5 times per week, enough to elevate heart rate, is enough to get all of the long-term health benefits, which are considerably large ([Healthcare Triage](https://www.youtube.com/watch?v=SFBBjynBpSw)). Also interesting: weight loss is mostly dependent on a proper diet, with exercise playing a small role ([Healthcare Triage](https://www.youtube.com/watch?v=fCtn4Ap8kDM)). There’s also apparently some risk that people who exercise will “reward” themselves with treats that have significantly more calories than they burned while working out.

## Learning
* **Learn through online courses and [the best textbooks](https://www.lesswrong.com/posts/xg3hXCYQPJkwHyik2/the-best-textbooks-on-every-subject)** instead of random blogs, podcasts, and articles. I’ve found Coursera, edX, and Udacity to all work well.

## Finances
* **Use an automated budgeting tool** (Mint or similar) for personal finance, as it’ll intelligently categorize transactions and track your budgets.
* **Spending**: advice from misc sources recommend rent spending of <30% gross income, groceries spending of $200-400/month, clothing spending of <5% net income.
* **Saving**: You'll want enough liquid money to cover at least 3 months of expenses (i.e. checking account), the rest in investments (take as much advantage as possible from tax breaks via retirement accounts). As you increase income, increase the % you save (keep some -e.g. 50%- to increas standard of living).
* **Investments** (this is what I do, and does not in any way constitute advice): if you only pick one book, use A Random Walk Down Wall Street by Burton Malkiel (TL;DR don't bother with alpha, use total-market funds to diversify across companies and economies).
  * I use low-cost ETFs to get broad exposure to US Total Market, Developed Ex-US, Emerging Markets ex-China, and China (separated out to have more control over weighting).
  * Note that Robo-advisers suffer from the terror of [compound fees](https://medium.com/@blakeross/wealthfront-silicon-valley-tech-at-wall-street-prices-fdd2e5f54905)
* Happiness increases with money until you’re making ~$70-80k (i.e. around where money stops becoming a stress factor and you can live “comfortably”) and then having more money has little impact. However, what you spend the money on can impact your happiness: favor 1) giving charitably, 2) buying experiences instead of possessions, and 3) **use money to free up your time** so you can do more of the things you enjoy [(80,000 Hours)](https://80000hours.org/articles/money-and-happiness/).

## Professional/Career
* Keep an open network; 90% of your random meetings will be a waste, but the other 10% will make up for it ([Sam Altman’s blog](http://blog.samaltman.com/productivity)).

## Meetings
* **Run meetings using the [Jeff Bezos technique](https://www.inc.com/justin-bariso/jeff-bezos-knows-how-to-run-a-meeting-here-are-his-three-simple-rules.html)** of having participants write up their thoughts beforehand and comment on each others’ write-ups; takes some time, but results in well-fleshed-out ideas and very efficient decision-making.
* **“Most meetings are best scheduled for 15-20 minutes, or 2 hours.** The default of 1 hour is usually wrong, and leads to a lot of wasted time.” ([Sam Altman’s blog](http://blog.samaltman.com/productivity))

## Misc processes/tools
* **Use f.lux to reduce blue light from your computer screen** to reduce eye strain and help you fall asleep easier.
* **Use Pocket (or similar) for easier bookmarking** of webpages.
* **Inventory your belongings** and use your annoyance at its length to throw things away and induce minimalism.
* **Subscribe to newsletters** instead of browsing aimlessly - I put out [my own](https://tinyletter.com/tech-ingester), but I recommend [The Morning Brew](https://www.morningbrew.com/?kid=94ccfe) for daily industry/financial news, [Hacker News Digest](https://www.hndigest.com/) to see what the community’s discussing, [MIT Technology Review](https://www.technologyreview.com/newsletters/) for misc tech, [AIDL Weekly](http://aidl.io/) and [Import AI](https://jack-clark.net/about/) for AI/machine learning, and [Benedict Evans'](https://www.ben-evans.com/newsletter/) for a good misc round-up.

# Other
## What I'm looking for/trying next
* **Simple things**
  * **More better newsletters**: contenders include FirstFt from Financial Times, ZeroHedge, Frontrunning, Levine on Wall Street, Quartz, WSJ
* **Tools**
  * **Internet history search**: perhaps [History Search](https://historysearch.com)
  * **To-do list schemes**: [Workflowy](https://workflowy.com/)
  * **Internet knowledge annotation**: [WorldBrain’s Memex](https://worldbrain.io/)
  * **A Virtual Assistant** (e.g. [Fin Personal Assistant](https://www.fin.com)) to automate scheduling meetings, finding restaurants, booking plane tickets, etc.
  * **Keyboard-based browser**: qutebrowser
  * **Password manager**: maybe 1Password
  * **Better shell**: maybe Z-shell
  * **tmux**: see this [gentle intro](https://hackernoon.com/a-gentle-introduction-to-tmux-8d784c404340?gi=a2db06c99825)
  * **Scripting all Mac settings and apps**: using Homebrew. Allows for a simple automated install on a new computer
  * **[Stylus](https://chrome.google.com/webstore/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne?hl=en)** for custom web site styling
* **Big ideas**
  * **A search engine for your personal knowledge graph**, connecting information sources with your written takeaways and facilitating consolidation, exploration, and synthesis.
    * Note that this is a big component of Stephen Wolfram's [Leading the Productive Life](https://blog.stephenwolfram.com/2019/02/seeking-the-productive-life-some-details-of-my-personal-infrastructure/); he more specifically includes a Personal CRM (database of contacts with geo-location, skills, affiliations, etc) and MetaSearcher (integrated text search over filesystem, emails, digitized and OCRd old physical documents, and everything else - and comes with some built in aggregators).
  * **A project management organization system capable of efficiently tracking design/requirements changes**: Mostly I’ve found that people always start with a design doc, and then 1) create whole new versions of the design doc every time there’s a change (such that the history is intact but it’s tough to track changes in a feature over time), 2) appending changes to the end (more concise and trackable, but makes evaluating any given state annoying), or 3) use JIRA (easy to track individual issues, but difficult to synthesize from)
  
## What I'm currently experimenting with
* **Full spectrum LED light** apparently gives great benefits from 10-15 minutes of use in the morning ([Sam Altman’s blog](http://blog.samaltman.com/productivity)). After a few months of using on weekends I've definitely noticed an immediate and positive "buzz" sensation, TBD on whether it becomes life-changing over the dark winter months.

## What I've tried that doesn't work
* Nutrition:
  * Intermittent fasting while also doing intense daily exercise: too little energy
* Newsletters:
  * The Skimm for daily news: a little fluffy/superficial, and mostly a subset of The Morning Brew
  * O’Reilly Newsletters: mostly too basic to be useful


## Disclaimer
Views expressed here are my own and not representative of any past or present affiliated entity.

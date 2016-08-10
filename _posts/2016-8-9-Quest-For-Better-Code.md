---
layout: post
title: The Quest for better Code
---

I often find that in the teams that I have worked on the incentives encourage coders to write a lot of bad code. Talk to a coder on such a team and they will tell you that they never intended for it to be that way and given a brand new project without a doubt they would design it brilliantly. There will be lots of tests, new feature X will be trivial to add, and now only if all of that legacy code could be throw out... I learned early in my career that unfortunately, this is often wishful thinking. Given a brand new project with time constraints and the same incentives leads to the same results.

So what happens? How is it that despite the best intentions of coders we end up with the same bug ridden code bases? This is a difficult question that I have spent a lot of time trying to seek an answer too. One of the problems I have noticed is that most coders that I have worked with focus to much on writing perfect code instead of focusing on writing better code in their everyday work. Perfect code is an unreachable bar so it is too easy to start cutting corners and justifying exceptions. Of course there is also the problem of having the right incentives to drive the right behavior but let us focus on what is the right behavior and save the incentives for another time.

Note: Quick disclaimer this is all based on my experience, conversations, and reading. Very much my opinion based on what has worked for me for both small (just me) and large (team of 30 and 5+ years of legacy) code bases. None of my ideas presented here are really new for example J. B. Rainsberger had this post on [The Four Elements of Simple Design](http://blog.jbrains.ca/permalink/the-four-elements-of-simple-design) many years ago.

## The Goal
I am going to make a couple of assumptions first. You are writing code for a customer so that they can solve a problem to accomplish a goal. Might be yourself, could be contracted work, or might be you also need to attract those users. Potentially there are explicit budgets but without a doubt there are deadlines. You are working with a team that has an aligned purpose. As a team of coders your goal then is to write your code by the deadline so that your customer can solve their problem to accomplish or work towards their goal without unexpected issues or confusion.

Given this goal there are a couple of interesting questions for your team to answer. What is the best way to solve the customer’s problem? Is there enough time and money? How do we minimize unexpected issues or confusion? My ideal definition of bug is anything that was unexpected or frustrating for both the user and the programmers. So rephrasing the last question, how do we minimize bugs?

There have been many attempts to answer these questions, usually by focusing on one and sacrificing the others. For example, a waterfall model of software development is essentially built around the idea of a fixed budget and deadline. It focuses on planning out what should be built (often with specs) and then executing on it. At some point ‘feature’ work stops to focus purely on bugs (or a subset of them). This approach of course assume that we will know the answer to the customer’s problem up front and avoiding bugs will be the result of pre-planning. After working on a plan for a while often cracks start to form because people realize that despite the plan the customer is confused and frustrated by the solution (or even worse the solution does not work).

I like to take a different approach based on some more assumptions, we do not know the solution to the customer’s problem (only guesses). The best way to understand if your solution works or if the customer is having unexpected issues or confusion with the solution is to get it (even if it is not complete) into their hands as early and often as possible and collect feedback. If we want to get the solution into their hands as quickly and frequently as possible code changes need to be easy to make quickly and safely (without introducing bugs) even as the code base scales. This is going to be far more economical in the long run as we are optimizing for finding a solution (hopefully the best) as quickly as possible.

Note: How to get the solution into your customer’s hands and collect feedback is also a difficult question. It is critically important as well because this feedback should be driving your code changes. For this post let us assume it has been solved and instead focus on making the code changes.

## Making safe code changes quickly
Let us first remember the assumptions we just made, we do not know the solution. This means that too much up front architecture work is going to be a waste of time. We need to assume our code is going to change. Also, we have a time budget! No time for generalizing all of our solutions. Finally, we are working on team, if we are going to minimize the amount of time to make safe changes we cannot have specific team members be bottlenecks. So if a team member goes on vacation (which I hope that they do) than anyone else should be able to accomplish the same coding tasks in about the same amount of time without introducing bugs.

Then what makes a good code change? 
1.	Readable code - Anyone should be able to quickly read and understand what the code is doing and why.
2.	Code should be tested - Not only should this be done in a way to enhance readability (should help answer why the code is written the way it is written) but this is critical for future changes being safe.
3.	Code change should be done in a way that minimizes complexity - What do I mean by complexity? Check out this [Taming Complexity with Reversibility]( https://www.facebook.com/notes/kent-beck/taming-complexity-with-reversibility/1000330413333156/) from Kent Beck at Facebook for the background and how Facebook solves this problem. An example of this is emphasizing simplicity to enhance readability. We can only keep so much in our short term memory so the code should be written in a way to minimize what we need to remember.
4.	The change needs to work as expected – This needs to be true in both the coder’s and the customer’s minds. So no bugs and also likely that data needs to be collected to understand if it works as the customer expected it to. 
Each of these four things are equally important for a safe code change that should make future changes by any teammate just as difficult if not easier than the current change.


## Stepping out of the theory
### Measuring code complexity
It is interesting to note how the previous points are all interrelated. Readability is enhanced when the complexity of the code is minimized and also when the test code is well written. If the code is less complex I often find it is easier to write tests. Which leads to a simple feedback mechanism for determining how complex your code is. Are the tests easy to write? If you want a more straight forward measure of code complexity consider the following properties. Is there any redundancy, is the coupling between dependencies minimized and obvious, does the code have strong cohesion, and is the correct encapsulation enforced? While unfortunately not giving a concreate value, answering these questions for potential solutions allows for their complexity to be compared.

### Safe (bug free) changes
One of the main catalysts to this theory forming in my mind was when I started to actively write code using Test Driven Development (TDD). In short TDD is about writing the test before writing the code. Uncle Bob outlines this approach in his post [The Three Rules of TDD](http://www.butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd). What you realize really quick with this approach is that you spend a lot of time changing existing code to remove redundancy and reduce complexity (for both your test code and the code being tested).

I had heard of refactoring in the past but did not truly embrace how powerful it can be until I was forced to constantly make changes to simplify my designs. So many great resources on refactoring, if you are looking for a book I would suggest Martin Fowler’s [Refactoring: Improving the Design of Existing Code](https://www.amazon.com/Refactoring-Improving-Design-Existing-Code/dp/0201485672), Joshua Kerievsky’s [Refactoring to Patterns](https://www.amazon.com/Refactoring-Patterns-Joshua-Kerievsky/dp/0321213351/), and if you are working in a legacy code base Micheal Feather’s [Working Effectively with Legacy Code](https://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052/).

Also depending on your code language there are some great automated refactoring tools. For example, [Resharper](https://www.jetbrains.com/resharper/) is kind of the gold standard for C# development. An automated refactoring tool makes the process of learning most of the basic refactoring’s so much easier. It is as simple as highlighting something and asking your IDE to “refactor this.”

If all the potential refactorings are a little overwhelming I would suggest checking out Arlo Belshee’s [The Core 6 Refactorings]( http://arlobelshee.com/the-core-6-refactorings/).

Want to make your code less complex? Remove your dependencies Brian Geihsler has some great posts on [The Dependency Elimination Principle](http://qualityisspeed.blogspot.com/search/label/dependency%20elimination%20principle).

### On Naming
Truthful naming is one of the most important things you can do to enhance readability. Whenever you find a name that means nothing or is lying. Update it to something more truthful. Arlo Belshee has a fantastic series on this topic [Good naming is a process, not a single step](http://arlobelshee.com/good-naming-is-a-process-not-a-single-step/).

### Writing great tests
There are a lot of different approaches to writing tests, for me I like to follow these rules. 
1.	Tests need to be fast (<10 ms) or I won’t run them. 
2.	Tests need to be 100% reliable, if a test fails the code is wrong or the test needs to be updated. This is for sustainability, as the number of tests scales I do not have time to figure out if an error was “expected” or not. 
3.	No two tests should be testing the same thing. This is also for sustainability, when I make a behavior change it should not take forever to update the test suite. 
4.	Avoid Mocks, Arlo Belshee outlines this approach in his blog under the [no-mock](http://arlobelshee.com/tag/no-mocks/) tag. If a test relies on the behavior of a dependency, then mocking out that behavior can lead to tests not failing when the dependencies behavior changes. For this reason, this is an exception to my previous rule.
5.	[Your test are just your spec. NBD.](http://arlobelshee.com/your-test-are-just-your-spec-nbd/) For example, Thing1 Should perform action D when event A occurs. This [post](http://arlobelshee.com/wet-when-dry-doesnt-apply/) from Arlo as well is a great example of this.

If I find myself struggling to write tests that means that there is probably a design problem in the code under test (it is too complex!) or potentially in the testing code.

One other exception to the above rules. When validating if external dependencies (code you do not control) work the way you expect them to, it is okay if those tests take longer and are not 100% reliable. Eric Gunnerson talks about this in approach in his post [Unit Test Success using Ports, Adapters, and Simulators](https://blogs.msdn.microsoft.com/ericgu/2014/12/01/unit-test-success-using-ports-adapters-and-simulators/).

## The Journey to Better
I hope that this helps inspire you that the promise of better code can happen with every change with whatever code you are working with right now. My second hope is that this gives you some language you can use to communicate with your team. Let me know if you found something confusing or helpful. I suspect as I experiment with new approaches my perspectives will change here as well so will link to updates as my thinking evolves. Best of luck!

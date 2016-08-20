---
layout: post
title: The Quest for Better Code
---

I often find that in the teams that I have worked on coders tended to write a lot of bad code (me included). Talking to my fellow coders I often heard frustration with these codebases expressed like, “This code is so hard to change! How did it get this way? Let’s just throw it all out so we can design it right.” This is often wishful thinking, given the same constraints and incentives lead to the same results.

So what happened? How is it that, despite our best intentions, we ended up with bug ridden codebases? One of the problems is that we focused too much on writing perfect code. Perfect code is an unreachable bar so it became too easy to start cutting corners and justifying exceptions. I have found that there is a more successful approach, instead of focusing on writing perfect code I now focus on making the codebase better with every change. Of course, there was also the problem of not having the right incentives to drive the desired behavior, but let us focus on what is the desired behavior and save the incentives for another time.

## Why I Seek Better Not Perfect
When I write software I am always doing so for a customer. I want the customer to use my solution to solve a problem they are facing. This customer might be myself, could be a contractor, or it might be a target market. There may be an explicit budget but, without a doubt, there are deadlines. Finally, I am almost always working with a team that shares my purpose. Our goal then is to write code by a deadline so that our customer can solve their problem without unexpected issues or confusion.

Given this goal, what is the best way to solve the customer’s problem? To answer this I, make one big assumption. We do not know the solution. If we are lucky we have a really good idea but almost certainly the final solution will be different then our initial thoughts. The best way to understand if a given solution works or has any bugs is to get the customer using it. The faster we can implement a change based on our user’s feedback the more iterations our solution will go through the better our solution is going to be. This is why I focus on making the codebase better not perfect, it must sustain this high velocity and be bug free.

*Note: Both how to get the customer using our solution and how to collect feedback are also difficult questions. For this post, I am going to assume these problems have been solved.*

## Sustainable Bug Free Changes
Before going any further, I should clarify what I mean by bug. I like to aim for Arlo’s definition [anything surprising, confusing or disappointing anyone]( https://twitter.com/arlobelshee/status/719525545805881345). So with that definition and given that we should expect to make lots of changes there are a couple things we need to avoid. First, too much up front architecture work as it would end up being a waste of time. Second, over generalizing our solutions, we have a time budget! No time for that. Finally, we cannot allow team members to become bottlenecks. When a team member leaves or goes on vacation anyone else should be able to accomplish the same coding tasks in about the same amount of time.

Then what defines a sustainable change?
1. Readable code - Anyone should be able to quickly read and understand what the code is doing and why.
1. Code should be tested - This is critical for ensuring future changes are safe.
1. Code changes should minimize complexity - What do I mean by complexity? Check out this post [Taming Complexity with Reversibility](https://www.facebook.com/notes/kent-beck/taming-complexity-with-reversibility/1000330413333156/) from Kent Beck at Facebook for the background and how Facebook solves this problem. An example of this is emphasizing simplicity to enhance readability. We can only keep so much in our short term memory so the code should be written in a way to minimize what we need to remember.
1. The change needs to work as expected - This needs to be true in both the coder’s and the customer’s minds. That means no bugs, which means that data needs to be collected to understand if the code works as the customer expects.

I listed these points out in a numbered list but I do not view one as more important than the others. Equal attention must be paid to them all to ensure that future changes are quick to make and bug free.

## Practical Tips for Sustainable Changes
### Measuring Code Complexity
When determining the complexity of a piece of code we can take advantage of the fact that tests are easier to write for less complex code. This can be used as a simple feedback loop, Are the tests easy to write? If no, then reduce the complexity. An example might be decoupling from or removing global state. Another approach is to evaluate the answers to the following questions for two solutions. Is there any redundancy? Is the coupling between dependencies minimized and obvious? Does the code have strong cohesion? Is the correct encapsulation enforced? The solution that better answers these questions is less complex.

### Guaranteed Bug Free Changes
The easiest way of preventing bugs is to never make a change that could introduce one. Enter refactoring, operations that can be performed on code that do not alter its observable behavior.

There are some great resources on refactoring, for a book I suggest Martin Fowler’s [Refactoring: Improving the Design of Existing Code]( https://www.amazon.com/Refactoring-Improving-Design-Existing-Code/dp/0201485672), Joshua Kerievsky’s [Refactoring to Patterns]( https://www.amazon.com/Refactoring-Patterns-Joshua-Kerievsky/dp/0321213351/), and specifically targeting legacy codebases Micheal Feather’s [Working Effectively with Legacy Code](https://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052/).

Also, depending on the programming language, there are some great automated refactoring tools. For example, [Resharper](https://www.jetbrains.com/resharper/) is kind of the gold standard for C# development. An automated refactoring tool makes the process of learning most of the basic refactorings much easier. It is as simple as highlighting something and asking the IDE to “refactor this.”

If all the potential refactorings are a little overwhelming, I suggest checking out Arlo Belshee’s  [The Core 6 Refactorings](http://arlobelshee.com/the-core-6-refactorings/).

### Using Readability to Encourage Simplicity
Truthful names are the best way to make code more readable. If I am reading a piece of code, a function name like “GetData” means nothing to me “GetBookNamesFromDatabase” would be more informative. This helps with understanding the complexity of the code and allows me to compartmentalize what I need to remember at any given point in time. When reading through some code whenever I find a name that means nothing or is lying. I like to update it to something more meaningful and truthful. This also leads to better code cohesion because as code names get longer. I find that I naturally split code that is doing multiple things to keep the names simple. For further reading, Arlo Belshee has a fantastic series on this topic [Good naming is a process, not a single step](http://arlobelshee.com/good-naming-is-a-process-not-a-single-step/).

### Writing Great Tests
There are a lot of different approaches to writing tests, but I like to follow these rules:
1. Tests need to be fast (<10 ms) or I won’t run them frequently enough. 
1. Tests need to be 100% reliable, if a test fails the code is wrong or the test needs to be updated. This is for sustainability, as the number of tests scales I do not have time to figure out if an error was “expected” or not. 
1. No two tests should be testing the same thing. This is also for sustainability: when I make a behavior change, it should not take forever to update the test suite.
1. Avoid Mocks, Arlo Belshee outlines this approach in his blog under the [no-mock](http://arlobelshee.com/tag/no-mocks/) tag. If a test relies on the behavior of a dependency, then mocking out that behavior can lead to tests not failing when the dependencies behavior changes. For this reason, this is an exception to my previous rule.
1. [Your test are just your spec. NBD.](http://arlobelshee.com/your-test-are-just-your-spec-nbd/) For example, “Plane Should be flying after it takes off” is describing an expected behavior of “Plane.” This [post](http://arlobelshee.com/wet-when-dry-doesnt-apply/) from Arlo also has great examples of this.

Like I mentioned earlier in the Measuring Code Complexity section, if I find myself struggling to write tests then that means there is most likely a design problem in the code under test (it is too complex!) or potentially in the testing code.

One other exception to the above rules. When validating if external dependencies (code that I do not control) works as expected, it is okay if those tests take longer than 10 ms to execute and are not 100% reliable. Eric Gunnerson talks about this approach in his post [Unit Test Success using Ports, Adapters, and Simulators](https://blogs.msdn.microsoft.com/ericgu/2014/12/01/unit-test-success-using-ports-adapters-and-simulators/).

### Use Tests to Drive Design Changes
An effective approach to sustainable changes is Test Driven Development. In short, TDD is about writing tests before writing code. Uncle Bob outlines this approach in his post [The Three Rules of TDD](http://www.butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd). My favorite thing about this approach is the constant feedback loop. Whenever it is difficult to write a test I immediately know it is time to refactor the code as there is a design problem.

### Bugs as Feedback
As I stated earlier I like Arlo’s definition [anything surprising, confusing or disappointing anyone]( https://twitter.com/arlobelshee/status/719525545805881345) for a bug. Important to note that this is only affective if when a bug occurs we take it seriously. Jay Bazuzi has a great post outlining a discussion about [BugsZero @ Agile Open Northwest 2016]( http://jbazuzicode.blogspot.com/2016/02/bugszero-agile-open-northwest-2016.html) on this topic.

## The Journey to Better
I hope that this helps inspire you to aim to always write better code and that my approach will give you some ideas to experiment with. My second hope is that this gives you some language you can use to better communicate with your team.
Let me know if you found something confusing or helpful via email (maybe eventually I will be convinced to setup comments). I suspect that, as I experiment with new approaches, my perspectives will evolve as well; we are on this journey together. So, fellow adventurer, I wish you the best of luck!

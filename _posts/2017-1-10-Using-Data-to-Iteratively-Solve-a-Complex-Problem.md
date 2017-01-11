---
layout: post
title: Using Data to Iteratively Solve a Complex Problem
---

In my current job working as a software engineer on the Office Suite at Microsoft, I have seen a transformation over the last couple of years from a 3-year waterfall release cycle to a more iterative monthly release cadence. Along with this, there has also been a transition to focus on using data to drive decisions instead of developer or project manager opinions. As a believer in [Agile practices](https://www.agilealliance.org/agile101/) and [iterative design](https://en.wikipedia.org/wiki/Iterative_design), this has been a very exciting evolution to be a part of! Microsoft still has a long way to go as an organization and as a company (so much legacy…) but it’s been great to see and experience a mostly positive trend.

While learning and reading about data driven iterative design, I have unfortunately not seen much written about the basics. Lots has been written about implementation approaches (Scrum, Kanban, or extreme programming to mention a few) but not a lot about developing the feedback engines necessary for them to succeed. Here are the steps I follow to build out a feedback engine when solving a complex problem.

## 1) Define the Problem to be Solved

I like to start by clearly stating the problem to be solved. To avoid miscommunication, I usually spend some time re-framing the question as the desired goal for a user. This is all about defining the value statement for users. Ideally, I want to keep it focused since it is better to do one thing well than to do two things poorly.

As an example, say I was solving the problem: “make communication between team members simple, concise, and seamless.” This could mean many different things, so after further conversation and brainstorming with folks we might agree upon the goal: “all team members understand what they need to do each day.”

## 2) Understand Who will Benefit from the Problem Being Solved

Focusing on the folks who will care if the defined problem is solved helps me make sure that I am getting feedback from the right people. Also, it helps from a business perspective (how large is the intended audience, how much would they be willing to pay for a solution, what is a financially feasible amount to invest in building out the solution, and who to market the solution to).

Taking the previous example, we might make the intended audience specific to a team, an industry or generalize it for any group of individuals who work together daily. I like my solutions to be focused so try to avoid generalizing too early. Also, there might be audience groups with competing interests that will make feedback more difficult to understand. I find that usually a balance needs to be struck between a large enough audience to make the investment worthwhile but small enough so that I can truly understand my users.

## 3) Define Success Measurements (Lag Measurements)

Once I have clearly stated the problem and defined the intended audience, I like to define a high-level measurement of success. With this analytical measurement, the core question I usually want to answer is: “What percentage of the intended audience is using my solution?” Why users are not using my solution is of course the real golden question, but having this as a baseline metric is a stepping stone to answering that. If the problem being solved is a recurring one, then another critical question I like to answer is: “What percentage of my users are returning?” 

These high-level metrics are pretty much useless alone. I find that they are affected by too many variables, and while I would like to take a scientific approach of only changing a single variable at a time, usually the amount of time it takes for these metrics to respond is just too long. Since time is also a variable, this becomes complicated. Not to mention, many users will likely only give the solution a single chance. This means that other metrics that respond faster and will indicate success are also needed.

## 4) Define Lead Measures

[Lead measures](http://www.nimbleams.com/blog/2015/2/17/lag-measures-versus-lead-measures/) are intended to be faster action signals that will indicate positive or negative changes in the Success Measurements. I have two main sources of lead measures.

### Desired End State

With step 1, I defined the problem to be solved as a desired goal for the user. At this point, I further break this goal out into the remaining desired end states. These end states might take many forms: the amount of time to achieve the goal, how much pain was required (or not required) to achieve the goal, or any risk taken (or not taken) by the user to achieve the goal.

For example, building on the original example goal “every day team members all understand what they needed to do that day,” some other desired end states might be: “every team member contributed every day”, “team members never did the wrong thing due to a miscommunication”, “team members only spent an hour each communicating with each other a day”, and “no single team member dominated communication.”

I then want to measure if users are reaching these desired end states (including the initial goal). The thinking here is that if users are not reaching the desired end states, or are experiencing pain to do so, then it is less likely they will return or recommend the solution to someone else. As my solution evolves, seeing how close each iteration is to accomplishing these end states allows for me to declare one version better than another.

Over time, figuring out what end states matter to the intended audience is the most difficult part of the iterative process.

### Factors External to the Solution

The success metrics will be affected by many things independent of the quality of the solution. These might include any of the following:

1. Financial cost of the solution to users.
1. End user’s willingness to pay (What is the perceived importance of solving the solution to users?).
1. Competitors.
1. Availability of the solution to the given audience.
1. Audience's knowledge of the solution.
1. Audience's desire to try the solution.
1. Others…

When I usually read about this topic, these external factors are often described as timing and marketing. Even if I cannot continually measure these, I like to understand them and at least make some estimates. I want to understand what is keeping users from using my solution.

## 4) Establish a Generic Feedback Channel

Knowing myself, I know that I am going to miss something. As much as I try to understand my audience going in, unless I am solving a problem for myself, I am not going to completely understand them or their needs. To this end, I build in a generic feedback channel so that users can tell me about any pain they suffered or ideas for improvements. I use this feedback as an opportunity to learn about my audience and refine the lead measures. I want to understand: do they matter? how much? And did I miss one? Other options to accomplish this are user studies or surveys.

If I am solving a problem using software, I also know that there will be bugs. So it is also important to me that when a user reports pain, I collect any context information so that I can quickly debug what happened. This means building bug reporting directly into the solution.

## 5) Iterate on the Solution

With all the measures in place, as I iterate on the solution, there are analytical lead measures that indicate the quality of one solution over another. Additionally, there is a feedback channel that is used to understand if the given lead measures are indicative of the success measures. Ideally with lead measures in place I can iterate very quickly to find an optimal solution.

I hope that these steps are easy to follow for anyone building out a feedback engine. Let me know through email if you have some thoughts on the approach. Thanks for reading!

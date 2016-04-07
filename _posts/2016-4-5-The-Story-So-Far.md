---
layout: post
title: The Story So Far
---

For the past two years I have been spending a significant amount of time torwards the goal of programming chess in the browser. The aim was to allow players to be able to play against one another remotly. While I have gotten part of the way to this goal what has actually happened is that I have learned a decent amount about different web programming approaches. Maybe one day I will have chess working completly, but considering that I am not actually a huge fan of chess (I know crazy considering I spent contless hours of my free time programming it) I would rather move onto something else. So now that I have spoiled the ending lets spoil it even further. Here is a screen shot of the current (maybe final) product.

[<img src="{{ site.baseurl }}/images/ChessInElm.jpg" alt="ChessWrittenInElm" style="width: 800px;"/>]({{ site.baseurl }}/images/2016-4-5-The-Story-So-Far/ChessInElm.jpg)
No seriously this is it, so yeah the ending has been spoiled so quit now. No point in continuing.

If I had been a smarter man I might have taken some screen shots throughout the process to better show off the stepping stones, but (un)fortunetly I am not. Most of the stepping stones are blocks of code anyway which lives on in source control forever. In a follow up post I will have some more screen shots showing off the game in action (instead of one that looks like it was ripped from [google](https://www.google.com/search?tbm=isch&q=svg+chess+board)). With the power of github pages as well should be able to link to some live demos.

## Path to today ##
While I won't dig into all of it here it the path that I have taken to get to the final product above.

1. Started coding the game platform in TypeScript (since javascript of course is for suckers) using Visual Studio 2013. Decided to use this as an opportunity to really learn TDD and how to write vertical features so started writing the tests first and scoping the work to try and always deliver the next piece of value to the player at regular intervals. This helped quite a bit with my sanity and kept the forward moment going for quite a long time.
1. Struggled with TypeScript/Javascript. Turns out when your writing TypeScript the more you know about Javascript the better. Spent a lot of time refactoring my code to continually get to a better place.
1. Throughout this process struggled with Visual Studio's support for TypeScript before finally deciding it was time to learn node.js. What finally pushed me was (as usual) the promise of a better language. My brother linked me to [this article](https://medium.com/javascript-scene/the-two-pillars-of-javascript-ee6f3281e7f3#.9glh0xtm8) by Eric Elliot. While now I disagree with many of the things Eric says this was definetly the push I needed to look into alternative options. It was actually Eric's follow up article on [functional programming](https://medium.com/javascript-scene/the-two-pillars-of-javascript-pt-2-functional-programming-a63aa53a41a40) which lead me to discover this great [FP intro book](https://github.com/MostlyAdequate/mostly-adequate-guide). More on this later.
1. Node.js and the javascript community is crazy, so many things to learn and yet so little time... Wrote several github projects to facilitate learning. Investigated writing the game platform in pure JS using Eric's stampit library. Decided that the lack of tooling (auto-complete and compile time checks) made it to annoying to work with.
1. Moved the TypeScript game platform and all of the Chess logic over to a Node.js packaged build system. I use a set of [common gulp tasks](https://github.com/greyepoxy/common-gulp-tasks) to build each package ([example usage](https://github.com/greyepoxy/common-gulp-tasks-recipe)). A follow up here that I might look into later is using [webpack](https://webpack.github.io/) instead. Another follow up here is to publish all of this code, currently this is in a private repository (not on github of course because who wants to spend money). I wrote a couple of helpful node packages that I suspect would be useful to others.
1. My next step with my project was to actually build the website around it. This is when I started to dig into learning about webpack, [react](https://facebook.github.io/react/), and [flux](https://facebook.github.io/flux/). Through researching this, one of the many flux solutions [Redux](https://github.com/reactjs/redux) and a javascript reactive solution [cycle.js](http://cycle.js.org/) I stumbled upon lead me to discover [elm](http://elm-lang.org/).
1. I liked elm so much that I decided to re-implement chess in it. This leads to a energic, exiting but ultimatly dissaponting relatioship with elm. Likely I will dig into this further at some point (the screen shot above is actually from the elm implementation).

Some might say that this is 6 steps to many, but I like to argue its probably still one step to few. I suspect that more then likely I am just making a big deal over nothing.
[<img src="{{ site.baseurl }}/images/ErmahgerdTrnershberl.jpg" alt="ChessWrittenInElm" style="width: 800px;"/>]({{ site.baseurl }}/images/2016-4-5-The-Story-So-Far/ErmahgerdTrnershberl.jpg)


Thanks for reading, I hope to follow up with more specifics of the more interesting thought processes and discoveries.   

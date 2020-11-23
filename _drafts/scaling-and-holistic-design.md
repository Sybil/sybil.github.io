---
layout: post
title: "Antipattern : Holistic design, Babel tower and scaling"
categories: ruby
---

In all my jobs scaling was always the grand goal of work. Whatever the size of the project, scaling was often an excuse to try fun technologies and refactor hated code.

It's a very easy argument to give to non-tech people.
Who doesn't want their project/enterprise to grow ?
Who does not want to feel like they have grownup problems, as if they were Facebook/Google/etc ?

The end solution for scaling is more or less always the same : more CPU, more RAM, more processes, etc.
In the web, the bottleneck was often the database, probably because these systems are stronger than any other layer and therefore become the foundation of many complex behaviors (what would we be without ACID and the sweet rollbacks ?).

What's strange is that in all places I worked, scaling was a consideration from the get go. So how could applications designed to be scalable end up not being it (when it's not incompetence or lack of manpower) ?

**Because of the holistic design**

What I call holistic design is this sweet mix of feature creep and the desire for perfection. Often perfection is misinterpreted as omnipotence. Doing one simple thing perfectly (here perfectly could be read as *mathematically proven*) is replaced with doing many things. Every missing feature is seen as a failure in the system. As soon as a user has a desire that live outside of the boundaries of the application, it is a bug. Fixing it brings the antipattern. Good will is the Troyan horse of antiscaling.

I deeply believe the human/social part plays a massive role (probably the biggest) in all architecture decisions. Like in every science, the myth of the lone problem solver/architecture god is still very pregnant but do not match the fact that the complexity of modern day problems require many people. No single brain can hold all the information nowadays.

So we have many people and they all deeply desire to solve all problems, to cover all user needs and to have a infailible system. In few iterations it ends up as a holistic design : all features are tied together. Whatever the flow the user do they can still reach anything. Any improvement is ported everywhere, just in case someone could need it, strong product decisions are mellowed so everyone could be happy, etc. I also believe developement seen as a craft leaves a huge love for the baby/product : when being reported an unsatisfied user it requires a strong detachment to realize that maybe they represent 0.00001% of the population and we don't care. Sometime it is impossible to know how many people are impacted. So, in doubt, we add a floor to the Babel tower[1].

It impacts heavily the codebase. An holistic design is a complete graph : every point is relied to all others. Whatever the splendid art that was build, services or components, libraries or packages, they all end up being tied together. Maybe they live in different places, maybe their messages respect a very well drawn API, but all know about everyone else, all impact each other.

Most of the time, it can be seen on the database level : every table has relations to many others. So from any place in the application, we can link to another feature or domain logic. Or from any point in time, we can rollback or get past information. From an holistic product, we went down to an holistic architecture.

This cannot scale :
- For the product  : imagine the 80s software, with 500 buttons proposing all gradients of a user desire.
- For a codebase : huge database bottlenecks, but even application ones. Every change can have unforseen and huge waves of impact until it reaches the faraway lands of this forgotten part.

In my opinion it can be even harder to change than solving technical challenges[2]. First, it can even be difficult to even see that we are in the holistic antipattern. Afterall it's the after effect of an uncounsious desire, so it is never acted, or discussed. Second challenging it could easily lead to breaking changes or challenging existing product visions.

Once detected, moving out of the antipattern can be really painful : solving it is more than a technical show (like let's rewrite it in xxx language a-la-mode, move to NSA-level datastore, etc) but potentially impacts existing features (or even require to remove them). This demands to refocus to the core, to rediscuss the existing. It can be painful : developer opinion is sometime unwelcomed on this subject (they look like they talk about product, not their technical craft) and this involves debates/hot discussions. Last part can be problematic, most people would rather refactor a whole application than do a one hour long heated meeting.

It also require to be always on guard, since this state can simply be reached by *fixing problems*. So your are in the antipattern, but in your everyday life you have the impression to move forward, to add this sweet new button, etc. And one day you look back and you realize that now it takes 6 months to add a feature. Or that users get lost in your product. Or simply that you watch [this video](https://www.youtube.com/watch?v=y8OnoxKotPQ) 10 times a day.

[1] I could probably write a whole article about this. Software world could probably learn a lot of existing craft (like the old medieval church bulding) and the old tales that they hold.

[2] I wonder how much this dream of an overeaching/omnipotent application is a lingering effect of our monoteist culture of having this one thing that covers everything.

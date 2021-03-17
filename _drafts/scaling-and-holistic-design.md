---
layout: post
title: "Antipattern: Holistic design"
categories: ruby
---

Whatever the size of the company I worked for, I always found the same antipattern, which often had a huge impact on the ability to scale. Sometime applications "designed" to scale were in fact hindered because of it: **holistic design**.

What I call holistic design is this sweet mix of feature creep and desire for perfection. It is a design that ends up trying to meet all end user needs instead of focusing  around a very specific (or core) problem.

Often perfection is misinterpreted as omnipotence. Doing one simple thing perfectly is replaced with doing many things. Every missing feature is seen as a failure in the system. As soon as a user has a desire that live outside of the boundaries of the application, it is a bug. Fixing it brings the antipattern. Good will is the Troyan horse of antiscaling.

I deeply believe the human/social part plays a massive role (probably the biggest) in all architecture decisions. For a simple reason : most system became complex enough to rely on many people, with nobody knowning everything about the codebase/product. Since all actors have partial information, a lot of decisions move from a single brain to a distributed discussion [1].

So we have many people and they all deeply desire to solve all problems, to make the user happy, to have an infailible system. In few iterations it ends up as a holistic design : all features are tied together. Whatever situation the user is in, they are able to access everything. Any improvement is ported everywhere, just in case someone could need it, strong product decisions are mellowed so everyone could be happy, etc. As crafters, developer deeply love their creation. When user insatisfaction is reported,  it is difficult to stay rational. It requires a strong detachment to realize that maybe this complaint represents 0.00001% of the population and we don't care. Sometime it is impossible to know how many people are impacted. So, in doubt, teams add a floor to the Babel tower[2].

It impacts heavily the codebase. An holistic design is a complete graph : every point is relied to all others. Whatever the splendid art that was build, services or components, libraries or packages, they all end up being tied together. Maybe they live in different places, maybe their messages respect a very well drawn API, but all know (secretly) about everyone else, all impact each other. Since most developers know this kind of heavy dependency is bad, it is hidden. Instead of having direct couplage, the correlation is made indirect. There are different ways to do it. Per example :
- Features relying on sync behavior in many systems. The processing order is critical and is hidden as a code byproduct. These systems can only work because another one has made some work beforehand (even if in term of pure implementation none of those systems references each other). So changing one breaks the whole chain.
- Enforcing very specific/custom user flows. Instead of having an holistic implementation, it becomes holistic features : whatever the user starting state, they are proposed the same set of features. But behind each feature (looking similar from the user point of view), there are many flows, all depending of the initial state. The holistic pattern stay hidden: officially all those flows are separate. This is a very brittle: any feature change can break this equilibrium by impacting many flows.
- Every reference to other dependencies is removed from the code, but most of the data or messaging format is in fact directly correlated to another piece of the application. So modifying it breaks by surprise other pieces (looking at you events based systems).
- On the data persistence level, with either having many relations or huge data inconsistency (depending of the choices made).

This cannot scale :
- For the product  : imagine the 80s software, with 500 buttons proposing all gradients of a user desire.
- For a codebase : huge database bottlenecks, but even application ones. Every change can have unforseen and huge waves of impact until it reaches the faraway lands of code folders.
- For the ability to even understand the application : since there are many side effects, deep couplage, unwritten dependencies, all is brittle.

In my opinion it can be even harder to change than solving technical challenges. First, it is difficult to simply realize the presence of the holistic antipattern. Afterall it's the after effect of an uncounsious desire (for perfection), so it is never acted, or discussed. Secondly, it often leads to breaking changes or challenging existing product visions since an holistic pattern offers a more "complete" user experience.

Once detected, moving out of the antipattern can be really painful : solving it is not a technical show (like let's rewrite it in xxx language a-la-mode, move to NSA-level datastore, etc) but potentially impacts existing features (or even require to remove them). This demands to refocus to the core, to rediscuss the existing. It can be painful : developer opinion is sometime unwelcomed on this subject (they look like they talk about product, not their technical craft) and this involves debates/hot discussions. This one is problematic, most people would rather refactor a whole application than do a one hour long heated meeting.

It also requires to be always on guard, since this state can simply be reached by *fixing problems*. So you're building the antipattern, but in your everyday life you have the impression to move forward, to add this sweet new button, etc. And one day you look back and you realize that now it takes 6 months to add a feature. Or that users get lost in your product. Or simply that you watch [this video](https://www.youtube.com/watch?v=y8OnoxKotPQ) 10 times a day. Or the new developers do not even understand the current flows and their potential impacts.

Some could say that this antipattern is just the pattern of a product gaining in complexity with time. I disagree : it is more difficult to do simple things than complex ones. A well done application shows how well maintainers have identified and abstracted problems. It offers a simple and straitforward way to help users. It does not propose many things, hoping one of them will be useful, because it already knows which ones are and which ones aren't. Being opiniated saves us from the holistic antipattern.

What do you think ?

[1] Like in every science, the myth of the lone problem solver/genius is still very pregnant but do not match the fact that the complexity of modern day problems require many people. No single brain can hold all the information nowadays. Articles are often signed by one researcher but hide that many poor PhD students were exploited to get it to complexion or that the article foundation themselves were explored by others.

[2] I wonder how much this dream of an overeaching/omnipotent application is a lingering effect of our monoteist culture of having this one thing that covers everything.

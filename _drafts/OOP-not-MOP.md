---
layout: post
title: "OOP, not MOP"
categories: ruby
---

Even tho today all of the fury is around functional programming -Object Oriented Programming can totally be used in functional languages-, I want to discuss a pattern that I saw in almost all projects I was involved with : Module Oriented Programming (MOP).

As its name implies, MOP is very nice to wash tiles, not so much to design applications. This pattern is officially dying, but I saw it come back in very unespected ways, mostly around misconceptions on what is beautiful OOP.

At the start, MOP was OOP for lazy people.
People didn't want to copy paste 5 lines of code because else they felt like they would be dirtying their craft, so instead they created modules.
Fools, little did they knew than copy-pasting was life and love and a very nice way of solving problems.
If I could copy-paste in real life I would use it all the time, but for strange reasons it was a shameful act in the development world.

In the DRY, factorizing dogma, one repeated line of code was proof of mediocrity. It led up to [infinites package lists](https://www.npmjs.com/package/istrue), all for the sake of NEVER duplicating/recoding anything.

It also allowed for half-baked design. Two flows share some behavior ? Let's copy paste the two underlying methods in a module and tada, we have a fully fledged architecture!
Most of the timne it smells like we have some missed abstraction, an objet that want to live, a concept that need clarification. Instead we share code.

It's what annoy the most in this notion : sharing code and methods (what modules allow) does not mean classes will share concepts or behavior.
Often these two different scenario mix each other and we end up with factorized code for unrelated objects. Later on, it makes refactoring really painful because with time :
- the module ends up having custom code to support edge cases that should have been a warning the module itself should not be there.
- the module ()


Instead of taking thew time of extracting and modelling the underlying object, why not simply copy paste the shared methods


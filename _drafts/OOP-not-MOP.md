---
layout: post
title: "OOP, not MOP"
categories: ruby
---

Warning : we'll be talking about ruby modules, not DDD ones.

Even though today all the fury is around functional programming -Object Oriented Programming can totally be used in functional languages-, I want to discuss a pattern that I saw in almost all projects I was involved with : Module Oriented Programming (MOP).

As its name implies, MOP is very nice to wash tiles, not so much to design applications. This pattern is officially dying, but I saw it come back in very unespected ways, mostly around misconceptions on what is beautiful OOP.

At the start, MOP was OOP for lazy people.
People didn't want to copy paste 5 lines of code, it would dirty their craft, so instead they created modules.
Fools, little did they know that copy-pasting was life and love and a very nice way of solving problems.
If I could copy-paste in real life I would use it all the time, but for strange reasons it is a shameful act in the development world.

In the DRY, factorizing dogma, one repeated line of code was proof of mediocrity. It led to [infinites package lists](https://www.npmjs.com/package/istrue), all for the sake of NEVER duplicating/recoding anything.

It also allowed for half-baked design. Two flows share some behavior ? Let's copy paste the two underlying methods in a module and tada, we have a fully fledged architecture!
Does it smell like we missed some abstraction ? An objet that want to live ? A concept that need clarification ? No no no, it is better to share code.

It's what annoy me the most in this notion : sharing code and methods (what modules allow) does not mean classes will share concepts or behavior.
Often these two different scenarios mix each other and we end up with factorized code for unrelated objects. Later on, it makes refactoring really painful because with time :
- the module ends up having custom code to support edge cases that should have been a warning the module itself should not be there.
- the module is not testable by itself, which is equivalent to : nobody can understand the module in isolation.
- the module strays further from g... from the domain.
- the module is so deeply coupled to classes (that often end up following a different method flow from each other) that it become a non euclidian blur.

You don't have time to extract and model the underlying object ? Save a module, copy paste code.
End of my TED talk.

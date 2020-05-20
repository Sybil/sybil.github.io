---
layout: post
title: "Antipattern : holistic design and scaling"
categories: ruby
---

In all my jobs scaling was always the grand goal of work. Whatever the size of the project, scaling was often an excuse to try fun technologies and refactor hated code.

It's a very easy argument to give to non-tech people.
Who doesn't want his project/enterprise to grow ?
Who does not want to feel like he has grown up problems, like Facebook/Google/etc ?

The end solution for scaling is more or less always the same : more CPU, more RAM, more processes, etc.
In the web, I felt like the bottleneck of everything was often the database, probably because these systems are stronger than anything else (like web frameworks) today. A lot a applications would crumble down without ACID (mainly atomicity) and it puts a lot of stress on the DB.

The issue with more of everything is that very often the application themselves are not designed to be scalable. But what's strange is that everywhere scaling was often a consideration from the get go. How can a dichotomy like that happen between the will and the facts ?

Because of holistic design.

---

title: "#100DaysToOffload Categorizing Code Changes"
microblog: false
guid: http://matti.micro.blog/2024/06/23/how-i-have.html
post_id: 4166632
date: 2024-06-23T00:39:00+0200
lastmod: 2024-06-23T13:34:32+0200
type: post
tags:
- "Dev Notes"
- "100DaysToOffload"
permalink: /2024/06/23/how-i-have.html
mastodon:
  id: 112662672007695088
  username: matti
  hostname: social.lol
---
In an effort to become more efficient, I wondered how I have tackled issues at work so far:

Here's a little categorization of how I approach different kinds of code changes.

(Disclosure: I don't do this literally, but intuitively ...)

First, I ask myself if the change is trivial or not. Is it just something really small and contained, like changing a constant or what is returned from a method? Or a small visual change? This is so easy that I generally only do that change and nothing else. Maybe I add a type hint or update some kind of documentation if it exists. But that's it. Hard to get more efficient here.

If the change is more complex, I subdivide this category immediately into two subtags: is it something entirely new or is it a substantial change of existing code.

What makes these two cases different is the kind of analysis (and implementation; see below) I'm doing. If it's new stuff, I try to imagine what a good, modern, sustainably maintainable version of the app or website I'm working on might be in general. What would be a good, extendable starting point? Very often the tech stack is set, but the question becomes how to use what is given in the intended/best™ way.

For example I recently was asked to implement a CRUD-App as part of the admin interface of a website. After some probing on what the appropriate tech stack might look like - since I hadn't yet done a greenfield implementation in this project - I knew what tech stack template to fill out. I decided what layers I needed, what build system to use for the frontend, how to bundle the backend code, how to test the code and how to run those tests in a pipeline on push. Some of these things were realized easily, others took longer, for some of them I had ideas for what modern best practices looked like, for others I had to research them. Because the system this crud app was a part of monolithic "portlet" system that subdivides the contents of a page into reusable widgets, we had to take this into account, even though we didn't need that much complexity. In the end, I built a relatively modern portlet-compatible crud app. While implementing the core features I learned more about the entities we were dealing with and how they connected to the rest of the website, which meant doing revisions of the main model a bunch of times and it turned out that the JavaScript module had to be relatively complex because we wanted some interactivity that I knew about but hadn't thought about hard enough beforehand. So yeah. Lots of extra work upfront to make working with this crud app nicer later and a good amount of revisions during the main implementation phase of the mvp to fulfill the architectural and quality criteria I had set for myself.

If it's a complex code change the cuts across lots of different already existing modules or classes, the question is more how we can make these classes friendlier to accept change in the future in general and how my changes could be implemented in such a way that they themselves can be changed easily. So not only the integration code but also the feature code should be extendable, readable and hopefully easier to reason about after I touched it.

Another task I had was to repair and update a multi-tenant system's copy tenant functionality. This was a complex task that cut through a big chunk of code. It was extra complex because the legacy system had some quirks you needed to know about and was very hard to test, because some of the classes were autogenerated and copying a tenant took minutes to complete. After a long and sometimes arduous process of trying to understand how the system worked and how its data was organized, I reimplemented the copy tenant functionality that had previously been based on copying its mostly hierarchical data on assumptions that didn't hold true anymore, so that it would not presume things that would lead to broken tenants, fixed a handful of bugs and unexpected behaviors on the way, but also made sure that the button "copy tenant" basically did what it did before, only now finally correctly. I'm not going to lie: I had tons of help to accomplish this herculean task and it's not humility that makes me give credit for most of the actual implementation in the end to one of my lead programmers. Big chunks of time were spent understanding the legacy code, figuring out where it went wrong and figuring out where and how to put the corrected code in a mostly non invasive way.

So both kinds of complex change consisted of chunks of implementation and blocks of analysis. Both types had some work that was extra in some way. So let's look at the details of that.

The implementation of new software consists of creating lots of new files, folders and "hooks" that connect the new to the old. We can always immediately work within best practices: Clear separation of concerns, no spaghetti code, native type hints throughout and tests from the start to name just a few.

Implementation blocks in already existing code of varying degrees of decay is different. We talk about refactoring and just making a sensible "hole", for us to fill with new features. We may need to change what a method returns, introduce a new service, rework an existing class, by adding properties, methods or making it conform to a new interface to make it more easily replaceable, change were business logic is located, accessed, or what it decides in what way. There are many ways to work with existing code. Some of them are about making the aforementioned hole for our new logic and some of them are about making it easier to comprehend the legacy code. I have yet to work in a project that actually took the time to do systematic refactoring that goes beyond just making a thing work. It's all rather piecemeal.

The analysis parts are also pretty different: The new stuff consists mostly of understanding the modern best practices in the context of the concrete implementation I'm supposed to do. How does Vite want me to work? How does a modern Symfony bundle look? Should models have fluent setters/getters? Should models be immutable? Many of these kinds of questions are about how to bring ideal conditions into my concrete implementation. On top of best practice questions are questions about how things work. Like Vite for example. It took me some time to figure out how Vite's library mode actually worked. How Vitest worked. How and why modern Symfony bundle practices wouldn't work within the context of our legacy system, etc. The last example is also a good example of how we have to figure out how these best practices and technology options out there in the world actually map onto our concrete case. Because sometimes they don't and we have to figure what that means for the project.

Analysis of old code often means just groking what it does and how it can be changed. If you know nothing like I did when I started working on the copy tenant functionality you may need to figure out the bigger picture as well as the details of the thing you're actually supposed to change. This has many dimensions to it. From guessing intentions of programmers that came before me, over parsing of algorithms and business logic, following call stacks and simply figuring out where to look to understanding the data that flows through a given system, there is always a lot going on.

When it comes to complex changes especially, but also trivial ones can exhibit this, there is always an amount of extra work involved. This extra work might be part of the analysis blocks or part of the implementation blocks.

This extra work could be adding a code quality tool. Or it could be cleaning up a a method, while making sense of it. Or it could be taking the time to really get into understanding the details of how validation is done. Some of this extra work makes essential work easier. Most of it makes the essential work more fun, I find.

Analyzed like this it becomes more clear to me, that part of my problem of being inefficient is that I enjoy the extra work and that I am kind of stubbornly hoping when embarking on a new programming adventure that the extra work could be my main work. In other words: I am behaving irrationally!

Going forward I'll have to limit the amount of extra work I do (e.g. less fucking around). That has to be part of the solution. Another point is that figuring out what to do and not fucking around and explore has been traditionally hard for me. I think (hope) that writing things down in a composable way using my trusty notes system will help me figuring out things faster, since I will be able to rediscover what I already figured out before.

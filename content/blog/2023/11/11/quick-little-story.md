---

microblog: true
guid: http://matti.micro.blog/2023/11/11/quick-little-story.html
post_id: 3690451
date: 2023-11-11T14:24:14+0200
lastmod: 2023-11-11T14:24:14+0200
type: post
categories:
- "Memories"
- "Dev Notes"
permalink: /2023/11/11/quick-little-story.html
mastodon:
  id: 111391896980262047
  username: matti
  hostname: social.lol
---
Quick little story: I was working on a relatively big task to duplicate a bunch of data in a system I barely know. Now, the biggest problem here was that the data in question was hierarchical sql data. That makes it tricky because relational tables (rows and columns) are not well suited to make it easy to traverse such trees. You could relatively easily use a migration logger functionality and click through the UI on the backend to record the sql that you need to migrate this data. But this gets messy quick and can go easily wrong. The more data you need to duplicate the more important it is that you do the right thing for an increasingly long sequence of manual actions. Also there is cleanup necessary afterwards, since the migration logger is not optimizing its lightly abstracted sql statements well. On top of that, I could not find a good interface to program my migration against either. It seemed that my options were:

1. use the UI and record the changes using the migration logger
2. write what you need using raw sql yourself


I decided to go with option 2. I found a great solution that did not require a nested set approach called a recursive common table expression. I felt like a genius. I also was sitting on my high horse, "How did no one ever come up with a good API for doing common things like: copying this entity over onto this branch? Well, I guess I have to do it myself…"

Even though progress was made to create migration helper functionality, it was slow and I had lots of questions regarding the structure of the data I was supposed to duplicate.

Yesterday my boss took 2 hours of his time to look at the problem with me. He pointed out that what I had been doing for the last three days was unnecessary. Of course, what could be done in the UI in the backend could also be accomplished programmatically. It wasn't even that hard. It had all the scaffolding for customization of the process I could have ever wanted. This will allow me to write a readable migration in a few hundred lines, with no later cleanup necessary. We solved a big chunk of my problem in no time.

I was embarrassed. Not only did I underestimate my colleagues and the maintainers before me, I also underestimated the system and its capabilities. I felt especially bad, because I thought I had done the right thing, like asking many questions and communicating with the project management why there was such a delay. I thought I was dealing with a hard problem - and in a vacuum it actually was a hard problem - but instead I just didn't know where to look or what to ask.

It's a new day and I think I take a bunch of lessons from this:

1. Ask more directly: Do not ask "Is it guaranteed that every group starts with a node that has itself no parent?", but ask "Is there an API to copy categories just like the UI has?". See also: [The XY Problem](https://xyproblem.info/).
2. Be okay with making such mistakes. I am new in the company. It is almost inevitable that I will run in circles and it may take some time before my knowledge of the system matches my level of general problem solving skills. Because I could have solved the hard problem - which is why I tackled it - I just didn't need to.
3. Accept your expertise level. As I said I am new here and at the same time I have programmed for a while so I generally know what I'm doing. This is a great recipe for falling prey to the Dunning–Kruger effect: That is overestimating one's ability in a particular context. I may be an okay problem solver, but I do not know the new system.

There is a certain inevitability to feeling a bit of shame while learning from mistakes. It's part of the journey in a field as complex as programming. I'm still learning to embrace these moments, understanding that they are not just hurdles but stepping stones towards greater expertise and confidence.

As I move forward, I remind myself to maintain a balance: to stay humble yet curious, to recognize the boundaries of my current knowledge while also questioning [established norms](https://www.snopes.com/fact-check/grandmas-cooking-secret/). This experience has taught me that becoming a better developer isn't just about accumulating knowledge, but also about the wisdom to question, to explore, and, most importantly, to learn from slightly embarrassing fumbles.

So, with these lessons in my toolkit, I am moving on - a little humbler and wiser, a bit more prepared, and as eager as ever to challenge and be challenged. After all, it's through questioning and exploring that we often find the most innovative solutions and grow beyond our imagined limits.

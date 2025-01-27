---

title: "A New Cross-Posting Workflow, Part 1: Requirements And Thoughts On Implementation"
microblog: false
guid: http://matti.micro.blog/2024/05/07/a-new-crossposting.html
post_id: 4056604
date: 2024-05-07T20:50:11+0200
lastmod: 2024-05-20T11:46:24+0200
type: post
tags:
- "Blog"
- "DailyDogo"
- "WeblogPoMo"
permalink: /2024/05/07/a-new-crossposting.html
mastodon:
  id: 112401526024764718
  username: matti
  hostname: social.lol
---
(2024-05-20 - EDIT: I have decided, that I do not have enough time to devote to this project at this time, however I would really like it and it was good to think this through for when I am able to pick it up)

You know what I don't like about my blog? The way it crossposts to other services. Micro.blog's understanding of cross-posting is as follows:

>Micro.blog cross-posting copies your posts from this feed to external services automatically when you post to your blog.

Which is not what I want. I would like it to work more in this way:

- Blog posts (with our without title) should be shared automatically on [my Mastodon account](https://social.lol/@matti) with a proper link, maybe an applicable hashtag. But it should be clear that I'm sharing a blog post, which is not the same as writing a toot and that difference shouldn't therefore be invisible by just tooting the same content 1:1 as I posted on my blog
- An exception are the [DailyDogos](/categories/dailydogo/) and other posts like it (not that there are any at the moment…). These should be shared with the image attached. Maybe there is not even a need for the link, but it would be fine if it would be there
- When I'm writing a toot, I'd like my blog to archive a copy of that toot. The archived version should include images, links and whathaveyou.

So basically there are two workflows with a couple of conditionals I would like to implement:

- Cross-Post all blog posts from my micro.blog to my mastodon (excluding posts that are archival copies of mastodon posts; denoted by being part of the category "archivalCopyOfToot")
	- if the post has a title, use the title to create a link to the post and add any applicable hashtags by converting the assigned categories of said blog post to the toot
	- if the post has no title
		- if the post has category of "tootAsIs"
			- add any images to the toot and post the contents of the blog post as is to mastodon (maybe add a link to the original on my blog)
		- if the post has no category of "tootAsIs"
			- add a short (80 Chars and up to the next full word maybe?) excerpt and otherwise behave like a titled post


I happen to have an [Echofeed](https://echofeed.app) account, which is part of the solution. I can point it at an RSS/JSON/Atom-Feed and it will post in a format I can specify to any of its supported services, which includes Mastodon and Micro.blog. It doesn't have any conditional logic, though, so I will have to provide it with feeds that only include posts that I want it to cross post.

On the micro.blog side, this is maybe [not trivial](/2023/06/18/the-hugo-template.html), but at least is possible, since micro.blog uses [Hugo](https://gohugo.io) and you can - if you know how - customize it quite a bit. I'll need three feeds:

- A feed with only title posts, excluding any posts with the category "archivalCopyOfToot"
- A feed with only non-title posts, including only those of "tootAsIs" (and excluding any from the category "archivalCopyOfToot")
- A feed with only non-title, excluding any of "tootAsIs" AND "archivalCopyOfToot"

I would then set up three echos that cross post to mastodon in the right way.

Mastodon on the other hand has [a feed of my posts](https://social.lol/@matti.rss) too, but it's much more limited and creating new custom feeds that filter posts based on e.g. a hashtag are not possible, I believe. This means that we can't filter for cross-posted blog posts and will necessarily import those items to our blog, too. I would really like to avoid having to run my own script - locally or on a server - talking to their api or whatever, so I think I'll will have to live with the fact these duplicated posts will be crossposted back to my blog…

What I can do is filter these posts out on the micro.blog side. Meaning posts that include a certain Hashtag like "crossPostByEchoFeed" (this could even be added inside Echofeed for the workflow that posts from Mastodon to MB and could be invisible to Mastodon followers) need to be excluded from the homepage, archive and any feeds of my blog (hashtags can be converted to categories using filters on micro.blog, so if I figure out how to filter by one or more categories in Hugo's template syntax, I should be fine implementing this). In that way they will be part of the blog, but they will not pollute the reading experience.

So yes. I have to set up some feeds and some logic to make undesired toots invisible but then I should be able to get what I want without the need to setup any scripts run by me.

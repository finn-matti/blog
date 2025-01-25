---

microblog: true
guid: http://matti.micro.blog/2024/04/12/buildinpublic-mbsync-it.html
post_id: 3988706
date: 2024-04-12T15:35:37+0200
lastmod: 2024-04-12T15:35:37+0200
type: post
categories:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/12/buildinpublic-mbsync-it.html
mastodon:
  id: 112258511219444931
  username: matti
  hostname: social.lol
---
#buildinpublic #mbsync It seems that I have a column in the posts table called sync_status that is `enum('pending','synced','deleted')` so it seems to me I need to set this to deleted if the file is missing, which implies that instead of iterating over the blog post files and marking the posts in the db I need to iterate over the blogposts in the db since otherwise I miss the deleted files. Does this make sense?

- Files:
  - 1
  - 2
  - 3
- Posts in DB
  - 1
  - 2
  - 3

I was checking the files against the db to find new and updated posts, but I'm now going to check the db against the files instead. I should still be able to find new/updated posts, but also posts that are missing from the filesystem.

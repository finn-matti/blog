---

microblog: true
guid: http://matti.micro.blog/2024/04/13/buildinpublic-mbsync-no.html
post_id: 3989273
date: 2024-04-13T10:36:14+0200
lastmod: 2024-04-13T10:36:14+0200
type: post
categories:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/13/buildinpublic-mbsync-no.html
mastodon:
  id: 112262996013630923
  username: matti
  hostname: social.lol
---
#buildinpublic #mbsync No tests, alright. What do we want to test here? If we call `markForSync()` a changed post, a deleted post, a new post and an unchanged post should all be detected correctly. So let's start with the simple case that a post in  the db and in the filesystem are the same.

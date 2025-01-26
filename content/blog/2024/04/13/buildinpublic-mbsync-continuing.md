---

microblog: true
guid: http://matti.micro.blog/2024/04/13/buildinpublic-mbsync-continuing.html
post_id: 3989269
date: 2024-04-13T10:31:19+0200
lastmod: 2024-04-13T10:31:19+0200
type: post
tags:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/13/buildinpublic-mbsync-continuing.html
mastodon:
  id: 112262976808448721
  username: matti
  hostname: social.lol
---
#buildinpublic #mbsync Continuing from yesterday. I will rewrite the markForSync method so it iterates over the posts in the db instead of the files to be able to detect deleted files as well. Just have to check if there are any tests to work with, or if I have to add them first.

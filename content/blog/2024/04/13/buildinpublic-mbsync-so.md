---

microblog: true
guid: http://matti.micro.blog/2024/04/13/buildinpublic-mbsync-so.html
post_id: 3989620
date: 2024-04-13T21:04:41+0200
lastmod: 2024-04-13T21:04:41+0200
type: post
categories:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/13/buildinpublic-mbsync-so.html
mastodon:
  id: 112265467384457683
  username: matti
  hostname: social.lol
---
#buildinpublic #mbsync So. Me the last few hours:

>I'm not distracted, I'm on a side quest.
— https://beige.party/@RickiTarr/112264314660393539

Where was I? Oh yes. Refactoring/Writing a test for the `markForSync` method. I have the starting point for the test, which creates a post using a factory and writes that same data to disk. Now we need to run the post through our method and see that the posts `sync_status` is not marked for creation/update/deletion.

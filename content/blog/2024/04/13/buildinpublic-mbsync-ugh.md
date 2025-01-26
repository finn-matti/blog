---

microblog: true
guid: http://matti.micro.blog/2024/04/13/buildinpublic-mbsync-ugh.html
post_id: 3989487
date: 2024-04-13T17:04:36+0200
lastmod: 2024-04-13T17:04:37+0200
type: post
tags:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/13/buildinpublic-mbsync-ugh.html
mastodon:
  id: 112264523326661792
  username: matti
  hostname: social.lol
---
#buildinpublic #mbsync Ugh. And even more problems. I use the laravel validated dto package, because I like working with DTOs and getting validation "for free" is nice. However:

If a post doesn't have a category the mb api returns an empty array. Fine. I can validate this as `'categories' => ['present', 'array'],`, but interestingly the DTOs saves this internally as null. And guess what? categories in not nullable anymore when I try to save a post with empty categories to the db. Hmpf.

---

microblog: true
guid: http://matti.micro.blog/2024/10/01/i-love-me.html
post_id: 4358098
date: 2024-10-01T13:30:11+0200
lastmod: 2024-10-01T13:30:11+0200
type: post
permalink: /2024/10/01/i-love-me.html
mastodon:
  id: 113231935374512443
  username: matti
  hostname: social.lol
---
I LOVE me some small functions/methods. For work I am implementing a class that replaces occurrences of the [German "SZ" ß/ẞ](https://en.wikipedia.org/wiki/%C3%9F). Here are some of the methods:

- replaceSz
- includesSz
- includesSmallSz
- includesBigSz

Am I going too far? 😅 I feel that "mini methods" like these make code more understandable, because you only have to grok _either_ the implementations or the composed logical blocks, but not both at the same time. Also stack traces become better and debugging is easier.

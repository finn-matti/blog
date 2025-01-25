---

microblog: true
guid: http://matti.micro.blog/2023/04/26/i-am-more.html
post_id: 2852672
date: 2023-04-26T09:29:23+0200
lastmod: 2023-04-26T09:29:23+0200
type: post
permalink: /2023/04/26/i-am-more.html
mastodon:
  id: 110263937667755889
  username: matti
  hostname: social.lol
---
I am more and more of the opinion that relying on semantic versioning conventions (e.g. using `"module": "^1.2.3",` in your package.json) is a bad idea. A convention is not a guarantee. Something like [Renovate](https://github.com/renovatebot/renovate) is safer, especially in combination with a good test suite.

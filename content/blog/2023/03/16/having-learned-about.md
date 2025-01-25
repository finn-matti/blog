---

microblog: true
guid: http://matti.micro.blog/2023/03/16/having-learned-about.html
post_id: 1835263
date: 2023-03-16T17:00:49+0200
lastmod: 2023-03-16T17:00:49+0200
type: post
permalink: /2023/03/16/having-learned-about.html
mastodon:
  id: 110033560988436389
  username: matti
  hostname: social.lol
---
Having learned about [mastodon's capabilities of being a ddos tool](https://github.com/mastodon/mastodon/issues/4486), I wonder: Are URL previews a dark pattern in itself?

I feel like you could argue they are, because they may seriously mislead you (a preview could be tailored in a malicious way), scale badly in a federated context (in the naïve case as implemented by mastodon) and responsibility for the problem is not as easily attributed. Should I as the user feel responsible?

It also shows that fundamental design decisions about software architecture are still very much a centralization problem. Or rather: They express the reality that somebody has to make a decision about these things. Having your own instance doesn't change a thing about that. If the protocol defines link previews in this way you have to follow suit in order to be compliant. No way around that.

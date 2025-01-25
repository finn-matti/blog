---

microblog: true
guid: http://matti.micro.blog/2024/04/20/after-a-lot.html
post_id: 4036064
date: 2024-04-20T20:21:35+0200
lastmod: 2024-04-20T20:21:36+0200
type: post
categories:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/20/after-a-lot.html
mastodon:
  id: 112304935523897941
  username: matti
  hostname: social.lol
---
After a lot of other stuff I'm back at it. TIL that php ENUMS are kind of hard to do assertions on in PHPUnit. `assertSame` and `assertEquals` both don't work.

What I can do though is this:

```
$this->assertSame(SyncStatus::Pending->value, $syncStatusAfter->value);
```

#buildinpublic #mbsync

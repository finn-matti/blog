---

microblog: true
guid: http://matti.micro.blog/2024/04/13/buildinpublic-mbsync-after.html
post_id: 3989316
date: 2024-04-13T12:45:01+0200
lastmod: 2024-05-15T20:23:26+0200
type: post
tags:
- "BuildInPublic"
- "mb-sync"
images:
- https://cdn.uploads.micro.blog/44388/2024/f642602c89.png
photos:
photos_with_metadata:
permalink: /2024/04/13/buildinpublic-mbsync-after.html
mastodon:
  id: 112263503856666846
  username: matti
  hostname: social.lol
---
#buildinpublic #mbsync After a late combined breakfast/lunch back at it. Still writing the testcase for storePost. I had to think about how to structure tests that rely on test data or rather needs a directory to write to. I generally like to mirror the structure of the app in my tests, so that I can find the things I need easily. I have now introduced a testData directory where I can write to/from the filesystem. It looks like this:

<img src="uploads/2024/f642602c89.png" width="600" height="290" alt="">

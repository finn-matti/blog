---

microblog: true
guid: http://matti.micro.blog/2024/04/12/buildinpublic-mbsync-alright.html
post_id: 3988685
date: 2024-04-12T15:17:32+0200
lastmod: 2024-04-12T15:17:32+0200
type: post
categories:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/12/buildinpublic-mbsync-alright.html
mastodon:
  id: 112258439958137974
  username: matti
  hostname: social.lol
---
#buildinpublic #mbsync Alright found something todo: `// TODO: mark post as deleted`

The way this app works is by downloading posts and keeping a hash in the database and also saving them to the filesystem. There is a rudimentary implementation for new and updated posts, but files that are deleted from the filesystem are not marked as deleted in the db. The db is what gets synced with mb though. So we need a field on the post that marks it as deleted, so that when we sync the next time the post can be deleted from mb.

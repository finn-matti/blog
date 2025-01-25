---

microblog: true
guid: http://matti.micro.blog/2024/04/13/buildinpublic-mbsync-alright.html
post_id: 3989666
date: 2024-04-13T22:42:14+0200
lastmod: 2024-04-13T23:28:16+0200
type: post
categories:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/13/buildinpublic-mbsync-alright.html
mastodon:
  id: 112265850957226033
  username: matti
  hostname: social.lol
---
#buildinpublic #mbsync Alright. The test for a post that is unchanged does the thing and I already created a similar test for a newly created post. However I don't like how the sync status is saved in the db. Or rather how different kinds of logic are reduced to only the sync state. We need to differentiate between the state of the sync itself (pending/synchronized/error) and what we sync (creation/update/deletion). At least I think it'd be nice to be explicit about it. Makes it more testable. So we need two fields in the db on every post:

- sync_status: pending, synchronized, error, none
- sync_intention: create, update, delete, none

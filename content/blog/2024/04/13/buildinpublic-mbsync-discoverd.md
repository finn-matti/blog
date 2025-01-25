---

microblog: true
guid: http://matti.micro.blog/2024/04/13/buildinpublic-mbsync-discoverd.html
post_id: 3989384
date: 2024-04-13T14:43:22+0200
lastmod: 2024-04-13T14:43:22+0200
type: post
categories:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/13/buildinpublic-mbsync-discoverd.html
mastodon:
  id: 112263968035277150
  username: matti
  hostname: social.lol
---
#buildinpublic #mbsync Discoverd another problem: I was allowing the categories field (json in the db) in my Post model to be null. Turns out if you do that you can't [cast that json to array](https://laracasts.com/discuss/channels/laravel/cast-to-array-not-working) through eloquent. So I changed that in my migrations, but this means that the assumption you can write a post to the db with categories being null doesn't hold anymore. So more yak shaving…

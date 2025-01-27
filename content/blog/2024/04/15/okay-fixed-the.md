---

microblog: true
guid: http://matti.micro.blog/2024/04/15/okay-fixed-the.html
post_id: 3990896
date: 2024-04-15T13:16:23+0200
lastmod: 2024-04-15T13:19:30+0200
type: post
tags:
- "Blog"
permalink: /2024/04/15/okay-fixed-the.html
mastodon:
  id: 112274950736241258
  username: matti
  hostname: social.lol
---
Okay fixed the theme next/previous links:

{% raw %}
```
{{ $cleanContentNext := .NextPage.Content | plainify }} {{ if gt (len $cleanContentNext) 20 }} {{ printf "%.20s" $cleanContentNext }} {{ else }} {{ $cleanContentNext }} {{ end }} {{ end }}
```
{% endraw %}

And the other problem seems to have been a category filter not having run through. There is no pagination, it just shows all the posts on one page. Which is fine for now.

- [Previously](/2024/04/15/my-theme-switch.html)

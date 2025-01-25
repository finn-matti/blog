---

microblog: true
guid: http://matti.micro.blog/2022/09/12/in-an-effort.html
post_id: 1664120
date: 2022-09-12T10:19:43+0200
lastmod: 2022-09-12T10:19:43+0200
type: post
categories:
- "Blog"
- "Setup"
permalink: /2022/09/12/in-an-effort.html
twitter:
  id: 1569239330111082497
  username:
---
<p>In an effort to make my blog perform better - lots of images means slow load times - I have updated all my images to use this somewhat undocumented micro.blog feature that resizes images:</p>
<blockquote>
<p>Micro.blog offers an endpoint to resize uploaded images. Once you upload the image, if you do [micro.blog/photos/](https://micro.blog/photos/#)##x/, but replace ### with the pixel width you want, followed by the full URL to the image, you’ll show an image with that width. For example, if I wanted the image at [json.blog/foo.jpg](https://json.blog/foo.jpg) to be 480px wide, I could use &lt;img src=“https://micro.blog/photos/480x/[json.blog/foo.jpg](https://json.blog/foo.jpg)”&gt;.</p>
<p><a href="https://help.micro.blog/t/optimal-image-size-resolution/427/2">@jsonbecker in the Micro.Blog Forums</a></p>
</blockquote>
<p>This first page load still takes a long while, since my home page weighs in at about 25 mb of mostly image data. But it's a start.</p>

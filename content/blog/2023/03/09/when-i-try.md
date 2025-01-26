---

microblog: true
guid: http://matti.micro.blog/2023/03/09/when-i-try.html
post_id: 1828556
date: 2023-03-09T15:00:18+0200
lastmod: 2023-03-13T11:26:03+0200
type: post
tags:
- "Dev Notes"
images:
- https://cdn.uploads.micro.blog/44388/2023/268880a450.png
- https://cdn.uploads.micro.blog/44388/2023/ceacd7f6ad.png
photos:
photos_with_metadata:
permalink: /2023/03/09/when-i-try.html
mastodon:
  id: 109993469110642554
  username: matti
  hostname: social.lol
---
When I try to figure how something works in my programming language I often use the service [replit](https://replit.com). It offers a simple bare bones php environment which is ready to go to test out some stuff, is portable and free to use.

One thing that is slightly annoying is that they only support PHP 7.4 out of the box, but it is very easy to upgrade the php version used to PHP 8. Let's start with an example:

```php
<?php
$str = "Hello, world!\n";
if (str_contains($str, 'llo')){
  echo 'YUP';
}
```

This code will not run as is on replit, because the function [str_contains](https://www.php.net/manual/en/function.str-contains) doesn't exist before PHP 8.

<img src="uploads/2023/f28919f82e.png" alt="Screen Shot 2023 03 09 at 14 39 02" title="Screen Shot 2023-03-09 at 14.39.02.png" border="0" width="599" height="490" />

So let's change that. Click the three dots in the side bar and reveal hidden files:

<img src="uploads/2023/268880a450.png" alt="Screen Shot 2023 03 09 at 14 41 39" title="Screen Shot 2023-03-09 at 14.41.39.png" border="0" width="371" height="262" />

Next, open the `replit.nix` file and change the used php version, like so:

```nix
{ pkgs }: {
  deps = [
    pkgs.php //from pkgs.php74
  ];
}
```

Without needing to do anything else we have instructed [nix](https://nixos.org) - the package and config manager underlying much of replit.com's functionality - to use the latest php package which happens to be php 8.

If we run our little test program now, it'll work:

<img src="uploads/2023/ceacd7f6ad.png" alt="Screen Shot 2023 03 09 at 14 47 10" title="Screen Shot 2023-03-09 at 14.47.10.png" border="0" width="278" height="600" />

NB: The version of nix on replit is not up to date, so trying to use `php82` to get the latest and greatest PHP Version 8.2 won't work. But php 8.0 is still better than php 7.4

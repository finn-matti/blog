---

title: "PHPStorm's keybinding system is ridiculous"
microblog: false
guid: http://matti.micro.blog/2023/07/10/phpstorms-keybinding-system.html
post_id: 3361720
date: 2023-07-10T11:52:04+0200
lastmod: 2023-07-10T18:14:07+0200
type: post
tags:
- "Setup"
- "Dev Notes"
permalink: /2023/07/10/phpstorms-keybinding-system.html
mastodon:
  id: 110689172412070191
  username: matti
  hostname: social.lol
---
It is no news that [I am pretty skeptical that PHPStorm is actually a good IDE](/2022/06/16/ide-troubles-phpstorm.html). I especially question their handling of international keyboards. You see, on an international keyboard like [the German one](https://en.wikipedia.org/wiki/German_keyboard_layout) the keyboard shortcuts `cmd + shift + 7` and `cmd + /` are virtually the same, because there is no way to type a `/` without typing `shift + 7`.[^1]

To my knowledge the only modern IDE that offers a default keymap for macOs that doesn't work out of the box with my default international keyboard is Jetbrain's offering. The reason is that some genius thought to implement key bindings without any understanding what symbols are necessarily typed by using a modifier key. So you end up with a keyboard shortcut like `cmd + /` that doesn't work in PHPStorm, but will work out of the box in VS Code.[^2]

P.S.: The problem is old btw.: [The offical issue in their bug tracker is 7(!) years old](https://youtrack.jetbrains.com/issue/IDEA-165950).

P.P.S.: Is this a hard problem? Maybe. The more interesting question to my mind is, though: Why is it a solved problem in all other IDEs? This is table stakes.

[^1]: By chance you can also type `cmd + devision symbol`, but that is not the same as a forward slash and is indeed - and this time correctly - its own shortcut in PHPStorm. Try to type that one on a keyboard without a numpad, though - which means this shortcut is useless on all(!) MacBooks - if you don't have an external keyboard attached.

[^2]: To be fair: The shortcut ends up being displayed as `shift + cmd + 7`, but at least vsc won't act like `cmd + /` and `cmd + shift + 7` are completely different key bindings (which they are not).

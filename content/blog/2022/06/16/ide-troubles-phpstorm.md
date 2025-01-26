---

title: "IDE Troubles: PHPStorm and VS Code"
microblog: false
guid: http://matti.micro.blog/2022/06/16/ide-troubles-phpstorm.html
post_id: 1599816
date: 2022-06-16T10:12:20+0200
lastmod: 2023-07-10T18:12:53+0200
type: post
tags:
- "Setup"
- "Dev Notes"
permalink: /2022/06/16/ide-troubles-phpstorm.html
---
<p>I work as a programmer for my day job. Right now I am working on two php projects. Coming from <a href="https://www.sublimetext.com">Sublime Text</a> but having had the need for more IDE features I came to love <a href="https://code.visualstudio.com">Visual Studio Code</a> and made it my home. VS Code is a great editor for PHP development, especially if you use the <a href="https://intelephense.com">Intelephense</a> extension. However, the bigger the project, the more it becomes apparent, that the performance of the language server is not <em>that</em> great.</p>
<p>I lived with this for many months now. Yesterday I started working on a new issue and thought to myself: “All of my dev team members use <a href="https://www.jetbrains.com/phpstorm/">Jetbrains PHPStorm</a>, I should give it a try.”. I had used <a href="https://www.jetbrains.com/idea/">Jetbrains Intelij Idea</a> for a brief moment a while back and only remembered being fairly unimpressed, but not exactly why I felt that way. Having now tried getting into their PHP IDE product, I have to say my impression has not really changed and now I also remember why.</p>
<p>Although the code intelligence performance is clearly better, it is the small stuff that gets me. The impetus for this post for example was that you can’t use standard shell shortcuts with the integrated terminal: <code>Control + R</code> (backwards history search) being one of my most often used commands.</p>
<p>I appreciated that they offer a keymap for people coming from Code to PHPStorm and as far as I can tell, the commands in it work. But customizing an IDE is more than just having the same default shortcuts for common tasks available in the new app. I have a bunch of my own shortcuts in code that use the pattern <code>CMD + H &lt;Key&gt;</code> (press <code>CMD + H</code> and then <code>&lt;Key&gt;</code>). I use <code>CMD + H</code>, because my last name start with H, so it was (and is) easier to remember. It just so happens that <code>CMD + H</code> is also a system wide shortcut for hiding an application. So when I tried to set up a frequently used shortcut to reveal the currently opened file in the sidebar navigation, <code>CMD + H S</code> the PHPStorm app was just hidden. In other words it did not “shadow” or override system shortcuts when asked. This feels even more arbitrary if we take those two things together: On the one hand standard shortcuts of the shell running inside the integrated terminal are shadowed per default - and this can also not be disabled -  and on the other hand wanting to shadow a system wide shortcut like <code>CMD + H</code> is not possible without remapping the shortcut within the OS. I feel like the IDE is not really playing along, but instead makes me jump through hoops.</p>
<p>These are only two compounding cuts of a thousand that make PHPStorm hard to love in my opinion. I have an especially hard time understanding the design decisions to remove long standing functionality from a shell by shadowing standard shortcuts. It’s just a bad idea. It does explain why my colleagues never use the integrated terminal, but have an extra shell window open to the side, to run terminal commands.</p>
<p>All in all I am very unimpressed by PHPStorm, but also worried: If the performance of Intelephense stays as bad much longer, I might have to look at other options. I know that Netbeans and Eclipse also have PHP features, I just don’t know anyone using, let alone loving these apps for PHP development…</p>

[Forward.](https://blog.martin-haehnel.de/2023/07/10/phpstorms-keybinding-system.html)

---

title: "Using rdfind To Deduplicate Obsidian Dropbox Backups"
microblog: false
guid: http://matti.micro.blog/2022/02/27/using-rdfind-to.html
post_id: 1518601
date: 2022-02-27T19:34:00+0200
lastmod: 2022-03-01T08:39:15+0200
type: post
categories:
- "Obsidian Tips"
images:
- https://cdn.uploads.micro.blog/44388/2022/a3023456cb.png
photos:
photos_with_metadata:
permalink: /2022/02/27/using-rdfind-to.html
---
*EDIT 2022-03-01: The following still works but I can't recommend using the aut-o-backups plugin. Its lack of features and configurability really makes it unusable for any real-world use-cases.*

This might be of interest for anyone who is using the [aut-o-backups](https://github.com/ryanpcmcquen/obsidian-dropbox-backups) plugin to automatically backup their [Obsidian](https://blog.martin-haehnel.de/2022/02/27/good-apps-obsidian.html) vault to Dropbox. The plugin is [intentionally](https://github.com/ryanpcmcquen/obsidian-dropbox-backups/issues/6#issuecomment-868897394) leaving out a lot of the complexity that is normally involved in dealing with backups, like pruning (only keep x backups) and deduplication. This post is about the latter.

The tool [rdfind](https://github.com/pauldreik/rdfind) can be used to deduplicate the backups and in so doing safe A LOT of storage (especially if you have included binary files like images).

[Dropbox is able to follow symlinks (or soft links)](https://askubuntu.com/questions/756308/does-dropbox-sync-hardlinks) so it's possible to deduplicate the created backups by converting duplicate files into symlinks pointing to only one file.

The following has been tested and is used on a Mac.

(**Please make a backup of your backups before attempting any of this!**)

1. Open the terminal
2. Install rdfind with [Homebrew](https://brew.sh) if you haven't done so already: `brew install rdfind`
3. Navigate to your backups folder: `cd ~/Dropbox/Apps/Obsidian\ Backups`
4. Run rdfind: `rdfind -makesymlinks true .`

You will get output looking similar to this:

```
rdfind -makesymlinks true .
Now scanning ".", found 2475 files.
Now have 2475 files in total.
Removed 0 files due to nonunique device and inode.
Total size is 467948959 bytes or 446 MiB
Removed 13 files due to unique sizes from list. 2462 files left.
Now eliminating candidates based on first bytes: removed 10 files from list. 2452 files left.
Now eliminating candidates based on last bytes: removed 0 files from list. 2452 files left.
Now eliminating candidates based on sha1 checksum: removed 2 files from list. 2450 files left.
It seems like you have 2450 files that are not unique
Totally, 223 MiB can be reduced.
Now making results file results.txt
Now making symbolic links. creating
Making 1406 links.
```

This can be run on regular intervals (once an hour or so) to deduplicate your backups. I use [Keyboard Maestro](https://www.keyboardmaestro.com) for this:

![](/media/uploads/2022/a3023456cb.png)

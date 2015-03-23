---
layout: post
title: Using Git dude with Growl on Mac OS X
---

[Git dude][dude] is an awesome little shell script that monitors the
repositories installed on your local development environment and then notifies
you when your colleagues make commits and push to remote.

To set up nice integration into Mac OS X with [Growl][growl], a global
notification system and pop-up notification implementation for the Mac OS X and
Windows operating systems.

To use git dude with Growl, you'll to install the Growl Extra plugin called
*Growlnotify*, which can be installed with [Homebrew][homebrew].

    $ brew install growlnotify
    $ brew install https://raw.github.com/gist/1289314/git-dude.rb

To have git-dude start tracking your repositories you simply need to create a
folder `~/.git-dude`  which contains a symbolic link to each repository you
want to track.

    $ mkdir .git-dude
    $ cd .git-dude
    $ ln -s ~/path/to/repository1
    $ ln -s ~/path/to/repository2


[dude]: https://github.com/sickill/git-dude
[growl]: http://growl.info/

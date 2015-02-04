---
layout: post
title: "Using Dropbox to sync Sublime Text across devices"
description: ""
category: ""
tags: [tutorial, how-to, sublime text, symlink, dropbox]
---

### Disclaimer

There are many good tutorials available out there. This is my own tutorial based on my own experience. If there are mistakes please do comment below and let me know.

## Problem statement

[Sublime Text 3][1] had been my favourite text editor since [my cousin][2] introduced it to me and for all those who uses Sublime for quite a while now would know the existence of [Package Control for Sublime][3] where you can install plugins, themes and such to enchance Sublime Text.

Now, the annoying part of this is when you have multiple devices that you use for coding. For every devices using Sublime Text you need to install the same plugins over and over again. Wouldn't it be nice if you could just install at 1 device and then every other devices will get the same update? I will show you how I do it (with reference from online of course).

## Important notes

To avoid disaster, you should exit Sublime Text before proceeding.

Remember, other than Sublime Text 3, you need 2 more things to make this work.

![Symbolic Link][5]
1. [Symbolic Link][4] (your OS most likely have it)
2. [Dropbox][6] (or something similar but I've only tried it with Dropbox so far)

Also, you will need to first understand where the packages are located for Sublime Text 3.

In sublime, go to Preferences -> Browse Packages... and it will lead you to where your packages are located. Since I'm using Linux, mine is at

` ~/.config/sublime-text-3/ `

and the 2 folders that we are going to sync are `Installed Packages` and `Packages` located there.

Also you need to decide where are you going to sync the packages in Dropbox. Mine I placed it in

` Dropbox/ST3/ `

It's entirely up to you to create a directory in Dropbox to sync those packages.

## Let's get started

It's basically just a few simple steps.

1. Create a directory in Dropbox for where you're going to sync the packages.
2. Move your `Installed Packages` and `Packages` folders to the Dropbox directory.
3. Create a symbolic link from your Sublime Text packages directory to link to the new directory in Dropbox.
4. ??
5. Profit.

Now everytime you install or remove a package it will all happen in Dropbox, thus synced.

Now in other devices, to sync with dropbox, delete your `Installed Packages` folder and `Packages` folder and repeat step 3. Viola !

Below are the commands to run to make all this magic happen on my PC.

{% highlight bash %}
# Create a soft link that points to Dropbox at sublime text 3 folder
ln -s ~/Dropbox/ST3/Installed\ Packages ~/.config/sublime-text-3/
ln -s ~/Dropbox/ST3/Packages ~/.config/sublime-text-3/
{% endhighlight %}

If you're in Windows...

{% highlight bash %}
# Change directory to sublime's packages directory
cd "C:\path\to\sublime text packages"

# Creates a soft link named Packages and point it to Dropbox
mklink /D "Packages" "C:\path\to\Dropbox\ST3\Packages"

# Creates a soft link named Installed Packages and point it to Dropbox
mklink /D "Installed Packages" "C:\path\to\Dropbox\ST3\Installed Packages"
{% endhighlight %}



If you now check your sublime text directory you will see the 2 folders `Installed Packages` and `Packages` there and when you access it, it will be in your Dropbox folder! It's like a shortcut but better. *A magical shortcut!*

I hope this helps open your mind to the possibilities of symlinking. I did a few hacks myself with it.

## References

For more similar tutorials, here's a few links:

- [Syncing Sublime Text 2 Settings via Dropbox][7]
- [Sync Sublime Text 3 settings with Dropbox][8]

[1]: http://www.sublimetext.com/ "Sublime Text Editor"
[2]: http://elijames.org/ "Eli James"
[3]: https://sublime.wbond.net/ "Package Control for Sublime"
[4]: http://en.wikipedia.org/wiki/Symbolic_link "Symlink"
[5]: /assets/img/2014-01-18/Symbolic_Link.png "Symbolic Link :P"
[6]: https://db.tt/qCezKKw "Dropbox"
[7]: http://misfoc.us/post/18018400006/syncing-sublime-text-2-settings-via-dropbox "misfoc.us"
[8]: http://www.alexconrad.org/2013/07/sync-sublime-text-3-settings-with.html "Alex Conrad"

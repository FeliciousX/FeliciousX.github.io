---
layout: "post"
title: "Use your PC as a router for your Raspberry Pi to go Online"
description: "Having trouble setting up your Raspberry Pi's connection? Just use your PC's connection!"
category: "Tutorial"
tags: [tutorial, raspberry pi, linux, networking]
---

I was inspired to write this article because [my friend, Eshan][1] told me about how Engineering students from
[my university][2] have been suffering from not being able to go Online with their Raspberry Pi in campus. 
I hope this article would help future Swinburne students with their Pi network problem. :)

If the following condition applies to you, you should definitely read on.

- Your PC is running *Linux*.
- You want to connect your Raspberry Pi to the internet.
- You can't go online because you don't have direct access / physical access to the router.
- You are on a network behind proxy and it's troublesome to set it up on your Pi.
- You have an extra LAN Port on your PC that you can use to connect to the Raspberry Pi.

## Note

If your PC is running Windows, I'm sorry but this tutorial does not cover how to make it work with Windows.
It's because I have not yet tried making my laptop as a router on Windows. Sorry :(

But if you do know how to make it work with Windows, let us know on the comments below :)

## Environment

First, allow me to clarify a few things.

In this tutorial, my Raspberry Pi is running [Arch Linux ARM][3] but your setup shouldn't matter. Any OS would work fine
as long as DHCP is installed and enabled, which most OS have it enabled default.

Now, here's the important bit. My laptop is running [Arch Linux][4]. Any Linux distro should be fine but Windows won't work
with this tutorial. Working with different distro? You just have to find the distro specific commands when installing with your package manager.

## Requirement

1. A LAN Cable to connect from your PC to the Raspberry Pi.
2. A PC with Linux installed and an internet connection.
3. SSH installed on ur PC.

## tldr Steps

1. Install [dnsmasq][5]
2. Configure dnsmasq to assign IPs to your LAN Ports.
3. Configure your IP tables to forward all connection coming in from LAN to Internet.
4. SSH into Pi and test connection.


[1]: http://diehardofdeath.tk/
[2]: http://swinburne.edu.my
[3]: http://archlinuxarm.org/platforms/armv6/raspberry-pi
[4]: http://archlinux.org/
[5]: https://wiki.archlinux.org/index.php/Dnsmasq

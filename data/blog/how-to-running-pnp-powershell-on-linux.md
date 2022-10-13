---
date: '2022-09-23T21:51:21.726Z'
title: How to running PnP Powershell on Linux
description: is running PnP Powershell usable on linux?
tags: ['Powershell', 'guide']
summary: How to running PnP Powershell on Linux
authors: ['default']
---

Last post we went through how to install Powershell and PnP on linux, in this post we are going make it easier to use :)

So how to we start using Powershell ? Well for short commands you can always start terminal:

![Image](/static/images/assets/screenshot-from-2021-01-23-23-02-32.png)

after that we type pwsh and powershell will start:

![Image](/static/images/assets/screenshot-from-2021-01-23-23-03-09.png)

Now your regular PnP commands will work as usual :) I've tested on SharePoint online and creating a team works perfectly:

![Image](/static/images/assets/screenshot-from-2021-01-23-23-10-10.png)

But what if you want to create a script? Well ISE doesn't exist for linux or it kinda does with help from Visual studio code:

By pressing Ctrl + P we can enable ISE mode. So what is ISE mode ? exactly how it sounds :) It converts your VS Code to Powershell ISE:

![Image](/static/images/assets/screenshot-from-2021-01-23-23-14-03.png)

![Image](/static/images/assets/screenshot-from-2021-01-23-23-17-29.png)

This works was same old ISE that we are used to with some extra features like getting a description on how command works:

![Image](/static/images/assets/screenshot-from-2021-01-23-23-27-45.png)

But what if you want to go back to the regular vs code, well press Ctrl + P and select disable ISE :

![Image](/static/images/assets/screenshot-from-2021-01-23-23-31-02.png)

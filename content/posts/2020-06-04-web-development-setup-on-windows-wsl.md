---
template: post
title: Web Development Setup on Windows + WSL
slug: windows-wsl-setup
draft: true
date: 2020-06-04T09:19:14.385Z
description: This guide will help you setup WSL (Windows Subsystem for Linux)
  and a web development environment where you feel at home!
category: Web Development
tags:
  - WSL
  - Web Development
  - Windows
  - Linux
---
Linux has been the go to for web developers for as long as I can remember. I still prefer using a Linux machine for development specifically, but there are things that are just better in Windows. The most important one: **Games** 🎮

![Photo by Daniel von Appen on Unsplash](/media/daniel-von-appen-h3gagi5txmu-unsplash.jpg "Windows!")

# What is WSL?

WSL stands for Windows Subsystem for Linux. This is a completely new take on how to run Linux alongside Windows. We all have been running VMs on Windows or dual booting our systems to achieve this. But both of the above have there cons, for instance:

* VMs are resource heavy and don't give the same performance as a native installation, especially noticeable on the more common consumer grade hardware.
* Dual booting on the other hand doesn't allow you to run both at the same time. Also poses challenges when trying to access files of one OS from the other, let alone using programs installed across them.

Well, WSL aims at solving both the above problems and a bit more

> The Windows Subsystem for Linux lets developers run a GNU/Linux environment -- including most command-line tools, utilities, and applications -- directly on Windows, unmodified, without the overhead of a virtual machine
>
> \- Microsoft
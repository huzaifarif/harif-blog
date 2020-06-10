---
template: post
title: Setup WSL on Windows [Part 1]
slug: windows-wsl-setup
draft: false
date: 2020-06-04T09:19:14.385Z
description: This guide will help you setup WSL (Windows Subsystem for Linux)
  and a web development environment where you feel at home!
category: Productivity Hacks
tags:
  - WSL
  - Web Development
  - Windows
  - Linux
  - Productivity
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

You can read more about it [here](https://docs.microsoft.com/en-us/windows/wsl/about).

## How can I get it?

#### Prerequisites:

Well WSL is available on all editions of Windows since the Fall Creators Update. WSL2 is available on all editions starting the May 2020 update (if you haven't received it yet head to [Update Center](https://www.microsoft.com/en-us/software-download/windows10) to grab it).

#### How to enable it:

1. PowerShell:

   * Press `⊞ Win` + `X` and choose **Windows PowerShell (Admin)** to open a PowerShell window with elevated rights.
   * Type/Paste the following command:

     ```powershell
     Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
     ```
2. Control Panel:

   * Press `⊞ Win` to open start menu.
   * Type **Turn Windows features on or off**

     ![Search and choose "Turn Windows features on or off"](/media/wsl-start-menu.png)
   * In the window that opens scroll down and select the item **Windows Subsystem for Linux**

     ![Select check box next to Windows Subsystem for Linux](/media/wsl-turn-on-feature.png)

   And that's it, you have enabled WSL 🎉

#### Linux means Distros right?

> UPDATE: If you want to try WSL 2 please head on to [Upgrade to WSL 2](#upgrade-to-wsl-2) section below than come back here and follow the next steps.
>
> Alternatively in the Windows PowerShell run `wsl --set-default-version 2` before proceeding.

Well, yeah! Now that we have enabled WSL lets head on to the Microsoft Store to grab one of the available distributions. Yes you heard that right. We'll be downloading Linux distribution just like any other app from the Microsoft Store!

* Open the Microsoft Store and search for **WSL**

  ![WSL Distros available on Microsoft Store](/media/ms-store-wsl.png)
* Select one of your liking. For this tutorial we'll be using the **[Ubuntu](https://www.microsoft.com/store/productId/9NBLGGH4MSV6)** distribution from Canonical.

  ![Selecting and installing Ubuntu distribution from the Microsoft Store](/media/ubuntu-ms-store.png)
* Once installed, we'll have an **Ubuntu** app installed and accessible just like any other app from the Start Menu or a desktop icon or pinned to Task Bar.

  ![Ubuntu app visible in Start Menu](/media/ubuntu-app-start.png)
* On launching it the first time it will install all dependencies and other stuff required for the distribution to work. Once done we'll have a fully functional Linux terminal at our disposal inside of Windows. Bye bye Cygwin and Git Bash.

  You'll have to setup admin user and password for Linux.

  ![Ubuntu bash on Windows](/media/ubuntu-bash-setup.webp)

## WSL 1 vs. WSL 2

Now that we have WSL enabled and our distribution setup we can either choose to stay with WSL 1 or upgrade it to use the newly released WSL 2.

#### WSL 2 Improvements

WSL 1 was powered by Linux binary translation layer whereas WSL 2 is powered by a full fledged Linux kernel running on the Hyper-V technology. Hence Hyper-V support is a prerequisite to move to WSL 2.

WSL 2 also brings significant increase in file system performance, as well as adds full system call compatibility.

You can read more about WSL 2 [here](https://docs.microsoft.com/en-us/windows/wsl/about#what-is-wsl-2) and comparison with WSL 1 and other caveats [here](https://docs.microsoft.com/en-us/windows/wsl/compare-versions).

#### Upgrade to WSL 2

* Enable the **Virtual Machine Platform** feature:

  ```powershell
  dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
  ```
* List currently installed Linux distributions:

  ```powershell
  wsl -l -v
  ```
* Choose the Linux distribution (Ubuntu in our case) and set the new version number to be used (2 in our case):

  ```powershell
  wsl --set-version Ubuntu 2
  ```

  PS: If the above command says you need to update your Linux Kernel [click here](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi) to download and install the Kernel update (for 64-bit) and re-run the above command or head on to [this page](https://docs.microsoft.com/en-us/windows/wsl/wsl2-kernel) for more information.

  PPS: This may take quite a bit of time depending on how big the Linux distribution is as it converts the entire file system to EXT4 and copies everything over there.
* If we want to make all future Linux distributions to default to WSL 2 we can set it like:

  ```powershell
  wsl --set-default-version 2
  ```

Well this is all for Part 1 of this series. In the next part we'll make Ubuntu much more functional by:

* OMZsh + Windows Terminal 💻
* Fix pathetic directory colors 🎨
* Install and setup VSCode to work with WSL ⚔
* Work with Linux GUI apps 👓

[Part 2 is live!](https://huzaifarif.dev/posts/spice-up-wsl)
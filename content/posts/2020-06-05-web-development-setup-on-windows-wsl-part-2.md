---
template: post
title: Setup WSL on Windows [Part 2]
slug: spice-up-wsl
draft: true
date: 2020-06-05T10:20:07.462Z
description: Once we've setup WSL let's get started to tweak it to serve us best
  and some productivity hacks to the bare bones Linux terminal.
category: Productivity Hacks
tags:
  - WSL
  - Web Development
  - Windows
  - Linux
---
If you haven't read [Part 1](https://huzaifarif.dev/posts/windows-wsl-setup) of the series or don't have WSL installed yet please read that first, I'll be waiting for you here!

![Photo by Kreeson Naraidoo on Unsplash](/media/kreeson-naraidoo-hqrrawhhu5w-unsplash.jpg "Let's jazz it up!")

Now that we've already setup the basic Ubuntu terminal on WSL it looks, well, pretty darn unpleasant. There are a couple of things which look pretty out of place the most obvious ones are the default fonts and the directory colors, yuk!

So let's start customizing it to make it look as sleek as possible.

## Installing Oh My Zsh!

Well most of you must be familiar with the Z shell already. If you haven't heard about it this is a shell replacement for bash which comes with handy plugins to ease our most common workflows, custom aliases and pretty themes.

1. Install Z shell:

   ```
   sudo apt install zsh
   ```
2. Make it your default shell:

   ```
   chsh -s $(which zsh)
   ```
3. Install Oh My Zsh:

   ```
   sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
   ```

Now restart your Ubuntu shell to be greeted with the Oh My Zsh terminal.

You can change the theme to your liking by editing the `~/.zshrc` file:

1. ```
   nano ~/.zshrc
   ```
2. ```
   # Find and change this
   ZSH_THEME="robbyrussell"

   # To this or any of the many themes found here: https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
   ZSH_THEME="agnoster"
   ```

You'll notice one thing, that for some of the fonts are all messed up now. Don't worry we'll fix those in the next step.

## Installing Powerline Fonts

1. ```
   git clone https://github.com/powerline/fonts.git
   ```

   Make sure to clone this to a Windows directory under `/mnt/` as we need to execute the PowerShell script on Windows.
2. Start a PowerShell instance as Administrator and execute the following script to install all the Powerline fonts:

   ```
   .\install.ps1
   ```

## Fix directory colors

You must have notices by now if you started using the Ubuntu bash that the directory colors are just awful. We'll be using the Solarized color palette from [here](https://github.com/seebi/dircolors-solarized).

1. Choose the one that suits you.
2. Fetch the chosen directory colors to directory on the Ubuntu file system.

   ```
   # using dircolors.ansi-dark
   curl https://raw.githubusercontent.com/seebi/dircolors-solarized/master/dircolors.ansi-dark --output ~/.dircolors
   ```
3. Update `~/.zshrc` by adding the following lines to use the directory colors

   ```
   ## set colors for LS_COLORS
   eval `dircolors ~/.dircolors`
   ```

## Configure VS Code to work with WSL

Microsoft has provided a pretty cool integration for VS Code to access files on WSL.

1. Install VS Code on Windows. Make sure to **Select Additional Tasks** during installation, and be sure to check the **Add to PATH** option so you can easily open a folder in WSL using the `code` command.
2. Install the [Remote Development extension pack](https://aka.ms/vscode-remote/download/extension) or just the [Remote WSL extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl).

   ![Install Remote WSL Extension](/media/remote-wsl-extension.png)
3. Now we'll edit the `~/.zshrc` file to allow us open WSL files in explorer and also to redirect output of the `code` command to not block the terminal instance while its running.

   ```
   nano ~/.zshrc
   ```

   Add the following lines

   ```
   # User configuration

   # Hide the user and computer name in our prompt
   DEFAULT_USER=$USER

   # Alias to open explorer in the current directory, returning true to override explorer's failure
   alias e.="explorer.exe . || true"
   https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl
   # Alias to open visual studio code and blackhole its output
   alias c.="code . > /dev/null"

   # Function to delegate to Windows to open each of its arguments
   start() {
       for file in "$@"
       do
           cmd.exe /C "$file"
       done
   }

   # File-based tab completion for the start function above
   compdef _files start
   ```

## Useful Oh My Zsh Plugins

There is a huge and ever growing list of Oh My Zsh plugins. Here I'll list a few of the very useful ones which I've been using everyday to increase my productivity.

1. [git](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git)

   Provides a handful of aliases and functions for normal git commands we use everyday.
2. [z](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/z)

   Easily jump around in the file system using indexed history without having to type in full directory paths.
3. [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

   Enable syntax highlighting in Ubuntu shell.

   ```
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```
4. [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

   This plugin adds suggestions to your commands as you type them based on history and completions.

   ```
   git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
   ```
5. Finally add all the above to `~/.zshrc` plugins list:

   ```
   plugins=(
       ...
       git
       z
       zsh-syntax-highlighting
       zsh-autosuggestions
   )
   ```

PS: You can find a full list of official plugins [here](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins).

## Windows terminal

So we've setup WSL and Oh My Zsh and have been using the Ubuntu app until now. But Microsoft has a great new [open source](https://github.com/microsoft/terminal) offering: **Windows Terminal**.

It is awesome for quite a couple of reasons:

1. Can be used as a replacement for Command Prompt and PowerShell both. o
2. Has tab support for multiple different session(s). Supports simultaneous Command Prompt, PowerShell, WSL.
3. Theme support 🎨
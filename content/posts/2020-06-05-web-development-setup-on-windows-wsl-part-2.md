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

## Installing PowerLine Fonts
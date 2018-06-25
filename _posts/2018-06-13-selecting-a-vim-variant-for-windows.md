---
layout: post
title: Selecting a Vim Variant for Windows
tags:
- vim
- gvim
- javascript
- typescript
- angular
- golang
- c#
- windows
---

I have started to use vim since a few months ago for all of the languages I use on my day to day development. On retrospective of good outcomes I hope to write a series of posts about **how to setup your own vim configuration**.

This first post focuses on selecting a vim variant for windows.

![gvim on windows]({{ site.baseurl }}/images/2018-06-26/gvim_typescript.jpg "Gvim Editing Angular on Windows")

Background
==========

Around year 2000 I used *vim* for a short period of a time. I had a computer with no internet access and learning *vi* was a good way to spend time learning something. This changed when I started working in the real world. Got much easier to work with an IDE with a mature tools echo system. 

Recently though, on an IoT project, I had work on Raspberry Pis a lot. Mainly with Raspbian Lite (with no UI). I had to brush up my vim knowledge. Upon googling a few things I was amazed how far the vim eco system had grown. Such learning changed my IDE from Visual Studio + Visual Studio Code to **vim**for **golang, C#, TypeScript, Angular, HTML, SCSS **and so on. 

So I thought I'd share what I learned with you, most probably in a few posts (not sure how many it will be though :) )


Selecting Between Many Vim Versions
-----------------------------------

Unlike back then there are many vim versions available now. 

- **vim** : the console vim commonly used on unix systems)
- **neovim** : a fork of vim that has been improved with a few *nice to haves*
- **gvim** : a gui wrapper around vim to treat it as a windows application, for windows. 
- **macvim**: a gui wrapper around vim to treat it as a mac application.

Depending on your OS of choice, you'd have 3 variants to select from. For windows it's vim, neovim and gvim.


Minimum Acceptable Requirements
-------------------------------

I have a minimum set of functional & non-functional requirements for my vim configuration. 

- **Performance**: no matter what features are in, it's gotta serve the performance of an editor.
- **Ability to add language support**: for Typescript, javascript, golang and C#
- **Ability to share windows clipboard** (a vim in WSL cannot share windows clipboard): This one is very crucial for me having to copy paste things back and forth between host and vim
- **Fuzzy file finder**: both installing and performance of the two variants **command-t** and **ctrlp** is different depending on the vim version.


I have installed all different variants on both Windows and Mac, **for windows my choice finally is gvim**. If you have used gvim, I can imagine your thought right now. Gvim is definitely not sexy when you first install it. But you can configure it to be :)

Let me justify, vim on command line, weather on windows bash, WSL (Windows Subsystem for Linux) or Command Line was not performant enough to work on project of considerable size. Lagged a lot.

Neovim, suffered from the same problem. In both there's also no way to use a different font from the command line font.

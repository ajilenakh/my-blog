---
date: 2025-01-18
description: "this is it"
image: "static/images/avatar.webp"
lastmod: 2025-01-18
showTableOfContents: True
tags: ["linux",]
title: "Linux Boot Process & File System"
type: "post"
---

## Introduction

I am doing a introduction to linux course over at  [Linux_Foundation](https://www.linuxfoundation.org/) today i learndrned about the boot process of linux and the filesystem of linux machines.

In short linux boot goes from  power on then the bios after with the bootloader starts and it calls the iniramfs(it is a file system image that contains programs and binary files that perfirn akk actuons nned to mount proper root fulesystem) and thats how the linux starts i wll go indepth about it later in the blog

The linux file system well in linux there is no concept of drives everythig is under a hyrarchy accounding to the lay caaled filesystem hierarchy ![this](static/images/cicd/cicd.png)
---
layout: post
title: My Very Personal T440p Arch Linux Installation Guide
date: 2024-05-04 20:45:00 +0800
category: Tutorial
tags: [tutorial]
---
I've been using macOS for pretty much 6 years now, and Windows since I was at the young age. In between I've always been curious about Linux but never really seriously learn or actually using them on a daily basis, until recently with me hosting Minecraft Server, I decided to use Ubuntu as the system and hosted Minecraft server on it. But for my secondary laptop, ThinkPad T440p. I've decided to go with something that's technically more suitable for more experienced Linux users, which is Arch Linux.

I decided to write this guide to myself to memorize things I did during the installation, pretty much everyone who used Arch just tell people to follow the Arch Wiki instead, it's actually a really good and detailed guide but it only covers the very basics, so I've decided to gather up stuffs that I've searched through the internet and make my own "customized" guide that hopefully could also help others to install Arch Linux with DE, I'll be using KDE in this guide but I'll also write a guide for XFCE too, not to mention I was originally going to use XFCE as my DE of choices but because of how it's actually not so suitable for laptop usages with its power management settings, I decided to switch to KDE instead. But I'll also include XFCE guide since I still think it's a really good and lightweight DE to use, but KDE is actually way more feature rich than XFCE. But in the end, just pick what you preferred. :)


## Basic Installation

### • Prerequisite
Bootable Arch Install USB ([Download Link](https://archlinux.org/download/)), I used [Ventoy](https://www.ventoy.net/en/index.html) personally but [Rufus](https://rufus.ie/) also works too. If you don't have Windows you can also use [balenaEtcher](https://etcher.balena.io), that program is cross-platform but I personally never used it before.
 
A working internet connection, Suggest using Ethernet since nobody knows if your Wi-Fi will work after installation. In my case Wi-Fi worked when booting into Arch USB but have to install drivers after installation.

### • Get started

Check BIOS settings, although you don't need to tweak much unlike dealing with Hackintosh, but if you have Secure Boot enabled, you have to disable it beforehand because Arch USB doesn't support Secure Boot, can be setup to work with secure boot after installation if desired. But I keep it disabled since I also have Hackintosh (macOS) on the system.

#### Boot into Arch Install USB

First verify if it's boot into UEFI with this command: `cat /sys/firmware/efi/fw_platform_size`
In most cases it should return: 64. If it shows: No such file or directory. You are most likely Legacy Booted.

Check internet connection with ping command: `ping -c 3 archlinux.org`

#### Partitioning Disk

Here I'll be using fdisk to list all the disks and then use cfdisk to do the partitioning job.

Enter `fdisk -l` to list all the disks. Check the disk you wanted to install

Then type `cfdisk /dev/sdb/`

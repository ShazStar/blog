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

#### Disk Setup

Here I'll be using fdisk to list all the disks and then use cfdisk to do the partitioning job.

Enter `fdisk -l` to list all the disks. Check the disk you wanted to install, mine will be on `/dev/sdc`.

Enter cfdisk by typing `cfdisk /dev/sdc`.

You will be greeted with cfdisk's TUI interface.

In here you'll have to setup 3 partitions, for each is EFI, Swap and OS itself.

I'll install Arch on my 240GB SSD, Here's how I'll setup my partitions:
EFI - 500MB
Swap - 20GB (Depends on your RAM and usage)
Root - The rest of the remaining storages.

If you don't know how much swap you need, you can use [SwapCalc](https://pickwicksoft.github.io/swapcalc/), it's a handy tool to calculate how much swap you might need.

Now that we are ready to setup the partitions, let's get back on PC.

In cfdisk, we first select "New" and type the size as we needed. For example if I wanted to partition with the size 512MB, type `512M`, for 120GB we type `120G`.

Move to "Type" and select size type, EFI system for EFI, Linux Swap for swap, no need to adjust root partition.

After finished the prequirements, move to "Write" to write changes, we are officially done on cfdisk, Quit it.

Now we'll need to format the partitions and enable swap:

EFI: `mkfs.fat -F32 /dev/sdc1`
Root: `mkfs.ext4 /dev/sdc3`
Swap: `mkswap /dev/sdc2` -> `swapon /dev/sdc2`

Mount File Systems:

Root: `mount /dev/sdc3 /mnt`
EFI: `mount --mkdir /dev/sdc1 /mnt/boot`
Swap: `swapon /dev/sdc2`

#### Base Installation and System Configuration

Base System Installation: `pacstrap -K /mnt base linux linux-firmware`
Fstab File Generation: `genfstab -U /mnt >> /mnt/etc/fstab`
Chroot into new system: `arch-chroot /mnt`

Timezone Setup:
Change the timezone to where you are. In my case, I'll set it to Taiwan, Taipei.

Timezone Set: `ln -sf /usr/share/zoneinfo/Asia/Taipei /etc/localtime`
Generate /etc/adjtime: `hwclock --systohc`

Localization Setup:
You can use any text editor for your preferring, I'll use nano in here.

Firstly you'll have to type `/etc/locale.gen` to edit locale gen file.
Secondly uncomment (Remove #) for your locale, I will uncomment both en_US.UTF-8 and zh_TW.UTF-8 UTF-8.
Save and Exit.
Do `locale-gen`.
Add LANG into /etc/locale.conf: `echo LANG=en_US.UTF-8 > /etc/locale.conf` (I use English as my primary system language across every devices so that's why it's not zh_TW.)

Network, Hosts and Hostname config:
Replace `ShazStar-T440p-Arch` of your choice.

Set Hostname: `echo ShazStar-T440p-Arch > /etc/hostname`

Add Hosts:
`echo "127.0.0.1 localhost" >> /etc/hosts
echo "::1 localhost" >> /etc/hosts
echo "127.0.1.1 ShazStar-T440p-Arch" >> /etc/hosts`

Install & Enable NetworkManager:
`pacman -S networkmanager
systemctl enable NetworkManager`

Change root user's Password: `passwd`

Install sudo and nano:
`pacman -S sudo nano`

Add new user and give sudo permission: 
Replace `shazstar` with your username of choice.

Add new user: `useradd -mG wheel shazstar`
If you want to add new user without sudo command privileges: `useradd -m [username]`
Set Password: `passwd shazstar`

Allow Wheel Group to use Sudo Commands: 
`EDITOR=nano visudo`
Find this line `#%wheel ALL=(ALL) ALL` and uncomment it.
Save and Exit.







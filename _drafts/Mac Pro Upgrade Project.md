---
layout: post
title: Mac Pro 2012 Final Upgrade Project
date: 2021-04-15 14:11:00 +0800
category:
tags: []
---
Before this start: I know I already made a [video](https://www.youtube.com/watch?v=VQ36UD8g7e0&list=PLN-BUs9Cvmoq_uD8xAyjY0BTSv7a4yaSw) about it in Feb 28th, 2021. But I still want to do a write up with this so let's fucking go.

Some people know I owned a Mac Pro 2012, it's been my main computer for probably 3 years+ at this point. In between I already did CPU, GPU, Ram and Disk upgrades but it's not close to what I desired. Around the end of 2020 I finally got a chance to get all the necessery parts for the missing hardware pieces for my Mac Pro. And this is what pushed me forwarded to did this "Final" upgrade for myself.

**So...What's the parts and the plans?**

First, I'm going to swap the Wi-Fi/BT card from the stock one to Apple BCM94360CD, which will enable full Continuity feature, AirDrop 2.0 feature to it.

Second thing I'm going to add is HighPoint RocketU 1144D USB 3.0 PCI-E Card. Since the last Classic Cheese Grater Mac Pro still don't ship USB 3.0 until Trash Can Mac Pro. Gladfully because of Trash Can, this card's chipset is natively supported by macOS so it's OOB.

Lastly, on the software part I'm going to install OpenCore and do a clean Catalina Install. As I'm upgrading the hardware, it's also a good opportunity to upgrade the system too.

<img src="{{ site.baseurl }}/images/20210415/Parts.jpeg" width="300"/>

**The Fun/Pain Part, Hardwares.**

The first thing I'm going to remove is the stock AirPort card, but...Things doesn't went smoothly as always. There's a screw that are so tighten that I couldn't get it removed. Took me 2 days to get them out, and as you can see I broke the standoff, also proven that it was really stuck.


<img src="{{ site.baseurl }}/images/20210415/Original AirPort Card.jpg" width="300"/>
<img src="{{ site.baseurl }}/images/20210415/Removed.jpg" width="300"/>

Moved on to the USB 3.0 Card, the process is much easier and painless, this is also part of the reason how I liked this Mac Pro's design, you barely need to use screw driver to upgrade some components.


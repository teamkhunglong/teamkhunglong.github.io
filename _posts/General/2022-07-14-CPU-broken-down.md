---
layout: post
title: "CPU broken down"
date: 2022-07-14 10:00:00 +0100
category: general
author: minh
tags: amd asrock ryzen
---

I have this workstation for 3 years now, and this is the first time it hang me up to dry.

In case you want to know, this is my configuration:
- Mobo: **Asrock X570 Taichi**
- CPU: **Ryzen 9 3900x**
- RAM: Corsair Vengeance RGB Pro 16GB (x4)
- GPU: MSI RTX 3080Ti Ventux 3X 12GB OC
- PSU: Leadex Platinum SE 1000W (80+ Platinum)

Last Saturday, out of nowhere, the server is not responding. I tried to reboot the machine, but it stuck in the boot loop. Mainboard code `07`. The "nice" thing is that in the mainboard manual, there is no code `07`

As a normal tech savy, I tried these things:
- [x] **CMOS** - Clear CMOS. Of course, still `07`
- [x] **Peripherals** - Unplug all the cable from SSDs, HDDs, USB devices. Reboot, still `07`
- [x] **GPU** - Change the graphic card to my RX570 that I'm sure it works properly. Reboot, still `07`
- [x] **RAM** - Remove the RAMs, leave only 1 stick at the time. Reboot, still `07`
- [x] **BIOS** - Flashback to older or newer firmware. (Yes, this motherboard can flash BIOS without CPU on). No luck, still `07`
- [x] **CPU** - Reseat the CPU, new thermal paste. Reboot, still `07`
- [ ] Going to reddit and cried for help !!!!!

So there are at least 3 people like me already, with the same-*ish* configuration, annually.
- [2019-11-06 Asrock - X570 Taichi - Troubleshooting - Error Code 07](https://www.reddit.com/r/ASRock/comments/dsblsg/asrock_x570_taichi_troubleshooting_error_code_07/)
- [2020-11-20 x570 Taichi - Dr Debug code 07 - need some help with what to try next!](https://www.reddit.com/r/buildapc/comments/jxy7ux/x570_taichi_dr_debug_code_07_need_some_help_with/)
- [2021-08-12 X570 Taichi Boot Looping Error Code '07', RMA'd it, new board aaaand '07' still!](https://www.reddit.com/r/ASRock/comments/p39i48/x570_taichi_boot_looping_error_code_07_rmad_it/)

> At this point, I'm sure that the CPU is the one to blame here
{: .prompt-tip }

I was hoping that the mainboard is dead, so I can replace that bloody south-bridge chipset fan, but it's just not this case. So, I went online and bought a second-hand 5900x for replacement.

I've just received the CPU yesterday, and everything works fine now. I was surprised that the CPU died. This is the first time that a CPU failed its job.

Fun fact: I bought the 3900x around $500, and now I spent €280 for the 5900x. Surprising how technology changes!
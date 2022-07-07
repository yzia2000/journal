---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
  import Cool from '../../components/Author.astro'
title: Experience installing linux for my bro on a Dell XPS
publishDate: 4 July 2022
name: Mohammad Yousuf Minhaj Zia
value: 128
description: What are these RAID ON and AHCI shenanigans?
---

<Cool name={frontmatter.name} href="https://github.com/yzia2000" client:load />

I will keep this short. This is not a guide or set of instructions and I haven't checked the Dell XPS
version. Just know that it has an Intel i7 8550u and an NVMe drive. This is more of a reminder of
the issues I had to deal with when installing Manjaro on it for future reference.

My brother is an aspiring software engineer about to enter university life. I encouraged him to install
linux on his machine. A lot of software engineering tools are built to support linux. You will be closer
to a production server environment. Lastly, you will get exposure into fundamental concepts that Windows
abstracts you away from like syscalls, filesystems and of the like. 
The goal was to install Manjaro Plasma dual boot. Chose Manjaro because I love the Arch ecosystem with pacman
and the AUR. 

First, I shrunk the C drive to create some free space. He wasn't too happy with that but a sacrifice
has to be made. Next I disabled secureboot and tried to boot into the live iso. But whats this? Manjaro
installer complains that partition was not found to install linux on. Looking a little bit deeper,
I realized that his Dell XPS defaults to Intel Rapid Storage Technology with RAID ON in SATA Controller.
We need AHCI for linux. IRST sets aside a 32GB SSD cache, without which your drive will function
much like a regular spinning disk (correct me if I am wrong). I doubt that made a huge difference
on an NVMe though.

Turned on AHCI, rebooted into live ISO. Everything worked like a charm. Created a separate root, boot
and swap partition and finished installation. For some reason, I couldn't choose /boot instead of
/boot/efi for mountpoint of the boot partition. Weird. I prefer /boot because its easier to set up
secure boot with MokManager. Can sign the linux image easily on refind.

Dual boot complete but with some UX issues. My brother plays valorant which requires secure boot.
Plus he has to switch between the SATA Controllers every time. Thats a huge pain.

First I enabled AHCI for Windows. The solution was to enable safeboot. Select AHCI in BIOS. Then
disable safeboot. Easy peasy. Now he doesn't need to switch between SATA controllers.

Next step was to deal with secure boot. I used refind and Preloader for this because you can set it up
in a single line. I booted into MokManager and signed the loader and kernel image. Refind
also allows me to boot into Windows without it being on the same EFI partition. Great, we have
secure boot set up with an easy way to switch between Windows and Manjaro with refind.

I booted into refind. Clicked on Windows. Wait, Bitlocker encryption prevents me from booting into
Windows and asks me for recovery keys. I didn't realise that my brothers Dell XPS has device encryption
enabled. This prevents Windows from being loaded from an unauthorised bootloader (refind) even
with Preloader signed hashes. No worries, I booted into Windows without
proxying through refind, disabled device encryption. 

Final product! No need to deal with boot settings and can switch between Windows and linux
off a simple GUI with fastboot enabled, secureboot and AHCI on both Windows and linux. No
performance regressions and life is great!

Too lazy to add links to reasources as you can easily google a bunch of them to understand more.
Read the ArchWiki because its great (can find out more about refind and Preloader instructions).
This post might help someone with knowledge about these components but stuck on a step. Hope
my brother can benefit from this setup to make his learning journey easier!

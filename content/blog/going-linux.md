+++
author = ["Bruce"]
categories = ["Computers", "Rambling"]
date = 2022-02-20T18:00:00Z
description = "I tried my hand at installing Linux on top of my Windows machine. It did not go as planned. "
image = "/images/tux.jpg"
product = "https://www.redbubble.com/i/poster/Linux-vs-the-Window-by-thebruce13/102771137.LVTDI?asc=u"
tags = ["Life"]
title = "Going Linux"

+++
( [Tux modeled by Andy Cuccaro](https://sketchfab.com/3d-models/tux-157de95fa4014050a969a8361a83d366) )

With Windows 11 releasing and rejecting my computer hardware to upgrade to it, I decided to jump ship to Linux. I'd like to say it was a smooth transition..but it wasn't.

## Installing Woes

First I tried to install [Pop_OS](https://pop.system76.com/) as it has been the recent [talk of the town](https://www.youtube.com/watch?v=_Ua-d9OeUOg) only to find that it won’t work with a dual boot with Master Boot Record (MBR) that Windows requires to work. The trail that led me to this took way too long. I tried everything I could think of. At first, it told me it couldn’t write to the kernel when I was setting up the partitions. Then it would freeze 70% of the time when I got partway through the setting up accounts. Other times it wouldn’t mount my drives correctly and hang indefinitely.

Then I thought it might have something to do with my UFIE boot or Secure Boot or Legacy boot. All these things I have to set up in my BIOS and constantly restart my computer. N-O-T-H-I-N-G worked. I decided that day to just boot into Windows and take a break from it. Only to see that Windows has noticed a ton of restarts and I’m locked out of my account for two hours. UAHAHHAHHHAAAAAAAAAAA.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/13699jZW4PZdx6" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

Then it would finally, gloriously, start to install. Only to run into an error saying there was a log of the error somewhere and I could try to reinstall. This went on for days before I saw that it [doesn’t even support MBR](https://github.com/spxak1/weywot/blob/main/Pop_OS_Dual_Boot.md#31-install-pop_os-first-windows-second-easiest) and I would have to install GRUB separately so I gave up on it.

So I settled with [Ubuntu Budgie](#) because of the dock it provided off the bat, and the nicer interface compared to stock Ubuntu. I will have to mention that Ubuntu is the primary OS I’ve used outside of this experiment and the one I am most comfortable with. The only other distro I have any experience with is a non-GUI CentOS that I had to use in college for networking courses.

Pop_OS was tossed out and Ubuntu was brought in. But it took me at least a week to get to this point. I’m about ready to give up on switching to Linux.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/3XEgV9kfwLy1i" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

I still hang in there because of the success I had on an old netbook from 2014 that I recently installed [Lubuntu](#) on and it runs fantastic. Especially when you consider it only has a single-core processor and two gigs of ram. I did that experiment because the keyboard on the [ThinkPad X100e](#) is phenomenal. I was able to open up GIMP on that netbook and do photo correction. This thing had trouble opening Firefox when it was running Windows 7. If you have a low-powered laptop or computer I highly suggest nuking the hard drive (backing up stuff first of course) and installing Linux on top of it. It resurrected an excellent piece of hardware.

So, after many, many attempts to partition the drives just right and set up the OS three more days go by trying to get it to recognize my drives and install the OS. I finally get it installed and get my setup going with apps I normally use installed. I shut it down, noticing an error that gets repeated, and then force shut it down thinking nothing of it, and go to bed.

The next day I turn my Linux machine on and am ready to get to work. I notice I forgot to install Slack so I go to get it from the Snap library store and . . . I see a notification that my root drive is full, WTH. I don’t know what to do and I got work that needs to get done that day. I shut down the machine and booted into Windows to get things taken care of. On my lunch break, I nuke the partitions with Linux and try again that night.

I can’t install it. I think that it is because I had the GRUB setup thinking there is an Ubuntu installation already there. So I think I need to repair the GRUB. I end up doing that off the live USB drive with Linux and I think I’m ready to go. I get through the installer for Ubuntu Budgie easily. I got to reboot, ready to play in Linux. Aaannnd, it boots to a black screen. SON OF A-. I shut it down and call it a night.

Time to install a stock version of Ubuntu to see if that fixes the filled hard drive. I can install a [plugin to get Plank installed](https://launchpad.net/plank) so I have a good enough time with the OS. Hopefully, this doesn't have the problems I had with the other two distros. I get it on the live USB boot into it. It is installed on the computer like butter, with no hiccups. I did choose the new option “Install alongside Windows” instead of setting up my partitions manually and that probably reduced some headaches. I had to double and triple-check that it was installed to the proper partition though. Restart the computer, back to a black screen. Time to go to bed.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/GXrojV8tqhxR7ZsZeI" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

The next day I have to google what I need to do to get it past the black screen and I [come across a solution](#) to toss “nomodeset” at the end of a line in GRUB. Sweet, I toss that in there and I am in Ubuntu and everything is working great.

Turns out there is an issue with NVIDIA cards (yes, you Linux veterans we know this is an issue – part of the reason why I wanted to go with POP_OS).

I then had the bright idea that if that was so easy, I could probably do that to Ubuntu Budgie as well. So I nuked the partition one more time and install Ubuntu Budgie alongside Windows, the same way I did with stock Ubuntu. Butter.

I am in, everything is working – I apply the long-term fix from the post I saw earlier and I get all my apps to install. It is now 1 am and I have work in the morning. I shut down and see that error scrolling through my screen again – force shutdown, go to sleep.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/gU25raLP4pUu4" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

I wake up the next day ready to work, I log into Linux and WTH my disk is full again! What is going on here? I end up googling it and [finding that Syslog and kernel.log were gigs worth of error messages.]() Guess I should have paid attention when shutting down. My computer was logging an infinite loop to these files and they got huge QUICK. I did a `tail -100` of each of them into a text file inside my Document folder and deleted them. I HAVE HARD DRIVE SPACE AGAIN.

Now I needed to fix my error that was filling up my log files. I opened up the ones I made inside my Documents folder and found this error. `PCIe Bus Error: severity=Corrected, type=Physical Layer` So I google that and I see I need to [modify my GRUB file once again](#). Get that in there. Restart, no error. I am finally in the clear.

After all of that, I fstarted installing apps from the package manager and that is probably one of the nicest experiences I've had setting up my programs. Blender, GIMP, Inkscape, Krita, and VSCode were all installed without a hitch.

I also needed Slack and Zoom installed and they weren't available in the app store. But with the [snap appstore]() I simply searched for them and installed them. Little did I know at the time that I could just add that to my software manager and pulled out a step.

Bluetooth compared to Windows is far superior. A pair of Bluetooth headphones that Windows would just not recognize were picked up immediately.

Getting a printer setup on Linux wasn’t awful but if I didn’t know how to get the IP address on my HP Printer, I would have been probably out of luck. HP does offer drivers for Linux for the printers, so that was very helpful.

Setting up my Razer Cyonisa and Mamba mouse was simple with [OpenRazer](https://openrazer.github.io/), however, the GUI interfaces for them are lacking behind the official Razer Synapse. But I did get them to be lit up how I would normally have them on my Windows Machine. I don’t want all the RGB but I do want to light-up keys.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/AsGnrla1K6FN7ajonc" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

## Day One

So I finally got today one using Linux as my primary driver. It started with my dialing into my work's VPN with the provided instructions and it connected without incident.

I noticed that the network for my work remote server is running slow. Wonder if there is a better way to get in than just using smb:// in the finder. Or if it is just how they set up the server to interact with Linux. I might need to put in a ticket with IT to get it addressed. Who knows? It's Linux after all.

The speakers were crackling when watching the video. [Found this stack exchange](https://askubuntu.com/questions/405071/static-and-crackling-in-my-hdmi-audio) to get it working. Restarted and it seems to be gone.

90% of the day went without incident otherwise until I had to transfer files from an SD card promptly.

I got my wife a new SD card for her Nintendo Switch and I wanted to transfer the games and saves that were on the old SD card and she wanted to play. So I kind of was on a time crunch. So I put the SD card into the computer and it didn't mount automatically. I decided that time was of the essence and rebooted into Windows.

Instantly I felt the difference. I have too many start-up apps cuz it took a while just for it to get to a workable state. Mind you I have an SSD installed even.

After spending the day in Ubunto Budgie, Windows 10 started to feel antiquated. Still, I was able to plug in my SD card and transfer the files without any hiccups. Piece of cake.

So far it has come to the conclusion that if time isn't a factor Linux is great but fiddling with mounting an SD card to transfer files wasn't worth the effort and, even the transfer speeds are faster, Windows got this one.

## The Weekend

I didn't spend a lot of time on my computer over the weekend. I mostly was in the living room with my wife and we played games on the Nintendo Switch. I did however scan some files and work on the heading image for another post. It worked just like a computer should.

However, I couldn't access the data on my other hard drives, where I was planning on storing the files for the heading image. It kept giving me an error saying they were read-only. I had to mount and then remount the drives following [this stack exchange]().

Turns out. Linux can't write to NTFS drives...if [Windows quick boot is on](https://manpages.ubuntu.com/manpages/bionic/en/man8/mount.ntfs-3g.8.html). Once I turned that off I was able to write files to my other drives.

I haven't installed any games on my Linux partition because I'm trying to keep it to just productivity and work items.

## Wrapping it up

The post is going to start to fizzle so I'm going to wrap it up here. My Linux install is stable and most everything works. I've been able to make banner images in Blender and graphics with GIMP without hiccups. I booted into Windows to launch Elder Scrolls Online and play other video games. I've been addicted to Halo Infinite so I'm not really on my PC to play games as much during this time. I can say that Linux is great but if you aren't super tech-savvy I can't recommend it yet. I had a lot of trouble getting it to the point where I wasn't opening the terminal every session. Now It is good to go and I will use it more often than Windows for sure. It is just a normal computer at this point. Unless an update borks the whole thing. We will see. That's all for now.
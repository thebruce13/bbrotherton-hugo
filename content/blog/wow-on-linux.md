+++
author = ["Bruce Brotherton"]
categories = ["Rambling", "Computers", "Gaming"]
date = 2026-02-15T11:30:00Z
description = "WoW is the game that I can't live without. I need to get it working on Linux."
image = "/images/wow-on-linux.jpg"
tags = ["life"]
title = "WoW on Linux"

+++
Holy hell, if there is one program that kept me on Windows, it’s World of Warcraft. It took me forever to figure out how to get it going and I couldn’t find a good guide that went through the whole process. The forums all say “use Lutris” or “run it through steam” and yes, those are the solutions, but it’s a few more steps than just installing and click run. So I’m here to help set that process up and help you get in to Azeroth. It shouldn’t matter but, I use Linux Mint, so if you’re on non-Debian distro, your mileage may vary. 

I want to point out before we get into this, World of Warcraft works out of the box, it’s the Battle.net launcher that causes all the headaches. You can navigate to the WoW.exe and double click it and it’ll run. However, updating is impossible, you have to use the launcher. My solution for awhile was just booting into Windows and updating from there.

## My setup

I dual boot Windows, or I used to, so my WoW files were all on my Windows partition. Windows only works with an NTFS partitions and mounting it is a bit finicky for Linux. Luckily, after you set up your fstab file correctly you can pretty much forget about it. If you only use one hard drive you can skip this part. 

### Setting up a second hard drive.

We’re going to do this through the GUI because as much as I’m modifying system files make sense it’s not for everyone. 

Open up your **Disks** program and find your second drive. Click on it then choose what partition you want to mount. In my case it’s the whole drive. 

Click the two cog wheels underneath where you choose your partition. Choose Edit Mount Options

![screenshot showing context menu selecting Edit Mount Options](/images/wow-on-linux-edit-mount.jpg)

Here we want to input

![sceenshot showing mount permissions for drive](/images/wow-on-linux-mount-setup.jph)

`uid=1000,gid=1000,umask=0022,nosuid,nodev,nofail,x-gvfs-show,x-gvfs-name=Cheats`

the `uid` and `gid` are the id’s for your user and its group, this gives you full control of the drive and [may be different from what I have](https://en.ittrip.xyz/linux/checking-uid-and-gid-in-linux) here. .

### Flatpak

Both Lutris and Steam can be installed using [flatpak](https://flatpak.org/). There is some debate on why this isn’t optimal as Flatpak apps are sand boxed.

If you do go this route make sure you also install Flat Seal and give the programs access to the places you plan to install the games. 

Otherwise, you can go to the programs webpage and download the .deb files to install them to your system.

## Lutris

[Lutris](https://lutris.net/) is a game launcher that supports a bunch of other launchers and gives us a lot of utility to run games on our Linux machine. 

### Installing Lutris

First you’ll want to head over to the Lutris webpage, Lutris.net. Click the “Download” button and then find the Distro you are currently using. Follow the instructions or the link to get it installed and you should be good to go. I’m using Linux Mint so I’ll have to download the .deb package and double click it to install. Like I said earlier, you can install it with `sudo apt install lutris`

Alternativley, and easiest is to install it through Flatpak. Which means you need to install Flatpak first then head to your Software Manager and search for then install Lutris. 

### Adding Battle.net

In Lutris you’re going to want to add a new game, click the `+` (Add Game) in the top left. 

Choose Search the Lutris website for installers

Search for Battle.net

Lutris says that Battle.net will not work reliably if installed on an NTFS drive (the one I have World of Warcraft installed to so Windows and Linux can access it) so I Install Battle.net to my home drive and then locate or install the game from battle.net to my game hard drive.

Install it from there and follow the directions, **don’t sign in when prompted**, finish the install, *then* run Battle.net and try to sign in. 

Chances are it won’t load properly so you will need to use a different runner for Battle.net. 

#### What the hell, it isn’t installing??

Thanks to GloriousEggroll for the video on how to get around this hang. [https://www.youtube.com/watch?v=PRY56C9Jce0](https://www.youtube.com/watch?v=PRY56C9Jce0)

Sometimes when you download it from the Lutris app it stalls out and you have to force quit the program. Do not abort or cancel the installation, let it timeout and force quit it.

Then you want to go to Battle.net website and download the installer by itself

If you closed Lutris, reopen it. Right click on Battle.net, click configure. Under the “Game Options” tab find the “Executable” entry and click the three dots to the right of it. Navigate to where you downloaded the installer and double click it. Click Save.

![screenshot showing choosing battle.net from lutris servers](/images/wow-on-linux-bnet.jpg)

Now to keep things running smoothly we will change the runner.

### Changing your runner

This is the part that trips me up every time I try to run Battle.net so this is for my benefit as much as yours. The first runner we should try is Proton-GE Latest second is GE-Proton (Latest). These both should already be installed into Lutris. I have no idea the difference between the two but one worked and the other didn’t 

The first step is to right click on Battle.net and click configure. Then navigate to the third tab, it should be “Runner options”

![screenshot showing battle.net in lutris](/images/wow-on-linux-lutris.jpg)

Under “Wine Version” choose Proton-GE Latest. Then click save in the top right.

![screenshot showing choosing runners in lutris](/images/wow-on-linux-runners.jpg)

## Launching Battle.net

Now we’ll double click on Battle.net to open the launcher. It will bring up the login interface and **now** we will enter our information to log in. Its possible you’ll have an issue with some graphical glitches - welcome to Linux. With the new Runner going it *should* run without a problem. 

We are starting with these two specifically because they are already installed and if they work, that’s fantastic jump into Azeroth and go kill some gnolls. However, in my case this did not work.

## Installing additional runners

Sometimes the ones that are built in wont work and you’ll need to download another runner. I had this experience in the past where I had to use a Wine staging build. You can install additional runners using apps like ProtonPlus or ProtonQT-Up.

**Using ProtonPlus**

[ProtonPlus](https://github.com/Vysp3r/protonplus?tab=readme-ov-file) is a manager for compatibility tools. It has a lot of utility but we’re only have the compatibility using Wine. When you open ProtonPlus make sure Lutris is in the top left and then scroll down until you find **Wine-Staging-Tkg (Kron4ek)**, click the chevron arrow and then download the latest version. This is the runner I needed to use in order to INSTALL Battle.net. I also had to use it in order to get Overwatch to load properly. If I were to suggest one to use it’s this Wine-Staging-Tkg (Kron4ek), however, as with anything in Linux your mileage will vary and the protons work well.

![screenshot showing runner options in protonplus](/images/wow-on-linux-kronk.jpg)

After you have installed a new runner, go back up this article to see how to choose it from the drop down in the Runner Options of Lutris. 

I think that is it. If you have any tips please make a pull request for this blog article at [githubpage]. 

## Additional Resources

While writing this article I found that Lutris itself has a known issues GitHub page for running wow. 

[https://github.com/lutris/docs/blob/master/Battle.Net.md](https://github.com/lutris/docs/blob/master/Battle.Net.md)

For sure give that a look-see. 

## Alternate Launchers

There are also other Launchers you can use out there.

[Faugus is also been rising as the easiest](https://www.youtube.com/watch?v=CpyDl8BWYv0) way to run Battle.net. However, it didn’t work for me, so I wrote this for Lutris. 

[Heroic](https://heroicgameslauncher.com/) is good for pretty much any game that is not on Steam or Battle.net. You can’t play Fortnight, but I play Shredders Revenge on the Epic game store and Heroic works well for that.

I also am too lazy to step through installing through Steam as it seems more complicated than using Lutris. Here is another blog post that goes over that. [https://www.gamingonlinux.com/guides/view/how-to-install-battle-net-on-linux-steamos-and-steam-deck-for-world-of-warcraft-and-starcraft/](https://www.gamingonlinux.com/guides/view/how-to-install-battle-net-on-linux-steamos-and-steam-deck-for-world-of-warcraft-and-starcraft/)

That’s all for now.
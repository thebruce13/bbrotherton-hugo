+++
author = ["Bruce Brotherton"]
categories = ["Rambling", "Computers"]
date = 2025-09-07T11:30:00Z
description = "Sometimes you have to use Windows, best keep them at arms length."
image = "/images/blind-windows.jpg"
tags = ["life"]
title = "Blinding Windows"

+++
As much as it pains me, I have my computer dual-booted with Windows. I’ve been having a hell of a time getting [Battle.net](http://battle.net/) to work reliably on Linux. Still, when I’m using it, I want to do what I can to stay secure and keep prying eyes off my stuff. I’m going to go through what I use to blind the all-seeing eye of Microsoft, and then go into what I use to make my experience with it a little nicer.

First, we start with DoNotSpy11, and then we will move into modifying the Host file. I’ll also throw in a couple of things, like how to create a local user account and disable those annoying hotkeys.

## DoNotSpy11

One of the first things I would do is download [DoNotSpy11 from pXC-coding](https://pxc-coding.com/donotspy11/). I take comfort in this product; they have been doing this since Windows 7. This gives you access to over 200 settings you can turn on or off. Letting you disable Apps from accessing just about anything. With the setting put into categories like “Advertising” or “Privacy” or even the reason I [jumped to Linux for the second time](https://www.brucebrotherton.com/blog/linux-again/), “Copilot”.

Personally, I turned off everything that had to do with Advertising. A lot of things I didn’t think Windows needed to know under Privacy. 

All items on Search to keep my Start Menu from bringing up unrelated searches when I type.

Everything that was labelled safe for Edge, since I don’t use it, I wanted it to have as little access as possible. However, I know it is integrated with the system, so I wasn’t comfortable removing all its access.

Everything that was labelled safe for Edge since I don’t use it I wanted it to have as little access as possible. However, I know it is integrated with the system so I wasn’t comfortable removing all its access.

Then I disabled everything to do with Copilot and Recall; they can fully eat my shorts.

Lastly, I disable anything to do with [Telemetry](https://www.geeksforgeeks.org/techtips/enable-or-disable-windows-telemetry/). It frees up resources and reduces the amount of stuff Windows gets from me.    

### Shut up Windows

I have also recently seen a program called [ShutUp10++](https://www.oo-software.com/en/shutup10). It has a much more friendly UI than DoNotSpy11 and has a few features that will make using Windows a little nicer, like turning off the “Lets finish setting up your PC” on boot. If DoNotSpy11 seems overwhelming, give this one a try. Honestly, I’ll probably be using this one more often than not.

## Host file

What is a [host file](https://en.wikipedia.org/wiki/Hosts_(file)), you may be wondering? And honestly, you shouldn’t ever have to wonder what it is. I only know its existence because I’ve taken college courses to be a network administrator.

What a host file is for is to have your computer map an IP address to a human-readable name called a hostname. So instead of remembering a bunch of numbers, you can just type in the name and the computer will route you there. Think of it as your Contacts on your phone, you know the name, the phone knows the number. We haven’t needed to maintain these manually for many years - DNS took over the grunt work once it was implemented.

However, we can still use this file to hijack requests and prevent them from reaching the designated source. We’re going to use the [loopback address](https://www.geeksforgeeks.org/computer-networks/what-is-a-loopback-address/#), 127.0.0.1, to tell the computer when it wants to contact certain hostnames (or URLs) that it should look back at itself instead of reaching out to the internet.

### Modifying the host file

Thank you to [Endurtech](https://endurtech.com/stop-windows-from-spying-collecting-data/) for providing this and doing the legwork. Go over to his site and buy him a coffee. But in case anything happens to that page, I will write out the instructions here.

- Open up Notepad as an administrator
- Click File→Open
- Navigate to `C:\Windows\System32\drivers\etc\
- Choose to show **All files** in the bottom right drop down
- open the “hosts” file
- Append these values to the end of the file.

```
127.0.0.1 data.microsoft.com
127.0.0.1 edge.microsoft.com
127.0.0.1 msedge.net
127.0.0.1 azureedge.net
127.0.0.1 msftconnecttest.com
127.0.0.1 activity.windows.com
127.0.0.1 bingapis.com
127.0.0.1 scorecardresearch.com
127.0.0.1 assets.msn.com
127.0.0.1 data.msn.com
```

Keep in mind, this will probably break some things. You can comment out lines using a # at the front to let Windows reach out and contact the server until you find the one that is causing things for you to break. In my case, the Weather app had broken icons for all the weather indicators; `assets.msn.com` needed to be commented out for the Weather app to get the icons to work again.

If you were REALLY interested in what your computer was reporting on, you could use a tool like [Wireshark](https://www.wireshark.org/) to watch what is going in and out of your network. A word of warning, don’t use this at work or at school - you will throw up all kinds of alarms for the IT team.

## Local User

Windows 11 has made it difficult to set up a PC without a Microsoft account. If you, like me, would rather not or have a reason to share files from your PC with people on your network, you’ll want a local user. If you have already set up your PC with a Microsoft account, not to worry, you can convert it to a Local Account.

### New local user

On a fresh install of Windows, you gotta completely disconnect from the Internet, so don't hook up your computer to WiFi or Ethernet.

Then press `shift + f10` and type `oobe\bypassnro`

The computer will restart, and then you'll see a new option that you don't have internet. Then you'll be able to create a local user without hooking it up to a Microsoft account.

However, Microsoft is killing this method in 2025; the new way to make a local user is to type:

`start ms-cxh:localonly` after pressing `shift+f10` .

Shoutout to [hsehestedt on elevenforum](https://www.elevenforum.com/t/a-new-way-to-create-a-local-user-account-better-than-oobe-bypassnro.34784/) for this solution.

### Windows S Mode

If you have a new PC with Windows S mode enabled, `Shift+F10` isn’t going to work for you - the command line is disabled entirely. The only way I knew how to get it working was to get the computer set up with a Microsoft Account, disable S Mmode, then you’re able to use the command prompt.

Shoutout to [thepineapple on elevnforum](https://www.elevenforum.com/t/new-local-account-method-access-unused-setup-screen-s-mode-supported.29973/) for this real nsolution

In this situation you will need to press `ctrl+shift+j` and then type `WinJS.Application.restart("ms-cxh://LOCALONLY")` . Then press `Esc`. Notice how similar it is to how you would do this outside of S Mode. 

### Make me a local

Making yourself a local user after hooking up to a Microsoft account is pretty straightforward.  Go to settings. Click your name in the top left. Choose Sign in as Local User. You still have to untangle yourself from OneDrive, though.

## Get a VPN

Look, nowadays, if you give a shit about privacy, you need a VPN. I use Mullvad, and I wouldn’t have known about it if I hadn’t investigated what Firefox uses for its VPN. It's non-subscription-based, so you will pay the ~$5.50 every month manually, with cash if you’d like, as long as you want to use it.

## Windows Tweaks

The rest of this article is less about keeping windows from spying on you and more about tweaking it so it’s less obnoxious.

The first thing I think to do, especially since it doesn't require additional software, is to remove the [web experience pack](https://helpdeskgeek.com/windows-web-experience-pack-what-it-is-and-how-to-update-it/).

`winget uninstall "windows web experience pack”`

This will remove the widgets panel as well as your start bar weather info. As someone who removes the search from my bar anyway, it's only a bonus. What I like about it is that, with removing the whole widget panel, I no longer get blasted with news articles when I press Win+W. It also removes widgets, things I don't use, so they have no reason to be on my machine. Which is a good rule of thumb: if you installed something to use it once, go ahead and uninstall it; you can reinstall it again later if you 

### [Open Shell](https://open-shell.github.io/Open-Shell-Menu/)

This one is a little more controversial, I think. This start menu replacer makes it look like Windows 7 and earlier. It's a little rougher around the edges, but if you aren't a fan of the new Windows 10 or 11 start menu, this is a good start to make it feel better. Especially if you are somehow moving from Windows 7 to 11.

The big part that I use from this is the custom start menu icon.

![Three circles depicting characters from the game Halo](/images/halo-start-w-small.png)

I have those Icons pulled from [this Reddit post](https://www.reddit.com/r/halo/comments/963cty/i_drew_some_halos_character_icons/) by SKYKiKi77 that I created, so it moves between Cortana, Master Chief, and Guilty Spark. I think it's pretty damn rad.

### [Explorer Patcher](https://github.com/valinet/ExplorerPatcher)

This is one of my favorite tools to make Windows my own. It has so many features that it feels like it should be included by default.

Are you someone who likes having the taskbar on the side or on the top? There is an option for that in Explorer Patcher.

Do you hate the new context menu? Turn it off.

Don't care for Windows having a bunch of hotkeys for programs you don't use? Kill 'em.

There is a multitude of options for this program. I mostly use it to customize my taskbar. I made it so my Start Button is on the far left and my files and tasks are in the middle. Just like how I have my panels set up on Linux. I also remove recommended and recent apps from the start menu. I am a person who only wants what I choose to be displayed there. Less clutter is good for my brain.

There is also an option to make the start menu look like Windows 8 or 10. I personally loved the metro tiles. 

There is a lot to explore in there - I highly suggest checking it out.

## Honorable mentions

### [Winaero Tweaker](https://winaerotweaker.com/)

This program contains a bunch of options to tweak your Windows installation and make it more fine-tuned to what you want; however, I have not used it extensively enough to give a review of its features. Though I’ve seen some of them unable to run, I now suggest using Explorer Patcher.

### [MyDockFinder](https://www.mydockfinder.com/index_en)

This one I recently stumbled upon that will give you a dock similar to a Mac. It's paid, but only about $8, and it brings a lot of features with it. Compared to the features that the Mac desktop environment has, this captures just about all of them. It also has themes you can get for it, so you’re not locked into the default style.

### [Wallpaper Engine](https://www.wallpaperengine.io/en)

Can't have this article without mentioning Wallpaper Engine. This has a ton of options for having animated backgrounds on your desktop. I think it's worth the money even if all I do is put a clock on my tiny screen. Clock background on my tiny monitor.

### [Windows Blinds](https://www.stardock.com/products/windowblinds/)

This is a paid customization tool that is packed with features. You can even get a skin to make it look like Vista. Stardock has a start menu replacer as well. These are nifty but a little overkill for what I want to do.

Anyway, Windows is bad, use Linux, [here is my t-shirt].(https://www.teepublic.com/t-shirt/77608139-resist-run-linux?store_id=125496) [![tshirt depeciting tux penguin with the words resist run linix](/images/resist-linux.jpg)](https://www.teepublic.com/t-shirt/77608139-resist-run-linux?store_id=125496) Thats all for now.
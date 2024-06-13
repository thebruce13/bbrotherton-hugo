+++
author = ["Bruce Brotherton"]
categories = ["Rambling", "Computers"]
date = 2024-06-12T11:30:00Z
description = "Windows is doing us dirty, all hail the Penguin."
image = "/images/tux-2.jpg"
tags = ["life"]
title = "Linux Again"

+++

Once again [Windows has done something](https://www.brucebrotherton.com/blog/going-linux/) I cannot agree with. Not only is it ending the life of Windows 10 and charging people to keep it. They are going full hog on AI and Copilot. If this was something I could opt in for or install on my own I wouldn’t be so aghast about it. Sadly - this is coming in a windows update and I can’t stomach it anymore. I have switched to Ubuntu Budgie and despite it having its struggles, I am pretty happy with it. 

## What did Windows Do?

So I have been a Microsoft Fan boy for as long as I can remember and I abhor Apple products. I even went back on my previous post about switching to Linux since I was able to forcibly install Windows 11 on my old hardware. When Copilot was introduced to Windows 11 I got an ick feeling. But I figured I would just [disable Copilot](https://www.elevenforum.com/t/completely-disable-and-remove-copilot-in-windows-11.23264/) and forget about it. Now, with Copilot being added a new feature to [screenshot your computer as you use it](https://wired.me/gear/microsofts-copilot-pcs-will-screenshot-virtual-activity/), I thought it was time to switch completely. 

## Is AI bad though?

I don’t trust this current generation of AI even though I have been using it a lot. I used ChatGPT to help write letters, write some regular expression, troubleshoot code, schedule my days, and am now trying to figure out how to start a Local Tech Support business and seeking its features to help me through the process. 

Most recently I couldn’t figure out an animated short and I [asked Copilot](https://sl.bing.net/dI88eYCjktg) to help me find it. Spoiler alert, it was [The Dover Boys at Pimento University](https://www.youtube.com/watch?v=cDN0LKfurCw). It was a little frustrating it kept bringing up things that I didn’t feel were related and ignoring parts of my prompt, be it got there.

I even started a new web page at [staticsociety.xyz](http://staticsociety.xyz) where I’ve been posting images that I prompted via [Bing Image Creator](https://www.bing.com/images/create) and [Automatic1111 with Stable Diffusion](https://github.com/AUTOMATIC1111/stable-diffusion-webui). It’s a blast coming up with crazy ideas and then seeing the results. I even used ChatGPT to help me come up with prompts to tweak out the ones I fed the models. 

Now though, whenever I see an AI created image in a slide deck or something that supposed to be professional, I get the ick. 

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/ew-O7eUXxYYkVXna" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

But I digress, I only want to use AI or have it available when I need it - not sitting on top of everything I do. Its not fully developed and isn’t at a point that it should be shoveled into everything we use. I like the idea of it as a tool, not a companion. Security wise I don’t trust it one bit. Especially with Copilot being able to screenshot sensitive information and [act as spyware](https://www.youtube.com/watch?v=cDN0LKfurCw). I can’t support it anymore. 

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/mrw-president-civil-LKTTAzGboJGzC" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

## So whats new with linux?

Welp, I had a hard go of it off the bat. When I upgraded to Windows 11, it botched my grub boot and took over. So I had to get that set back up. It was complicated, because I thought my grub was corrupt and I had to restore it. Turns out I had to make Windows switch to it using the command line edtior with this command.

`bcdedit /set {bootmgr} path \EFI\ubuntu\grubx64.efi`

I followed a [guide from Tech Blog](https://techblog.dev/posts/2021/12/how-to-fix-missing-grub-boot-menu-after-a-windows-update/) to fix it. Took a day, but it was up and running. 

### Permission Issues

Then the almighty permission issues. I wanted to run Steam games off a separate drive but for some reason it just couldn’t launch anything. I would click play, Steam would say “Launching” the game would launch and then immediately quit. 

Turns out since I installed Steam via [Flatpak](https://www.flatpak.org/) I need to install [Flatseal](https://flathub.org/apps/com.github.tchx84.Flatseal) in order to tell Steam that the drives were available. However, I wasn’t done there.

I ended up trying to modify the `/etc/fstab` file and successfuly got it working I ended up having to use the [UUID method](https://www.cyberciti.biz/faq/linux-finding-using-uuids-to-update-fstab/) in order for it to figure it out. This gave easier permissions for the system to get to the folders. 

After two days of getting this all figured out I got my games working.

### Plex Server

I then need to get my Plex server up and running. I also ran into permission issues [running my virtual machine](https://www.brucebrotherton.com/blog/you-need-a-streaming-server/) inside of Linux and sharing my hard drive to Plex. It ended up being I needed to update my Virtual Box Guest Utilities. But now that is up and running too!

## Glad to be on Linux

After these hardships, Ubuntu has been treating me well. I can play games, even with Steam Link, watch any of my media on Plex, do my work and run most of the programs I already had installed on a separate “Programs” had drive with [Wine](https://www.winehq.org/), no extra steps required. 

So far it has been workable and I only had to run Windows once in order to get a Java update done foe Elder Scrolls Online. Still haven’t figured out how to fix that yet but I’ll get there. 

It seems that I’m not the only one who’s on this journey, [r/linux has noticed more posts about going linux as well](https://www.reddit.com/r/linux/comments/1d46h6p/has_there_been_a_sudden_influx_of_linux_newbie/). 

And at the end of the day. Since Microsoft recalled recall, switching back to windows when I’ve had enough troubleshooting of Linux it’s like I never left. Thats all for now.

[https://blogs.windows.com/windowsexperience/2024/06/07/update-on-the-recall-preview-feature-for-copilot-pcs/](https://blogs.windows.com/windowsexperience/2024/06/07/update-on-the-recall-preview-feature-for-copilot-pcs/)
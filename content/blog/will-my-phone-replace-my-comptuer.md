+++
author = ["Bruce"]
categories = ["Productivity"]
date = 2022-01-10T13:00:00Z
description = "Is it possible to replace my entire desktop with just my Samsung? Diving into the idea of what it would take to do so and figuring out if we are there."
image = "/images/broken-screen.jpg"
product = "https://www.redbubble.com/i/poster/Mobile-Takeover-by-thebruce13/98551605.LVTDI?asc=u"
tags = ["Rambling", "Life"]
title = "Will my phone replace my comptuer?"

+++
So I have been questing to make my Android phone my primary device. Workstation, gaming, creative, and social media device. The criteria for this was that I didn't need to install a virtual machine or remote into a computer to do the majority of it.

Disclaimer, I will be using my main computer and using Xbox Game Pass to remote into for gaming. However, there are ways to play games without using these services either with an emulator or games from the play store.

Also, at this time, the article is theoretical. I just want to explore the tools out there and give insight to see what is possible with a mobile device. I don't have the time or effort to use this for a week or a month. Though if you want to see a [video by Byte Review](https://youtu.be/wnx67I7rv_Q) who used his Dex for a week in 2019, his review is really good and inspired me to even consider this.

![A screenshot of my current Dex desktop.](/images/screenshot_20211231-000423_samsung-dex-home.jpg)

Pictured above is a screenshot of my current Dex desktop. As you can see, it is almost the same as using Linux or a Chromebook.

## Hardware

For a full list of a setup, I suggest checking out [Matthew Moniz has a great rundown](https://youtu.be/e9L0dZIXXns) of what he uses to get the most out of his Dex setup. I'll detail what I'm using below.

I'll be using my [Samsung Galaxy S20 FE](https://www.amazon.com/Samsung-Factory-Unlocked-Smartphone-Pro-Grade/dp/B08FYTSXGQ), its about $700 retail on Amazon and that is about the price for a mid-range laptop, so I feel like it is a decent benchmark even though I didn't choose it for this experiment. It is essential that I'm using a Samsung Device as it has [Samsung Dex](https://www.samsung.com/us/explore/dex/) and that will be replacing my desktop experience. Although a coworker of mind found on his One Plus that he also had a [desktop app built in under settings](https://wccftech.com/how-to/how-to-use-the-hidden-desktop-mode-on-android-10-devices/). So maybe Samsung is going to get a run for its money soon here. 

I'll also need a dock in order to run my phone in desktop mode, you <em>can</em> use a USB-C chord into your computer and run Dex in a window. However, that will render the experiment moot because you are using a computer then.

Therefore, the dock I'll be using is by [Baseus](https://www.amazon.com/Samsung-Docking-Station-Baseus-Adapter/dp/B07ZR54JHV/ref=sr_1_3?crid=1JG9SU9NHQZ8K&keywords=baseus+samsung+base&qid=1640927911&sprefix=baseus+samsungba%2Caps%2C2312&sr=8-3) and it works pretty well and is a bit less than the [official dock by Samsung](https://www.amazon.com/Samsung-Experience-Included-International-Warranty/dp/B06XD4S8J1/ref=sr_1_4?crid=1GLW2ID471DX3&keywords=samsung+dex&qid=1641586005&sprefix=samsung+de%2Caps%2C195&sr=8-4). Quick note that I started this journey with my Samsung S8, which is about $200 on Amazon, and I still believe you could work this using that, but it will be a bit less powered. That is why I have this particular dock on hand. If I were to buy a new one, I'd probably get this [Baseus Dock with an Ethernet port](https://www.amazon.com/Baseus-Docking-Charging-1000Mbps-Ethernet/dp/B08XB5JQVY) so I could hard line my phone instead of relying on WiFi or something similar.

I am going to assume you have a keyboard and mouse around to do this. If you are buying new ones you'll want to go with Bluetooth, this will give you one super clean setup.

If you are going to be working with large files, I would recommend getting an external USB 3.0 hard drive and maybe a micro-SD card to slot into the dock. Phones have limited space and the more we can keep for Apps the better.

With that, we need a 1080p monitor and we're good. You aren't going to see any benefit using a 4k monitor, the device just isn't up to it.

Lastly, I have a Razer Kishi that I'll be using primarily for gaming. This isn't necessary as any Bluetooth controller will work, it is just my preferred method because it turns my phone into a Nintendo Switch. However, I use a PS4 controller when I want to play when it is in desktop mode.

I also have some Bluetooth headphones that I use for audio.

## My Job

What I needed to complete my job as a Front-End Developer was really just getting an IDE running and git. Thankfully that has been made incredibly simple with git getting [Code Spaces](https://github.com/features/codespaces) in 2021. Now all I need to do is navigate to my git repository and open up codes spaces by pressing the period key. This is how I edit this current webpage outside the Forestry.io CMS.

I still think it's valuable to have the capability outside of git and an internet connection to be able to work on websites. So, there are two apps I know I'll need. Something for terminal and an IDE.

The terminal is pretty straight forward, [Terminux](https://play.google.com/store/apps/details?id=com.termux). It works just the same as a linux terminal and I was immediatly comfortable in it. I was able to install Node.js and run commands very quickly. This is where I start to recommend that external drive. Node modules is a monster so you will wanna have some space outside your phone.

![](https://i.redd.it/tfugj4n3l6ez.png)

For an IDE, I settled with [ACode](https://play.google.com/store/apps/details?id=com.foxdebug.acodefree). It was a no-nonsense code highlighter that just worked on the phone. It has syntax highlighting and formatting. All the bells and whistles I've come to love by having IDEs.

If you wanted to get into the nitty gritty and make a web-based version of VSCode that you hose on your phone, [Develoquent has a video tutorial on how to set this up.](https://youtu.be/OtbFjfVC4XQ)

Now I never tried to get php running but I know with the ability to install python or node that should be as simple as installing a plugin and doing npm run on it. I want to do React or Vue and all you need for that is node modules.

## Gaming

I said before my primary modes for gaming on my phone are with Xbox Game Pass and using Steam Link on my main computer. However, the amount of quality games on the play store makes this more a nice to have than a necessity. My top three games on mobile are

1. Epic Seven
2. King of Fighters All Stars
3. Final Fantasy Tactics: War of the Lions

I'm a sucker for gotcha games but Final Fantasy Tactics is a special soft spot in my heart. The fact that that fully fledged console game is available as an app shows that there is more to the app store than Free to Play games.

Still if I want to use this as a replacement to my gaming rig, I'll need a way to play larger titles. I really like Xbox Game Pass for this as I can just load up the app and pick a game and get going. There is a latency issue with inputs being slightly delayed so I am stuck playing easy mode in Halo. But in other games where you can account for the delay better, you'll do fine.

Further still with the absolute insane backlog of older games you can load up an [emulator](https://www.retrogames.cc/) and be just fine. There are apps you can download as well for games all the way up to PS2 and beyond. So yeah, I am covered in the gaming department. The Samsung Galaxy S20 FE also has a 122hz display so I'll even be able to play games that support a higher refresh rate.

## Hobbies

I like to make 3d art with Blender and use Krita on my desktop PC and I haven't been able to find replacements for these two hobbies on my phone yet. However, I am aware of plenty of 2d drawing apps and I'll just have to take my pick. The cool thing about Android is that it also supports drawing tablets so my [XP pen](https://www.xp-pen.com/product/613.html) works fine when I plug it in. I've seen some apps in play store for 3d but I just haven't given them a try. Still waiting on the Krita and Blender app for Android.

Even if I had the capability to use these apps, rendering would end up being a problem and I'd have to send that off to a [render farm](https://us.rebusfarm.net/en/) in order to do large projects.

## Misc. Activities

We all know that mobile devices consume social media like nothing else on the planet so there are no worries there. It is also fantastic at consuming videos so those are all already set to go. With the dock I can hook up my phone to a larger screen and have a better experience and since its HDMI we'll have better sound than my phone's speakers. I could also replace my Roku with this. Although, I don't think I'd appreciate my texts popping up in the middle of watching a movie.

> Compared to a tower or laptop, this setup is absolutely silent.

If I need spreadsheets, email, or a word processor Google docs has me covered. So that is most everything I do outside of gaming and making art on my computer.

## Drawbacks

Okay, so just about everything can be done on a phone. However, there are some serious limitations to using it as the only device.

1. Currently you can only have up to 3 or so apps open at a time. The phone can get overloaded quickly and start getting hot. It will limit its processing power once it gets to that point.
2. While your phone is your computer you have no phone. You can use the text app right on the screen and take calls using a speaker phone or Bluetooth headphones. But you can't pull it out use it while you are waiting for something to load.
3. Some apps don't work the same in desktop mode. An example is Animal Crossing Pocket Camp. Usually, your clicks don't register as touches and it's a struggle to use on the desktop mode. Some app developers just don't make it to work for Dex.

## Workarounds

### Storage

As I stated before, you are going to want an external hard drive. However, cloud storage has gotten very good, and if you don't need to run scripts on local files and just need to have them available, the cloud is the way to go. Now, I know this requires an internet connection, and if that isn't an option for you, a thumb drive might be a good alternative to a full-sized hard drive for things you need all the time.

### Remote Computing

Now I know the main idea of this was to replace my computer without needing a physical machine or remoting into another desktop. However, I won't leave you hanging in case you wanted to use these.

If you were up to setting up your Windows computer to be able to be used [via Remote Desktop](https://www.thewindowsclub.com/connect-android-to-windows-microsoft-remote-desktop) you can, it is a little more involved than the next solutions, but it is an official solution.

The first choice I'd use is [Parsec](https://parsec.app/) on the other hand is setup to try and keep your view at 60fps as it originally was set up for video gaming. And it is great at this. You have to keep a 5g WiFi connection or hard line the connection to get the most of it.  If your connection goes the usability goes with it. Just keep in mind that the program has be installed on both the machine and your phone.

On this note I also like to connect to my computer using [Steam Link](https://store.steampowered.com/app/353380/Steam_Link/). In a way it is superior to Parsec because it has a virtual game pad, so I don't <strong>need</strong> a controller to play games. Also needs a PC app and mobile app. I end up fighting with this more often than I do Parsec, so it will remain my number two.

[TeamViewer](https://www.teamviewer.com/en-us/) is another good choice to remote into my desktop. This is perfect for general computer usage, but it falls short when I'm using a graphics software. Sometimes the connection is a bit more solid than Parsec and I need to use it to get some troubleshooting figured out. Remember this also requires you to have both apps installed on the desktop and the phone.

What if you don't have a desktop machine to remote into? I only really know about [Shadow](https://shadow.tech/) because [Linus Tech Tips has reviewed it](https://youtu.be/0BQ4bXNdEQI).

<iframe width="100%" height="315" src="https://www.youtube.com/embed/0BQ4bXNdEQI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Shadow is set up for getting you gaming. Because of this focus, your latency is reduced, similar to how Parsec is set up. It is as close as you are going to get to working on a physical desktop without having one. Its pricing is pretty good at $29.99 a month and would be the way I'd go if I didn't have a desktop to work off of.

## Conclusion

I'd say it's 85% safe to replace my PC with my Samsung Galaxy. An unexpected side effect of using just my phone is the quickness of getting into a desktop environment. Just plug it in and we are working. Another one was how quiet everything was. Compared to a tower or laptop, this setup is absolutely silent. I can do just about everything with it considering the apps are available. And with subscription services like Shadow, the reality of needing a physical desktop in my house to work in 3D is greatly reduced. Really, my <span style="text-transform:uppercase">Nvidia</span> 1060 is really getting outpaced with the newer graphics cards nowadays so maybe it's time. Maybe one day I'll be able to give this a thorough test run but I don't have the patience for it, just the idea that is possible is enough. That's all for now.
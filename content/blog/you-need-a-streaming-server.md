+++
author = ["Bruce"]
categories = ["Computers", "Rambling"]
date = 2023-11-01T01:00:00Z
description = "You need to get a streaming server set up. Unlock the media you already own."
image = "/images/plex-stream.jpg"
tags = ["Life"]
title = "You Need Your Own Streaming Server"

+++
Now a days it seems that every streaming service out there wants to nickel and dime you every step of the way when all you want to do is watch Pirates of the Caribbean on the toilet.
<div style="width:100%;height:0;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/YZIiXdt43y0M0" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>
 
Or the infinite that is their digital catalog makes you spend more time looking for something to watch than watching a show.
 
Even music isn’t great, when you spend $10 a month and listen to the same 10 albums all year long. While being bombarded with advertisements for artists that you have zero interest in.
 
If you are a millennial or a gen-x, you are sitting on a goldmine of CDs and DVDs just waiting to be harvested into your own streaming server.
<div style="width:100%;height:0;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/Bl1t1DdP6iASI" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>
 
 If ditching the streaming services has been on your mind, let me guide you to some resources and get you on the path of truly cutting the cable.

## What kind of computer do I need?

If you are thinking of a server as a huge rack of hard drives and computers stacked on on top of the other, you’d be correct. However, we won’t be needing anything quite as extreme with our home streaming service. What we’ll need is a dedicated computer and some hard drive space.
 
If I had my dream setup I would have bought a [mini pc off of Amazon](https://www.amazon.com/Beelink-Pro-Desktop-Computer-1000Mbps/dp/B0C89TQ1YF/ref=sr_1_8?crid=2LHBY9IYG51RR&keywords=Beelink&qid=1698936155&s=electronics&sprefix=beelink+%2Celectronics%2C265&sr=1-8&ufe=app_do%3Aamzn1.fos.18ed3cb5-28d5-4975-8bc7-93deae8f9840) and thrown either a [terabyte external hard drive](https://www.amazon.com/Beelink-Pro-Desktop-Computer-1000Mbps/dp/B0C89TQ1YF/ref=sr_1_8?crid=2LHBY9IYG51RR&keywords=Beelink&qid=1698936155&s=electronics&sprefix=beelink+%2Celectronics%2C265&sr=1-8&ufe=app_do%3Aamzn1.fos.18ed3cb5-28d5-4975-8bc7-93deae8f9840) on it or a [M2 solid state](https://www.amazon.com/SAMSUNG-MZ-V8V1T0B-AM-980-SSD/dp/B08V83JZH4/ref=sr_1_1?crid=2XVXZLOR73P3Z&keywords=m2+solid+state+drive+1tb&qid=1698936301&sprefix=m2+solid+state+%2Caps%2C171&sr=8-1&ufe=app_do%3Aamzn1.fos.18ed3cb5-28d5-4975-8bc7-93deae8f9840). Either way it would be powerful enough and have enough storage for anything I’ll likely throw at it. 
 
However, if you have an old PC or laptop kicking around you’ll have more than adequate horsepower to get your streaming server up and running.
 
Now, if you are planning on hosting more that 2 or 3 people at a time, streaming 4k videos, you are going to need some beefier equipment. But we’re not going to worry about that today. And since we are looking at DVD quality - a potato will be enough.
 

#### But what if I don’t have another pc?

If you, like me, didn’t have a second pc on tap that was ready to be your streaming server, don’t worry. It is possible to install streaming server software onto your main computer.
 
The only problem I had with that is then when someone wanted to stream while I was using the pc they could cut into resources I’d need to play video games or get work done.
 
The solution I came up with is to create a virtual machine using [Virtual Box](https://www.virtualbox.org) and running Ubuntu on it.
 
My computer isn’t too top the line anymore so I couldn’t dedicate a ton to this virtual machine. I gave it 2 of my 4 cores to use, 4 gigs of my 16 gigs of Ram and 64mb from my graphics cards 6gig vram. This runs pretty good for me and I haven’t seen any problems with one person streaming. I also have a hard drive that my Windows host has access to that is [passed into my virtual machine](https://docs.oracle.com/en/virtualization/virtualbox/6.0/user/sharedfolders.html). That way I can manipulate files in windows and keep my server minimized for 90% of the time.  

## What software do I need?

There are pretty much two options when choosing a software to run you streaming server, Plex and Jellyfin. Plex is a freemium service where Jellyfin is open source and completely free.
 
I chose to run Plex because it has an app on just about every device. It’s paid subscription is $5.99 a month or you can pay yearly OR you can purchase a lifetime subscription. With Plex premium you get the ability to download your content to your devices, something I absolutely need. It has other features but that’s the main one. There is yet another alternative that will let you stream to your mobile device and that is a one time fee of $5.99. I started with that but again, needed the download. If you want to go this route, [Linus Tech Tips has a great video](https://www.youtube.com/watch?v=XKDSld-CrHU) about it. 
 
Jellyfin has apps on the platforms that matter. They aren’t quite there to get downloads working but once they do I may switch from Plex to them. Other than that, its a great route to go because, since it’s open source, it will only get better with time. Linus Tech Tips also has a [video on setting Jellyfin up](https://www.youtube.com/watch?v=jKF5GtBIxpM) along with pros and cons. 
 
Either way they are both solid options and I would suggest you look at them both and decide for yourself.
 

## Getting your media onto your server.

Now that we’ve covered the hardware and software we need to fill our server with stuff. You are going to want to read the documentation about how to set up folders on your server to get the most out of them.

- Here is a link on how to do it for Plex
- and how to set them up for Jellyfin.

 
 My first content I got onto my server was from the Internet Archive where you can download episodes of Popeye among other shows.
 
I grabbed a few episodes and threw them on the servers hard drive. Right away it picked them up knowing it was a series and I was off to the races. Though I would have greatly benefited if I read the documentation on how to name series files.
 
Next I wanted to download a copy of the YouTube videos I created a while back to see how that would work out.
 
I used the [WonderFox](https://www.videoconverterfactory.com) HD video converter to download it and put it on my server. It was a little tougher than the Popeye experience because it didn’t sort it into a show because it wasn’t one. Still was happy to have it available.
 
After that, I wanted to try and copy a personal DvD I had so I also purchased WonderFox DvD ripper. It worked great and was on my server. 
 
Now these tools could be used to grab media from any YouTube video or DvD but these are the ones I started out with. 
<div style="width:100%;height:0;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/8JCwuk8n2Y6iI" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

Music was next. I already had a bunch of folders that I had as backups of my Zune so I just moved those over to my streaming server and pointed the server to look there for music. I then downloaded my iTunes library and Amazon music I purchased and out them on the server.
 
There was some pain getting the server to correctly identify the songs and albums but I was okay with it.  I’m now listening to my tunes anywhere I go. Now I can hit shuffle and press next until it lands on a song I’m feeling. And it will because I don’t have an algorithm telling it what song is going to be next.
 

## Freedom

So I’m at the point now that if I want a certain piece of media I can reach into my collection from the past, bring it to my server and have it available to stream whenever I want. My personal out of pocket for this whole project was about $65. That is way less than the Disney+ bundle that is going on right now and I don’t have adds either.
 
This also lets me have all my media in one place, so I don’t have to go searching for where to find the next Pirates of the Caribbean movie.
 
I even have access to One Pace so I can finally catch up to the series in time for it to end!

<div style="width:100%;height:0;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/SJXzadwbexJEAZ9S1B" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>


The biggest surprise for me, however, was having access to all of my old music. It has been wonderful listening to albums I haven’t heard from in a long time and totally forgot even existed. I’ve launched Apple Music since I have it from a family plan to sample music but I would rather buy it as I need it rather than try and navigate the user interfaces of streaming services to get to it.  

## Sidenote about VuDu

I wanted to take a second to talk about buying movies from VuDu or Google Movies or Apple TV. I would vote yes 100 times. I love the library I’ve built on VuDu it’s been a lifesaver. Sadly, not everything is available on there and some of the stuff I have physically isn’t available anywhere. Say for instance you had an original trilogy of Star Wars that had Sebastian Shaw as a force ghost, you can’t buy that now. 
<iframe width="560" height="315" src="https://www.youtube.com/embed/uaqPK6s77hY?si=5mr6Pk6-ErKH9YpP" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
I have all the extended edition of Lord of the Rings on VuDu and I don’t plan to ever move that onto my own streaming server. Plus, these services allow you to download shows as you wish and have better encoding and quality throttling as you need it than my streaming server does. And it’s great that a lot of physical copies of movies come with a digital code too. Still, licensing is a thing and could potentially rip those away from me. So, yeah. I love it a lot more than a streaming service, but it can get pricey and isn’t guaranteed. With your own server you control the files and can add to it as you see fit with a community’s help you likely have access to more than you could watch in a lifetime.
 
So get in there and get your own family streaming service a go. It may be enough to drop at least two services off your bill. Good luck! That’s all for now.
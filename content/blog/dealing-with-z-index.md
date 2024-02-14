+++
author = ["Bruce Brotherton"]
categories = ["Front End"]
date = 2022-01-24T15:15:00Z
description = "Z-index is something that normally you don't have to worry about it, until you do. Figuring it out is troublesome at first and often APIs abuse it to ensure they have what they made sit on top of whatever is on the website."
image = "/images/card.jpg"
product = "https://www.redbubble.com/i/art-board-print/Flying-Cards-by-thebruce13/100098465.5E8EA"
tags = ["Beginner", "Css"]
title = "Dealing with Z-index"

+++
Z-index is something that normally you don't have to worry about it until you do. Figuring it out is troublesome at first and often APIs abuse it to ensure they have what they made sit on top of whatever is on the website.

## TL;DR

Z-index is determined by the order it is placed on the page. Whatever is put on last sits on top. And, like a deck of cards, if you pull one specific card out and place it on top you'll be seeing that one first. Just make sure you have the element's position set to relative or static.

## How the browser stacks content

So in order for us to tackle the issues that arise with the z-index, we need to first know how the browser behaves normally when stacking pieces of content. [MDN has a good example](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/Stacking_without_z-index) of what a z-index looks like if none are applied. And essentially it follows the rule that the last thing that is placed in the HTML is on top of everything else on the page. I like to think of it as how [Magic the Gathering's stack order](https://magic.wizards.com/en/articles/archive/beyond-basics/stack-and-its-tricks-2017-11-30). The idea is that the players put down cards and at the end of the phase they are resolved from the top down. Similarly, in our code - the last thing we put on the page has the highest z-index and is on top of the rest. This is the default behavior and what the element will assume if you set:

    z-index: auto;

## Setting a z-index

The first thing to know when you are setting a z-index is that it can only be applied to a [positioned element](https://www.w3schools.com/css/css_positioning.asp). That means you have to set `position: relative` or absolute, or fixed. Anything other than static.

The reason is when you set a z-index you are positioning it now. In the z-axis, similar to a 3d plane in graphics software.

The moment you set a z-index other than auto on an element you are manually ordering the stack of how things are displayed on the page. And this gives you a lot of power. In this case, using less is more. The less you set the z-index on a page the less trouble it will cause you down the road.

If you are writing custom CSS, I would recommend trying to keep your values low so they don't get hard to manage. I typically don't go much higher than a z-index of 10 with my elements.

### Z-index and children elements

By default, the child of an element is restricted to the z-index of its parent. If you manually set the z-index of a parent element it locks the children to its subset of z-index ranges. [Here is a JsFiddle](https://jsfiddle.net/brucifer906/tcdob258/1) showing this in action.

<script async src="//jsfiddle.net/brucifer906/tcdob258/1/embed/result,html,css/"></script>

In it, you'll see that the parent element that had a z-index set to 0 prevents its children from having a higher value than that. Even if we set its child element to 999, it will not appear on top of the other square that is set to 1.

### Negative Z-index

Negative z-indexes behave pretty much the same as regular z-indexes. It is just important to know that if the parent has a z-index of anything other than auto it will still keep the negative one above it. [This stack exchange](https://stackoverflow.com/questions/33217407/css-negative-z-index-what-does-it-mean) has a very good example of it.

It talks about how when you set an element's z-index to anything but `auto` it creates a new stacking context. This is what I talked about when things get stuck inside the parent earlier. However, if we leave the z-index alone on the parent, the child element can go under its parent; We didn't create a boundary for it.

Now, I had a time where I needed to use a `::before` element inside of a div to darken it but I needed to keep the text on top of it. The method I went with is setting its parent to `0` and then setting the `::before` to `-1`. That way the div itself has its stacking context set and the `::before` will be stuck in it and not go below the element it on top of.

<script async src="//jsfiddle.net/brucifer906/kye2tm5q/16/embed/result,html,css/"></script>

#### Max Z-index

Browsers have a [max z-index of 2147483647](https://stackoverflow.com/questions/491052/minimum-and-maximum-value-of-z-index). I want to start off saying, <strong>please don't</strong>. If at all possible, avoid putting astronomical values in for your z-index. I know this isn't always possible when you are using a framework or an API that insists that their element sits on the top of everything on the webpage and makes their `z-index: 999`. Still, you can likely use what we talked about earlier and set its parent to a reasonable number, thus reining in these out-of-hand values.

Otherwise, a popular method of setting [z-index is in sets of hundreds]() or tens.

## Debugging Z-index

It can be super tricky when you need to figure out why something isn't respecting the Z-index as you set it. Going through things to figure out just where it went wrong can be tricky. First, you'll want to see if its parents are set to have a z-index, which will probably get you going on the right path. If it is set with a CSS file you can't access, you can try to override the value and set it to `auto` that'll restore the parent to be in its natural order and let its children be their own z-index independent from their parent. The auto will meld it back into the page as if it wasn't set.

Other than that, I tend to set the z-indexes high and see if that puts them in the right spot and then dial it back until it is just barely above what I was trying to keep it on top of.

### 3D View on Edge

If you need a visualizer to see what is where concerning z-index; Microsoft's Edge browser -right now- is the only browser that can [display 3D view](https://blogs.windows.com/msedgedev/2020/01/23/debug-z-index-3d-view-edge-devtools/).

![A 3d representation of z-index on a webpage.](https://app.forestry.io/sites/lfvcddm-c6yjvg/body-media//images/z-index-edge.png)

#### Opening 3D View on Edge

These are the steps I have to go through to get the 3d view to be visible on my computer.

1. Open Inspector by pressing F12 or ctrl/cmd+shift+i
2. Click the plus sign in the top right of the inspector and choose "3D View"
3. Click the "DOM" tab (this will load the dom into the inspector view)
4. Click the "Z-index" tab

## Conclusion

Z-indexes are something you occasionally have to modify and the biggest thing to keep in mind is that you need to have the element with a position absolute or relative on it. And the parent of a positioned element, if it has a z-index, creates separate min and max of what the children can be. That's all for now.
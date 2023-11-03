+++
author = ["Bruce"]
categories = ["Front End"]
date = 2022-06-02T04:00:00Z
description = "Looking at block vs inline and how it changes the way the box model behaves. "
image = "/images/inline-block.jpg"
product = "https://www.redbubble.com/i/poster/Block-and-Inline-by-thebruce13/112643751.LVTDI?asc=u"
tags = ["Box Model", "Beginner", "Css"]
title = "Box Model: Inline and Block Elements"

+++
When I originally started to write this blog post I was going to make one master post about each component that make up the box model. However, after I wrote most of it, I realized there is a lot that goes into each part of the box model. And they would be better suited to have thier own post.

So here we are. This is the first part of several. We will be talking about display inline vs block. We're starting here because the way the rest of the properties behave depends on if it is block or inline.

The property in particular that is going to be examined is `display` there are many values you can set this to. But they will fall into two types within the context of box model, inline or block.

**Inline Display Properties**

* Inline
* Inline-block
* Inline-flex
* Inline-grid

**Block Display Properties**

* Block
* Grid
* Flex
* Flow-root

Knowing what elements are inline and what elements are block is one of the main building blocks of front-end design. There is a lot that gets affected when you set the display value. The first one we will look into is how children elements are affected.

## Children Elements

When you set the display value on an element you are telling them how you want it to show up on the page but values like flex and grid really upend the flow for the child elements. 

[Rachel Andrew has a fantastic series](https://www.smashingmagazine.com/2019/04/display-two-value/) about that where she dives into the nitty-gritty of `display`. Pretty much you need to know when you are setting an element to display: block. you are setting two values: block and flow. You can see all of the different values on the [MDN article for display](https://developer.mozilla.org/en-US/docs/Web/CSS/display). The first value is how the container will behave in the flow of the document and the second is how its contents will behave.

For example, when you set something to `display: inline-flex` you are setting the container to be `inline` and the inside elements to be set to `flex` items. Essentially that hyphenated word sets the display property as such. `display: inline flex`. If you want more detail about how this works I <span style="text-transform: uppercase">highly</span> suggest reading the Rachel Andrew article I linked earlier. For now, it is enough to know that what you set it to can affect what it contains. But what does this have to do with Box Model?

## Display Inline and Box Model

Inline is named as such because it has the element stay inline with its neghboring content. Things like a span would render imperceptable to the user because it stays within the content.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;">
<iframe src="https://giphy.com/embed/cirUel4KlD2Cfz3gUF"
width="100%" height="100%" style="position:absolute"
frameBorder="0" allowFullScreen></iframe></div>

Inline affects how the elements of the box model are displayed, namely that vertical padding, margin, and top/bottom borders don't affect the surrounding elements.  However, the space they take up horizontally will be calculated and respected. This JS fiddle illustrates how it works out:

<script async src="//jsfiddle.net/brucifer906/r9vwjhd6/3/embed/result/"></script>

The text with the border has these attributes:

    .border {
      padding: 2%;
      margin: 2%;
      border: 2px solid blue;
    }

as it shows, there is space to the left and right but not to the top and bottom. This same ignoring of rules is applied to the height attribute. An inline element with a height or width property set will have it ignored. If you need an inline element to be taller, you can modify it using the [line-height attribute](https://www.brucebrotherton.com/blog/brief-talk-about-line-heights/). Wider, you can set the padding, margin, [letter-spacing](https://www.w3schools.com/cssref/pr_text_letter-spacing.asp), or [word-spacing](https://www.w3schools.com/cssref/pr_text_word-spacing.asp). That about wraps it up for inline elements and the box model, but we need to talk about one more thing before moving completely into Block elements.

### Inline-Block Elements

Inline-block elements, as the name suggests, are a hybrid of inline and block. This display property is incredibly useful when you need things to be a set height. It is worth keeping in mind this works similarly in inline-flex and inline-grid. I use this just about every time I need to put a menu together.

I typically will use an unordered list to make a nav, this makes it easier for screen readers to parse that it is a list of items. However, this makes all the list items displayed as `list-items` which behaves similar to a block-level item. This is not ideal for when you want them to go across the width of the page instead of up and down. So if we set the items to `display: inline-block` we can set the width of them to a percent so they only take up so much room. So if we have 5 items in the nav we can set the width to `width: 20%` and it'll respect that width and leave them to be all in one line.

Full Disclosure, this is the old way of managing this - nowadays I'd be reaching towards the parent element (the `ul`) and set it to `display: flex; justify-content: space-between;` this will throw its child elements in one row regardless of what they have their display property set to and space them out nice and evenly.

## Display Block and Box Model

Now that inline elements are wrapped up we can move on to block elements. They are called block elements because they make a whole new box to work on. It breaks the flow of the elements and will take up as much space as it can.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;">
<iframe src="https://giphy.com/embed/1FZqAOn4hzGO4"
width="100%" height="100%" style="position:absolute"
frameBorder="0" allowFullScreen></iframe></div>

Block elements will repsect all widths, heights, paddings, margins you set on them. . . mostly. There are a lot of things inside a block element that have stuff to worry about and we're going to go into them all in later posts. Right now, if you set any of them as a unit like px, em, rem; they will calculate and be respected. One thing that may throw you for a loop is when you set a width on an element and then a padding on it.

### How Big is that Box?

By default web elements are set up with sizing being content-box focused. That will make it so that the size of the box starts at the content portion ( the center ) an then expands from there. So, if you set the width to 100px and then add 10px of padding to the left and right it will have a calculated width of 120px. This was the default behavior for the web and set in [the CSS 2.1 specification](https://drafts.csswg.org/css-sizing/#box-sizing). Because when the W3C introduce additional features they make sure old specs don't break, they will not change the default behavior. That is excellent for backwards compatability but, when we are trying to lay out our web elements it is very confusing.

The alternative is to use `box-sizing: border-box` this will make is so when you set a width on something then add padding the content portion will shrink to accomodate the padding and the width will stay the same. So if we had the following code for two boxes:

    .box {
      width: 200px;
      padding: 20px;
      border: 5px solid red;
    }

But set one to `box-sizing: border-box` and the other we left at `box-sizing: content-box` we would end up with two different width items. The **border-box** would be 200px wide and the **content-box** would be 250px wide. This JSfiddle illustrates it. It also contains some JavaScript that calculates the widths in a console . 

<script async src="//jsfiddle.net/brucifer906/qawgh42o/2/embed/result,js,html,css/"></script>

It is worth mentioning that border-box starts its width at the edge of the border. Thus both the border and the padding will make the content area shrink in order to accommodate them.

The last thing I want to touch on here is that the content can't be less than 0. So if you have a width of 100px and set the border to be 300px it will push outside of the width of its container and give you some funky results.

I think that is all for now. I'll be following up with the finer points of height and width properties next time.
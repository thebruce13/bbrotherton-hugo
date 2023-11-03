+++
author = ["Bruce"]
categories = ["Front End"]
date = ""
description = ""
draft = true
image = ""
product = ""
tags = ["Css"]
title = "Box Model"

+++
The worldwide web is a collection of boxes. Every piece of content is a box. Boxes rule the world. But what is this "Box Model"? How can you use it to your benefit? Let's take a closer look at it so we know how we can break outside this wrapper.

## TL;DR

The Box Model is one of the base foundations of the web. The size of the box depends on five things.
•	Width
•	Height
•	Padding
•	Border
•	Margin
Know these properties and you can mess with the box model in just about every way. Just be wary that inline elements don't respect all of them.

There is a bunch in this post, honestly, it should have been three.

## Inline vs Block

Default elements in HTML are laid out as `display: inline` or `display: block` there are many in the two categories and you can check all the \[inline elements here\] and all the \[block elements here\]. Inline elements are designed to flow with the content. So when you wrap some text with  `<span>` it won’t break the line or respect any properties that affect the vertical spacing of an element and will also ignore the width attributes. However, it gives you the ability to change anything else with CSS. With the example below the text with the blue background has some margin and padding that are applied to the top and bottom as well as a border. All of those would change the height of the element if it was `display: block` , however, with inline, it will flow content as if there was no height set to it.

<script async src="//jsfiddle.net/brucifer906/sejLdhy6/26/embed/result,html,css/"></script>

### Inline-Block

There is a way to get inline elements to respect the vertical attributes. That is to assign the element to have `display: inline-block`. This will allow the element to stay in the flow but allow you to apply styles that normally wouldn't be respected by an inline element.

### Flow-root, Flexbox, and Grid

There are three other types of `display` properties and they are `flow-root`, `inline` and `grid`. While these are all awesome display types, when it comes to the box-model they all behave as if they are `display: block` so we won't be going further into them. Though, keep `flow-root` in mind for when we mention margin collapse later.

## How Big is that Box?

Part of the box-model is how the boxes are sized, or rather, their `box-sizing` and there are two values for this.

* `content-box`
* `border-box`

I have a preference for border-box, and [I set everything to it](https://www.brucebrotherton.com/blog/css-inherit-property/). But we will explore them both here.

### Content-Box

`box-sizing: content-box` is the out-of-the-box way content is defined on the web. It was how the [specification was in CSS2.1](https://drafts.csswg.org/css-sizing/#box-sizing) and is, therefore, the default. When box-sizing is set to content-box it is telling the browser that the element's content is where the width will be coming from (you know, the most inner box in the graphic).

For example, let's imagine this scenario:

We have a bunch of text that we only want to be 500px wide, we want a border around it but not sitting exactly on its edge. We also want to give it some breathing room around its other elements so it won't feel cramped around them either. Our code would look like this:

```  
.cool-box {
  width: 500px;
  padding: 10px;
  border: 2px solid currentColor;
  margin: 10px;
}
```

And that will make sure that our text stays right where we want it inside the box. It won't get any smaller no matter what kind of padding or border we place on it. This is great if we have elements that only need to worry about content, the full width of the piece would end up being 524px wide and that is confusing when you are trying to set up the layout of a page.

### Border-Box

Border-box is the solution to using elements for layout. It makes setting attributes a lot more predictable and makes my brain hurt less when setting up things for websites.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;">
<iframe src="https://giphy.com/embed/13FrpeVH09Zrb2"
width="100%" height="100%" style="position:absolute"
frameBorder="0" allowFullScreen></iframe></div>

When the element is set to `box-sizing: border-box` it calculates the size that you set as where the border ends (the line around the padding and content in the picture) and then squeezes in the content down so it will respect that set size you set on it.

Back to our previous example when we set the width to 500px,  it would remove 24 pixels from inside the box, reducing the size the content can fill up. The content area can never be less than 0. If you tried to make a box take up no width but kept the padding, the padding won't collapse into itself to reduce the space, it would surround the 0 sized content and keep its width.

## Setting Properties

Setting the properties of these elements in the box-model is simple enough though there are some differences between them.

### Content Box: Width and Height

You can set the width and height with[ just about every unit available](https://www.w3schools.com/CSSref/css_units.asp). The only caveat is that when you set the height of an element in percentages it will not calculate it unless its [parent has a defined height](https://stackoverflow.com/questions/7049875/why-doesnt-height-100-work-to-expand-divs-to-the-screen-height). It can't calculate 100% of \[undefined\].

<script async src="//jsfiddle.net/brucifer906/vLroey5a/embed/result/"></script>

[An example of this can be found on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/width). Here are a couple of examples below. As stated before, the content cannot be less than 0, any negative values will be invalid.

     width: 100px; /* set to 100px */
     width: 20em; /* set to 20 times the container's font size */
     width: 50%; /* set to 50% of the container */
     width: 15rem; /* set to 15 times the base font size */
     width: auto; /* the default set width */

### Padding

[Padding](https://developer.mozilla.org/en-US/docs/Web/CSS/padding) can use the same units as width. Just like the content box, negative values will be invalid. There are a couple methods you can use to set padding, all at once, individually, or 2 by 2.

All at once is also considered the shorthand. And it is set in the order of top|right|bottom|left.

`padding: 10px 1rem 0.75em 10%`

Notice you can mix units inside of the declaration. It could be very handy for when you need a certain value on the top and bottom and a variable value on the left and right.

Two by two is where you can set the top and bottom and the left and right in a shorthand fashion.

`padding: 0.5rem 5%`

This rule will give us padding on the top and bottom and 5% to the left and right. That way it'll shrink the passing between things as the browser squeezes in. A good technique when coding for responsive design.

After this we can set all four the with the same value by setting just one value.

`padding: 1rem`

This will set the padding on all four sides to 1rem.

Lastly, we can set padding with individual attributes.

`padding-left: 0`

This is a common way to reset the padding on an unordered list. However there is another way you can reset this, using `padding-inline-start` go over these settings in [my blog post "You're Padding All Wrong"](https://www.brucebrotherton.com/blog/you-re-padding-all-wrong/). You are able to set the four sides individually in simliar fasions.

    /* Set all sides to have 5px of padding */
    padding-top: 5px;
    padding-right: 5px;
    padding-bottom: 5px;
    padding-left: 5px;

### Margins

Margins are set very similar to padding. Being able to se them all at the same time,

    margin: 1rem 2% 0.5em 0.1vw; /* Set four individual values */
    margin: 0 auto /* set 0 top and bottom and fill what space is around on the left and right */
    margin: 0; /* set marign to 0 on all sides */
    margin-left: 10px; /* set margin on lef to 10px */
    margin-bottom: 10vw /* set margin on the bottom to 10% of the window width */ 

One of the biggest differences between margins and paddings is that the `auto` setting is not 0 on left and right but [is 0 on top and bottom](https://www.w3.org/TR/CSS2/visudet.html#Computing_heights_and_margins). Whereas for padding it is 0 all around.

Also, margin can be negative! This can be handy when you need things to be shoved one way or another. <script async src="//jsfiddle.net/brucifer906/fvnxd3ap/embed/result,html,css/"></script>

Although, if you need to move something with an animation, it is suggested to use transforms to [achieve the 60 frames per second](https://medium.com/outsystems-experts/how-to-achieve-60-fps-animations-with-css3-db7b98610108) because they are the easiest for the browser to render.

### Borders

The last thing we will go over is [Borders](https://www.w3schools.com/cssref/pr_border.asp), they have the most stuff to style, though they are probably the most straightforward to use. This is the property that is used to calculate our width when we set our `box-sizing: border-box` The width is applied to this part of the box model and then any padding or border is applied within the border, and it squeezes our content box in.

There are three properties to a border, the [width](https://www.w3schools.com/cssref/pr_border-width.asp), the [style](https://www.w3schools.com/cssref/pr_border-style.asp), and the [color](https://www.w3schools.com/cssref/pr_border-color.asp). Each of them can have a value set for any side of the box. Style is required in order for the border to be displayed and take up space. The default value for border are as follows:

    border-width: medium; 
    border-style: none; 
    border-color: currentColor;

If currentColor is unfamiliar to you, it will allow you to apply whatever color the font is to the border color. Typically you will be setting the border with the shorthand `border` property like so:

`border: 2px solid #2ad`

This will put a line all around the box that is 2px wide that is a rad blue color. Now, what are each of these? Well, the border property is setup like so: `border: width style color`. And each of those can be set individually if you would like.

    border-width: 2px;
    border-style: solid;
    border-color: #2ad;

Now each of these properties can all be applied similar to padding and margin. So we can set the top, right, bottom, left like so:

    border-width: 2px 0.125rem 5px 1px; /* top: 2px, right: 0.125rem bottom: 5px; left: 1px */

#### Border Width

Border-width, as you can see in the above example, can accept most units, however, percent is [not applicable according to the CSS spec](https://drafts.csswg.org/css-backgrounds/#propdef-border-top-width).

There are also keywords you can use for border and they are:

* Thin
* Medium
* Thick

The actual size of them is up to how the browser wants to implement them but they will always follow that thin is the thinnest and thick is the thickest.

#### Border Style

Border style is responsible for if the border is displayed or not. If it is set to "none" the border's width gets set to 0 and not displayed. There is a multitude of styles to choose from. "Solid" is the go-to for today's flat design, but there are many more.

    /* Keyword values */
    border-style: none;
    border-style: hidden; 
    border-style: dotted;
    border-style: dashed;
    border-style: solid;
    border-style: double;
    border-style: groove;
    border-style: ridge;
    border-style: inset;
    border-style: outset;

Each of these you'll have to try out yourself - they all change the style of the border and are pretty self-explanatory. All except for "hidden"; it behaves just like "none" [unless it is applied to a table](https://www.sitepoint.com/border-style-css-property#border-style__bordersvalue2).

You can apply these on a border-by-border basis or all around.

    border: solid dotted groove ridge;
    border: solid;
    border-bottom-style: double;

#### Border Color

Same as the other properties, you can apply `border-color` to each or all.

    border-color: cyan /* all borders are cyan */
    border-color: red green blue yellow; /* red top, green right, blue bottom and yellow left */

Its default value is `currentColor` and it will take whatever color is applied to the font and put that for the border color. A great thing to use when you are making buttons that also have hover states. It lets you have a "set it and forget it" kind of implementation.

<script async src="//jsfiddle.net/brucifer906/9ty6c51e/embed/result,html,css/"></script>

* inline vs block
* how big is that box (box-sizing)
* setting prop
  * Width
  * Height
  * Margin
  * Padding
  * Border
* outline and box-shadow tricks
* margin collapse
  * fixed
* overflow
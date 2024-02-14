+++
author = ["Bruce Brotherton"]
categories = ["Front End"]
date = 2021-10-10T00:30:00Z
description = "A brief introduction to the inhert property of CSS."
image = "/images/inherit.jpg"
product = "https://www.redbubble.com/i/poster/Inherit-Abstract-by-thebruce13/95903015.LVTDI"
tags = ["Css", "Beginner", "Tips and Tricks"]
title = "CSS Inherit Property"

+++
The inherit property in CSS is a tricky one. One of my favorite ways to use it is to set box-sizing.

## Inherit on box-sizing

```css
html {
  box-sizing: border-box;
}

*, *::before, *::after {
  box-sizing: inherit;
}
```

This inherited box-sizing setting is [slightly better best practice](https://css-tricks.com/inheriting-box-sizing-probably-slightly-better-best-practice/) than just setting it across the board. It will then allow for elements that are designed to use `content-box` to work correctly. Like if you have a plugin or component that has the styles set that way. If you are more interested in box-sizing, [CSS-Tricks has a good article about box-sizing](https://css-tricks.com/box-sizing/).

Here we want to talk about `inherit` and how you can use it on your projects. Earlier I made a [post using it for a background-image](https://www.brucebrotherton.com/blog/breaking-the-wrapper/) in order to make an element appear outside of its container. But first, we'll take [the definition from MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/inherit):

> The **`inherit`** CSS keyword causes the element for which it is specified to take the [computed value](https://developer.mozilla.org/en-US/docs/Web/CSS/computed_value) of the property from its parent element.

## Inherit on link colors

It is a really handy when you want things to be brought through on children items. I constantly have to borrow styles from the parent elements. One way I do this is when I have to change the color of the background for a section, I also have it set up the color of the text.

```css
.background-black {
  background-color: #0a0a0a;
  color: #eee;
}
```

This sets up the section to be black and the color of the text white. Now, usually you don't set a color on your paragraph tags so we aren't going to worry about that. However, I almost always set my links to a certain color. For this example we'll set it to black.

```css
a {
  color: #0a0a0a;
}
```

So as you can imagine, if we had a link inside of this `.background-black` it'll become invisible. An easy fix would be to just set the color to white.

```css
.background-black a {
  color: #eee;
}
```

But now what if we had three different colors and each had to have their own text color?

```css
.background-black {
  background-color: #0a0a0a;
  color: #eee;
}

.background-yellow {
  color: #fc0;
  color: #7462e0;
}

.background-image {
  background-image: url(...);
  color: #000;
}
```

At this point we will use our friend `inherit`. We can group them all under one rule with one value.

```css
.background-black a,
.background-yellow a,
.background-image a {
  color: inhert;
}
```

This way they will grab their color from the background rules, inheriting the styles and looking perfectly in line with the text surrounding it.

**A quick warning about matching your links to your paragraph text:** [You need to make them look distinguishable from the rest of the text](https://webaim.org/techniques/hypertext/link_text#appearance) AND have a hover/focus state that is different than its original state. By default links have an underline so they look different that way. A way I take care of the hover is to remove the underline.

```css
a:hover {
  text-decoration: none;
}
```

### Wrapping up Link Styles

Using and [advanced attribute selectors](https://moderncss.dev/guide-to-advanced-css-selectors-part-one/#attribute-selector) we could write this whole rule in one go.

```css
[class*="background-"] a {
  color: inhert;
}
```

This rule will select any element that has a class that contains "background-" and then its `a` tag to apply the color to it.

## Going on from here

Inherit is one of the niche rules you can use instead of writing excessive CSS. With some forethought you can make things magically and seamlessly work together. It is worth reading up on the difference of inherit, initial, and unset. [The MDN article about inherit I linked earlier](https://developer.mozilla.org/en-US/docs/Web/CSS/inherit) is a good place to start. I also suggest reading about how [some attributes have inheritance by default](https://developer.mozilla.org/en-US/docs/Web/CSS/inheritance) and some do not. That's all for nw.
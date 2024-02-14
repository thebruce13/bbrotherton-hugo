+++
author = ["Bruce Brotherton"]
categories = ["Front End"]
date = 2021-11-01T23:00:00Z
description = "Talking about the CSS property line-height."
image = "/images/lines.jpg"
product = "https://www.redbubble.com/i/poster/Lineheight-Abstract-by-thebruce13/95903141.LVTDI"
tags = ["Beginner", "Tips and Tricks", "Css"]
title = "Brief talk about Line Heights"

+++
Line height, you love it you need it. And according to [WCAG 2 you need it to be 150%](https://www.w3.org/TR/WCAG20-TECHS/C21.html) or more. So what do you do?

## TL;DR

The easiest way to make your site comply with the WCAG guidelines is to set the `p` line height to 1.5. This is super quick and dirty but it is like 90% of where this needs to be. Still there are other areas where you may need to address this.

```css
p {
  line-height: 1.5;
}
```

## Why Don't We Use Units?

[Line height](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height) is one of the few properties in CSS that do not require a unit at the end of it. Although you can put an `em, rem, px, %` on it. It is best practice to not.

Why? You ask. It is because of how this property is [inherited down to its descendants](https://drafts.csswg.org/css-inline/#line-height). If we set the line-height with `em`s it is based off where it was first set and then that height is set down to its descendants.

[As you can see with this fiddle](https://jsfiddle.net/brucifer906/khtb37xs/). The example on the left has set the line height on the wrapper to `1.5em` and the one on the right has it set to simply `1.5`. This is something that is a little unpredictable and undesired. However, the heading is way spaced out on the other because the font-size is bigger - this is also undesired.

Notice, however the paragraph looks identical on each example. That is because the `em` in this case is based off of the document's font-size and so is the `p`'s font-size. We might want to make the rule a little less overreaching in order to keep things looking right.

[Now in this next example jsfiddle](https://jsfiddle.net/brucifer906/khtb37xs/3/) they are both looking fine, however I've added a `big` to a couple words to make them stand out more, notice that the line-heights on each are slightly different. In this context it could be understandable to use either `ems` or no unit. However, it isn't as forward thinking because we aren't always sure what our font sizes will be on our elements and could lead down a rabbit hole of trying to control the line-heights.

On some sites I've been asked to increase the line height to 2 as well as bring up the font-size. This would cause an overall larger effect and if a heading was slapped in the middle there with an `em` line height it could look really squashed.

This behavior is also exhibited with percent, rem, and px. Using no unit gives it a more forgiving "set-it and forget-it" when it comes to children of the parent that gets the line-height.

So, yeah. That is my long winded case for not putting a unit at the end of your line-heights. But also be aware of what level you are setting them on. That's all for now.
+++
author = ["Bruce Brotherton"]
categories = ["Front End"]
date = 2022-02-06T05:00:00Z
description = "There is a different way to get your padding inline other than setting padding: 0; Come a long and see."
image = "/images/packing-s.jpg"
product = ""
tags = ["Tips and tricks", "Css"]
title = "You're padding all wrong"

+++
I just recently found other padding and margin options besides the typical `padding:0 0 0 0` and `margin: 0 0 0 0`. I was inspecting a tricky list item that wasn't behaving and I discovered: `padding-inline-start: 40px`, the browser default. So instead of brute-forcing this with `padding-left: 0` I used `padding-inline-start` instead and my problem was solved.

Now, as a bit of an old hat in web design, I was used to just putting in padding-left on my unorganized lists to make them fall in line with the text. Typically, that was enough, and I never had to think about it again. And as you can see from this JSFiddle, there is no difference between padding-inline-start and padding-left.

<script async src="//jsfiddle.net/brucifer906/uk7qL2d6/2/embed/result,html,css/"></script>

However, this is kind of overkill when adjusting these values. And as I discovered while researching this, less versatile than using the `padding-inline-start`.

## Coding for Other Languages

So, if we were in a world where all languages read left to right we'd have an easy time. The padding-left would work, and we'd be set. However, the reality is that languages get written in more than one way. Some from top to bottom, others from right to left.

Now if we had a list of items that go across the top and run down vertically, we'd want to set our `padding-top` to modify the spacing.

<script async src="//jsfiddle.net/brucifer906/8dkv3osh/3/embed/result,html,css"></script>

However, `padding-inline-start` automatically adjusts for where the start of the line padding begins! It'll do the same adjustment if the language goes right to left.

Btw, to set these writing rules - if you didn't already know - it is with the property `writing-mode`

    .vertical-right-to-left {
    	writing-mode: vertical-rl;
    }
    
    .right-to-left {  
    	writing-mode: rl;
    }

## Setting up the Fab Four

In Latin based languages we are setting the padding-left or padding-inline-start. However there are 3 other properties that will set our padding-top/right/bottom as well. Here is a table showing what we would pick to set each of these up.

<table border="1" cellspacing="0"> <tr><th>New</th><th>Old</th></tr> <tr><td>padding-block-start</td><td>padding-top</td></tr> <tr><td>padding-block-end</td><td>padding-bottom</td></tr> <tr><td>padding-inline-start</td><td>padding-left</td></tr> <tr><td>padding-inline-end</td><td>padding-right</td></tr> </table>

This sets up our padding across all four sides if we need it setup this way. Now I don't want to say you should do this for everything, if an element is there for display purposes you don't or maybe shouldn't use these properties on it. Or if it is set up to be the same accross all four directions the simple `padding: 1rem` is better.

Setting the padding will end up overriding these values no matter where they are set in the cascade.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;">
<iframe src="https://giphy.com/embed/rh0W2vpayXMac"
width="100%" height="100%" style="position:absolute"
frameBorder="0" allowFullScreen></iframe></div>

## There is Margin too

As there is padding, there is also margins and they follow the same naming convention, just replace padding with margin so it will readout `margin-block-start` and that would take care of your margin-top. So, knowing this we could affect our paragraph tags to have a margin without doing a hard `margin-top: 0.5rem;` or if you were being fancy, you would do this:

    p {
        margin-top: 0; 
    }
    
    p + p { 
    	margin-top: 0.5rem; 
    	margin-bottom: 0; 
    }

But this is another brute force method to get our paragraphs to follow a style we want. By default, the browser has `margin-block-start` and `margin-block-end` set to `1em`. We can just target them to work how we want. It is pretty much identical to how we did it in the past but, it is targeting the right values to override and is more adaptable for when we switch what direction the text goes.

    p {
        margin-block-start: 0; 
    }
    
    p + p { 
    	margin-block-start: 0.5rem; 
    	margin--block-end: 0; 
    }

### Margin Collapse

There is a word of caution when playing with margins on elements and that is with margin collapse. It is still a problem I struggle to wrap my head around. These properties will respect it just as setting the margin traditionally on items does. I modified the [MDN article about margin collapse's](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing) example code here to show that it behaves the same.

<script async src="//jsfiddle.net/brucifer906/zLx4sjpy/embed/html,css,result/"></script>

[Carlos Filho has a great article](https://dev.to/camfilho/margin-collapse-explained-by-images-361e) with images to illustrate the behavior of margin collapse. I suggest you give it a go if you run into trouble with margins.

## What about IE?

Yes, there is a chance older browsers won't work with these rules, according to [caniuse.com](https://caniuse.com/?search=padding-inline-start "Can I use statistics for padding-inline-start") these rules are not supported in IE11 or Classic Edge and were implemented in Chrome 69, which was released in September 2018. This will make things tricky because there is no easy progressive enhancement for these rules, if you set a margin or padding it will overwrite them.

There is a workaround using CSS where you can target IE 10+ and give them padding instead. So our styles would look something like this:

    p {
      margin-inline-start: 0px
    }
    
    @media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
      /* IE10+ CSS styles go here */
      p {
        margin-left: 0;
      }
    }

There are other[ CSS hacks to target IE browsers](https://gist.github.com/vidaaudrey/c16774076391d09e7ec7dbb7ed7a3189) that you can use if you need to get them to work properly. There are also [conditional comments](https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/compatibility/ms537512(v=vs.85)?redirectedfrom=MSDN) that you could use to bring in IE-specific styles, unfortunately, they are were no longer supported by IE11.

And that is all there is really to know about these newish padding rules. Guess it pays to see what the browser is putting on your elements by default. That's all for now.
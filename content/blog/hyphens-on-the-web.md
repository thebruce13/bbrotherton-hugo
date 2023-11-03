+++
author = ["Bruce"]
categories = ["Front End"]
date = 2021-12-01T04:00:00Z
description = "How do end of line hyphens work? Lets dive into hyphens on the internet and how we can get these words to wrap."
image = "/images/hyphens.jpg"
product = "https://www.redbubble.com/i/poster/Hyphens-Abstract-by-thebruce13/95902382.LVTDI"
tags = ["Beginner", "Tips and tricks", "Css"]
title = "Hyphens on the Web"
tshirt = "https://www.teepublic.com/poster-and-art/26017863-hyphens"

+++
## TL;DR

There is a set place for words to hyphenate and based on your set language in the HTML tag, the computer will insert hyphens where they belong. However not all words will hyphenate (especially proper nouns). `overflow-wrap: break-word` will make those words break without a hyphen.

```html
<style>
  .hyphenate_force-break {
    hyphens: auto;
    overflow-wrap: break-word;
  }
</style>

<html lang="en" class="hyphenate_force-break">
  ...
</html>
```

## Using Hyphens

When I was in high school I always thought that when I wanted to use a hyphen at the end of a word, I could just slap one down and continue the word on the next line. It didn't matter to me if it was the first letter or the one just before the last, I needed to break the word up and I was running out of space. However, that just isn't how hyphens work.

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/OMZRxGyZZ6fGo" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

Now, for an in-depth look at when to use hyphens in your context I highly recommend [Tara McInnis' four part article](https://5catsproofing.com/she-had-gold-green-catlike-eyes-hyphenation-and-compound-adjectives/) about hyphens. However, we are particularly interested in her last entry, End of Line Hyphens. These are the only ones we can affect using CSS and they are the topic of discussion because we're trying to fix when words are too long for their container.

The first thing we need to set the language of the site, if this is missing the browser cannot insert hyphens in words correctly because it doesn't know what dictionary to compare the word to. In the example below, I've shown a few languages and country codes that are available to the lang attribute. [W3 schools has a full list of available languages](https://www.w3schools.com/tags/ref_language_codes.asp), with a link to [country codes](https://www.w3schools.com/tags/ref_country_codes.asp) as well. Keep in mind that if you were to combine a language with a country that isn't recognized to speak that language it will [stick with the default language](https://stackoverflow.com/questions/11318961/what-is-the-difference-between-html-lang-en-and-html-lang-en-us). It is a good idea anyway if it is relevant, because, it could help with search engines and screen readers.

    // Set Language to English
    <html lang="en">
     
    // Set Language to English, Country: Great Britan  
    <html lang="en-GB">
    
    // Set Language to English, Country: United States 
    <html lang="en-US">  
    
    // Set Language to German
    <html lang="de">

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;"> <iframe src="https://giphy.com/embed/hvU6wNliMXsc" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

### Hyphens have rules

Once the language is set the browser will know where it can start breaking up words. Of course since different languages have different syntaxes; hyphens also follow certain methods. I'll discuss a couple of them here, I only have experience in English so rules may vary based on your language and how it decides to use [soft wraps](https://drafts.csswg.org/css-text/#soft-wrap-opportunity).

#### Capitals and Hyphens

My first issue was words that were long in my headings. These already had large fonts to begin with but when I gave them the ability to be extra large, they were unreasonable on mobile. And, guess what - **if a word is capitalized, it won't get hyphenated**. You can check out [my jsfiddle that has a few examples](https://jsfiddle.net/brucifer906/3u9v4ejx/10/) on hyphenating capitals and words. This right here is 99% of my struggles with hyphens.

> The Unicode Annex (UA) may use language-tailored heuristics to exclude certain words from automatic hyphenation. For example, a UA might try to avoid hyphenation in proper nouns by excluding words matching certain capitalization and punctuation patterns.
>
> \- [W3C Editor Draft - Hyphenation Opportunity](https://drafts.csswg.org/css-text/#hyphenation-opportunity)

#### Word Lengths and Hyphens

According to the [W3C Working Draft on Hyphenation](https://www.w3.org/TR/css-text-4/#hyphenation) that unless our UA can figure out a better method to break the word, our CSS will only break words that are longer than 5 characters and needs at least 2 letters before and after the break. There is a CSS rule to override this behavior and an example is below,

```css
/* This will allow the UA to set the minimum length of the word,
 however, it will force it it have a minimum of 3 before
 and 4 letters after the hyphen. */
p { hyphenate-limit-chars: auto 3 4; }
```

With this we could make sure our end of line hyphens follow the Chicago Manual of Style.

> * There is a minimum of two letters before the break. That means if the first syllable of a two-syllable word doesn’t have at least two letters, you can’t break the word.
> * There is a minimum of three letters after the break. Again, that means that for a two-syllable word, the second syllable must have at least three letters, or you cannot break the word.
>
> \- [5 Cats Proofreading](https://5catsproofing.com/the-end-of-the-line-hyphenation-and-word-breaks/)

#### Consecutive Hyphens

[Richard Rutter article about hyphens](https://medium.com/clear-left-thinking/all-you-need-to-know-about-hyphenation-in-css-2baee2d89179) is fantastic and you should read it. In it he talks about hyphen ladders and how in English you should limit it to about two in a row. However, in German they have many ladders because of the nature of their words. By default, there is no limit to [how many hyphens can happen](https://www.w3.org/TR/css-text-4/#propdef-hyphenate-limit-lines) in a row, if you wanted to change this you would use this code:

```css
p { hyphenate-limit-lines: 2; }
```

#### Last Line Hyphens

The last rule I want to cover here is the last [line of the paragraph](https://www.w3.org/TR/css-text-4/#propdef-hyphenate-limit-last). Should it get hyphenated? The default behavior for CSS is yes. I think that is okay, because the user already has seen hyphens through the document and the last word being hyphenated won't be a surprise. Still aesthetically I could see wanting to keep the last word of the paragraph together and you can do that with this rule:

```css
p { hyphenate-limit-lines: always }
```

## Force Wrapping Text

So all of this ability to finesse our hyphens we still are left with words that stick off the page and will not get hyphenated. If there isn't a [syllable ](https://www.unicode.org/reports/tr14/tr14-47.html#Dictionary)in the word for the browser to insert a soft wrap it won't get hyphenated. An example word is that is monosyllabic is "squelched." So how are we going to make this fit on the page then?

### Overflow-wrap vs Word-break

There are two ways to break words up without hyphens.

```css
p { overflow-wrap: break-word; }
/* or */
p { word-break: break-word; }
```

Now these two do the same thing, and actually word-break: break-word will override [overflow-wrap](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow-wrap) regardless of its value. Off the bat I'm going to tell you to use overflow-wrap simply because [word-break: break-word is deprecated](https://developer.mozilla.org/en-US/docs/Web/CSS/word-break).

<div style="width:100%;height:0;min-height:200px;padding-bottom:25%;position:relative;">
<iframe src="https://giphy.com/embed/3o6wrASxYzLbE9JWE0"
width="100%" height="100%" style="position:absolute"
frameBorder="0" allowFullScreen></iframe></div>

To be honest I didn't know about overflow-wrap until Rachel Andrew linked me to an article of hers called ["Making things Better"](https://rachelandrew.co.uk/archives/2020/04/07/making-things-better/) you should definitely read it, it talks about a lot of the things I am interested in on the web and thinking a little outside the content-box.

## Manual Hyphens

I would be remiss if I didn't mention that you can insert your own word breaks for hyphens using the `&shy;` or **s**oft **hy**phen unicode character. You will need to set your css hyphenate to _auto_ or _manual_ in order to achieve hyphens using this character. It will allow you to insert line break hyphens wherever you choose regardless of any other rules. The browser will insert a hyphen at this point first and then, if there is still part of the word that is too long, it will continue to hyphenate. Granted, that is only if `hyphens: auto` is set, otherwise it will only wrap where you put in the `&shy;` character. [This jsfiddle](https://jsfiddle.net/brucifer906/q256maph/1/) has examples of how it will work given the three types of hyphen attributes.

### Standard Hyphens

So far we've only talked about auto hyphens and not the standard ones you can just insert where ever. The hyphen, em-dash, en-dash, and the non-breaking hyphen. Now just as there are rules that dictate when the browser can insert hyphens there are rules in grammar of when to use these other types of hyphens.

#### Hyphen - &amp;hyphen;

A [hyphen](https://www.toptal.com/designers/htmlarrows/punctuation/hyphen/) is used when things are closely connected, taking an example from Tara's article earlier, "well-behaved" would use a standard hyphen. Honestly, I throw these out willy-nilly because I am not an certified grammar expert. So I'll be paraphrasing [Marvin Forte](https://marvinforte.com/hyphens-en-dashes-and-em-dashes-dont-let-friends-dash-incorrectly/) for the next two dashes. 

#### En Dash – &amp;ndash;

The [en dash](https://www.toptal.com/designers/htmlarrows/punctuation/en-dash/) is a little longer than the hyphen and is usually the same width of the N character. It is typically used to signify "through" like two dates. 

> I grew up during the 90s,  1990 – 1999.

#### Em Dash — &amp;mdash;

The [em dash](https://www.toptal.com/designers/htmlarrows/punctuation/em-dash/) is the longest of the hyphens. It is typically the same width of the letter M and is used to break up a sentence or in place of quotations.

#### Non-Breaking Hyphen ‑ &amp;#8209;

The [non-breaking hyphen](https://www.toptal.com/designers/htmlarrows/punctuation/non-breaking-hyphen/) is something new to me and you'd think that after I've written this blog post all about hyphens I'd have known about it but I came across if after a client asked if it existed. It does! I like to use it when putting in telephone numbers on a page so they don't drop to the next line. 

#### Horizontal Bar ― &amp;horbar;

This last dash isn't a hyphen at all but I wanted to include it in case you just needed something with a little more [umph](https://www.google.com/search?q=umph&rlz=1C5CHFA_enUS949US959&ei=fpUCYq-tPIWmptQPgpecOA&ved=0ahUKEwiv5IPtvvD1AhUFk4kEHYILBwcQ4dUDCA4&uact=5&oq=umph&gs_lcp=Cgdnd3Mtd2l6EAMyBAgAEEMyBAgAEEMyBwgAELEDEAoyBQguEIAEMgQIABBDMgsILhCABBDHARCjAjIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQ6BwgAEEcQsAM6BwgAELADEEM6CggAEOQCELADGAA6EgguEMcBENEDEMgDELADEEMYAToMCC4QyAMQsAMQQxgBSgQIQRgASgQIRhgBUIMPWOgPYLgQaAJwAngAgAGIAYgBiAGSAQMwLjGYAQCgAQHIARLAAQHaAQYIABABGAnaAQYIARABGAg&sclient=gws-wiz) than other hyphens. I can't give you rules on this one maybe best to keep to stylistic elements. 

## Conclusion

So that is the long and short of it. When you have really big fonts that start with capital letters, your browser isn't going to want to hyphenate it and you'll have to rely on `overflow-wrap: break-word` to get the job done. This will give us the closest we can to having things be intelligible while providing our users with tools to make the webpage a little more friendly. That's all for now.
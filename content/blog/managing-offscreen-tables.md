+++
author = ["Bruce"]
categories = ["Front End"]
date = 2021-10-22T23:02:00Z
description = "A method to display tables offscreen when they are too big."
image = "/images/table-1.jpg"
tags = ["Responsive Design", "Javascript", "Tips and tricks", "Css"]
title = "Managing Offscreen Tables"

+++
What do you do when you have a table on your website and you need it to be viewable on mobile? [CSS Tricks has an excellent post about responsive tables](https://css-tricks.com/responsive-data-table-roundup/) and getting the data to shift and look correct on mobile. Most of them have some very fancy tricks to make them viewable and all of them are viable. My method is a little simpler in its approach.

## TL;DR, The Code

[My codepen](https://codepen.io/brucebrotherton/pen/VwvPvaW) has everything all put together so if you're looking for a quick look at it all or can pretty much figure it out from there. It's available. However, if you'd like a dive into each bit we will start with why this is the method I chose.

## The Problem

What we were facing was user generated tables inside our Content Management System (CMS), think WordPress. And given that the user could put whatever they wanted inside the cells we couldn't predictably scale down the columns to fit the text. Users also had the option to set the columns a set width, even further messing up the design. This left us with the problem that this table could be any width and would push outside our website and past the frame of the mobile device. This, of course, was unacceptable.

### The Easy Fix

The quick fix is to just slap `overflow-x: scroll` on a wrapper div and call it a day. This will allow the user to scroll left or right on the table and access all the info.

<div style="width:100%;height:0;min-height:200px;padding-bottom:200px;position:relative;"><iframe src="https://giphy.com/embed/12e5dX36aMp2Ba" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div><p><a href="https://giphy.com/gifs/something-how-front-12e5dX36aMp2Ba">via GIPHY</a></p>

Sadly that isn't enough. How can a user know there is additional content to the right without some sort of indicator? We could use an arrow but, unless we have a bunch of them, going down the entire side, there is a chance people will miss it _(actually I've seen this done and you could even hook up a click event to the arrows to make it scroll for you)._ We chose a subtler approach to make shadows on the sides to indicate there is more content to the left or right, kind of as like its a roll of parchment.

## Figuring out the HTML and CSS

Just like our example above, we will be wrapping the table in a DIV so we can set its properties for the overflow, as well as some other necessary CSS styling.

```html
<div class="offscreen-scroll">
  <table>...</table>
</div>
```

So now that we have this wrapping `.offscreen-scroll` div we can start setting up the CSS to add the shadow to the table. All of our code will be hitting this div so it is imperative that it is wrapped in it. First we got to setup our wrapper to be able to contain the shadows and be able to scroll left and right.

```css
.offscreen-scroll {
	position: relative; /* Contain the shadows inside it. */
	width: 100%; /* Be as wide as it's container */
	max-width: 100%; /* Not let it get any wider than the container */
	overflow: auto; /* This rule allows us to scroll left and right but only when we need to */
	overflow-y: hidden; /* Makes sure the vertical scrollbar dosen't show up */
}
```

Now we are going to set up the shadows on for the wrapper using the [pseudo element](https://developer.mozilla.org/en-US/docs/Web/CSS/::after) `::after`. Below are rules that both the left and the right shadows share.

```css
.offscreen-scroll::after {
	content: '';
	position: absolute;
	top: 50%; /* Center the shadow vertically, part 1 */
	left: 0;
	z-index: 1; /* Keep shadows above the content inside the wrapper */
	transform: translateY(-50%); /* Center the shadow vertically, part 2 */
	width: 100%;
	height: 200%; /* Stretch the area outside the bounds of the container so we don't see top and bottom shadow */
	pointer-events: none; /* Be able to click through the shadows */
	transition: box-shadow 0.5s; /* Fade in the shadows */
}
```

After those rules have been set up it is a matter of adding the box shadows to the left and right or both. It is simply a matter of offsetting the X value of box-shadows in order to place the correct side inside the wrapper. Otherwise we setup the spread to be 10px so it insets the same on both sides. [You can read more about the box-shadow property over at MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow)

```css
.offscreen-scroll.shadow-right::after {
	box-shadow: inset -10px 0 10px rgba(0,0,0,0.25);
}

.offscreen-scroll.shadow-left::after {
	box-shadow: inset 10px 0 10px rgba(0,0,0,0.25);
}

.offscreen-scroll.shadow-left.shadow-right::after {
	box-shadow: inset 0 0 10px 10px rgba(0,0,0,0.25);
}
```

## On to the JavaScript

Now that we have the CSS setup we will need to make it so it will work when you scroll. Currently nothing will appear different. The first thing we want to check for is the all important `.offscreen-scroll` wrapper. If it isn't there, we need to add it. Once it is confirmed to be wrapping our table we will need to throw it into a variable.

```javascript
// Grab all the
const offScreenScrollers = document.querySelectorAll('table');

const wrapTable = function(table) {
  // If the wrapper was put there manually, we don't need a second one.
  if ( !table.parentElement.classList.contains('offscreen-scroll') ) {
    const wrapper = document.createElement('div');
    wrapper.classList.add('offscreen-scroll');
    table.parentNode.insertBefore(wrapper, table);
    wrapper.appendChild(table);
  }
}

offScreenScrolller.forEach( function(table){
  wrapTable(table);
  // Grab the wrapper
  const offscreenWrapper = table.parentNode;
});
```

Next we will be checking to see if the table has scrollbars or if it is past the max width of the table. Keep in mind we are still working within our `forEach` loop from above.

```javascript
// Setup variables to be used later
let hasHorizontalScrollbar = false;
let maxWidth ='';

/* Check the wrapper scrollable width vs it's displayed width. */
const hasScrollBar = function(){
  hasHorizontalScrollbar = offscreenWrapper.scrollWidth > offscreenWrapper.clientWidth; // Checks if the scrollWidth is wider than the clientWidth, if so makes the variable true.

  if ( hasHorizontalScrollbar ) {
    offscreenWrapper.classList.add('shadow-right');
  } else {
    offscreenWrapper.classList.remove('shadow-right', 'shadow-left');
  }
}();
```

So far this will run when the page is loaded, that is because of the `()` at the end of the function declaration. Fun fact, that is called an IIFE (pronounced iffy) or [Immediately Invoked Function Expression](https://developer.mozilla.org/en-US/docs/Glossary/IIFE). Now it'll attach the shadow to the correct side of the table when you load up. However, it won't move so when the user scrolls it'll just stay in one spot.

<div style="width:100%;height:0;min-height:200px;padding-bottom:300px;position:relative;"> <iframe src="https://giphy.com/embed/ao9uBG75JSIcE" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

We we'll have to set some javascript to make the shadow stick to the edge of the screen when they scroll. Still inside the `forEach` loop

```javascript
function tableScrollHandler(table){
  var scrollPosition = Math.abs(table.scrollLeft - offscreenWrapper.scrollLeft); // Get the current scroll position
  var maxWidth = getMaxWidth();
  var maxScroll = table.clientWidth - maxWidth; // Get the furthest the user can scroll
  var percentScrolled = (scrollPosition/maxScroll).toFixed(2); // See how far the user has scrolled

  // Offset the psudo element to stay with the current view.
  offscreenWrapper.style.setProperty('left', scrollPosition + 'px');
  hasScrollBar();

  // Toggle shadows
  if ( hasHorizontalScrollbar === true ){
    if ( 0.05 < percentScrolled && 0.95 > percentScrolled ) {
      offscreenWrapper.classList.add('shadow-right', 'shadow-left');
    } else if ( 0.05 >= percentScrolled ) {
      offscreenWrapper.classList.add('shadow-right')
      offscreenWrapper.classList.remove('shadow-left')
    } else if ( 0.95 <= percentScrolled ) {
      offscreenWrapper.classList.add('shadow-left')
      offscreenWrapper.classList.remove('shadow-right')
    }
  } else {
    offscreenWrapper.classList.remove('shadow-right shadow-left');
  }
}

offscreenWrapper.addEventListener('scroll', function(){ tableScrollHandler(table) } );
```

So this will get the bar in there, moving left and switching sides when it gets closer to the other edge. And we are just about done. The last thing we need to do is recalculate the need for the shadow and where the offset sits when they scale down the window.

```javascript
window.addEventListener('resize', function(){
  hasScrollBar();
  getMaxWidth()
});
```

And that is just about it. We can now zoom from left to right with the shadows on the side.

<div style="width:100%;height:0;min-height:200px;padding-bottom:200px;position:relative;"> <iframe src="https://giphy.com/embed/ClFhnciqiinwk" width="100%" height="100%" style="position:absolute" frameBorder="0" allowFullScreen></iframe></div>

<span style="text-transform: uppercase">But wait</span>, what is this? The shadows don't stick to the edges of the screen! If your computer is anything like mine it can't calculate the correct spot for where they should be while its scrolling. A easy way to fix this is to put an outline on the wrapper div so it is still shaded while it pulls off the edge of the page.

```css
.offscreen-scroll::after {
  outline: 105vw solid rgba(0,0,0,0.25);
}
```

We made it 105vw so it will be larger than the viewport so no matter how fast the user moves that scrollbar around it will still be darkened. The cool thing is this adds a little bit of fun to the page because it gives the window a little bit of overlapping action.

Now I personally don't like setting a transform value in the the HTML style tag so I would swap that with a CSS variable. `--left` seems appropriate. This will change these lines on our CSS and our JS.

```css
.offscreen-scroll::after{
  transform: translate( var(--left,0),-50%);
}
```

This one will go inside of the loop.

```javascript
// Set the left css vairalbe 0
offscreenWrapper.style.setProperty('--left', '0');
```

Update the tableScrollHandler, where it has `style.setProperty('left' ...` with this

```javascript
offscreenWrapper.style.setProperty('--left', scrollPosition + 'px');
```

## Wrapping it up

Here is the CSS all put together.

```css
/* Offscreen table shadow CSS */
.offscreen-scroll {
	position: relative;
	display: flex;
	width: 100%;
	max-width: 100%;
	overflow: auto;
	overflow-y: hidden;
}

.offscreen-scroll::after {
	content: '';
	position: absolute;
	top: 50%;
	left: 0;
	z-index: 1;
	transform: translate( var(--left,0),-50%);
	width: var(--maxwidth, 100%);
	height: 200%;
	pointer-events: none;
	transition: box-shadow 0.5s, left 0.05s linear;
	outline: 105vw solid rgba(0,0,0,0.25);
}

.offscreen-scroll.shadow-right::after {
	box-shadow: inset -10px 0 10px rgba(0,0,0,0.25);
}

.offscreen-scroll.shadow-left::after {
	box-shadow: inset 10px 0 10px rgba(0,0,0,0.25);
}

.offscreen-scroll.shadow-left.shadow-right::after {
	box-shadow: inset 0 0 10px 10px rgba(0,0,0,0.25);
}
```

Here is the JavaScript

```javascript
// Grab all those tables baby!!
const offScreenScrollers = document.querySelectorAll('table, [data-offscreen-scroll]');

offScreenScrollers.forEach( table => {
	// If the wrapper was put there manually, we don't need a second one.
	if ( !table.parentElement.classList.contains('offscreen-scroll') ) {
		const wrapper = document.createElement('div');
		wrapper.classList.add('offscreen-scroll');
		table.parentNode.insertBefore(wrapper, table);
		wrapper.appendChild(table);
	}

	// Grab the wrapper
	const offscreenWrapper = table.parentNode;

	// Set the left css vairalbe 0
	offscreenWrapper.style.setProperty('--left', '0');

	// Check if the wrapper has a scrollbar.
	var hasHorizontalScrollbar = false;
	var maxWidth ='';
	function hasScrollBar(){
		hasHorizontalScrollbar = offscreenWrapper.scrollWidth > offscreenWrapper.clientWidth;

		if ( hasHorizontalScrollbar ) {
			offscreenWrapper.classList.add('shadow-right');
		} else {
			offscreenWrapper.classList.remove('shadow-right', 'shadow-left');
		}
	};
	hasScrollBar();

	// If the parent container is smaller than the window, that is the max width. Otherwise use the window width.
	// Obviously will break if the parent isn't responsive.
	function getMaxWidth(){
		var maxWidth = offscreenWrapper.parentElement.clientWidth < offscreenWrapper.clientWidth ? offscreenWrapper.parentElement.clientWidth : window.innerWidth;
		return maxWidth;
	}

	window.addEventListener('resize', function(){
		hasScrollBar();
		getMaxWidth()
	});

	function tableScrollHandler(table){

		var scrollPosition = Math.abs(table.scrollLeft - offscreenWrapper.scrollLeft);
		var maxWidth = getMaxWidth();
		var maxScroll = table.clientWidth - maxWidth;
		var percentScrolled = (scrollPosition/maxScroll).toFixed(2);

		// Offset the psudo element to stay with the current view.
		offscreenWrapper.style.setProperty('--left', scrollPosition + 'px');
		hasScrollBar();

		// Toggle shadows
		if ( hasHorizontalScrollbar === true ){
			if ( 0.05 < percentScrolled && 0.95 > percentScrolled ) {
				offscreenWrapper.classList.add('shadow-right', 'shadow-left');
			} else if ( 0.05 >= percentScrolled ) {
				offscreenWrapper.classList.add('shadow-right')
				offscreenWrapper.classList.remove('shadow-left')
			} else if ( 0.95 <= percentScrolled ) {
				offscreenWrapper.classList.add('shadow-left')
				offscreenWrapper.classList.remove('shadow-right')
			}
		} else {
			offscreenWrapper.classList.remove('shadow-right shadow-left');
		}
	}

	offscreenWrapper.addEventListener('scroll', function(){ tableScrollHandler(table) } );
})
```

That's all for now, I hope this gets your tables in order so people with phones know about all your awesome table content that is off the screen. I'd suggest you take a look at the [codepen provided](https://codepen.io/brucebrotherton/pen/VwvPvaW) to see it in action.

**Update 4/19/2023**
I discovered that using the transform property instead of the left will remove the lag that seemed to happen when interacting with the element. The code is updated on this page to use that now.
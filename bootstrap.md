# Bootstrap conversion

## Source from Project 1 of Eric Meyer's book On CSS.

This project went a long way to taking a late 90s early 00s web page and began to use CSS to take care of visual layout. The simplified HTML structure is arguably easier to maintain, yet there is still a bit of cruft left in to handle layout, which is anathema to today's way of thinking. Beyond that, it doesn't really provide enough semantic structure to the information being laid out. Don't even get me started on how it is not responsive (that wasn't even a thing when this book was written).

So, we will take this project a step further.  We will apply some HTML semantics to the page.  And will use Bootstrap to handle the layout and get the page to be a little more responsive.

I think that the hardest part of this assignment will be doing something about the masthead background image.  I will save that for last, because I don't know how I am going to do it, but I would like to not edit the asset and instead do something to deal with it in CSS.  We'll see if that is even possible.

First we will make a copy of the old file to use as a reference.

Next let's rip out all the CSS, because we need to work on adding bootstrap and working on our markup, before we even need to worry about styling again.

Now we'll  set the `doctype` correctly:

```
<doctype html>
```

Let's go get bootstrap and include the necessary files.  Go to [Get Bootstrap](http://getbootstrap.com) and download the latest distribution of bootstrap.

For now we will only include the stylesheet as I don't think we will need to use anything that requires any of the features that have JavaScript as a dependency.  Since I am riding along with you guys as I do this, I may change my mind down the line and add those assets in.  I will include the font files for referential integrity of the CSS files, and I can at least replace the asterisks in the ratings with a groovier icon.

So, I will make a **css** folder and put the following files in it (including the *.map file so Chrome won't bitch at me):

```
bootstrap.css
bootstrap.css.map
```

and I will create a **fonts** folder and include all the files there.

Now let's reference the bootstrap css and see what we get without doing anything at all.

```
<link rel="stylesheet" href="css/bootstrap.css">
```

If we look at the high-level page layout, we have the three standard *rows* of content:

* header
* content
* footer

So, not really a modern way of making a masthead bar, I will leave it alone and not try to create what this company should be doing today.  For one, it is generally good to have some site-wide navigation, but that can come from the team after we get the sit layout done in bootstrap.  The upshot is that this needs to be in a `header` element since it is the header. and we will break the two table cells into to two `div` elements:

```
<header>
	<div>...</div>
	<div>...</div>
</header>
```

I will keep the ids since those add some semantics to the content. When we start applying bootstrap styles, we can consider removing those ids (assuming they aren't being used for some other purpose).

Before we section off the next part, I will need to format the code a bit, since the content and the footer are mixed together in a big, ugly layout table. I need to see what I am working with as I start to dismantle it.

Since the footer stuff doesn't belong there, let's rip it out and put it in its own `footer` section. Again each of the table cells we will turn into `div` tags. We'll keep the ids for now:

```
<footer>
    <div id="feedback"><a href="/feeback.html">Feedback - Contact</a></div>
    <div id="tg">Travel Guide</div>
    <div id="copyright">Copyright 2002</div>
</footer>
```

I have been wanting to focus on semantic markup and avoid bootstrap for the time being, but I will make an exception this time.  Namely, bootstrap provides a class called `container` that I want to use for my content section:

```
<div class="container">
...
</div>
```

That action brings a ton of consequences.  Lots of font and margin/padding changes.  But also, it leads us to start thinking in terms of what bootstrap will want from us for the layout.  This is not a bad thing though, as we can use it to get rid of all the table mess and start to think about semantics again on the other side.

The first thing I notice is that the page below the header is essentially divided into two columns. Even though there is the right column, it is up under the breadcrumb widget, so our two columns are the **Destinations** column, and everything else.  I am not sure if the semantic intention was to give so much weight to **Destinations**, but given the layout, that is what I will assume.

Bootstrap uses a grid system to lay out content horizontally.  The grid is divided into 12 columns and you decide how many of those columns the content should occupy.  My screen resolution is much larger than was typically for back in the day, but from working the excercise I have a feel for how far to zoom everything in, which in my case was ``<ctrl> - +` 5 times.

Left-side was set at 120px. Right-side at 150px.  Content takes up the remainder.  Left and right give us 270px.  In 2002/2003 average screen widths were transitioning from 800px to 1024px.  So that means that content was taking up between 530px and 754px.

We will be dividing our second column into two columns also.  The bootstrap grid system works is that within containers, the container itself is dividing up into 12 columns.  So, working backwards, if we figure out how the content and the right side divide up their space, that should give us some insight into how much to allocate to the left side and everything else. Clear as mud.

The right column was supposed to take up a fixed width of 150px and the content was somewhere between 530px and 754px which has the right side taking up between 22% and 16.5%.  I will go with the latter to start.

What do we have now? I am going to start with 2 columns for my left side and 10 columns for everything else.  With the "everything else", I will have my content use 10 columns and my right side to take 2 columns.  Hopefully that will be close.  

When I code this up I need to remove some table stuff as well. My result will be this structure:

```
<div class="row">
	<div class="col-sm-2">
		Left side
	</div>
	<div class="col-sm-10">
		Everything else
	</div>
</div>
```

Note: I just spent several minutes trying to figure out why my layout was not rendering correctly.  Since I have the page zoomed in, the bootstrap media queries are being hit and causing a smaller form factor to fire. I will change my classes from **md** to **sm** which is probably the right answer anyway, since back in the day, that is what the screen resolution was in a way.

I will put the left side stuff in first.  I will leave the links in a table for now, but **Destinations** I will make an `<h2>`:

```
<h2></h2>
```

That's really big.  So, I will need to style that down the road.  Alternatively, it could just mean that for **sm** this layout is simply inappropriate.  When I size back out to regular size, there is a crap-ton of whitespace, so there is definitely some decision I will need to make about form factors before all is said and done.  But right now is not the time, because there are still an uncomfortably large number of tables lying around.

Referring back to the old layout, we have two rows, one for the breadcrumbs that will take up all 12 units. And one that is shared by our content and our right side bar, which we already decided would take 10 and 2 respectively.  So, let's annihilate a couple more tables.

First two rows:

```
<div class="col-sm-10">
	<div class="row">
		...
	</div>
	<div class="row">
		...
	</div>
</div>
```

Then just one row inside our second row div, with a 10 column and a 2 column:

```
<div class="row'">
	<div class="row">
		<div class="col-sm-10">
			...
		</div>
		<div class="col-sm-2">
			...
		</div>
	</div>
</div>
```

Okay, it is obvious that `col-sm-2` is wrong.  Let's bump that up:

```
<div class="col-sm-9">
...
</div>
<div class="col-sm-3">
...
</div>
```

Already, using bootstrap and modern coding shows its advantage.  That was much easier to do than it would have been in the past.

In retrospect, there is one table that I think I will leave in.  The ratings stuff is tabular in nature, so I believe it makes sense to leave that one.  Each of the units in this right-hand bar though, seem to be panels to me, so I will make them panels. (Making the left-hand nav a panel, might be my solution over there too...  but maybe I have to give up the left-hand nav as out-dated and come up with a new solution.  Too soon to tell... forward.)

So, panels:

```
<div class="col-sm-3">
	<h4>Ragged Point Inn &amp; Restaurant</h4>
	<div class="panel panel-default">
		<div class="panel-heading">Ratings</div>
		<div class="panel-body">
			...
		</div>
	</div>
	<div class="panel panel-default">
		<div class="panel-heading">Price</div>
		<div class="panel-body">
			...
		</div>
	</div>
	<div class="panel panel-default">
		<div class="panel-heading">Contact</div>
		<div class="panel-body">
			...
			</div>
	</div>
	<div class="panel panel-default">
		<div class="panel-heading">Nearby Stops</div>
		<div class="panel-body">
			...
		</div>
	</div>
```

In the first panel, we will leave the table, and I will come back to that, because bootstrap has some table stuff that we should be able to use.

The price text I just put right in that panel's `panel-body`.

The **Contact** and **Nearby Stops** I changed from tables to `ul` because bootstrap lets us do a lot of stuff with `ul` and `ul` is the right answer anyway since this is list stuff.

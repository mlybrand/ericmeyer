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



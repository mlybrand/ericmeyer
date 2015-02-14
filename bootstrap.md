# Bootstrap conversion

## Source from Project 1 of Eric Meyer's book On CSS.

This project went a long way to taking a late 90s early 00s web page and began to use CSS to take care of visual layout. The simplified HTML structure is arguably easier to maintain, yet there is still a bit of cruft left in to handle layout, which is anathema to today's way of thinking. Beyond that, it doesn't really provide enough semantic structure to the information being laid out. Don't even get me started on how it is not responsive (that wasn't even a thing when this book was written).

So, we will take this project a step further.  We will apply some HTML semantics to the page.  And will use Bootstrap to handle the layout and get the page to be a little more responsive.

I think that the hardest part of this assignment will be doing something about the masthead background image.  I will save that for last, because I don't know how I am going to do it, but I would like to not edit the asset and instead do something to deal with it in CSS.  We'll see if that is even possible.

First we will make a copy of the old file to use as a reference.

Next up is to set the `doctype` correctly:

```
<doctype html>
```
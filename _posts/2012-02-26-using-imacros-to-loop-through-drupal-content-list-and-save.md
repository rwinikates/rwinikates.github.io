---
layout: post
title: Using iMacros to loop through Drupal content list and save
date: "2012-02-26 16:17"
permalink: "blog/using-imacros-loop-through-drupal-content-list-and-save"
category: blog
tags: 
  - archive
published: true
---

#  Using iMacros to loop through Drupal content list and save

On a recent client project, I imported several hundred nodes from a legacy
system.  The problem was, when looking at the individual nodes, the titles
didn't appear.  After hitting edit and then save on that node though, the
title would show up.

After spending some time trying to figure out where the logic was that was
killing my titles, I decided to try fixing this another way.  I first tried a
variety of save commands through
[VBO](http://drupal.org/project/views_bulk_operations), but sadly
unpublish/publish, changing authors, nor just resaving all the nodes fixed my
issue, leading me to think that the nodes needed some piece of content (even
if blank or null) from the node submission form.

Stymied from a more elegant solution, with my deadline looming, I turned to my
old friend, the [iMacros Firefox extension](https://addons.mozilla.org/en-
US/firefox/addon/imacros-for-firefox/).  For those unfamiliar, it allows you
to record macros in your browser and then loop them in an automated fashion.
I recorded what the macro looked like to load the /admin/content screen, hit
the edit link and then hit save on the resulting screen.  This is what that
looked like:

````powershell
TAB T=1

URL

GOTO=[http://CLIENTDOMAIN/admin/content](http://CLIENTDOMAIN/admin/content)

TAG POS=1  TYPE=A ATTR=TXT:edit

TAG POS=1 TYPE=INPUT:SUBMIT FORM=ID:press-release-node-form ATTR=ID:edit-submit
````

This was all hunky dory, but would only do it for the top node on the content
list.  I had to find a looping variable.  Enter the {{!LOOP}} variable.  All I
had to do was change the position tag of the first instruction to correspond
to the loop iteration number and my browser was off to the races:

````perl
TAB T=1

URL

GOTO=[http://CLIENTDOMAIN/admin/content](http://CLIENTDOMAIN/admin/content)

TAG POS=\{{!LOOP\}}  TYPE=A ATTR=TXT:edit

TAG POS=1 TYPE=INPUT:SUBMIT FORM=ID:press-release-node-form ATTR=ID:edit-submit
````

Sadly this is a slower than I might like, but in the time its taken me to
write this post, my browser has looped through this macro 50 times, so it is
acceptably low involvement that I think I can use it to finish out this
project.  

Drop me a line if you have ideas as to why the nodes wouldn't show
the tile without manually saving it through the browser!
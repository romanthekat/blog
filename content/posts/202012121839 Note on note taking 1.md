---
title: "[11/100] Note on note taking 1"
date: 2020-12-06
draft: false
---

From time to time I review the way I do my notes taking.
I have a lot of notes on different themes, both personal and work stuff.
And for last few years I've being emacs org-mode.
I've tried quite a lot of different things and apps, from simple text files without any structure up to specialized tools. Yet still I come back to org-mode.

For a quite some time I've being reading about [[202012051855 Zettelkasten]].
In simple words - do short atomic notes, and interconnect such notes.

One note, [Create speculative outlines while you write](https://notes.andymatuschak.org/z2uXyfV67dnWLUKg1iDbsrHk3DGjtNWTxSTah), suggested an interesting idea - such atomic notes can get use of outlines. Table of content helps you get the context. Create a note of links to other notes.

It clicked that very moment - I started completely the other way around.

Org-mode in it's core is an overpowered outliner - hierarchy of notes.

But an attempt to make strict data hierarchies always ended up with problems for me - some notes 'belong' to several places at the same time, they have multiple 'parents'. 
Placing under one parent doesn't work - you are gonna lost it, you simply forget where _exactly_ you put it year+ ago. Finding them becomes an issue.
Adding links under all parents helps, but feels wonky. 
The fact it 'belongs' in several places confuses, that's an extra cognitive load. 

As a result I've restructured my notes about 5-6 times. 
Apparently it's really painful to have a 7+ levels of collapsable data.
Each time I tried to split the information in simpler chunks, often - simplifying the hiearchy.
[PARA Method](https://fortelabs.co/blog/para/) generally helps.
Yet still - hierarchy doesn't always work, current work flow exhasting at a time. 'A web' of associations should more native - at least feels so.

The thing I dislike at the moment is cognitive load I have with current notes taking process, searching notes, adding links, extracting useful things.
Up to a point I don't want to write new notes - finding the 'place' to add it consumes your time more than writing itself.

Reflecting on the way I write and read my notes, I found out that there are several things I care about the most:
## Important
- based on simple local text files, like markdown - so there is no vendor lock
- works offline
- supports links to notes
- has searching in notes
- possible to setup backups
- available on desktop and mobile
- has tags [[202012062108]] support (though not that critical)

## Nice to have features
- supports links to files on file system
- vim-mode for notes writing
- supports inline images
- backlinks generation

Thus I'm gonna give a try to zettelkasten/roam-like tools.
I will use Org-roam or The Archive apps in the next few months. 
---
title: "[13/100] 235 read articles and automatic outliner"
date: 2020-12-19
draft: false
---

For a few days I've being reading [zettelkasten](https://zettelkasten.de) related articles and previously mentioned [notes of Andy Matuschak](https://notes.andymatuschak.org).
Making totally about 235 articles. 
That was quite a long read. Tons of interesting stuff, resulting in some notes of/for myself.

Speaking of notes - so far 'web of interconnected notes' idea works fine for me. 
Connections you make usually based on your thinking and associations, as a result navigation feels natural - easy to remember and use.

But outline notes haven't being forgotten - that is a useful tool.
For example, when you read a book, or try to create get a grasp of something complex - starting with outline note can be useful. 
You keep refering to it to keep the context, making it more detailed as you go further. 
Preferably you create it manually during top-to-down thinking.
Alternatively, if you see possibly related ideas, or see some pattern in data, you can add such 'index' note in down-to-top way.

I once thought: if you have interconnected notes can you create such a context/index note automatically, can it be useful?
While doing it 'manually' you revisit all these notes, re-thinking all that thoughts again, you get more benefits of it. But possibly automatic summary can be useful too.

As a result I conducted an [experiment](https://github.com/EvilKhaosKat/r-notes), small program that accepts filepath to a note, then it checks the links from this note to other notes, recursively doing it again and again.

[Result](https://github.com/EvilKhaosKat/r-notes/) looks this [way](https://github.com/EvilKhaosKat/r-notes/blob/main/outliner.png) in The Archive app.
Seems like 3 levels of connections (note->links->links of links) work well. 
It doesn't overload you with tons of related notes (even 4 levels can be pretty messy), while giving you some extra context.
It doesn't support backlinking at the moment. Probably links itself should have a context (_why_ a note relates to other note - what was written nearby).
But still I've used it a couple of times.
So the experiment was successful. Though manual approach probably is more beneficial.

p.s. there was the same idea implemented by one of the authors from https://zettelkasten.de - a [ruby gem](https://github.com/DivineDominion/zettel-outline-rendering) back from 2016.
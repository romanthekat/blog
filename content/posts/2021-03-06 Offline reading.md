---
title: "[20/100] Offline reading"
date: 2021-03-06
draft: false
published: true
---

I rely on several apps and offline mode for reading. 

Probably the main app for me is [Pocket](http://getpocket.com). There are a lot of great articles you can find, and most of them will be saved in there.
Some will be tagged (top priority/first to read things, usually).  
On the other hand, I'm kinda curious in [wallabag](https://wallabag.org) (self-hosted open source solution with mobile version).

As a data source I often use RSS, for quite a set of blogs.  
I like the idea of 'pulling' information, rathen than 'being pushed' (as in email subscriptions, for example).  
Currently I use [Reeder](https://reederapp.com): it has mobile, desktop, native, blazing fast, apps.

Sometimes I want to keep reference material - a pdf file, or a collection of cheatsheets.  
For that I use [Zotero](https://www.zotero.org) - easy way to save a page or a file, collect, and organize such data. As an app and browser plugin.

Sometimes the whole site is needed. It could be something like [The Twelve-Factor App](https://12factor.net), [Learn X in Y minutes](https://learnxinyminutes.com), or dead and then reborned as a book ['statistics and cats'](https://www.litres.ru/vladimir-savelev-10569666/statistika-i-kotiki-28731109/).  
Old good 'wget' helps me with that: `wget -r -k -l 7 -p -E -nc https://12factor.net`  
Used options are: recursive, with offline links transformation, up to 7 levels deep, with all the static files, using .html extension, without rewriting existing files (helpful if you continue downloading).

There is also a niche case - offline documentation with searching. Usually IDEs have that out of the box, in some form, yet still I like to have offline documentation for different languages/frameworks ready to use.  
[Dash](https://zealdocs.org) or [Zeal](https://zealdocs.org) works here nicely.

Surely all these things are kept in a cloud(s). Which also helps with syncing between devices.  

And there are books, of course - but that's another story.


P.S. funnily I had quite a reproducible crash with desktop version of Pocket. Once I saved 6k+ articles 'for later', search and an article selection caused immediate failure.  
Had to 'fix' that by removing ~2k old pages: opened web version, sorted, filtered, and then executed in console (since there was no ability to bulk-select-remove at a time):  
```js
var list = document.getElementsByTagName("article");
for (let item of list) {
    item.click()
}
```
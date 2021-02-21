---
title: "[6/100] Food delivery notifier and 'machine learning'"
date: 2020-11-21
draft: false
---

There is a simple project of mine called [food delivery notifier](http://github.com/EvilKhaosKat/food-delivery-notifier).
It checks current food delivery status and shows it in system tray. As for me - a bit more convenient than constantly refresh the page.

Currenlty supported service has a map and coordinates info, it shows courier location.
So knowing how far away a courier is from restaurant or your place allows you to assess how long you'll be waiting for delivery.

Simple distance-based heuristic implemented a while ago is useful, but prone to errors.

So I'm thikning about more sophisticated estimation logic.

First I'm going to add order information logging, write down series of events - order created, is in cooking state, in delivery, and so on.
Having such logging on the app level is fast to implement.

After that - data can be transformed to extract some 'knowledge' out of it - basically how much time did it require to deliver the order.

My guess is if I gather enough records like 'date, restaurant, delivery time' combined with some regression-model (random trees, for example) it will do much more precise and reliable prediction, which can be actually used.
At the moment I think that combination of distance to restaurant, day time, weekday, and total cost can be sufficient.

Of course, all this data is only a small part of real delivery logistic process, there are a lot of details which are unknown.

But maybe it will work
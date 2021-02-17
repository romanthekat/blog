---
title: "[7/100] Food delivery notifier: first ML results"
date: 2020-11-24
draft: false
---

So the idea of using ML in [food delivery notifier](https://github.com/EvilKhaosKat/food-delivery-notifier) service did and did not work out.

On the one hand - everything went relatively smooth.
It was good to remember how to use python and ipython notebook, prepare and parse data (finite state machine for the win!), try out few regression models, make some 'insights'.

On the other hand - accuracy is really low.
It does predict 'scale' right, hour-two, but makes severe mistakes.

I've tried 8 different regression models so far, all of them are generally bad at assessing delivery time.
Only 'decision tree' approach gave me positive r2 score, though at 'weak' correlation level.

In other words - it does not really predict the outcome.

It is either lack of data (only ~300 entries), or mistakes in code, bad models tuning, or given data does not represent the process (it's much more complex, but we don't have the data on that); or a combination of all these things :)

I end up using following features:
- total cost
- distance between restaurant and home
- date, split in: year, month, day, day of the week, hour, minute

In these barely working models features importance is strange: it seems like total order cost is the most valuable parameter, while distance goes next, being ~3 times less important.
Minute of an order (start of hour/end of hour somehow?) goes next, and restaurant after that.
Other barely affecting the result.

That's not reliable at all, but funny to think about.

So, I will probably gather more data, and someday return/retry the whole thing, maybe with different results

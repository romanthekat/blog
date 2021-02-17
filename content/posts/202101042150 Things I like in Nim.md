---
title: "[16/100] Things I like in Nim lang 1"
date: 2021-01-05
draft: false
---

#language
There is an open-source programming language called Nim.
It is a statically typed compiled language, looks a lot like python (small amount of syntax noise combined with spaces for identation/code blocks).

Example from official site:
```nim
import strformat

type
  Person = object
    name: string
    age: Natural # Ensures the age is positive

let people = [
  Person(name: "John", age: 45),
  Person(name: "Kate", age: 30)
]

for person in people:
  # Type-safe string interpolation,
  # evaluated at compile time.
  echo(fmt"{person.name} is {person.age} years old")
```

A 'bigger' example, reading json from file and mapping it to an object:
```nim
//{
//    "name": "Some app",
//    "entries": [
//        {
//            "startTime": "2021-01-04 22:21:45 +00:00",
//            "caption": "start"
//        },
//        {
//            "startTime": "2021-01-05 22:21:45 +00:00",
//            "caption": "end"
//        }
//    ]
//}
import json

type 
  Entry = ref object
    startTime: ZonedTime
    caption: string

  App = ref object
    name: string
    entries: seq[Entry]
 
 
 let app = readFile("data.json")
             .parseJson()
             .to(App)
```

So to my taste it looks pretty clean.

Also Nim compiles fast (10k+ SLOC per second), which is convenient and hard to overestimate.

Nim supports 'higher-order functions', so you can do easily do something like that:
```nim
import strutils, sequtils

let input = ["1", "2", "3", "4", "5"]
let sum = input
            .mapIt(it.parseInt)
            .filterIt(it > 2)
            .foldl(a + b)
```

Besides that, it also supports so-called Uniform Function Call Syntax (also can be found in Dlang).
UFCS allows any function to be called using the syntax for method calls using first parameter as a receiver, for example (from Wikipedia):
```nim
type Vector = tuple[x, y: int]
 
proc add(a, b: Vector): Vector =
  (a.x + b.x, a.y + b.y)
 
let
  v1 = (x: -1, y: 4)
  v2 = (x: 5, y: -2)
 
  v3 = add(v1, v2)         //this way
  v4 = v1.add(v2)          //or this way
  v5 = v1.add(v2).add(v1)  //or chain it
```

It simplifies calls chaining, and feels somewhat like Kotlin's extensions - you can add a 'method' to any type.

And I'm not gonna talk about metaprogramming/templates/macroses this time.

Nim memory management is GC, there are several garbage collectors out of the box: refc|arc|orc|markAndSweep|boehm|go|none|regions.
Overall performance is good, ~rust/go like (for [example](https://github.com/kostya/benchmarks)).

Most recently added ARC/ORC GCs are automatic references counting/with cycles detection algorithms, with a twist - fully deterministic at _compile time_.
More on that [here](https://nim-lang.org/blog/2020/10/15/introduction-to-arc-orc-in-nim.html), and probably later after some tests.

Curiously, JetBrains recently added official Nim plugin to a number of theirs' IDEs. (not speaking of vim/emacs/vscode/etc. plugins)

There is also a packet manager called 'nimble', it also capable of simple project scaffoldings. That's really handy to have.

So for me Nim language is a real fun to use - you simply get used to nice amount of features combined with good readability and fast compilation and guarantees the language gives you. 
It's almost like you have everything you need.

The only thing I miss at this moment (apart from it being wildly popular) is 'interfaces' abstraction, which can be often found in other languages. 
I like the idea of 'checks' over 'behaviour' rather than over (generic) type.
On the other hand there is 'concepts' abstraction here, which technically should be a kind of superset to interfaces. But it's still experimental.

Thus from time to time I keep using Nim for little things here and there. Hoping to use it more in the future
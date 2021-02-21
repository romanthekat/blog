---
title: "[15/100] Ruby Christmas present and perspectives"
date: 2020-12-26
draft: false
---

As usual new major update for Ruby lang was announced on 25th of December.
Cool thing about this year - that's a [release 3.0](https://www.ruby-lang.org/en/news/2020/12/25/ruby-3-0-0-released/), aka [Ruby 3x3](https://blog.heroku.com/ruby-3-by-3).
Main things are:
- performance (x3 in certain benchmarks)
- new concurrency primitives (actor-like abstraction called Ractor and Fiber#scheduler for async event pool)
- optional typing (RBS files for types hinting and typeProf tool for types inference)

As for me, things I somewhat missed in Ruby were type hinting and more convenient concurrency primitives, especially once same ideas were added in Python (with async syntax and type hints). Gonna wait for ractors leave experimental.

Another ruby-related interesting thing recently announced is [Hotwire](https://m.signalvnoise.com/html-over-the-wire/) - server-side rendering technique, based on websockets, for fast delivering HTML pieces to the client. 
An alternative to SPA+JSON API and classic server side rendering.
That also reminds me about [LiveView](https://hexdocs.pm/phoenix_live_view/Phoenix.LiveView.html) from Elixir's Phoenix framework - quite the same idea of reactive updating client state/page without heavily relying on Javascript/client side MVC frameworks, keeping the rendering at server side.

What I like about all of it: yet another 'old' language joined the race of current industry well-embraced things: typing and concurrency. 
There are also several new languages getting traction - like golang, kotlin, rust.

I enjoy that there is something nice, interesting, promising happening non-stop. That never ending evolution is great, it eventually will bring us even more cool stuff
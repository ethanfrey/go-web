# Some general go best practices

(Found on the web)

The basics on using the language well: https://golang.org/doc/effective_go.html

A few more details on various points: https://talks.golang.org/2013/bestpractices.slide#1

A very nice overview of higher-level concepts to apply:
  https://peter.bourgon.org/go-best-practices-2016/
  
Some links that stood out are below


## Naming

A set of guidelines for naming things in go: https://talks.golang.org/2014/names.slide#1


## Configuration

Adding lots of config options can make it hard to expose a simple API.  Here are some ideas:

First, Dave Cheney walks through the standard approaches (which work fine for smallish number of arguments), and presents the idea of functional options: http://dave.cheney.net/2014/10/17/functional-options-for-friendly-apis

And, if you like the approach, read more in depth about functional options (and auto-generating the "undo") here: https://commandcenter.blogspot.de/2014/01/self-referential-functions-and-design.html
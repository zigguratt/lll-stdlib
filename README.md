# lll-stdlib

## A standard library of LLL macros.

*WARNING: `stdlib.lll` is a work in progress. There will be changes and additions.*

In my explorations of LLL over the past few months I've come up with a set of macros that make working with the language easier, and make reading the Lisp-like source code clearer. Some of the things that appear in these seemingly simple macros took a very long time to resolve owing to the dearth of LLL documentation&mdash;or even source code, for that matter.

I'm hoping to change this situation by creating and documenting these macros, publishing [other](https://github.com/zigguratt/ens-in-lll) LLL-based [projects](https://github.com/zigguratt/lll-constructor), writing [articles](http://blog.syrinx.net/the-resurrection-of-lll-part-1/), and participating in [online](https://gitter.im/ethereum/go-ethereum/name-registry) and [real-life](https://www.meetup.com/Ethereum-Developers/) communities to spread the news that LLL is a perfectly viable contract development language.

### The code

Since LLL is probably unfamiliar to most visitors to this repository, I'll go through the code step-by-step, clarifying what's happening at each step. You'll notice that I've added a fair bit of documentation to the macro library to make it easier to understand. The documentation is in Ethereum's [Natural Specification Format](https://github.com/ethereum/wiki/wiki/Ethereum-Natural-Specification-Format) which uses [Doxygen notation](http://www.stack.nl/~dimitri/doxygen/index.html). There's currently nothing that can extract this documentation from LLL source, but at least it's there if and when that capability does arrive.

*To be continued...*

# A standard library of LLL macros.

*WARNING: `stdlib.lll` is a work in progress. There will be changes, additions, and deletions.*

In my explorations of LLL over the past few months I've come up with a small set of macros that make working with the language easier, and make reading the Lisp-like source code clearer. Some of the things that appear in these seemingly simple macros took a very long time to resolve owing to the dearth of LLL documentation&mdash;or even source code, for that matter.

I'm hoping to change this situation by creating and documenting these macros, publishing [other](https://github.com/zigguratt/ens-in-lll) LLL-based [projects](https://github.com/zigguratt/lll-constructor), writing [articles](http://blog.syrinx.net/the-resurrection-of-lll-part-1/), and participating in [online](https://gitter.im/ethereum/go-ethereum/name-registry) and [real-life](https://www.meetup.com/Ethereum-Developers/) communities to inform others that LLL is a perfectly viable contract development language.

## The code

Since LLL is probably unfamiliar to most visitors to this repository, I'll go through the code step-by-step, clarifying what's happening at each step. You'll notice that I've added a fair bit of documentation to the macro library to make it easier to understand. The documentation is in Ethereum's [Natural Specification Format](https://github.com/ethereum/wiki/wiki/Ethereum-Natural-Specification-Format) which uses [Doxygen notation](http://www.stack.nl/~dimitri/doxygen/index.html). There's currently nothing that can extract this documentation from LLL source, but at least it's there if and when that capability does arrive.

## How macros work

LLL macros do one thing: they substitute symbols in source code with the value that's been assigned to the symbol in its macro definition. This process happens at compile time. For example, with a macro definition like this:
```
(def 'scratch-one 0x00)
```
when the compiler encounters the string "scratch-one" in an LLL source file it will substitute that string with `0x00`. Similarly, given this macro definition:
```
(def 'shift-left (input)
  (mul input (exp 2 224)))
```
when the compiler encounters
```
(shift-left (calldataload 0))
```
in source, it replaces that code with
```
(mul (calldataload 0) (exp 2 224))
````
LLL macros fall into two categories: simple assignments&mdash;what I call *constants*&mdash;and more extensive code substitutions. Both effectively do the same thing, but I find it helpful to separate them out conceptually in order to clarify source code.

## Constant definitions

*To be continued...*

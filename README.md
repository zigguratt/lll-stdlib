# A standard library of LLL macros
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
At the top of the `stdlib.lll` file is a set of simple assignments. The first two should be self-explanatory: `true` and `false`. LLL doesn't have a concept of booleans so this is a convenient way to use `true` and `false` in your code instead of `1` and `0`. In case it was unclear, macros are defined using the LLL keyword `def`.

The next macro, `stdlib-version`, is used to verify that you're using the appropriate version of this macro library in your contracts. A simple comparison between this number and the number you've defined in your source allows you to abort your contract's deployment if there's a version mismatch.

`hold-back`, here defined as `1000`, is the amount of gas that is withheld from the amount being sent to another contract to pay for its execution. The idea is that your contract will need gas to continue execution in the event that the callee "throws" and consumes all gas sent to it. So instead of sending all of your gas, you hold back a small amount. `1000` is a bit high, but it's also an extremely small portion of 1 eth so it's not unreasonable.

The next set of macros under *Memory layout* define how memory is used by these macros. The first two, `scratch-one` and `scratch-two`, aren't [Dr. Seuss characters](http://vignette4.wikia.nocookie.net/seuss/images/d/d3/Thing1-and-thing2.jpg/revision/latest?cb=20131013015212) as you might expect. They're used as temporary memory locations for various operations. In this library only `scratch-one` is used, but it's not unusual for both to be used for a longer keccak hash calculation.

*To be continued...*

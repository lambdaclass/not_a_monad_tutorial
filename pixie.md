# Interview with Timothy Baldridge, creator of the Pixie language

> We interviewed [Timothy Baldridge](https://twitter.com/timbaldridge), creator of [Pixie](https://github.com/pixie-lang/pixie), a small, fast, native lisp with _magical powers_. We hope you try it out!

![Timothy Baldridge](./img/timothybaldridge.jpeg)

### Please tell us a little bit about Pixie’s inception and the road to the current status.

I've been a language hacker for years, and have played around with RPython (PyPy’s tool-chain) for some time. I've always had it in the back of my head that a lisp on RPython would be a good project. But it seems like this time it’s really taken off.

I started the project about 3 months ago, and by now it’s grown quite a bit. The standard library is about to hit 2000 loc (lines of code), and we have about half a dozen contributors. Not bad for only a few months work.

### Why a new language? Is Pixie an exercise in language design, an attempt to build a language to target production code or is that still to be determined?

There are a few experiments I’ve tried at different times in Pixie’s lifecycle, but at this point I’m really aiming for Pixie to be a “Python-esque lisp”. That is to say, if you’re doing lightweight scripting, or want something that boots fast and runs well on low-end systems, Pixie might be a good fit. Basically I want it for all those times I’d reach for Python instead of Clojure.

### What are Pixie’s main features?

- It’s a lisp.
- It stresses the use of immutable data structures.
- It’s not hosted on the CLR, JVM or any other pre-existing VM.
- It’s quite fast as it includes a tracing JIT.
- FFI (Foreign Function Interface) support is currently quite primitive, but FFI on par with Python’s ctypes or Lua’s FFI are planned and in the works.

### What is the reason behind including transducers from the start?

Much of what is needed for a robust run-time can be built with transducers. Operations such as hashing a collection, converting a collection to a string, or even comparing two collections, can be built with transducers. And since the JIT produced by RPython is a tracing (instead of a method) JIT, transducers are extremely efficient, often faster than transducers implemented in other languages.

### Why would developers choose Pixie? Who are Pixie’s target users?

If you like Clojure, but are unhappy with the start-up time, or if you want something outside of the JVM ecosystem, then Pixie may be for you. For much of my work Clojure is a perfect choice, but once in a while I find myself reaching for a lighter language, like Python. Hopefully Pixie will allow me to stay in a Lisp in those situations as well.

### Why did you implement it in Python?

Technically I implemented Pixie in RPython, which is a subset of Python that can be compiled to C with the PyPy translation tool-chain. The reason I chose RPython instead of C really comes down to the PyPy tool-chain’s feature set. Namely it supports a GC out-of-the-box, and if you write an interpreter in RPython you can put a few hints in the code, and it’ll spit out a JIT for that interpreter. This has saved me countless hours of work.

### How does Pixie compare to Clojure?

Since Pixie implements its own VM, it’s different in many ways. We don’t claim that Pixie is a “Clojure port”, as that locks us into following Clojure in all ways. Instead we take inspiration from Clojure, keep what we like, discard what we don’t, and improve what we can.

Performance-wise, Pixie can be faster than Clojure in some areas, mostly around boxing, as Pixie can remove boxing in tight loops, even when using transducers, or other higher-order-functions. However our GC is way less mature than the JVM GC, so I wouldn't expect it to out-perform Clojure in all (or even most) cases.

### What can experienced Lisp users expect from Pixie?

First, pixie is fast. Really fast. We can obtain the performance normally only found in a compiled language, while remaining completely dynamic. We also have a complete set of immutable data structures, including vectors and hash maps. So perhaps the best way to describe it is: Clojure with the lightweight feel of Python.

### When do you plan to release a stable version?

Thats TBD, probably not till early/mid 2015 when the language stabilizes a bit. Also I’d like to release the first version with full support for Windows, something we haven’t even started yet.

### Were there other experimental languages you worked on before Pixie?

Probably one of the best known projects was clojure-py which was a port of Clojure to the Python VM. But I’ve been working on languages most of my life. In fact, the first language I ever wrote was when I was in high-school. It was a small interpreted language named PhaLinks and was terrible, but I learned a lot from the effort. I also acquired a distaste for parsers in the process. Which, incidentally, is why I stick with Lisp these days: Lisp parsers are super easy to write.

### Do you think that developing Pixie made you a better programmer?

Of course, if you’re not learning something every day of your life, you’re doing something wrong.

### What difficulties are associated with designing a programming language from scratch?

One of the biggest is figuring out the right balance between performance and desired features. Many times in the development of Pixie I've wanted to add a certain feature, but then found out that if I tweaked it a bit, it’d be much faster. So now there’s a choice to be made, do you have the perfect language, written exactly the way you want, or do you want something that performs much better, but is lacking some cool feature.

### What reading material do you recommend for implementing your first programming language?

I recommend googling for tutorials like “writing a Lisp in X” or “writing a simple Forth”, and going from there. Also, read the source code from other languages. I learned most of what I know of language development simply by reading papers online, and studying source code of existing projects.

_December 8, 2014_

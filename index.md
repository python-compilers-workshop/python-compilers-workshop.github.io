---
layout: default
---

# Python Compilers Workshop

*What:* A workshop to bring together folks working on different
approaches to **native-code compilation for Python**, to share
experience, discuss future plans, and explore possible points of
collaboration. One particular question to discuss is whether and how
we can use JIT or AOT compilation techniques to accelerate C
extensions like `numpy` or `pandas` without having to rewrite
these extensions for every new compiler (as is the current
state-of-the-art).

*When/where:* **July 11-12**, 2016 in **Austin, Texas**, co-located
with the [SciPy 2016](scipy2016.scipy.org) conference. (This is just
before the main conference, and overlaps with the SciPy tutorial
days.)

*Venue:* TBD

*Who:* Open to the public. However
[RSVP's are appreciated](mailto:njs@pobox.com) for planning purposes,
and so that I can update the confirmed attendees list below.

*Organized by:* Nathaniel Smith <njs@pobox.com>


## Motivation

There's an intense and growing interest in techniques for compiling
Python or near-Python languages; a partial list of projects includes
[Numba](http://numba.pydata.org/),
[Pyston](https://github.com/dropbox/pyston), [PyPy](http://pypy.org/),
[Cython](http://cython.org/),
[Pythran](https://github.com/serge-sans-paille/pythran),
[Pyjion](https://github.com/Microsoft/Pyjion),
[Nuitka](http://nuitka.net/),
[Numexpr](https://github.com/pydata/numexpr),
[HOPE](www.cosmology.ethz.ch/research/software-lab/HOPE.html), ...

Given the wide variety of efforts here, now seems like a
good time to compare notes!

In addition, the numerical/scientific community is particularly
interested in these tools as a way to speed up Python code that uses
libraries like `numpy` -- and accomplishing this will require solving
unique technical and organizational challenges. In principle it's not
too difficult to compile Python code that uses `numpy` -- your
compiler "just" has to be compatible enough with the CPython C API to
call `numpy` directly, and all of the above projects either meet this
bar, or are anticipated to meet it soon. (In particular, both Pyston
and PyPy have developers actively working on this.) But if you want
`numpy`-using code to run *faster* than it does with CPython -- which
after all is the whole point of having a compiler -- then your
compiler needs some way to "see inside" `numpy`'s internals in order
to apply optimizations like unboxing, inlining, and loop fusion. And
this is impossible when calling extensions using the CPython C API.

Historically the main solution to this problem has been to start
rewriting parts of `numpy` directly inside the compiler infrastructure
-- projects that have gone down this road to a greater or lesser
extent include Numba, PyPy, Cython, Numexpr, and probably others. And
if nothing changes then this trend will only accelerate -- at an
obvious cost in duplicate effort, compatibility, code maturity, and
the ability to evolve and improve `numpy`'s semantics. Can we do
better? Could there be some way to write a library like `numpy` so
that a single codebase could simultaneously target CPython and the
newer compilers, while achieving competitive speed in all cases? If
so, can we make that happen? If not, then what's the next-best
alternative?


## Schedule

TBD -- probably we'll start with a few short talks to set the stage
and then switch to unconference mode.


## Confirmed attendees

TBD


## Sponsors

Sponsors: TBD

We anticipate that we will have travel funding available for
open-source developers who need the help. If this applies to you then
[please get in touch](mailto:njs@pobox.com).


## Travel information

See the [SciPy 2016 web site](http://scipy2016.scipy.org/) for
suggestions on
[lodging](http://scipy2016.scipy.org/ehome/146062/332952/?&&),
[transportation](http://scipy2016.scipy.org/ehome/146062/332955/?&&),
and other travel details.


## Code of conduct

(TBD -- maybe we can just point to SciPy's?)
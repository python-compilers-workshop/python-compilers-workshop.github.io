---
layout: default
---

# Python Compilers Workshop

*What:* A workshop to bring together folks working on different
approaches to **native-code compilation for Python**, to share
experience, discuss future plans and common interests, and explore
possible points of collaboration -- especially with regard to
numerical/scientific programming.

*When and where:* **July 11-12, 2016** in **Austin, Texas**,
co-located with the [SciPy 2016](http://scipy2016.scipy.org)
conference. (This is just before the main conference, and overlaps
with the SciPy tutorial days.)

*Venue:* TBD

*Who:* Open to the public. However
[RSVP's are appreciated](mailto:njs@pobox.com) for planning purposes,
and so that I can update the confirmed attendees list below. In
addition, we anticipate that we will have travel funding available for
open-source developers who would otherwise find it difficult to
attend. If this applies to you then
[please get in touch as soon as possible](mailto:njs@pobox.com).

*Organized by:* [Nathaniel Smith](https://vorpus.org)
([njs@pobox.com](mailto:njs@pobox.com))


## Motivation

There's an intense and growing interest in techniques for compiling
Python or near-Python languages to native code; a partial list
includes [PyPy](http://pypy.org/), [Numba](http://numba.pydata.org/),
[Pyston](https://github.com/dropbox/pyston),
[Cython](http://cython.org/), [Nuitka](http://nuitka.net/),
[Pythran](https://github.com/serge-sans-paille/pythran),
[Pyjion](https://github.com/Microsoft/Pyjion),
[Numexpr](https://github.com/pydata/numexpr),
[HOPE](www.cosmology.ethz.ch/research/software-lab/HOPE.html), ...

Now seems like a good time to compare notes! Plus there are lots of
questions that seem like they could benefit from some cross-project
collaboration. For example:

* If I wrap a C function using Cython/CFFI/SWIG/..., can we somehow
  expose the original C function to Numba/PyPy/Pyston/etc. to cut out
  the wrapper overhead? What about vice-versa: if I have a Python
  function that's been JIT-compiled and I pass it to some Fortran code
  like
  [`scipy.optimize.fmin`](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.fmin.html#scipy.optimize.fmin),
  could there be some way for `scipy` to call the JIT-compiled
  function directly? Can Numba and Pyston benefit from PyPy's work on
  CFFI?

* Does it make sense to run Numba on PyPy or Pyston?

* The Python 2 vs. Python 3 split is very painful for anyone working
  on compilers/interpreters. What strategies have worked or not
  worked?

* A number of the compilers above can take code like

  ~~~python
  total = 0.0
  for num in range(10000):
      total += num
  ~~~

  and perform inlining, unboxing, etc. to compile it down to a tight
  native loop that far out-performs CPython. This is possible because
  they have intimate knowledge of built-in Python constructs like
  `float`, `int`, and `range`.  And a number of them have good enough
  CPython C API compatibility that they can -- or will soon be able to
  -- execute the same code, but using `numpy`:

  ~~~python
  import numpy as np
  total = 0.0
  for num in np.arange(10000):
      total += num
  ~~~

  But if you're using the CPython C API to call `numpy`, then you
  can't do unboxing/inlining/loop fusion/etc., because `numpy` objects
  are a total black box to the compiler, and so this `numpy`ified
  version of the loop will run at about the same speed in a
  state-of-the-art JIT as it would in CPython.

  The traditional way to solve this -- as seen in e.g. Numba or
  Numexpr -- is to give the compiler built-in knowledge of `numpy`
  types and operations, essentially reimplementing `numpy` inside each
  compiler. But this strategy has a number of obvious downsides in
  terms of duplicated effort, subtle incompatibilities, increased
  testing load for downstream projects, the ability to continue to
  evolve and improve `numpy`'s semantics, and the potential need to
  then repeat the whole exercise for other projects like
  [`dynd`](http://libdynd.org/) (a `numpy` competitor) or
  `pandas`. And this question is becoming particularly urgent, since
  not only has Numba already started down this road, but Pyston and
  PyPy are both working on passing the `numpy` test suite right now
  and are likely to soon move from worrying about correctness to
  worrying about speed.

  Can we do better? Could there be some way to write a library like
  `numpy` so that a single codebase could simultaneously target
  CPython and the newer compilers, while achieving competitive speed
  in all cases? If so, what would it take to make that happen? If not,
  then what's the next-best alternative?


## Schedule

TBD -- probably we'll start with some talks from different projects to
outline their approaches and name some problems they're worrying
about, and then switch to unconference mode.


## Confirmed attendees

TBD


## Sponsors

TBD


## Travel information

See the [SciPy 2016 web site](http://scipy2016.scipy.org/) for
suggestions on
[lodging](http://scipy2016.scipy.org/ehome/146062/332952/?&&),
[transportation](http://scipy2016.scipy.org/ehome/146062/332955/?&&),
and other travel details.


## Code of conduct

TBD (maybe we can just point to SciPy's?)
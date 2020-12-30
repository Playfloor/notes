---
tags: latex
---
# Why LaTeX Sucks

> Note: This is more of a rant than a coherent stream of thought,
> however, I do believe in the problems I pose.

As my thesis work becomes partially about writing,
I find myself constantly fighting LaTeX.
It all started while writing a presentation for a talk
(I work backwards sometimes and writing the presentation first allowed me to organize details in my head).

## Problem 1 - There are too many compilers

The template I used required LuaTeX (or LuaLaTeX, the several names the community gives to things is ridiculous),
I simply switched over but then the presentation wouldn't compile due to fonts,
I figured some were missing, so I installed them, and then, it was fonts again...
I was unable to fix the problem, LuaTeX doesn't seem to know where the fonts are,
this disables me from using *modern* fonts.

> *[30/12/2020]* - I found the problem to be an *actually* missing package from TeXLive - `kpfonts-otf`.
> The package should come pre-installed (and at least for next Ubuntu versions it does).
> The CTAN page reads: *This package is meant to be installed automatically by TeXLive, MikTeX, etc.*
> No comments.

*Enter my thesis template.*
I figured I could simply switch compilers and no harm would come from it, *I was wrong*.
I started receiving errors due to missing fonts, which *are installed*.

Latexmk however, ran fine. This is ridiculous, imagine that you had to use different Java compilers based on what library you used,
not build systems, compilers.
Besides, TeX compilers all seem to be programmed differently, each supports its set of flags, etc.
pdfTeX for example, requires you make 4 different calls to build a single document (`pdftex && bibtex && pdftex && pdftex`),
just imagine that to build a single binary you had to call `gcc` 4 times, in 2021!

## Problem 2 - There are too many libraries

I know this is a criticism to have, but the thing is that just like JS libraries, TeX libraries are mostly useless,
hacks built on hacks to solve other hacks.
I find it amazing that anyone was able to get anything done when taking into account the amount of existing TeX libraries,
it seems to me that everyone was just spending their time writing weird hyper-specific purpose libraries.

Besides the fact that the full TeXLive distribution is around 5GB and you probably use 1% of the available libraries is also disturbing.
There is no package management, it is imbued with the OS or whatever weird LaTeX distro you're using.
You can't call `tex install package`, you download it from CTAN and hope your compiler detects it.

## Problem 3 - Inertia

The most ridiculous thing I remember using a library for was to split a table cell diagonally and add text to each side,
I shouldn't need an extra hack on top of the existing library, it should come by default!
The [package](https://www.ctan.org/pkg/slashbox) is older than me, it is almost 30 years old and countless TeX documents must depend on it,

I find this ridiculous, yet I was not expecting anything different - "If it ain't broken, why change it?" -
we say to ourselves, while we accumulate tech debt over years.

Imagine the time saved if the package had been added as a feature to the original library.
This is even worse for non-native speakers,
while in this case searching "diagonal table cell" is not hard to come up,
for a more specific term it is orders of magnitude harder,
especially if the term is not directly translatable.

## Conclusion (for now)

While I can't contest that LaTeX is amazing, I can't also stay silent and pretend it doesn't suck.
There is just nothing better and academics dislike change,
maybe if designers were forced to use it we would have something better.

I think we ought to learn our lessons and move on,
instead of building a new LaTeX version and perpetuate the suffering of millions of users,
we can simply decide we will no longer take it and try to create a new system.
Hell, compile the new system for all I care,
I just don't want to deal with LaTeX directly.
stb_image_resize2
=================

single-file public domain (or MIT licensed) image resize library

This project discusses security-relevant bugs in public in Github Issues, and it may take significant time for security fixes to be implemented or merged. If this poses an unreasonable risk to your project, do not use stb libraries.

By Jeff Roberts.

<a name="stb_libs"></a>

FAQ
---

#### What's the license?

These libraries are in the public domain. You can do anything you
want with them. You have no legal obligation
to do anything else, although I appreciate attribution.

They are also licensed under the MIT open source license, if you have lawyers
who are unhappy with public domain. Every source file includes an explicit
dual-license for you to choose from.

#### How do I use these libraries?

The idea behind single-header file libraries is that they're easy to distribute and deploy
because all the code is contained in a single file. By default, the .h files in here act as
their own header files, i.e. they declare the functions contained in the file but don't
actually result in any code getting compiled.

So in addition, you should select _exactly one_ C/C++ source file that actually instantiates
the code, preferably a file you're not editing frequently. This file should define a
specific macro (this is documented per-library) to actually enable the function definitions.
For example, to use stb_image_resize2, you should have exactly one C/C++ file that doesn't
include stb_image_resize2.h regularly, but instead does

    #define STB_IMAGE_IMPLEMENTATION
    #include "stb_image_resize2.h"

The right macro to define is pointed out right at the top of each of these libraries.

#### <a name="other_libs"></a> Are there other single-file public-domain/open source libraries with minimal dependencies out there?

[Yes.](https://github.com/nothings/single_file_libs)

#### If I wrap an stb library in a new library, does the new library have to be public domain/MIT?

No, because it's public domain you can freely relicense it to whatever license your new
library wants to be.

#### Some of these libraries seem redundant to existing open source libraries. Are they better somehow?

stb_image_resize2 is somewhat different from the other stb libraries
in that it is trying to be the final version of a resampler - the
most general, the fastest, support all SIMD, etc. We aren't precious
about any of this, use whatever works best for you, and if you
see a place we could be better let us know.

#### Can I link directly to the table of stb libraries?

You can use [this URL](https://github.com/nothings/stb#stb_libs) to link directly to that list.

#### Why single-file headers?

Windows doesn't have standard directories where libraries
live. That makes deploying libraries in Windows a lot more
painful than open source developers on Unix-derivates generally
realize. (It also makes library dependencies a lot worse in Windows.)

There's also a common problem in Windows where a library was built
against a different version of the runtime library, which causes
link conflicts and confusion. Shipping the libs as headers means
you normally just compile them straight into your project without
making libraries, thus sidestepping that problem.

Making them a single file makes it very easy to just
drop them into a project that needs them. (Of course you can
still put them in a proper shared library tree if you want.)

Why not two files, one a header and one an implementation?
The difference between 10 files and 9 files is not a big deal,
but the difference between 2 files and 1 file is a big deal.
You don't need to zip or tar the files up, you don't have to
remember to attach *two* files, etc.

#### Why "stb"? Is this something to do with Set-Top Boxes?

No, they are just the initials for Sean's name, Sean T. Barrett.
This was not chosen out of egomania, but as a moderately sane
way of namespacing the filenames and source function names.

#### Do you have any advice on how to create my own single-file library?

Yes. https://github.com/nothings/stb/blob/master/docs/stb_howto.txt

#### Why public domain?

I prefer it over GPL, LGPL, BSD, zlib, etc. for many reasons.
Some of them are listed here:
https://github.com/nothings/stb/blob/master/docs/why_public_domain.md

#### Why C?

Primarily, because I use C, not C++. But it does also make it easier
for other people to use them from other languages.

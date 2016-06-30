---
layout: post
title: Consider extracting this function
---

Often when reviewing my code, somebody will tell me: this function is quite
long. Why don't you see if you can pull out some parts of it into a separate
function.

It's common wisdom that functions should be kept fairly short, and much of the
time this is completely reasonable advice. But everything is a tradeoff, and
this is also the sort of advice that can be indiscriminately and dogmatically
applied without properly considering whether it is beneficial. My experience is
that situations arise fairly frequently in which a single long function is much
preferable to many short functions, and I wish to dispel the notion that long
functions are somehow *inherently* a bad idea.

Clearly it's desirable to reduce duplication by extracting common logic into
reusable functions. I have no problem with that. And (almost) any function $$f$$
can be decomposed into two subfunctions $$f_1$$ and $$f_2$$. But often
programmers will recommend splitting up a large function into smaller
components---for the sake of readability---even if it doesn't result in any code
reuse.

Does the decomposition really aid readability if the subfunctions are *only ever
called once*? Or perhaps twice? My position is: not always; and it might well
end up making things worse.

Extracting code into separate functions reduces locality of reference and makes
reasoning about the code more difficult: we have to track the control-flow as
it jumps in and out of various callees. This can easily be justified if we have
less code to maintain and verify overall as a result due to code reuse, but if
the callees are only ever invoked from one place it's harder to see what
desirable property is gained to balance out the increase in cognitive overhead.

"But surely," you say, "if the functions are well-named, there is no cognitive
overhead---one simply infers the semantics from the name of each function and
there is no need to worry about what the code inside is actually doing."

This completely misses the point. Far and away the most common reason for me to
be looking at a piece of code is because I suspect that there is a bug in it,
and I want to confirm or deny that suspicion. Therefore, in the most common
case, I *inherently* cannot trust that any function works as advertised. The
only possibility is to assume that every part of the code is a complete scam and
is lying to me.

In this situation, if there are no auxilliary function calls, I can simply read
the code top-to-bottom and verify that each line makes sense and is doing what I
expect. However, if we've extracted everything out into many different function
calls, I have to mentally inline each call in order to convince myself that
there is no bug, and I might as well have just left the logic inlined in the
caller in the first place.

Obviously I don't mean to imply it's okay to write an entire program as a
single, massive function, or anything like that. But sometimes a function just
does a bunch of relatively specific things and there aren't really any useful
abstractions to pull out of it. Anecdotally, if I consider only relatively sane
code that I've seen, written by people who generally know what they're doing, I
can think of very few occasions in which the readability has been hampered by
overly long functions, and far more in which it has been seriously compromised
by random cascades of deeply-nested function calls that needlessly obscure what
is happening and demand careful inspection on every viewing &#x25A0;

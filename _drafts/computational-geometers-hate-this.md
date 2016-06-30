---
layout: post
title: >
    Computational geometers hate this! One weird old tip for perfect continuous
    collision detection over closed sets
categories: code
---

If you don't care about the theoretical basis, you can skip the next couple of
sections.

### Mathematics

* Let $$X\subseteq\mathbb{R}^n$$ and $$x\in X$$. A *$$k$$-dimensional
  neighbourhood in $$X$$* of $$x$$ is a $$k$$-dimensional convex subset of
  $$X$$ containing $$x$$ in its interior.
* Let $$X\subseteq\mathbb{R}^n$$ and $$k\ge 0$$. We say $$x\in X$$ is a
  *$$k$$-vertex of $$X$$* if it has no $$k$$-dimensional neighbourhood in $$X$$.
* We say two subsets $$A$$ and $$B$$ of $$\mathbb{R}^n$$ are *non-penetrating*
  if for each $$x\in A\cap B$$, and $$(n-1)$$-dimensional neighbourhoods $$C_A$$
  in $$A$$ and $$C_B$$ in $$B$$ of $$x$$, $$C_A$$ and $$C_B$$ are parallel.
* TODO: this only really makes sense for sets which have interior everywhere;
  and hence is equivalent to intersecting interiors. Otherwise e.g. parallel
  lines can pass through each other without ever becoming penetrating. Is there
  a better/simpler definition? Or make penetrating not dependent on convex?

### Theorem

There are two parts. In each, let $$A$$ and $$B$$ be non-penetrating (closed)
subsets of $$\mathbb{R}^n$$.

1. Let $$T:\mathbb{R}^n\times[0,1]\rightarrow\mathbb{R}^n$$ be continuous with
$$T(x,0)=x$$ and $$T(A,1)$$ penetrating $$B$$. Then there is a largest
$$\lambda\in[0,1)$$ such that $$T(A,\lambda)$$ and $$B$$ are non-penetrating,
and this $$\lambda$$ satisfies $$T(A,\lambda)\cap B\ne\varnothing$$.

2. Let $$A\cap B$$ be nonempty with at least one of $$A$$ and $$B$$ bounded.
Then either $$A\cap B$$ contains an $$(n-1)$$-vertex of $$A$$, or it contains an
$$(n-1)$$-vertex of $$B$$.

#### Proof

1. Why must such $$\lambda$$ exist? Possibly has something to do with the
[closed map lemma](https://en.wikipedia.org/wiki/Open_and_closed_maps): i.e.,
$$T(A,[0,1])$$ closed so $$T(A,[0,1])\cap B$$ closed.

   If $$\lambda = 0$$, then the conclusion is true by assumption, so consider
$$\lambda > 0$$. Pick any $$x\in T(A,\lambda)\cap B$$ and suppose for
contradiction that we have non-parallel $$(n-1)$$-dimensional neighbourhoods
$$C_A$$ in $$T(A,\lambda)$$ and $$C_B$$ in $$B$$ of $$x$$. Let $$T_\lambda$$
be defined on $$\mathbb{R}^n$$ by $$x\mapsto T(x,\lambda)$$ and set
$$C = T_\lambda^{-1}(C_A)$$. Then $$T$$ continuously deforms $$C$$ to $$C_A$$
over $$[0,\lambda]$$, so $$T(C,[0,\lambda))$$ must intersect $$C_B$$; this
contradicts minimality of $$\lambda$$. [Needs more explanation: e.g. show
$$T(C,[0,1])$$ contains open neighbourhood of $$x$$?]

2. $$A\cap B$$ is a nonempty, closed, bounded subset of $$\mathbb{R}^n$$, so it
must have a bounding sphere that is "minimal" in the sense that some point
$$x\in A\cap B$$ lies on the surface of the sphere. If this $$x$$ is neither an
$$(n-1)$$ vertex of $$A$$, nor of $$B$$, we can find $$(n-1)$$-dimensional
neighbourhoods $$C_A$$ in $$A$$ and $$C_B$$ in $$B$$ of $$x$$. Since $$A$$ and
$$B$$ are non-penetrating, $$C_A$$ and $$C_B$$ are parallel, and hence
$$C_A\cap C_B$$ is an $$(n-1)$$-dimensional neighbourhood of $$x$$ in
$$A\cap B$$. But $$C_A\cap C_B$$ must lie partially outside of the bounding
sphere, contradicting minimality.

### Interpretation

I assume it isn't a new result, since it isn't particularly complicated, but
who knows. The proof is my own invention, at least.

Note that any open set has no $$k$$-vertices for any $$k$$; and any intersecting
open sets are necessarily penetrating.

Intuitively, a $$k$$-vertex of $$X$$ is a point that lies on a
$$(k-1)$$-dimensional face of $$X$$, where that face is "sufficiently convex"
in some sense; for example:

* In $$\mathbb{R}^2$$, a polygon's $$1$$-vertices are its convex vertices (in
  the usual sense), and its $$2$$-vertices are the points that lie on any of its
  edges.
* In $$\mathbb{R}^3$$, a polyhedron's $$1$$-vertices are its vertices (in the
  usual sense) that are "sufficiently convex" (i.e. not saddles, and so on); its
  $$2$$-vertices are the points that lie on any of its convex edges, and its
  $$3$$-vertices are the points that lie on any of its faces.
* Any point on the surface of an $$n$$-dimensional closed ball is a
  $$1$$-vertex, for any $$n$$.

Note that any $$k$$-vertex of $$X$$ is automatically a $$(k+1)$$-vertex of
$$X$$. (The definition of $$k$$-vertices is very similar to that of
[$$k$$-extreme points](http://en.wikipedia.org/wiki/Extreme_point), but slightly
more convenient for our purposes.)

Similarly, the intuitive interpretation of "non-penetrating" is that the two
sets involved overlap in at most a trivial way. Observe that $$A$$ and $$B$$
being non-penetrating implies that $$A\cap B = \partial A\cap\partial B$$,
although the former property is slightly stronger: for example, two crossed line
segments in $$\mathbb{R}^2$$ intersect only in their boundaries but are still
"penetrating" by this definition (unless the intersection point is the endpoint
of one segment).

### Probably not needed

1. Let $$T:\mathbb{R}^n\times[0,1]\rightarrow\mathbb{R}^n$$ be continuous with
$$T(x,0)=x$$, and $$\lambda\in[0,1]$$ smallest such that $$T(A,\lambda)$$
intersects $$B$$. Then $$T(A,\lambda)$$ and $$B$$ are again non-penetrating.

   [Now if $$T(A,\alpha)$$ and $$B$$ are penetrating for some $$\alpha$$, why
   must such $$\lambda$$ exist? Possibly has something to do with the [closed
   map lemma](https://en.wikipedia.org/wiki/Open_and_closed_maps): i.e.,
   $$T(A,[0,1])$$ closed so $$T(A,[0,1])\cap B$$ closed.]

1. If $$\lambda = 0$$, then the conclusion is true by assumption, so consider
$$\lambda > 0$$. Pick any $$x\in T(A,\lambda)\cap B$$ and suppose for
contradiction that we have non-parallel $$(n-1)$$-dimensional neighbourhoods
$$C_A$$ in $$T(A,\lambda)$$ and $$C_B$$ in $$B$$ of $$x$$. Let $$T_\lambda$$
be defined on $$\mathbb{R}^n$$ by $$x\mapsto T(x,\lambda)$$ and set
$$C = T_\lambda^{-1}(C_A)$$. Then $$T$$ continuously deforms $$C$$ to $$C_A$$
over $$[0,\lambda]$$, so $$T(C,[0,\lambda))$$ must intersect $$C_B$$; this
contradicts minimality of $$\lambda$$. [Needs more explanation: e.g. show
$$T(C,[0,1])$$ contains open neighbourhood of $$x$$?]

1. Let $$T:\mathbb{R}^n\times[0,1]\rightarrow\mathbb{R}^n$$ be continuous with
$$x\mapsto T(x,0)$$ the identity map, and $$\lambda\in[0,1]$$ with
$$T(A,\lambda)$$ and $$B$$ penetrating. Then there exists a (largest)
$$\alpha<\lambda$$ such that $$T(A,\alpha)$$ and $$B$$ are non-penetrating,
but have non-empty intersection.

1. By assumption we can find $$x\in T(A,\lambda)\cap B$$ and non-parallel
$$(n-1)$$-dimensional neighbourhoods $$C_A$$ in $$T(A,\lambda)$$ and $$C_B$$ in
$$B$$ of $$x$$.

Let $$T_\lambda$$ be defined on $$\mathbb{R}^n$$ by $$x\mapsto T(x,\lambda)$$
and set $$C = T_\lambda^{-1}(C_A)$$. Then $$T$$ restricted to
$$C\times[0,\lambda]$$ continuously deforms $$C$$ to $$C_A$$, so
$$T(C,[0,\lambda))$$ must intersect $$C_B$$; this contradicts minimality of
$$\lambda$$. [Needs more explanation?]

1. We use the fact that if $$f:\mathbb{R}^n\rightarrow\mathbb{R}^n$$ (or
$$f:\mathbb{R}^n\times[0,1]\rightarrow\mathbb{R}^n$$) is continuous and
$$U\subseteq\mathbb{R}^n$$ is homeomorphic to $$\mathbb{R}^k$$, we can find a
subset $$K\subseteq f^{-1}(U)$$ such that both $$K$$ and $$f(K)$$ are again
homeomorphic to $$\mathbb{R}^k$$. [Definitely needs justification.]

1. Let $$v$$ be a unit vector and $$\lambda\in\mathbb{R}$$ be the smallest
$$\lambda\ge 0$$ such that the translation $$A+\lambda v$$ intersects $$B$$.
Then $$A+\lambda v$$ and $$B$$ are again non-penetrating.

First consider the following lemma:
if $$C_0$$ and $$C_1$$ are non-parallel $$(n-1)$$-dimensional neighbourhoods
of $$x$$ in $$\mathbb{R}^n$$, and $$v$$ is any unit vector, we can find
$$\varepsilon_0 > 0$$ such that $$C_0+\varepsilon v$$ and $$C_1$$ intersect
for every $$0\le\varepsilon\le\varepsilon_0$$.

To see this, without loss of generality let $$x = 0$$. Since $$C_0$$ and
$$C_1$$ are non-parallel and $$(n-1)$$-dimensional, their linear span is the
whole of $$\mathbb{R}^n$$, and for sufficiently small $$\varepsilon > 0$$ we can
write $$\varepsilon v = v_0+v_1$$ with $$\pm v_0\in C_0$$ and
$$\pm v_1\in C_1$$. But then $$\varepsilon v-v_0 = v_1$$ lies in
$$(C_0+\varepsilon v)\cap C_1$$.

First consider the following lemma:
if $$C_0$$ and $$C_1$$ are non-parallel $$(n-1)$$-dimensional neighbourhoods
of $$x$$ in $$\mathbb{R}^n$$, then we can find an open set $$U$$ contained in the
convex hull of $$C_0$$ and $$C_1$$.

To see this, without loss of generality let $$x = 0$$. Since $$C_0$$ and $$C_1$$
are non-parallel and $$(n-1)$$-dimensional, their convex hull is an
$$n$$-dimensional neighbourhood of $$x$$ in $$\mathbb{R}^n$$. Then [?].

1. If $$\lambda = 0$$, then the conclusion is true by assumption, so consider
$$\lambda > 0$$. Pick any $$x\in A+\lambda v\cap B$$ and suppose we have
$$(n-1)$$-dimensional neighbourhoods $$C_A$$ in $$A+\lambda v$$ and $$C_B$$ in
$$B$$ of $$x$$. If $$C_A$$ and $$C_B$$ are non-parallel then by the lemma, there
is $$0<\varepsilon<\lambda$$ with $$(C_A-\varepsilon v)\cap C_B$$, and hence
$$(A+(\lambda-\varepsilon)v)\cap B$$, nonempty; this contradicts minimality of
$$\lambda$$.

By the lemma we then
have an open set $$U\subseteq T(A,\lambda)\cap B$$. Clearly we can find
$$a\in A$$ with $$(a,\lambda)\in T^{-1}(U)$$. The inverse image of $$U$$ is open
by continuity of $$T$$, so we have $$\varepsilon > 0$$ with
$$\lambda-\varepsilon>0$$ and $$(a,\lambda-\varepsilon)\in T^{-1}(U)$$; thus
$$T(a,\lambda-\varepsilon)\in B$$. This contradicts minimality of $$\lambda$$.

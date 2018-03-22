---
layout: page
title: Keeping things straight
description: Learning how to not be confused
---

Math can be difficult for a lot of reasons. Some steps require clever
insights. Sometimes one has to keep a lot in mind. But sometimes, all
that's required is keeping things straight. I'd like to give a few
examples, moving from trivial to slightly more confusing.

#### Example 1

Let `x` and `y` be two positive (real) numbers. If `2x = y`, which is
the bigger number?

Hopefully you answered `y`. But can you intuit why someone might want to
answer `x`? There's _two_ of them, and two is bigger than one, after
all!

If you can't even imagine thinking such a ludicrous thought, good
for you. You _grok_ math at a certain level that not everyone does,
believe it or not.

#### Example 2

We know that the formula y = x<sup>2</sup> traces out a parabola. What
about y = (x+5)<sup>2</sup>? Is that the parabola shifted right or left?

It is shifted left: when x=-5, y=0. Can you imagine thinking "well we
_added_ five, so it's shifted right?" Can you sense how it's the same
kind of mistake as before?

Again, if you cannot, then congratulations!

#### Example 3

You have a 2D vector space with basis {x, y}. You're given some linear operator
A, and a rotation operator R. If you've forgotten: just like a vector is an
entity that can be *written* as a sequence of numbers, an operator is an entity
that can be *written* as a matrix. Confusing the entity and its representation
is bad for the health.

Some questions:

---

**Q1.** Given some vector w, which vector is *w rotated by R*?

  1. Rw
  1. R<sup>-1</sup>w

**Q2.** We want to find the coordinates of w with respect to the axes (Rx, Ry)
(i.e., the original axes rotated by R). This is equivalent to which of the
following?

  1. The coordinates of Rw w.r.t. the original basis.
  1. The coordinates of R<sup>-1</sup>w w.r.t the original basis.

**Q3.**
Which operator behaves like A but with respect to basis {Rx, Ry}? For
example, if A projects onto x, then this operator projects onto Rx.

  1. RA
  2. AR
  3. RAR<sup>-1</sup>
  4. R<sup>-1</sup>AR

**Q4.**
We want to find the matrix representing A with respect to the axes (Rx, Ry).
This is equivalent to the matrix of one of the following operators in the
original basis. Which one?

  1. RA
  2. AR
  3. RAR<sup>-1</sup>
  4. R<sup>-1</sup>AR

---

**A1.**
Rw, by definition.

**A2.**
R<sup>-1</sup>w. 

Rotating the axes or the 'unrotating' the vector will yield the same
relationship between the vector and the axes, and it is this relationship that
matters when getting coordinates.

**A3.**
RAR<sup>-1</sup>.

RAR<sup>-1</sup>w = (R(A(R<sup>-1</sup>w))). This has the effect of
first "unrotating" w, then applying A, and then rotating it back.

Let's use the example where A projects onto the x direction. Then the 
operator we want should project onto Rx. Thus, if applied to Rx itself,
it should be a no-op.

Let's see what RAR<sup>-1</sup> does to
Rx. It first unrotates it, to get x. Then it applies A, which is a no-op. 
Then it rotates it back to Rx. Thus, the whole thing is a no-op, as expected.

**A4.**
R<sup>-1</sup>AR.

Rotating the axes or 'unrotating' the operator will result in the same
relationship between the two. Since RAR<sup>-1</sup> rotates the operator,
R<sup>-1</sup>AR unrotates it (rotates it by R<sup>-1</sup>).

Nonetheless, maybe you'd like some equations.
In the following terrible explanation, you must switch from thinking of the
w, A, and R as vectors and operators, to thinking of them as sequences
or matrices of numbers (namely, their representations in the original
basis. This is a *terrible* idea; don't try this at home).
Let B be the matrix we are trying to find. Note that:

  * R<sup>-1</sup>Aw can be thought of as either (R<sup>-1</sup>A) applied
to w in the original basis, or as Aw written in the new basis (per **A2**).

  * BR<sup>-1</sup>w is another way of writing Aw in the new basis:
R<sup>-1</sup>w is w in the new basis, and by hypothesis B
is the representation of A in that basis.

Therefore, R<sup>-1</sup>A = BR<sup>-1</sup>. Right-multiply by R to get
B = R<sup>-1</sup>AR.

Also notice the analogy Rw : R<sup>-1</sup>w :: RAR<sup>-1</sup> : R<sup>-1</sup>AR

Rotating a vector (or operator) is the opposite of writing it in the
rotated basis.

---

If that was all blindingly obvious to you, good job! I have to plod my
way through it every time I encounter it, and often lose the plot. At each step
there is only one way to go wrong (confusing the entity and its representation)
but there are a few steps in which you can make the mistake. If you make the
mistake an even number of times (hopefully zero) you end up with the right
answer.

Witness Sal Khan confusing it
[here](https://youtu.be/PiuhTj0zCf4?t=11m42s) (through
12:40) and then reiterating the correct reasoning at
[13:55](https://youtu.be/PiuhTj0zCf4?t=13m55s).


#### Bonus question

On an NYC subway line, there is a local and express version of the
train. The express train only visits a subset of the stops, except
late at night, when it makes all stops. The local train always makes all
stops. This is a partial image of the express train schedule:

<img src="a-train.jpg" width="300" height="300" />

You're waiting at W 4th St and need to get on a train that makes all
stops. Problem is, you're not sure at what time of night the express train
makes all stops. There's one approaching now. Can I infer that it is on
the night schedule?

**Answer**: That crescent is a moon. The express always makes black stops, 
and at night it *also* makes crescent stops. So seeing it stop at W 4th is no 
indication of whether it's making local stops yet. Wait for the local train.

Alternatively, you might correctly reason that "it *only* makes crescent
stops at night" (as in "the only time it makes crescent stops is at
night") but then a few seconds later misinterpret that sentence as "at night it
*only* makes crescent stops." But that makes no sense -- isn't it supposed to 
make *all* stops at night? Maybe I'm wrong about the crescent. Maybe the dark
circle means nighttime! So now "it *only* makes dark stops at night." Wait,
does that mean "at night it *only* makes dark stops?" Maybe it *is* safe to
get on! Wait, no no, let's start from first principles. During the day, it
either makes crescent stops, dark stops, or both. Three possibilities. Same for
at night. Which of those nine combinations fits the constraints I have? ...

Can you imagine being that silly? No?

Well la-di-da, *Kurt Gödel*.


### Conclusion

It's a very important skill to be able to keep concepts straight. Often
it's more important than being clever.

Part of the problem in the train case was trying to encode "the only time it 
makes crescent stops is at night" into the shorter but ambiguous "it only 
makes crescent stops at night." Ideally you'd mentally model these things in a 
nonverbal and hard-to-confuse way. You'd reason through it clearly once, and
then reuse the model you built later.

When learning any new concept, you want to build up a conceptual scaffolding
early, otherwise you can't make sense of later concepts. But sometimes you need
those later concepts to choose sensibly between competing mental models. And
it's hard to keep multiple new models in mind at the same time.

This is made harder by the fact that rarely do [engineers](http://swefordummies.blogspot.com/2018/01/confusing-networking-terminology.html) 
or [physicists](http://ml4dummies.blogspot.com/2018/01/qm-and-confusing-terminology-redux.html) ensure
that things are unambiguous. So you're trying to build on a shaky foundation,
often making the process of learning software or physics exponentially harder
than it should be. If you're really smart and can detect these inconsistencies,
or flexible enough to work around them, great. 

But if you're long on pedantic and short on clever, then good luck.

<!-- TODO move the swe / qm posts to github -->
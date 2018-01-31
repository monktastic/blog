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

You have a 2D vector space with basis {x, y}. You're given some operator
A, and a rotation operator R. Some questions:

---

**Q1.** Given some vector w, which vector is w rotated by R?

  1. Rw
  1. R<sup>-1</sup>w

**Q2.** Which of the following would give you the _representation of w_
in the basis {Rx, Ry}?

  1. Writing Rw in the original basis.
  1. Writing R<sup>-1</sup>w in the original basis.

**Q3.**
Which operator behaves like A but with respect to basis {Rx, Ry}? For
example, if A projects onto x, then this operator projects onto Rx.

  1. RA
  2. AR
  3. RAR<sup>-1</sup>
  4. R<sup>-1</sup>AR

**Q4.**
Which of these vectors, when written in the original basis, will give
the *representation* of A with respect to {Rx, Ry}?

  1. RA
  2. AR
  3. RAR<sup>-1</sup>
  4. R<sup>-1</sup>AR

---

**A1.**
Rw, by definition.

**A2.**
R<sup>-1</sup>w. Rotating the axes counterclockwise has the same effect
as rotating the vector clockwise.

**A3.**
RAR<sup>-1</sup>.

RAR<sup>-1</sup>w = (R(A(R<sup>-1</sup>w))). This has the effect of
first "unrotating" w, then applying A, and then rotating it back.

For example, if w = Rx then this unrotates it so that w = x, then
applies the projector A (which is a no-op), and then rotates it back to
Rx, thus giving us the no-op we wanted in the new basis.

**A4.**
R<sup>-1</sup>AR.

It is slightly harder to give an intuitive answer for this one, but you
can work the math out for yourself.

Notice the analogy Rw : R<sup>-1</sup>w :: RAR<sup>-1</sup> : R<sup>-1</sup>AR

Rotating a vector (or operator) is the opposite of writing it in the
rotated basis.

---

If you had no trouble with that, good job! Witness Sal Khan confusing
it [here](https://youtu.be/PiuhTj0zCf4?t=11m42s) (through 12:40) and
then reiterating the correct reasoning at [13:55](https://youtu.be/PiuhTj0zCf4?t=13m55s).


### Conclusion

A lot of mathematical reasoning is not about cleverness, but keeping
things straight. Even when there are only two things to keep straight,
it can require careful attention not to bungle it.

Open question: does getting better at keeping one kind of thing straight
help you keep other kinds of things straight? How strong is this effect?
What's the best way to train it?

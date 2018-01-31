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
with respect to the basis {Rx, Ry}?

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
Which of these operators, when written in the original basis, will give
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

It is slightly harder to give an intuitive answer for this one, but it
is a good exercise to work the math out for yourself.

In the following explanation, you must switch from thinking of the
w, A, and R as vectors and operators, to thinking of them as sequences
or matrices of numbers (namely, their representations in the original
basis. Yes, this is a *terrible* idea; don't try this at home).
Let B be the matrix we are trying to find.

  * R<sup>-1</sup>Aw can be thought of as either (R<sup>-1</sup>A) applied
in the original basis, or as Aw written in the new basis (per **A2**).

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
way through it every time I encounter it, and often lose the plot.
In a sense there's only one way to go wrong, but there are many places
you can make that one mistake in a problem like **Q4**.

Witness Sal Khan confusing it
[here](https://youtu.be/PiuhTj0zCf4?t=11m42s) (through
12:40) and then reiterating the correct reasoning at
[13:55](https://youtu.be/PiuhTj0zCf4?t=13m55s).


#### Bonus question

On an NYC subway line, there is a local and express version of the
train. The express train only visits a subset of the stops, except
late at night, when it makes all stops. This is a partial image of the
express train schedule:

<img src="a-train.jpg" width="300" height="300" />

You're waiting at W 4th St and need to get on a train that makes all
stops. Problem is, you're not sure at what time of night the change
happens. There's an express train approaching. Is it safe to get on?

You're pretty sure you've gotten on during the day at W 4th. Also that
crescent looks suspiciously like a moon.

**Answer**: During the day it *only* makes black stops, and at night it
*also* makes crescent stops. So seeing it stop at W 4th is no indication
of whether it's making local stops yet. Wait for the local train.

Alternatively, you might correctly reason that "it *only* makes crescent
stops at night" (as in "the only time it makes crescent stops is at
night") but then a few seconds later misinterpret it as "at night it
*only* makes crescent stops" and thus, since it's stopping at W 4th,
it's running on the daytime schedule, and therefore it's making only express
stops, but wait a minute that makes no sense, but what if I'm wrong and
end up in Harlem.... Also, maybe I should invert my reasoning because
I'm *not* sure I've gotten on at W 4th during the day, and
again because the black circles look like a dark sky, oh wait now I
have four times as many cases to work through....

Can you imagine being that silly? No?

Well la-di-da, Ms. Fields Medalist.

(Now imagine that this is about something more abstract than trains,
and somehow you haven't even realized that you have to mentally distinguish
express *trains* from express *stops*, and there are a dozen **known**
unknown axes, and yet a dozen _more_ **unknown** unknown ones. Yeah,
welcome to software.)

### Conclusion

A lot of mathematical reasoning is not about cleverness, but keeping
things straight. Even when there are only two things to keep straight,
it can require careful attention not to bungle it.

Open question: does getting better at keeping one kind of thing straight
help you keep other kinds of things straight? How strong is this effect?
What's the best way to train it?

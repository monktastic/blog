---
layout: page
title: Quantum mechanics and you
description:
---

## Overview

[This](https://www.youtube.com/watch?v=DfPeprQ7oGc)
is a clip from the New Age movie "What The Bleep Do We Know?"

It is a great clip for (1) explaining the double-slit experiment,
and (2) demonstrating how many people grossly misunderstand the
conclusion of the experiment.

Detection devices do not need to be conscious. Nonetheless, in a twist
of irony, the actual conclusion may be far more bizarre than that. See
[here](act-5.html).


## Modeling the world

This will require a bit of math, but I'm going to simplify the notation.
In the two-slit experiment, when the electron (`E`) encounters the
screen, it can go one of two ways (left or right). We normally
write this:

`|E_left> + |E_right>`

Let us take some liberties, replacing the symbols with words. "Or" is
not technically precise, but it will do for our present purposes:

`E left or E right`

At this point it is possible to detect the "or" by means of an
interference experiment. This is what causes the light and dark bands.

Now, if a detector (`D`) is placed at the slits, then the state becomes:

`(E left and D left) or (E right and D right)`

You don't see a term like `E left and D right` because that would
just indicate a faulty detector.

One side-effect is that `E` *by itself* will no longer show interference.
The light/dark bands vanish. On the other hand, there *is* in theory an
experiment that would demonstrate interference on the `E`-`D` *joint*
system, but it's very hard to do in practice, and not easy to
describe[1].

If `D` were a single particle, and we had precise control over both `E`
and `D`, then we could actually demonstrate that joint interference. In
fact, this is crucial for quantum computing, which
today we can only do with a very small number of carefully controlled
particles[2]. That number is growing every day, and we have no evidence
that there is a theoretical ceiling.

This theoretical ability to demonstrate interference is important. It is
what allows us to say "it's not that the system is in one state but we
don't know which; it is still in a *combination* of those states." Until
you've seen the result of the experiment (directly or indirectly), it
is not meaningful to say that the electron "actually" went one way.

This is the point at which some people lose the plot. See, for example,
the [4:25 mark](https://www.youtube.com/watch?v=DfPeprQ7oGc) from
the clip in the intro:
```
The electron decided to act differently, as though it was aware that
it was being watched!
```
Sounds spooky, right? They even give the detector an eyeball with
creepy eyelashes. But it didn't "decide" anything and it wasn't "aware"
of anything -- unless you also think a pool ball is "aware" of the
cue ball hitting it and "decides" to move as a result. It's really
just straightforward physics and math, although some misunderstand
and think that detectors must be conscious.

The detector has in *one* sense "measured" the electron: in each
"branch" of the superposition, the detector is correctly displaying
the electron's path. But from *your* perspective, there is no reason
to say that one outcome has actually occurred, and in this important
sense you should not consider it "measured." This is the second way
in which people commonly lose the plot.

Anyway, as objects (such as the detector) interact with the experiment,
they become part of it. When the electron hits the
screen (`S`), the screen registers it on the left or right:

`(E left and D left and S left) or (E right and D right and S right)`

And so on. *Every* physical object that encounters the system gets
"split" in two, joining the superposition. It is as though there are
two "branches" to the experiment, evolving in parallel.

If this is so, then when does the `or` disappear? When do you get to say
there is really one answer?

This question is called the "measurement problem," and it is unresolved.
See [here](act-5.html) for one bizarre possibility.

## References and notes

[1] Understanding *why* you can show interference on the joint system
but not individual parts requires some math. This note is for the
reader who is already well-acquainted with QM (but is not necessarily
acquainted with the [density
matrix formulation](https://en.wikipedia.org/wiki/Density_matrix)). We
will omit normalization constants.

Consider a qubit in state `|psi> = |0> + |1>` measured with respect to
the following basis:

`{ |A> = |0> + |1>, |B> = |0> - |1> }`

Note that because `<B|psi> = 0`, the result will never be `B`. This
result can be interpreted as the result of interference. In particular,
`<B|0>` and `<B|1>` (the "two paths" from `|psi>` to `|B>`) have
opposite amplitudes and are said to "destructively interfere."

Now let the qubit become entangled with a "measuring device":

`|psi'> = |0>|X> + |1>|Y>`

Where `|X>` and `|Y>` are orthogonal.

If you calculate the probability of `|psi'>` being measured as `|B>`
(e.g., by applying the projector `P_B @ I`), you will find that it is
50%, as would be predicted if the particle were in a classically
indeterminate mixture of `|0>` and `|1>`. The interference has
"disappeared" with respect to either sub-state alone. In the density
matrix formulation, this is equivalent to taking the
[partial trace](https://en.wikipedia.org/wiki/Partial_trace) and
noticing that the off-diagonal terms have disappeared.

On the other hand, because `|psi'>` is still just a superposition
(in the tensor-product space spanned by
`{ |0>|X>, |0>|Y>, |1>|X>, |1>|Y> }`),
we can still demonstrate interference on it (e.g., by noting that it
is never measured as `|0>|X> - |1>|Y>`).

Note that this inability to demonstrate interference on `|psi'>` can
fall along a spectrum, depending on the inner product of `|X>` and `|Y>`.
The smaller that inner product, the more the loss of interference.

[2] If they are exposed to the environment, then lots of stray particles
will become involved. Then it becomes impossible to exhibit interference
on the `E`-`D` pair for the same reason it is impossible to exhibit
interference on `E` alone after it encounters `D`. This is known as
*decoherence*.

Yet it is still
theoretically possible to exhibit interference on the `E`-`D`-`trillions
of stray particles` system, if only we were extremely technologically
advanced.


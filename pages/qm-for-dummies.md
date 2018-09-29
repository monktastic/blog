---
layout: page
title: Quantum mechanics for dummies
description:
---

## Overview

People sometimes make New Agey claims about quantum mechanics, only to be shot
down by frustrated physicists. It can be hard to separate the wheat from the
chaff. A genuine understanding of QM does depend on some heavy-duty math, but it
turns out that the foundational issues can be approximately understood with
relatively little.

Here I will try to communicate the essential points (and common
misunderstandings) with as little math as necessary. I'll include footnotes for
those with some background.

---

### Superposition, interference, and entanglement

A particle can be in a *superposition* of states. A particle in a superposition
of spin-up and spin-down can be written:

`|U> + |D>`

Given the right experiment, this state will exhibit something called
*interference*. It is this interference that proves to us that it is in a
superposition [1]. This is important because it means that there is not yet a
single, well-defined result.

We can let this particle interact with a second one in such a way that the new
particle's spin *matches* the first's. Using numbers to differentiate the two
particles, the new joint state is:

`|U1>|U2> + |D1>|D2>`

This tells us that *if* either particle is measured as spin-up, so will the
other be, and similarly for spin-down. This means that the states are
*entangled.* This joint state is still a superposition, which means that the pair
of particles together can exhibit interference given the right experiment [2]. 
But it turns out that if you measure the first particle *alone*, it won't [3].
The first particle now behaves classically.

This is what happens in the famous two-slit experiment: when the particle gets
entangled with a detector, it can no longer show interference. This brings us
to our first misconception:

> *The electron decided to act differently, as though it was aware that
it was being watched!* 
>
> -- New Age movie [What The Bleep](https://youtu.be/DfPeprQ7oGc?t=4m25s)

It didn't *decide* anything, and it wasn't *aware* of anything -- unless you
also believe that billiard balls "decide" to move when they are "aware" they
have been hit by a cue ball. There's nothing strange going on here.

On the flip side, this is often used to convince people that consciousness has
nothing to do with QM -- after all, *any* physical detector would cause this
effect. But this, too, misses the point.

### Decoherence

In the two-particle system given above, it is possible to show interference, but
only if you have precise control over both particles. This is only possible in
extremely careful lab settings. With a macroscopic detector, there are way too
many particles involved, and so any hope of demonstrating interference is
completely dashed. This fact is known as *decoherence.* You don't even need an
explicit detection device for this: stray air molecules and photons bouncing off
your experiment will do the job. This is why quantum computers are so hard to
build.

We can now write our state as:

`|U1>|U2>|Ex> + |D1>|D2>|Ey>`

Where `|Ex>` and `|Ey>` are states of the *environment* that differ due to their
interaction with the experimental particles. Just as the first particle alone
could no longer show interference after entanglement with the second, the first
two particles cannot show interference now that they're entangled with the
environment. This leads us to the second misconception: 

> *If you simply stick a cat in a box and link its fate to the outcome of some quantum event, you’re not likely to put it in a superposition of alive and dead, because decoherence **will almost instantly force it into one state or the other***. 
>
> -- [Quanta magazine](https://www.quantamagazine.org/real-life-schrodingers-cats-probe-the-boundary-of-the-quantum-world-20180625)

Decoherence does *not* force it into "one state or the other"; it simply
prevents the two branches from interfering [4]. Why does this matter? In the
above state, suppose none of the particles or environment have interacted with
you. We can write this as:

`(|U1>|U2>|Ex> + |D1>|D2>|Ey>) @ |You>`

Don't worry too much about what `@` means (it's called a "tensor product"). This
just says that you are not entangled with the experiment yet. From your
perspective, there are *still two possibilities*, despite the fact that it is
*practically* impossible to demonstrate the fact.


### Many Worlds

At some point, you interact with the experiment. The two branches will affect
you in different ways (for example, in the Schrödinger's Cat experiment, one
will cause you to experience a dead cat, and the other a live one). This means
you are now entangled with it:

`|U1>|U2>|Ex>|You_x> + |D1>|D2>|Ey>|You_y>`

At this point, it is as though there are two "copies" of you, each seeing just
one result. Whereas before you could *not* say there was one result, now you
*must* (unless you are willing to confront a decaying cat and pretend it is
possibly still alive). Even stranger, now you can say that the cat *has been
dead*, even though a moment ago you could not say it was dead.

Now, it is true that from "God's perspective," there are still two
possibilities, but note that you never have God's perspective. From *your*
perspective, the world did indeed suddenly transition from there being no
objective truth about the cat's fate, to there being one. And it happened
precisely when the experiment entangled with *you*, personally. In this sense,
you do occupy a unique role in the place you call "the universe."

But note that **you** are made of many particles. Which of those particles,
*exactly*, need to become entangled with the experiment before you should say
there is a result?

### Consciousness

Because of decoherence, this is not a question we can address experimentally,
either now or for the foreseeable future. Instead, let's take a step back and
ask: when can you be *sure* that there is a result? Experiencing a decaying cat
is an obvious *upper bound*: the result certainly occurs *no later* than this.
In other words, being *conscious* of a result (or it becoming "entangled with
the conscious parts of your brain", if you like) is a clear upper bound.

Now, can we *tighten* that bound? For example, should you say there is a
result when it has only entangled with your *toe*? There seems to be no good
reason to consider your toe different from random air molecules in the room. 
Entanglement with your toe should be thought of as:

`(|U1>|U2>|Ex>|Toe_x> + |D1>|D2>|Ey>|Toe_y>) @ |You>`

"You" are still not entangled. The same reasoning applies to the "unconscious
parts of your brain." We might be tempted to say that *obviously by the time it
entangles with any part of your brain, there is a result*, but in principle, we
have no more reason here than we did long before it reached your brain -- and we
*didn't* have sufficient reason then. "Your brain" is not special, except
insofar as it relates to consciousness.

In other words, we have *no good reason* to draw the line anywhere earlier than
"your consciousness," even if we have no clear scientific definition of that
term. In this sense, it *is meaningful* to talk about definite results only
coming into being when they encounter your consciousness[5].

This is why you should be skeptical of any claims that "consciousness has
nothing to do with QM." And, appeals to authority aside, you should also know
that you're in good company if you think otherwise:

> *I think consciousness will remain a mystery. Yes, that's what I tend
to believe. I tend to think that the workings of the conscious brain
will be elucidated to a large extent. Biologists and perhaps physicists
will understand much better how the brain works. But why something that
we call consciousness goes with those workings, I think that will remain
mysterious. I have a much easier time imagining how we understand the
Big Bang than I have imagining how we can understand consciousness.*
>
> &nbsp; ...
>
> *I’m not going to attempt to define consciousness, in a way that’s connected
with the fact that I don’t believe it will become part of physics. And that
has to do, I think, with the mysteries that bother a lot of people about quantum
mechanics and its applications to the universe.*
>
> &nbsp; ...
>
> *Quantum mechanics kind of has an all-embracing property, that to completely make
sense it has to be applied to everything in sight, including ultimately, the
observer. But trying to apply quantum mechanics to ourselves makes us extremely
uncomfortable. Especially because of our consciousness, which seems to clash
with that idea. So we’re left with a disquiet concerning quantum mechanics,
and its applications to the universe. And I do not believe that disquiet will go
away. If anything, I suspect that it will acquire new dimensions.*
>
> &nbsp;
>
> -- Edward Witten, a physicist so overpoweringly smart that
his fellow theoretical physicists casually throw around terms like
["smarter than anyone else"](http://www.nytimes.com/1987/10/18/magazine/a-theory-of-everything.html?pagewanted=all)
and "head and shoulders above the rest"

### Idealism and nonduality

> *For quantum mechanics ... all we really have to do (most people believe) is
think about it in the right way. No elaborate experiments necessarily required
(although they could help nudge us in the right direction, no doubt about that).
But if anything, that makes the embarrassment more acute. All we have to do is
wrap our brains around the issue, and yet we’ve failed to do so.* 
> 
> &nbsp;
> 
> -- (Caltech physicist) Sean Carroll

Here's a crazy way of thinking about it. What if the world comes into being with
your consciousness because *your consciousness* and *the world* are two ways of 
talking about the very same phenomenon?

Even without QM, it should already be apparent to you that what you experience
as "the world" is made of your own mind. Listen to a sound. What could that (or
any other experience) *be*, other than your own mind, illuminated?

In a nighttime dream, your environment is similarly made entirely of your own
mind -- but crucially, it is not made of the dream *character's* mind, nor
happening inside his or her *brain*. It is made of the mind of the *dreamer*
(your waking self), who exists *beyond* the confines of the dream.

The possibility on offer here is that what you call "the world" is your dream,
made of your mind -- but what "you" are is not the character you normally take
yourself to be, but *that which dreams realities into being*. That which looks
through your eyes; whose mind manifests as existence itself.

Obviously, most physicists would bristle at this suggestion. Where is the
evidence for such a wild hypothesis? On the other hand, if this really *were*
your dream, who could discover it but you? You would have to *wake up* or
*become lucid*, like that guy Buddha (who you dreamed up to remind *you* how
to wake up).

There is more to be said, but we will save it for another piece.


### Other approaches to QM

This document would not be complete without mentioning other interpretations of
QM.

The most popular interpretation of QM (amongst physicists) since its inception
has been the "Copenhagen Interpretation." Leaving aside the issue that nobody
can seem to agree on what, exactly, it is[6], we can take it as roughly saying
that the two branches of the wave function "collapse" into one, sometime long
before it reaches you (it not *in actuality*, then at least *in practice*,
so who cares). As we are able to do better and better experiments, it is
becoming increasingly obvious that this doesn't really explain anything.

Other approaches exist, too, but none are very popular. Most of the modern
interpretations run into the issues mentioned in this piece.


---

## Footnotes

The first three are for those with some background in QM.

1. For example, if the state `|z+> + |z-> `is subjected to a measurement along
the x-axis, it will always yield `|x+>`. A *classical* mixture of `|z+>` and 
`|z->` would have given it only 1/2 the time.

2. Consider the probability that the state `|x+>|x+> + |x->|x->` is measured
as `|z+>|z->`. It never will, whereas a classical mixture would give that result
1/4 of the time.

3. Given joint state `|z+>|z+> + |z->|z->`, how often will the first particle
be measured as `|x+>`? We can rewrite the state as `|x+>|x+> + |x->|x->` to see
that the answer is 1/2, which is what we expected when it was in a classical
mixture of `|z+>` and `|z->`.

4. [The decoherence myth](https://plato.stanford.edu/entries/qm-decoherence/#SolMeaPro):

   > Unfortunately, naive claims of the kind that decoherence gives a complete
   answer to the measurement problem are still somewhat part of the ‘folklore’
   of decoherence, and deservedly attract the wrath of physicists (e.g. Pearle
   1997) and philosophers (e.g. Bub 1997, Chap. 8) alike.

   See also [this answer](https://physics.stackexchange.com/a/374212/118804).

5. This is sometimes glossed over by inserting the caveat "definite result *from
your perspective*", but this is small consolation: your perspective is the only
one you'll ever have, and *from* that perspective, this is indeed the first time
that the world with the corresponding result can properly be said to exist.

6. [The most embarrassing graph in modern physics](www.preposterousuniverse.com/blog/2013/01/17/the-most-embarrassing-graph-in-modern-physics/).

   > *I think Copenhagen is completely ill-defined, and shouldn't be the
   favorite anything of any thoughtful person.*

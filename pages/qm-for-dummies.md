---
layout: page
title: Quantum mechanics for dummies
description:
---

## Overview

People sometimes make New Agey claims about quantum mechanics, only to be shot
down by frustrated physicists, who sometimes overshoot and claim that it has
nothing whatsoever to do with consciousness. The truth is probably somewhere in
the middle.

A genuine understanding of QM does depend on some heavy-duty math, but it turns
out that the foundational issues can be approximately understood with relatively
little. Here I will try to communicate the essential points (and common
misunderstandings) with as little math as necessary. I'll include footnotes for
those with some background. For fun, I'll end with my own (decidedly "New Age")
interpretation.

---

### Superposition, interference, and entanglement

A particle can be in a *superposition* of states. A particle in a superposition
of spin-up and spin-down can be written:

`|U1> + |D1>`

The state `|U1>` is the spin-up component, and `|D1>` the spin-down component.
The `1` is there to indicate that this is our first particle, since we shall
soon be adding more.

Given the right experiment, this state will exhibit something called
*interference*. Understanding the details requires some math[1]. The important
point is that there is some experiment we can do to confirm that the particle
isn't in "either one state or the other (but we don't know which)," but instead
in a quantum combination of the two. *The existence of such an experiment is 
how we know that there isn't a single result yet.*

Next, we let this particle interact with a second one in such a way that the new
particle's spin *matches* the first's. Using numbers to differentiate the two
particles, the new joint state is written:

`|U1>|U2> + |D1>|D2>`

The state `|U1>|U2>` means that both particles are *up*. The other possibility
is `|D1>|D2>`, where they are both down. The sum `+` indicates that they are in
a superposition of these possibilities. In both cases, the particles agree on
their spin -- a phenomenon known as *entanglement*. Because the joint state is 
a superposition, the right experiment conducted on **both particles together**
will show interference[2], confirming that the pair is *not* in a 
definite-but-unknown (i.e., classical) state. It is still quantum; there is no 
definite result yet.

But something funny happens when you restrict your attention to either particle
*alone*: it won't show any interference[3]. This means that although the pair
(and therefore each particle *in* the pair) does not have a definite result, you
will be unable to detect this fact *unless your experiment involves both 
particles.* Any restricted experiment will erroneously make you believe that
the particle *is* in a definite state (that you are just now finding out).

### The two-slit experiment

Recall what happens in the famous two-slit experiment: when there is **no**
detector, the particle exhibits interference at the screen. When there *is* a
detector, the particle shows no interference. If you haven't worked out the
math, this might seem spooky. Why did the particle's behavior change? To hear
it from some, this is magic:

> *The electron decided to act differently, as though it was **aware** that
it was being watched!!* 
>
> -- New Age movie [What The Bleep](https://youtu.be/DfPeprQ7oGc?t=4m25s)

But it didn't *decide* anything, and it wasn't *aware* of anything -- unless you
also believe that a billiard ball "decides" to move when it is "aware" it has
been hit by a cue ball. That may be your prerogative, but QM lends no support
here.

When the detector is turned on, the particle entangles with it. The two are in
a joint superposition:

`|Particle left>|Detector left> + |Particle right>|Detector right>`

That's what it *means* to be a detector, after all: the particle's state and the
detector's are in agreement. And as we learned before, measuring one part of
such a system alone will not cause interference. Thus, the particle, measured by
the screen, shows no interference.

I realize this may not be the most satisfying answer about what's happening. I
haven't exactly explained "why" entangled particles don't show interference
individually; I only told you that the math explains it. But we could ask the
same about gravity: *why* do two masses attract? At some point you must just
accept that it's how things work, and rejoice that we've found a mathematical
framework that makes accurate predictions around it.

But the story doesn't end there. There may still be something strange. To
appreciate it, we have to go deeper....

### Decoherence

What we learned before extends beyond two particles: if you want to show
interference, you need control of *all* the particles that have become related
to each other through entanglement. This is only possible in extremely precise
lab settings. Otherwise, trillions of stray air molecules and photons would
bounce off your experiment and become entangled with it, dashing any hopes of
wrangling them together to demonstrate that they are together in a
superposition. This fact is known as *decoherence*. It is the reason quantum
computers so hard to build.

We can now write our state as:

`|U1>|U2>|Ex> + |D1>|D2>|Ey>`

Where `E` is the environment, and `|Ex>` and `|Ey>` are the two different ways
it reacts with the different possibilities. Just as the first particle alone
could no longer show interference after entanglement with the second, the first
two particles cannot show interference now that they're entangled with the
environment. And since recapturing all the environmental particles is in
practice almost impossible, decoherence tells us that we can hereafter perform
all calculations on the two particles *as though* they have a definite (though
unknown) state. In other words, they appear to be classical.

This leads us to the second misconception: 

> *If you simply stick a cat in a box and link its fate to the outcome of some quantum event, you’re not likely to put it in a superposition of alive and dead, because decoherence **will almost instantly force it into one state or the other***. 
>
> -- [Quanta magazine](https://www.quantamagazine.org/real-life-schrodingers-cats-probe-the-boundary-of-the-quantum-world-20180625)

This is misleading. The different outcomes for the cat certainly lead to
different outcomes for its environment, and because of that entanglement, we
cannot demonstrate interference on the cat, *even in principle*. Considered
as an isolated system, the cat is not in a superposition. But the cat *plus
environment* still is. So there is still no answer to the question "which way
did the experiment turn out?"

Notice how easy it is to lose the plot. For this reason, it is a common
misconception that decoherence has solved the "measurement problem"[4] --
roughly speaking, the question of when a measurement outcome *really* happens.

This is the real heart of the issue, and where things get interesting.

> *I suspect that a substantial majority of physicists who use quantum
  mechanics in their everyday work are uninterested in or downright
  hostile to attempts to understand the quantum measurement problem.*
>
> &nbsp;
> 
> -- (Caltech physicist) Sean Carroll

### Many Worlds

In the above state, suppose none of the particles or environment have 
interacted with **you**. We can write this as:

`(|U1>|U2>|Ex> + |D1>|D2>|Ey>) @ |You>`

Don't worry too much about what `@` means (it's called a "tensor product"). This
just says that you are not entangled with the experiment yet: you are still
outside it. From your perspective, there are *still two possibilities*, despite
the fact that it is *practically* impossible to demonstrate the fact.

At some point, you interact with the experiment. The two branches will affect
you in different ways (for example, in the Schrödinger's Cat experiment, one
will cause you to experience a dead cat, and the other a live one). This means
you are now entangled with it:

`|U1>|U2>|Ex>|You_x> + |D1>|D2>|Ey>|You_y>`

From the perspective of the Many Worlds Interpretation of QM (MWI), it is as
though there are two "copies" of you, each seeing just one result. Whereas
before you could *not* say there was one result, now you *must*. Even stranger,
now you can say that the cat *has been dead*, even though a moment ago you could
not say it *was* dead.

From your perspective, the first time the cat can be said to have a well-defined
fate is when it entangles with you, specifically. Is this weird? On one hand,
notice the caveat "from your perspective." For anyone still outside the system,
there is still no well-defined result. So the situation is symmetrical for
everyone, and you are not special. Maybe it's not so weird after all.

On the other hand, "from your perspective" is just another way of saying "in
your world," and *your* world is just this place you normally call "*the*
world." The cat's fate is now sealed not only for you, but for all other
inhabitants in "the world." So it *is* meaningful to say that the cat became
dead for *everyone in the world* precisely when it entangled with *you*. The
fact that "everyone" lives inside your private reality does not make things any
less weird.

There are other interpretations of QM, but for the most part, unless they
include a nasty "collapse" postulate (which we'll briefly revisit later), this
is where you're forced.

### Consciousness

There's one very important bit we've glossed over. Note that **you** are made of
many particles. Which of those particles, *precisely*, need to become entangled
with the experiment before you should say there is a result?

Because of decoherence, this is not a question we can address experimentally,
either now or for the foreseeable future. But let's look at what we *do* know.

When you *experience* a decaying cat, you really ought to be able to call it
dead. So becoming *conscious* of the result is an obvious *upper bound*: the
result certainly occurs *no later* than this. Now, can we say that it happens
any earlier?

Well, should you say there is a result when it has only entangled with your
*toe*? There seems to be no principled reason to consider your toe different 
from, say, the door of the room you're in. Entanglement with your toe should be 
thought of as:

`(|U1>|U2>|Ex>|Toe_x> + |D1>|D2>|Ey>|Toe_y>) @ |You>`

"You" are still not entangled. The same reasoning applies to the "unconscious
parts of your brain." We might be tempted to say that *obviously by the time it
entangles with any part of your brain, there is a result*, but in principle, we
have no more reason here than we did long before it reached your brain -- and we
didn't have sufficient reason then. "Your brain" is not the relevant piece here;
your consciousness is. The fact that consciousness clearly relates to the brain
causes us to conflate the two and say imprecise things like "the result occurs 
when it entangles with your brain."

We have *no good reason* to draw the line anywhere earlier than "your
consciousness," even if we have no clear scientific definition of that term. In
this sense, it *is meaningful* to talk about definite results only coming into
being when they encounter your consciousness.

This is why you should be skeptical of any claims that "consciousness has
nothing to do with QM." You should also know that you're in good company if you
think otherwise:

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
> -- Sean Carroll

Here's a crazy way to wrap your brain around it. What if the world comes into
being with your consciousness because *your consciousness* and *the world* are
two ways of talking about the very same phenomenon?

Consider a nighttime dream. What you think of as an external world is really
your own mind, illuminated. But that mind is not happening within the brain of
the character navigating the dream. It is the mind of the *dreamer*; your waking
self; a being that exists beyond the confines of the dream. If the dream
character were to introspect carefully, she would discover that she and the
dreamer are the same. This is called becoming *lucid*.

Similarly, listen to a sound right now. What could that (or any other
experience) *be*, other than your own mind, illuminated? All empirical evidence
suggests that this mind is caused by something inside your skull. But consider
the possibility that this is just an artifact of this particular dream.

The possibility on offer here is that what you call "the world" is your dream,
made of your mind -- but what "you" are is not the character you normally take
yourself to be, but *that which dreams realities into being*. That which looks
through your eyes; whose mind manifests as existence itself.

Obviously, most physicists would bristle at this suggestion. Where is the
evidence for such a wild hypothesis? On the other hand, if this really is your
dream, it would be silly to wait for someone else to provide you with evidence
of it. If you're disheartened by the fact that nobody else seems to have woken
up, just remember that this is *your* dream; your branch; your world. If you
want to become lucid, begin by noticing that it is made of your mind, and then
notice that you ought to be *very* skeptical about the cause and nature of that 
mind[7].

This is (very roughly) what the Buddha was suggesting for becoming lucid in
this dream. If you're wondering why he wasn't flying around, I guess you should
ask yourself. This is *your* dream, after all.

### Other approaches to QM

This document would not be complete without mentioning other interpretations of
QM.

The most popular interpretation of QM (amongst physicists) since its inception
has been the "Copenhagen Interpretation." Leaving aside the issue that nobody
can seem to agree on what, exactly, it is[5], we can take it as roughly saying
that the two branches of the wave function "collapse" into one, sometime long
before it reaches you. 

This collapse postulate is an abomination in physics, being the only
nondeterministic and irreversible law we've ever needed to shoehorn in. And as
we are able to do better and better experiments[6], it is becoming increasingly
obvious that collapse is very unlikely anyway.

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

5. [The most embarrassing graph in modern physics](http://www.preposterousuniverse.com/blog/2013/01/17/the-most-embarrassing-graph-in-modern-physics/).

   > *I think Copenhagen is completely ill-defined, and shouldn't be the
   favorite anything of any thoughtful person.*
   
6. For example, in [this experiment](http://physicsworld.com/cws/article/news/2010/mar/18/quantum-effect-spotted-in-a-visible-object),
they were able to put trillions of particles into superposition.

7. In brief, consider two hypotheses: (1) the world is material in nature, and
(2) it is mental. If you try to assign probabilities to these possibilities, you
will find yourself making assumptions that are not falsifiable, and generally
presuppose the desired conclusion in one way or another. Thus there is no
principled way to assign probabilities to these, let alone an infinitude of
other strange metaphysics. All you can be sure of is that "something seems to be
happening." It is this fact that I am calling "mind," leaving aside the question
of what mind actually is*.


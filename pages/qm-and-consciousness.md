---
layout: page
title: Quantum mechanics and consciousness
description:
---

## Overview

Does consciousness have anything to do with QM? New age types often insist that
it does, and frustrated physicists often counter that this stems from a terrible
misunderstanding.

While a proper understanding of QM does require a solid foundation in linear
algebra and differential equations, the relevance of consciousness can be
understood much more simply.

Here I will try to communicate the essential points (and common
misunderstandings) with as little math as necessary. I'll include footnotes for
those with some background. For fun, I'll end with my own (decidedly "New Age")
interpretation.

I hope this enables the lay reader to understand the issue more clearly (though
apparently even "quantum" physicists -- whose work rarely if ever requires them
to consider these philosophical issues -- have found some bits informative).

---

### Superposition, interference, and entanglement

A particle can be in a *superposition* of states. A particle in a superposition
of spin-up and spin-down along the x-axis might be written:

`|U1> + |D1>`

The state `|U1>` is the spin-up component, and `|D1>` the spin-down component.
The `1` is there to indicate that this is our first particle, since we shall
soon be adding more.

The crucial point is that unlike a classical particle, this particle cannot be 
said to exist in _either_ one state or the other. Even the popular description
of it being in "both states at once" is inaccurate. Something more subtle is
going on.

Exactly what that subtlety _is_ requires some linear algebra to understand
properly[1], but the important point is this: if we choose to measure the
particle's spin along the x-axis, we will either get the answer _up_ or _down_.
And yet, _before_ we measure it, there exists something called an _interference
experiment_ that can *prove* that the particle does not yet have an x-spin 
(as opposed to _having_ a definite spin that we are merely unsure about).

If this is confusing, just remember this crucial point: 
*the outcome of such an experiment is how we know that there isn't a single
result yet.* If the outcome *does* show interference, the particle is still in a 
superposition; otherwise, it has a well-defined state.

Now, we can let this particle interact with a second one in such a way that the
new particle's spin *matches* the first's. That is to say, we *entangle* them.
Now neither has a well-defined spin, and yet *if* we measure either particle's
spin, the other will have the *same* spin.

Using numbers to differentiate the two particles, the new joint state is
written:

`|U1>|U2> + |D1>|D2>`

The component `|U1>|U2>` means that both particles are *up*. The other component 
is `|D1>|D2>`, where they are both down. The sum `+` indicates that they are in
a superposition of these possibilities. Because the joint state is a
superposition, the right interference experiment conducted on **both particles
together** will show interference[2], confirming that the pair is *not* in a
definite-but-unknown (i.e., classical) state. It is still quantum; neither
component is definite yet.

But something funny happens when you restrict your attention to either particle
*alone*: if you do an interference experiment on one particle by itself, *it
will not show any interference*[3]. In other words, it will appear that the
particle *did* have a definite (if unknown) spin when we measured it.

Let's recap. We start with a particle in a superposition, which ensures that it
does not have a well-defined spin in the given direction. We could even do an
interference experiment to prove this. Then we *entangle* it with another
particle -- essentially, just letting it interact with any particle in such a
way that the second particle's behavior *differs* based on the spin of the
first. Now we *ignore* the second particle and do an interference experiment
on the first. Lo and behold, it shows no interference, making it seem as though
the first particle *did* have a well-defined spin.

The key point is this: in order for an interference experiment to show
interference -- in order to detect that a system is indeed in a superposition --
the experiment must involve _all_ of the entangled particles.

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
been hit by a cue ball.

When the detector is turned on, the particle *entangles* with it. The two are in
a joint superposition:

`|Particle went left>|Detector shows left> + |Particle went right>|Detector shows right>`

That's what it *means* to be a detector, after all: the particle's state and the
detector's are in agreement. And as we learned before, measuring one part of
such a system alone will not demonstrate interference. Thus, the screen, which
measures interference on the particle alone (ignoring the detector), will not
show any interference.

I realize this may not be the most satisfying answer about what's happening. I
haven't exactly explained "why" entangled particles don't show interference
individually; I only told you that the math explains it. But we could ask the
same about gravity: *why* do two masses attract? At some point you must just
accept that it's how things work, and rejoice that we've found a mathematical
framework that makes accurate predictions around it.

At this point, it is easy to conclude that the detector acted as a measuring
device and "collapsed" the particle's state, thus demonstrating that
consciousness is irrelevant (because any physical detector will do). Indeed,
many popular articles do just this.

But this doesn't tell the whole story. Because even though the isolated particle
indeed appears to have "collapsed" (does not show interference), we promised
that *the system as a whole* is still in a superposition, and that the right
interference experiment ought to demonstrate this. In other words, "before we
look" (more on this later), the experiment still has two possible outcomes
(corresponding to the left and right paths), and it's theoretically possible to
prove this.

Unfortunately, there's a "small" catch....

### Decoherence

What we learned before extends beyond two particles: if you want to demonstrate
interference, you need control of *all* the particles that have become
entangled. In general, this is very difficult: if a photon bounces off of your
experiment, it will carry information about it away at the speed of light.
You'll never catch it. Even if you do your experiment in the dark, trillions of
air molecules will interact with it, and you'll never get precise control over
all of them.

Therefore, superposition is only possible to demonstrate in extremely precise
lab settings. In any real-world context, you lose control almost instantly. This
fact is known as *decoherence*. It is the reason quantum computers so hard to
build.

Denoting the environment (e.g., photons or air molecules) as `E`, we can now
write the entangled state as:

`|U1>|U2>|Ex> + |D1>|D2>|Ey>`

Where `|Ex>` and `|Ey>` are the two different ways the environment reacts with
the different components. Just as the first particle alone could no longer show
interference after entanglement with the second, the first two particles cannot
show interference now that they're entangled with the environment. And since
recapturing all the environmental particles is in practice almost impossible,
decoherence tells us that hereafter, any experiment done on a subset of the
whole system will make it appear as though it has a well-defined state. And if
all (practical) experiments make it *seem* so, then we might as well say that it
*is* so.

This leads us to the second misconception: 

> *If you simply stick a cat in a box and link its fate to the outcome of some quantum event, you’re not likely to put it in a superposition of alive and dead, because decoherence **will almost instantly force it into one state or the other***. 
>
> -- [Quanta magazine](https://www.quantamagazine.org/real-life-schrodingers-cats-probe-the-boundary-of-the-quantum-world-20180625)

This is misleading. The cat is not in a superposition, but the *cat plus
environment* still is. Nothing has been "forced" into one state, even if all
reasonable experiments make it appear so.

Notice how easy it is to overlook the problem or sweep it under the rug. It is
a common misconception that decoherence has solved the "measurement problem"[4]
-- roughly speaking, the question of when a measurement outcome *really*
happens.

So far, all we have said is that *in practice*, real-world systems never appear
to be in superpositions; they appear to collapse very rapidly. Yet, the theory
(and experiments) seems to suggest that if we take a sufficiently broad view,
any experiment is forever in a superposition: there is no result yet. So the
question remains: when does there *actually, really* (not just practically)
become just one result? This must happen, right? After all, we only ever *see*
one result.

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
interacted with **you**. As before, we have:
 
`|U1>|U2>|Ex> + |D1>|D2>|Ey>`

Since you have not interacted with the experiment, we can include you as
follows:

`(|U1>|U2>|Ex> + |D1>|D2>|Ey>) @ |You>`

Don't worry too much about what `@` means (it's called a "tensor product"). You
can treat it like multiplication and distribute it over the sum:

`|U1>|U2>|Ex>|You> + |D1>|D2>|Ey>|You>`

In both the left and right components, you are simply `|You>`. The fact that
there is no difference in the two cases signifies that your state does not
depend on it: you have not interacted with the experiment in a meaningful way
yet. Given how easy it is for information to leak out of an experiment, actually
achieving this state is very difficult. Nonetheless, in this state, from your
perspective, there are *still two possibilities* -- despite the fact that it is
*practically* impossible to demonstrate the fact.

At some point, you interact with the experiment. The two branches will affect
you in different ways (for example, in the Schrödinger's Cat experiment, one
will cause you to experience a dead cat, and the other a live one). This means
you are now entangled with it:

`|U1>|U2>|Ex>|You_x> + |D1>|D2>|Ey>|You_y>`

When we look at the problem this way, an elegant answer presents itself: instead
of saying that there is only one result, why not simply admit what the math is
telling us: there are two results, occupying two different "branches" of
reality. In each branch there is a copy of you, seeing the corresponding result.
Problem solved!

From your perspective, the first time the cat can be said to have a well-defined
fate is when it entangles with you, personally. Is this weird?

Perhaps not. After all, the situation is the same for everyone else. If you've
entangled with the experiment but your friend hasn't, she will consider it to
have no result yet even though you do. Still, when you compare notes later,
you'll discover that you agree.

On the other hand, consider carefully how things look for you. The only world
you can ever know is *your* world, and *in* that world, experiments do not have
outcomes until they entangle with you, personally. In your world, nobody else
has this "power." You can (indeed, should) treat them as physical systems,
whose role differs in this critical way from yours.

> *This [reduction of the quantum state] takes place whenever the result
  of an observation enters the
  consciousness of the observer - or, to be even more painfully precise,
  my own consciousness, since I am the only observer, all other people
  being only subjects of my observations.*
>
> -- (Nobel laureate) Eugene Wigner

There are other interpretations of QM, but for the most part, unless they
include a nasty "collapse" postulate (which we'll briefly revisit later), this
is where they're forced.

This still doesn't seem to implicate consciousness though. For that, we must
reason more carefully.

### Consciousness

Let's return to one very important bit we've glossed over. Note that **you** are
made of many particles. Which of those particles, *precisely*, need to become
entangled with the experiment before you should say there is a result?

Because of decoherence, this is not a question we can address experimentally,
either now or for the foreseeable future. But let's carefully revisit what we
*do* know.

When you *experience* a decaying cat, you really ought to be able to call it
dead. So becoming *conscious* of the result must be what mathematicians would
call an *upper bound*: the result certainly occurs *no later* than this. Now,
can we say that it happens any *earlier*?

For example, should you say there is a result when it has only entangled with
your *toe*? There seems to be no principled reason to consider your toe
different from, say, the door of the room you're in. Entanglement with your toe
should be thought of as:

`(|U1>|U2>|Ex>|Toe_x> + |D1>|D2>|Ey>|Toe_y>) @ |You>`

"You" are still not entangled. The same reasoning applies to the "unconscious
parts of your brain." We might be tempted to say that *obviously by the time it
entangles with any part of your brain, there is a result*, but in principle, we
have no more reason here than anywhere else. You are free to treat the rest of
your brain as part of the environment.

The point is that *being conscious of a result* is the first evidence we ever
have of there *being* only one result. In addition, the theory gives us no
reason to say (indeed, every reason *not* to say) that there is only one result
*before* this point. The fact that you are unable to exploit this enormous 
superposition *in practice* ought not make us sloppy and say that it is not 
there *in principle*.

This is why you should be skeptical of any claims that "consciousness has
nothing to do with QM." It's true that the third-person phenomenon you call
"consciousness" -- the thing you *believe* that others have, but can never prove
-- is not special in QM. But the *first-person* experience you call "my
consciousness" *is* intimately connected with it. QM is *very much* about the
relationship between "the world" and *your* consciousness. Or, to be even more
painfully precise, *my* consciousness, all of you being subjects of my
observations....

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

Notice that what you call "the world" is an amalgamation of experiences --
sensory experiences together with thoughts and ideas (including the idea that
there must be a "real world" sitting *behind* those experiences and causing 
them).

Now, instead of thinking of consciousness as a property that you *have*, think
of it as the very *fabric* of your experiences; what they are *made of*. Listen
carefully to a sound, and try to get a sense of how it is made of your own mind,
illuminated.

In other words, what you have been calling "the world" is a modulation of your
own consciousness. From this perspective, it should not be surprising that a
definite world comes into being only when it encounters your consciousness: they
are two ways of describing the same phenomenon.

Notice that the same thing happens during nighttime dreams: what you thought was
an external world is actually your own mind, illuminated. But whose mind is it,
exactly? Not the dreamer's, since she (and her brain) is an illusion. It refers
to a being that *transcends* the dream, yet experiences it from within, through
the eyes of the dream character.

The possibility on offer here is that what you call "the world" is your dream,
made of your mind -- but "you" does not refer to the character you normally take
yourself to be. You are *that which dreams realities into being*, whose mind
manifests as the universe itself, taking on the limited perspective of the
character you call "me." This is what various spiritual traditions are trying to
convey to you: *wake up and discover this for yourself*. You are the Buddha,
going through a crazy trip called "this bozo navigating physical reality."

Obviously, most physicists would bristle at this suggestion. Where is the
evidence for such a wild hypothesis? On the other hand, if this really is your
dream, it would be silly to wait for someone else to provide you with evidence
of it. If you're disheartened by the fact that nobody else seems to have woken
up, just remember that this is *your* dream; your branch; your world.

If you want to become lucid, begin by noticing that this is all made of "your"
mind, and then notice that you ought to be *very* skeptical about the cause and
nature of that mind[7].

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

7. For example, you may think that the simulation hypothesis is unlikely,
whereas the person next to you might consider it very likely. Your disagreement
will (probably) not be settled by evidence, since each perspective is built on
untestable assumptions. Similarly, you cannot unbiasedly assign probabilities
to the hypotheses that the world is made of stuff (materialism) vs mind
(idealism). You can pick one and live with the consequences of your choice,
but this is not the same as it being *correct* or even *likely*.

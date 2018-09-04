
## Overview

Everyone knows that QM is weird, but few people seem to appreciate what,
exactly, is weird about it. There are common misconceptions that cause people
to think that some things are weird when they're not, and that other things are
not weird when they are.

Here we will give a brief overview of QM for the layperson, taking care to 
point out some common misconceptions. I'll avoid using math in the main 
article, but include it in the footnotes for the interested reader.

## Intro

Physicists learn QM "the hard way." As Scott Aaronson [points out](https://www.scottaaronson.com/democritus/lec9.html), 
it is generally not until years of solving incredibly complex differential 
equations that they get to the interesting (and simple) stuff:

> *Today, in the quantum information age, the fact that all the physicists 
had to learn quantum this way seems increasingly humorous. For example, I've 
had experts in quantum field theory -- people who've spent years calculating 
path integrals of mind-boggling complexity -- ask me to explain the Bell 
inequality to them. That's like Andrew Wiles asking me to explain the 
Pythagorean Theorem.*

As a result, the layperson is led to believe that his understanding of the
strangeness of QM *must* be deficient, when in fact it *can* be appreciated 
through careful reasoning. This is exacerbated by the apparent distaste the 
physics community has for thinking too hard about the problem. CalTech 
Physicist Sean Carroll:

> *I suspect that a substantial majority of physicists who use quantum
  mechanics in their everyday work are uninterested in or downright
  hostile to attempts to understand the quantum measurement problem.*

So just what is this "measurement problem" and why does it provoke hostility?
To understand that, let's first take a whirlwhind tour of the basics.

## Superpositions, interference, and entanglement

### Superposition and interference

Particles have many observable properties ("observables" for short), such as
spin, position, and momentum. Whenever we "look" at a particular observable,
it has a well-defined value (such as *spin up* or *spin down*), but at any
other time, it can be in a **superposition** of these states. It is impossible
to explain precisely what this means without using math. For now, it is enough
to understand that it means two things:

1) When we actually *measure* the observable, it will come out randomly in one
of its constituent states.

2) This is *not* the same thing as *classical* uncertainty (i.e., we cannot
simply say "it is *already* in one of those constituent states, but we don't
know which"). We can do what's called an **interference** experiment to prove
that a particle is in a superposition and not just a classical mixture.

### Entanglement

Now, say we have a particle in a superposition of *spin-up* plus *spin-down*.
Suppose it encounters another particle, causing the latter's spin to change so
that it matches the first's. What we now have is a superposition of "first
particle is spin up *and* second particle is spin up" plus "first particle
is spin down *and* second particle is spin down." You can think of this as
having applied classical mechanics to each "branch" separately.

If we measure either particle's spin, it will tell us about the other's. The 
particles are said to be **entangled**. In a sense, the second particle acts
as a *detector* for the first (and vice versa). Indeed, anything you call a 
"detector" had *better* give you information about the thing it is detecting, 
or else it is a rather poor detector.

Now something interesting happens if we isolate the first particle and measure
its spin: namely, it will no longer show any signs of interference. To show
interference, you must look at *both* particles together. Again, understanding
exactly *why* requires some math, but once you understand it, it is not
particularly weird.

What this means is that if you consider only a *subset* of particles in a
superposition, that system will not "look" quantum. You will be able to reason
about it in a classical way, making it easy to forget that the broader system
is still in a superposition.

Before we continue, now is a good time to note that Einstein did in fact
refer to (the effects of) entanglement as "spooky action at a distance." If
you want to understand why, you should read about Bell's Inequality. But this
is not the particular spookiness we are after.

## Decoherence

In a carefully controlled lab setting, it may be possible to sequester your
particles such that you can demonstrate interference on them together. But
outside of such a strict setting, stray particles are liable to get involved.
For example, a photon might bounce off your apparatus and fly away at light
speed. Since it carries some information about your experiment, it is
entangled with it. Since you will never catch it, you have no hope of
demonstrating interference on the system as a whole. In most environments there
will also be trillions of air molecules getting in on the action. You might as
well call your experiment classical.

This problem is known as *decoherence*. It is merely entanglement run amok.
Therefore, all of the same issues that apply to entanglement apply to
decoherence: it effectively prevents us from demonstrating that our
experimental system is in a superposition, but it *does not say that the
superposition has disappeared*. It has merely grown to include lots of other
things. Thus the system is still not in a well-defined state, no matter how
hard it is to *demonstrate* the fact.

We are now equipped to understand some common misconceptions.

## Misconception 1: The two-slit experiment is spooky

In the famous two-slit experiment, an electron (or other particle) is put into
a superposition of *having gone through the left slit* and *having gone 
through the right slit*. As a result, it produces an *interference pattern*
on the detection screen.
 
Next, we decide to put detectors at the slits and repeat the experiment, to 
figure out which way the electron "really" went. When we do this, the 
interference pattern disappears. If you didn't know anything about QM, you 
might make silly claims like this New Age movie:

> *The electron decided to act differently, as though it was aware that it 
was being watched!!*

But it wasn't "aware" and it didn't "decide" anything -- unless you also
believe that a billiard ball "decides" to change direction when it is "aware"
it has been hit. The electron interacted with a physical detector. The two
are now *entangled*. As we learned, that means that the first particle
should not show interference. This may be interesting, but it is not spooky
in the least.

And it's not just New Agers [who flub this](http://www.bbc.com/earth/story/20170215-the-strange-link-between-the-human-mind-and-quantum-physics):

> *The most famous intrusion of the mind into quantum mechanics comes in the 
"double-slit experiment". ... Simply by observing a particle's path – even 
if that observation should not disturb the particle's motion – we change the 
outcome.*

There's nothing about "mind" in here. Any particle that entangles with the
electron will cause this effect. The relevance of "mind" only comes in later 
(as we shall see).

Once you understand the error in such claims, it becomes easy to think that
the core problem has been resolved -- but it hasn't. The particle may not
show interference, but the system as a *whole* is still in a superposition:
"electron went left and detector shows left and screen records left" plus
"electron went right and ...." And yet you will only *see* one result. Why?

This brings us to....

## Misconception 2: Decoherence solves the measurement problem

The other famously weird (thought) experiment is Schrödinger's Cat. In this 
experiment, a radioactive particle does (or does not) decay, which triggers 
(or does not) a device, which then kills (or does not) a cat. Now the 
particle, device, and cat (not to mention lots of random air molecules 
and photons) are *together* in a superposition which has two "branches":

1) Particle decayed and device triggered and cat died and air smells and ...

2) Particle did *not* decay and ... cat did *not* die and ....

In any experiment of this size, decoherence will be an insurmountable problem.
That is, we will be very hard-pressed to *show* that the system is in a
superposition. But (until you entangle with it), it is technically still in one.
It is just plain wrong to say that it has a well-defined state, just because
you can't show any interference. And yet, this seems to be a very [popular 
misconception](https://www.quantamagazine.org/real-life-schrodingers-cats-probe-the-boundary-of-the-quantum-world-20180625/)[1]:

> *If you simply stick a cat in a box and link its fate to the outcome of some quantum event, you’re not likely to put it in a superposition of alive and dead, **because decoherence will almost instantly force it into one state or the other.***

## The measurement problem

The measurement problem, in a nutshell, is why, when, and how (and heck, even
*if*) we end up with *one* result when everything seems to suggest that the
two possibilities continue to exist. So how do we resolve it? There are
basically three possibilities.

1) QM needs to be modified in some way (as in [de Broglie-Bohm theory](https://en.wikipedia.org/wiki/De_Broglie%E2%80%93Bohm_theory)). This is
not very popular.

2) Something "collapses" the superposition somewhere, into just one branch.

  There is no evidence for such a process. We have not found a size or count 
limit where we cannot demonstrate interference (assuming we actually have
control over all the particles). It would also violate some of the deepest 
known principles of physics. It only exists because it's easier than 
confronting the weirdness head-on.

  This is roughly called the Copenhagen Interpretation, and it has been the
party line for over a century, despite it being ill-defined and making very
little sense[2].

3) You *don't* see only one result. Instead, as you entangle with the system,
there become two "copies" of you, each occupying a different "world," and each
seeing one result. This is roughly the Many Worlds Interpretation (MWI). It
requires no additional assumptions and violates no foundational principles. As
a result, it is gaining popularity.

  Does this resolve the weirdness? It depends on your perspective. Yes, from
"God's" perspective, the system just keeps evolving as it interacts with you,
the same as it does for anything else. But from *your* perspective, you seem
to occupy a unique role. *You* are where the buck stops for all superpositions.

 Before an experiment entangles with you, you can (theoretically) show that
it's in a superposition. Not only that, but anyone else you talk to (who is
therefore *also* outside of the experiment) can demonstrate it too. But *after*
you entangle, neither you nor they will be able to do this. In a sense, you
are where the buck stops for *everyone*. *This* world is *your* world.

# Some philosophizing

Whether you take MWI literally, this natural extension of the system becoming
entangled with you has some interesting consequences regarding how you might
conceive of your existence and experience. Let's take a look at a few.

### You as a temporary phenomenon

Suppose you are about to entangle with Schrödinger's Cat, and ask yourself:
what are the odds that I will see a dead cat?

In one sense, the question is meaningless. It is *certain* that you will see 
*both* results, not just one. There are no "odds" involved there.

But you might protest: I *will* see one result, even if "another copy of me"
sees the other. And if I run the experiment enough times, I can tally up a
probability distribution (which should be 50-50). This gives meaning to the
question "what are the odds?"

How can these two views be reconciled?

The problem lies in assuming that the "I" asking the question now is going to
continue along one path, so that it can be the same "I" answering whether the
cat is dead or alive. A better model would be to say that "I" is a *momentary*
phenomenon, existing only *now*. Nothing links your present self to the future
self, except for memories.

### You as the sum total of your experience

This whole time we've been talking about the experiment becoming entangled with
"you," but what, precisely, is this "you?" If your *toe* entangles with the
experiment (and the signal has not traveled up your leg), the toe is as much
an external piece of equipment as anything else. Even the unconscious parts of
your brain ought to be treated this way, as far as we know[4].

The measurement problem comes into being because you *experience* one result.
Clearly this has something to do with your experience, or consciousness. A
simple resolution is to say that *you* refers to the *conscious parts of your
brain.* You *are* that conscious process, in its entirety.

Right now there are some neurons firing, producing the visual experience of a 
screen in front of you. You are not located at some distance *from* those 
neurons firing; you *are* those neurons firing. Put another way: that "screen" 
*is* you -- as are all the other sights, sounds, tastes, smells, textures, 
thoughts, etc. that constitute your experience of the world.

It is an illusion to feel that you are located at some distance from your
experiences. Together, they *constitute* "you."


## Penetrating the illusion

So what happens when these two illusions -- the illusion of continuity, and
the illusion of separation -- are punctured?

First, it's not even obvious that they *can* be punctured. Perhaps you are
stuck perceiving the world from this illusory perspective, and the best you
can hope for is to understand it really well. But does that help you live your
life in any way?

Even if it *could* be punctured, would that be desirable? Or would it be
[like having a stroke](https://www.ted.com/talks/jill_bolte_taylor_s_powerful_stroke_of_insight) -- at best,
interesting for a short while?

I'd like to propose another, very strange, possibility. Don't say I didn't warn
you.



---


[1] [The decoherence myth](https://plato.stanford.edu/entries/qm-decoherence/#SolMeaPro):

   > Unfortunately, naive claims of the kind that decoherence gives a
complete answer to the measurement problem are still somewhat part of
the ‘folklore’ of decoherence, and deservedly attract the wrath of
physicists (e.g. Pearle 1997) and philosophers (e.g. Bub 1997, Chap. 8)
alike.

   See also [this answer](https://physics.stackexchange.com/a/374212/118804).

[2] [The most embarrassing graph in modern physics](www.preposterousuniverse.com/blog/2013/01/17/the-most-embarrassing-graph-in-modern-physics/).

> *I think Copenhagen is completely ill-defined, and shouldn't be the favorite anything of any thoughtful person.*

[3] Which is to say, just *before* you entangle with the experiment, other
people can discover that it is still in a superposition and show you
evidence of the fact. Afterward, everyone will agree with the outcome you
see.

[4] You might wonder: how do we *know* that unconscious parts of the brain do
not count? But the real question is, do we have any reason to believe that they
*do* differ from other physical objects? It seems we do not. And yet, such
unconscious information is likely to affect your conscious experience at some 
point, however minuscule the effect.

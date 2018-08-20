
# What decoherence is and why it does not solve the measurement problem


### Superposition

Particles have a property called *spin*, which can be *up* or *down*. A particle
can also be in a *classical* combination of those, which means roughly that it's
*actually* in one state **or** the other but we don't know which. If that's the
case, then we can answer various questions about it by doing a case analysis: 
"*if* it's in *spin-up*, then ... and if it's in *spin-down* then ..., therefore 
on average, ...."

Alternatively, the particle can be in a quantum *superposition*, in which case
there exist questions for which a case analysis will give the wrong answer. In
fact, this is how we can *know* that a particle is in a superposition: we ask
such a question, and check whether the answer agrees with the case analysis or
not. This is called *doing an interference experiment.*

To give a rough analogy, imagine that you and I decide to play the following
game. I pick a person at random from the world population and ask you a 
question:

> *How many Y chromosomes does the chosen person have?*

You reason as follows:

> *There's a 50% chance it's a male, in which case he has one Y chromosome.
There's a 50% chance it's a female, in which case she has zero. So on average,
we expect 0.5 Y chromosomes.*

This is most excellent reasoning. If we play the game a thousand times, you
should expect to find roughly 500 Y chromosomes. If the actual number differs
by a lot, you should suspect that something is wrong. For example, maybe the
proportion of men to women isn't really 1:1. And yet, if you were to check,
you'd find that it *is*. And yet, by the laws of QM, this is normal. A
particle *can* have 50-50 odds of being *up* or *down*, and yet there are facts
about it that cannot be derived by reasoning about each case separately and then
joining those results.

When a particle is in a superposition, it is not correct to say that it is
*either* in one state *or* the other. It does not have a well-defined value.
Yet, whenever we "look" at a particle's spin, it is always either *up* or
*down*. How do we reconcile these facts? When and how does the particle's spin 
obtain its actual value? This is known as **the measurement problem**.

> *I suspect that a substantial majority of physicists who use quantum
  mechanics in their everyday work are uninterested in or downright
  hostile to attempts to understand the quantum measurement problem.*
>
> &nbsp;
>
> -- Sean Carroll

### Entanglement

Suppose our particle (in a spin superposition) encounters a second particle,
causing the latter's spin to change and match the first's. Since we don't
actually know the spin of the first, we don't know the spin of the second 
either. All we can say is "either both particles are spin-down or both are 
spin-up." Just like before, though, this is still a quantum superposition: we 
cannot say that they *actually* have a spin that is unknown to us. And as with 
all superpositions, there is (theoretically) a way to *demonstrate* this fact. 
We say that these particles are *entangled*. All this means is that knowing
something about one particle tells you something about the other.

But something interesting now happens: if you choose to *ignore* one of the
particles and only look at the other one, that particle's spin will no
longer behave in a quantum way. It will obey *classical* statistics; all 
questions about it can now be answered by "case analysis." The particles
*together* are in a superposition, but either one alone *appears* to be 
classical. If you want the first particle to "look quantum", you must undo the 
entanglement.

As it happens, one of the fundamental laws of QM is that *all operations are
reversible.* If two particles can become entangled, they can also become
*un*entangled -- at least in theory. But doing so requires careful control over
both particles. This is often hard in practice.

### Decoherence

Imagine you have a single particle in a spin superposition in the laboratory.
Unfortunately, it is not well shielded, and a stray photon bounces off of it
in such a way that the two particles become entangled. Because photons move at
the speed of light, you have no hope of catching it to undo the entanglement.
As a result, your experiment is now ruined: even though your particle does not
have a well-defined spin, you will be unable to demonstrate this fact.

This process is called *decoherence.* In any reasonably-sized experiment, lots
of stray particles from the environment (air molecules, photons, etc.) are going 
to prevent you from exhibiting the quantum effects you want to. But a critical 
point is that *the system as a whole* -- your particle plus the stray 
particles -- are together still in a superposition. Being able to *demonstrate*
this may be far outside the realm of present (or even presently *imaginable*)
technology, but this is not the same thing as saying that the particle has a
well-defined state. It doesn't.

Nonetheless, a lot of popular writing on QM suggests that decoherence solves
the measurement problem. It does not[0].

---

Now let us look at some examples.

### The two-slit experiment

In the famous two-slit experiment, an electron (or other particle) is put into
a superposition of *having gone through the left slit* and *having gone through
the right slit*. A "case analysis" would go like this:

> If it went through the *left* slit, it would land *here*, and if it went
through the *right* slit, it would land *here*. Therefore, the places it can
land are *these two places combined*.

As you probably know, this reasoning fails. The particle can end up in a 
variety of surprising places, forming a light-dark interference pattern.

Next, you decide to put detectors at the slits, to figure out which way the
electron "really" went. When you do this, the interference pattern disappears,
and the classical reasoning succeeds! If you didn't know anything about QM, you
might make silly claims like this New Age movie:

> *The electron decided to act differently, as though it was aware that it was 
being watched!!*

But unless you believe that a billiard ball "decides" to change direction when 
it is "aware" it has been hit, all of this anthropomorphizing is unnecessary.
The electron *struck* a physical detector. The two are now *entangled*. This
isn't weird; all it means is that the detector gives you some information
about the particle. Indeed, if it did not, then it would be a pretty poor
"detector."

As we learned before, this entanglement allows us to reason classically about 
the particle: it can only land *here* or *here*. And yet, as we said, the 
system *as a whole* is still in a superposition of two states:

1) Electron went left and detector shows left and screen shows left.

2) Electron went right and detector shows right and screen shows right.

This doesn't mean that one of the paths has *actually* happened yet; it just 
means that *for all practical purposes* we can pretend like it has.

So when does one path "actually" happen? We must go deeper....

### Schrödinger's Cat

In this experiment, a radioactive particle does (or does not) decay, which
triggers (or does not) a device, which then kills (or does not) a cat. 
Now the particle, device, and cat (not to mention lots of random air molecules 
and photons) are *together* in a superposition which has two "branches":

1) Particle decayed and device triggered and cat died and air smells and ...

2) Particle did *not* decay and ... cat did *not* die and ....

Decoherence has very rapidly put an end to our ability to demonstrate the
superposition, but *it still exists*. This point is unfortunately very often
misunderstood[1]. So again: where does one path become *real?*

## Solutions to the measurement problem

There are roughly three possibilities:



---



[0] [The decoherence myth](https://plato.stanford.edu/entries/qm-decoherence/#SolMeaPro):

   > Unfortunately, naive claims of the kind that decoherence gives a
complete answer to the measurement problem are still somewhat part of
the ‘folklore’ of decoherence, and deservedly attract the wrath of
physicists (e.g. Pearle 1997) and philosophers (e.g. Bub 1997, Chap. 8)
alike.

   Roger Penrose (2004), The Road to Reality, pp. 802-803:
   > ...the environmental-decoherence viewpoint ... maintains that state 
vector reduction can be understood as coming about because the
environmental system under consideration becomes inextricably entangled
with its environment.[...] We think of the environment as extremely
complicated and essentially 'random' [... but] there is **no general 
principle providing an
absolute bar to extracting information from the environment.**[...]
Accordingly, such descriptions are referred to as FAPP [For All Practical
Purposes].

   See also [this answer](https://physics.stackexchange.com/a/374212/118804).


[1] See, for example, this piece from Quanta Magazine (emphasis mine):

> If you simply stick a cat in a box and link its fate to the outcome of some quantum event, you’re not likely to put it in a superposition of alive and dead, because decoherence **will almost instantly force it into one state or the other**.



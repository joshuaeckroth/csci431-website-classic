---
title: Knowledge representation
layout: note
---

# Knowledge representation

The majority of the following discussion comes from Davis et al.,
"[What is a knowledge representation?](http://www.aaai.org/ojs/index.php/aimagazine/article/viewArticle/1029)"

A knowledge representation is:

- a *surrogate* for real-world entities

- an *ontological commitment* about what kinds of entities are
  relevant

- a *fragmentary theory of intelligent reasoning*, expressed in
  terms of three components: (1) the KR's idea of what makes
  intelligent reasoning, (2) the inferences that are possible in the
  KR, and (3) the inferences that it "recommends"

- a *medium for pragmatically efficient computation*; the KR offers
  guidance for organizing information to facilitate making the
  recommended inferences

- a *medium for human expression*

## KR is a surrogate

Reasoning about the world is an internal process. If an agent wishes
to plan how to assemble a bike then the agent must "think" about
wheels, chains, handle bars, and so on. These entities must exist in
the agent's "mind" if it is to think about them. We expect the agent
to be able to *plan* how to assemble a bicycle without needing to
physically manipulate bicycle parts.

Thus, the knowledge representation provides a surrogate for real-world
entities. If the KR is useful, the actions that can be performed
internally (as the agent is "thinking") will more-or-less match what
the corresponding real-world actions do to real-world entities. For
example, the agent's understanding of what "lock the wheel into the
frame" does to a wheel and a frame should match the real world (the
wheel is now stuck to the frame, and if the frame is lifted, the wheel
comes with it, etc.).

For any entity (surrogate) in the knowledge representation, we have to
be sure we have a good argument for:

- "correspondence": what does this entity in the KR represent in
  reality?

- "fidelity": how well does it match what it is supposed to
  represent?

All representations are imperfect; some detail is always left out (for
pragmatic concerns if not oversight). Things can go wrong. Locking the
wheel into the frame may not work on some occasion (say, the frame is
bent). We will never be able to represent all possibilities.

## KR is an ontological commitment

All representations are imperfect, and details must inevitably be left
out; furthermore we typically do not attempt to represent every
object and fact in the known universe. Thus, whenever we use a
knowledge representation, we are making a (possibly implicit)
commitment to the existence of certain entities and not others. If we
want to build an agent that can assemble and fix bicycles, that agent
presumably has no use for facts about the Napoleonic Wars. So to the
bicycle-fixing agent, those historical facts simply do not exist. It
has no way of thinking about them.

Davis, et al. describe this feature of KRs as the "focusing" or
"glasses" effect, because the agent is effectively wearing glasses
that limit its focus.

> The focusing effect is an essential part of what a representation
offers because the complexity of the natural world is overwhelming.
We (and our reasoning machines) need guidance in deciding what in the
world to attend to and what to ignore. The glasses supplied by a
representation can provide this guidance: In telling us what and how
to see, they allow us to cope with what would otherwise be untenable
complexity and detail. (*op cit.*)

Figuring out what ontological commitments to make, that is, what is
relevant to the agent, is a big problem. Also a problem is giving the
agent an understanding of what is *not* represented. Assembling a
bicycle in zero gravity is likely much more difficult; so can the
agent just assume it is operating in Earth-like gravity? Why can it
make that assumption? Where *is* that assumption in the agent's
programming and knowledge?

These problems are elucidated by John McCarthy, by way of an example:

> Three missionaries and three cannibals come to a river. A rowboat that
seats two is available. If the cannibals ever outnumber the
missionaries on either bank of the river, the missionaries will be
eaten. How shall they cross the river?
>
> Obviously the puzzler is expected to devise a strategy of rowing the
boat back and forth that gets them all across and avoids disaster
[...]
>
> Imagine giving someone the problem, and after he puzzles for a while,
he suggests going upstream half a mile and crossing on a bridge. 'What
bridge?' you say. 'No bridge is mentioned in the statement of the
problem.' And this dunce replies, 'Well, they don't say there isn't a
bridge.' You look at the English and even at the translation of the
English into first order logic, and you must admit that 'they don't
say' there is no bridge. So you modify the problem to exclude bridges
and pose it again, and the dunce proposes a helicopter, and after you
exclude that, he proposes a winged horse or that the other hang onto
the outside of the boat while two row.
>
> You now see that while a dunce, he is an inventive dunce. Despairing
of getting him to accept the problem in the proper puzzler's spirit,
you tell him the solution. To your further annoyance, he attacks your
solution on the grounds that the boat might have a leak or lack
oars. After you rectify that omission from the statement of the
problem, he suggests that a sea monster may swim up the river and may
swallow the boat. Again you are frustrated, and you look for a mode of
reasoning that will settle his hash once and for all. --- J. McCarthy,
"[Circumscription---A form of non-monotonic reasoning](http://cogprints.org/410/)," 1980

## KR is a fragmentary theory of intelligent reasoning

The reason we build and employ knowledge representations is to
facilitate inferencing or reasoning that's intelligent. The KR embeds
a theory of intelligent reasoning. This theory is fragmentary because
we have (so far) been unable to build a KR, with an accompanying
inferencing procedure, that captures all intelligent reasoning. One
might be able to argue that, in principle, building such a complete
theory is impossible.

There are three fundamental questions related to a KR's embedded
theory of intelligent reasoning:

### What is intelligent reasoning?

The field of AI has discovered/invented many varieties of intelligent
reasoning. We have deduction (which is what we'll study), induction,
abduction, reasoning by analogy, probabilistic reasoning, case-based
reasoning, etc. Each of these are closely related to certain knowledge
representation data structures.

### What can we infer from what we know?

Deduction famously cannot yield any new facts; a deductive conclusion
does not state anything more than what was already present in the
premises. However, induction and abduction, for example, are
"ampliative" forms of reasoning because they offer new facts (which
may be wrong; deduction, on the other hand, is never wrong).

If we want ampliative inference, we have to keep this in mind as we
build the knowledge representation. In this case, deduction cannot be
our only inference tool.

### What should we infer from what we know?

Often the set of inferences available to use is enormous. Which just a
handful of premises and the method of deduction, we can often deduce
many irrelevant facts. How does the agent guide the inference process
so that it can meet certain goals?

## KR is a medium for pragmatically efficient computation

AI systems must eventually *do* something; they must compute. So, we
need our knowledge representation to be computationally
pragmatic. It's easy to think up knowledge representations that are
simple, beautiful, precise, and... unwieldy. The tricks for making a
KR useful but also pragmatic can be quite sophisticated. We'll avoid
dealing with this issue. However, when we look at
[Prolog](/notes/prolog.html), it is important for us to keep in mind
that Prolog is useful precisely because it limits the expressiveness
of the KR in order to keep the inferencing computationally efficient.

## KR is a medium for human expression

> If the representation makes things possible but not easy, then as real
users we might never know whether we misunderstood the representation
and just do not know how to use it or whether it truly cannot express
some things that we would like to say. A representation is the
language in which we communicate; hence, we must be able to speak it
without heroic effort.

## Making it happen

When we actually create systems that solve AI problems, we need to
decide on one or more knowledge representations. There are two general
categories of KRs: procedural and declarative.

### Procedural knowledge

This is the form of knowledge with which you are probably most
familiar. Procedural knowledge is, essentially, a program. If you want
to give your robot knowledge about how to navigate a maze, you write
code to navigate a maze. This code will probably first find the
locations of nearby walls and exits, and make a choice about where to
move based on criteria embedded in the algorithm.

In another case, an industrial robot may be programmed to perform a
certain sequence of actions (maybe with a few variations depending on
context), such as assembling part of a car. The "knowledge" is
embedded in the procedure (the algorithm).

Compare this description of procedural knowledge with the way
cognitive psychologists describe procedural knowledge: they say that
procedural knowledge includes recognition of a face or reacting to a
joke. For them, it is "tacit" knowledge because it cannot be described
by the person who has it; exactly what knowledge is brought to bear is
not conscious to the agent. This is similar to our description because
knowledge that is embedded in an algorithm likewise is very difficult
to extract and explicate outside of its active use.

Note that our prior work with the 8-puzzle used procedural knowledge:
the board states were generated based on an algorithm; there was no
separate "description of a board" that we consulted.

### Declarative knowledge

Knowledge that is explicitly represented separately of its use is
declarative knowledge. "I declare that such-and-such is the case!" It
is knowledge that is true independently of how it happens to be used
in some context.

Procedural knowledge is generally specific to the algorithm in which
it is embedded. Thus, there has been less of a drive to create
"universal" ways of representing procedural knowledge (well, perhaps
we can think of programming languages as universal representations of
procedural knowledge).

On the other hand, declarative knowledge, being essentially universal
in nature (not tied to a particular active context like procedural
knowledge is), has experienced centuries of formalization. If we want
to say something universal, perhaps we should have a universal way of
saying it!

We'll look at four ways of "saying" declarative knowledge, each more
sophisticated than the last. We'll explicitly note that these forms of
logic have nothing to do with programming (nothing to do with
procedures). However, in order to actually build software with
declarative knowledge, we'll next look at a programming language that
sort-of approximates a certain logical formalism.


---
title: Turing Test
layout: note
---

# Turing Test


![Turing](/images/turing.jpg){: .right}


The Turing test is the name given to Alan Turing's test for mechanical
intelligence. He called it the "Imitation game," which is described
below. We also look at variations suggested by Daniel Dennett to
support his claim that the Turing test is actually very
strong. Turing's original description can be found in his 1950 paper,
"[Computing machinery and intelligence](http://www.loebner.net/Prizef/TuringArticle.html)."

## The imitation game

The game is played by three people: a man (*A*), a woman (*B*), and an
interrogator (*C*) who may be of either sex. The interrogator stays in
a separate room. The object of the game is for the interrogator to
determine who of *A* and *B* (known to the interrogator as *X* and
*Y*) is the man and who is the woman.

The interrogator asks questions of *A* and *B* such as: Will *X*
please tell me the length of his or her hair?

*A* wants *C* (the interrogator) to come to the wrong
conclusion. Thus, *A* may say his hair is long (which, we are
supposing, gives *C* reason to think that *A* is a woman, i.e. that
*A* is *B*).

Clearly, some measures must be taken so that *C* cannot simply see or
hear who is the man and who is the woman. So conversation happens
through a typewriter.

*B*, unlike *A*, wants *C* to come to the right conclusion. So, *B*
may say, "I am the woman!" But so might *A*.

## What's happening?

Before we talk about replacing one of these players with a machine, we
should try to understand what Turing is doing here. Let's take it for
granted (as I suppose he did) that men and women are quite different;
that there is some *fundamental* distinction and a sophisticated
interrogator might have a chance of telling them apart. (This must be
Turing's belief because the imitation game is pointless if there is no
reasonable way to distinguish the players, for example distinguishing
identical twins with similar life experiences, neither of whom you
know closely.)

So, given that men and women are very different, person *A* would
succeed in confusing the interrogator (making *C* believe that *X* is
*B* rather than the true answer, *A*), and similarly, person *B* would
fail in convincing *C* of the truth, if *A* is a better imitator of a
woman than *B* is, and furthermore that *B*'s arguments to the
contrary fail.

Thus, *B* may win (expose *A* as a man) if *A* is a bad imitator or
*B* has really strong arguments.

Suppose *C* gets the right answer only p% of the time (perhaps with
different interrogators but the same *A* and *B* players; Turing is
unclear here). This performance p% is important to keep in mind.

## Replace the man with a machine!

Now we are ready to understand why Turing set up this game to test
machine intelligence. If we replace *A* with a machine (perhaps *B* is
still a woman, perhaps not, but of course is a human), then we have a
test for machine intelligence.

Now, the machine is trying to convince the interrogator that it is a
human, but the human is not. The human is trying to convince the
interrogator that he or she is a human, but the machine is not.

Just as, supposedly, a man would find it difficult to imitate a
woman, a machine would probably find it difficult to imitate a
human. Yet, if the machine is not only able to act like a human but
also (or alternatively?) to counteract the arguments produced by the
human, then the machine is quite intelligent indeed.

Some interrogator may be naive. Thus, I believe this performance p%
is relevant. If the same machine and human players (or perhaps
different human players) can convince different interrogators more
often than p% of the time, then the machine has passed the test. The
machine need not achieve perfect performance (p = 100%), just has to
beat human performance. (Because, presumably, humans are the most
intelligent creatures that can be used in this test.)

I don't believe there is any reason to suppose a man can successfully
convince a judge he is a woman and the woman is a man more than 50% of
the time. If a man could do this, then he acts like a woman better
than most other women, and furthermore can counteract their arguments
to the contrary. Because the woman is arguing as well, maximum
performance near 25% is probably more appropriate. Anyway, the
machine's goal is to beat that figure, not achieve perfect
convincing. The existence of a machine that can consistently convince
a judge that it is human and the human is a machine, even though the
human is begging for mercy, is an amazing thought!

\[Note, I've since read that this understanding of the Turing Test, in which the machine is trying to convince the judge it is a human, is a "neutered" version. Originally, it is said, Turing expected the machine to be tasked with convincing the judge that it is a woman, which is an easier task since the questions from the judge would not revolve around what it means to be a human. Read "[The Voice of the Turtle: Whatever Happened to AI?](http://www.aaai.org/ojs/index.php/aimagazine/article/view/2106/1996])"
(PDF) by Lenat (2008).\]

## A historical note

Descartes somewhat "predicted" the usefulness of such a test,
even though he believed machines would never be able to pass it, in
principle (because he thought machines could never respond to their
environments):

> If there were machines which bore a resemblance to our bodies and
imitated our actions as closely as possible for all practical
purposes, we should still have two very certain means of recognizing
that they were not real men. The first is that they could never use
words, or put together signs, as we do in order to declare our
thoughts to others. For we can certainly conceive of a machine so
constructed that it utters words, and even utters words that
correspond to bodily actions causing a change in its organs. … But it
is not conceivable that such a machine should produce different
arrangements of words so as to give an appropriately meaningful answer
to whatever is said in its presence, as the dullest of men can
do. Secondly, even though some machines might do some things as well
as we do them, or perhaps even better, they would inevitably fail in
others, which would reveal that they are acting not from
understanding, but only from the disposition of their organs. For
whereas reason is a universal instrument, which can be used in all
kinds of situations, these organs need some particular action; hence
it is for all practical purposes impossible for a machine to have
enough different organs to make it act in all the contingencies of
life in the way in which our reason makes us act. ---
[Source](http://plato.stanford.edu/entries/turing-test/)

## The Turing test is quite strong

All quotes are from Dennett, "Can Machines Think?" (1985)

> Remember, failure on the Turing test does not predict failure on those
others, but success would surely predict success. His test was so
severe, he thought, that nothing that could pass it fair and square
would disappoint us in other quarters. Maybe it wouldn't do everything
we hoped---maybe it wouldn't appreciate ballet, understand quantum
physics, or have a good plan far world peace, but we'd all see that it
was surely one of the intelligent, thinking entities in the
neighborhood.
>
> [...]
>
> Terry Winograd, a leader in AI efforts to produce conversational
ability in a computer, draws our attention to a pair of sentences.
They differ in only one word. The first sentence is this: "The
committee denied the group a parade permit because they advocated
violence." Here's the second sentence: "The committee denied the group
a parade permit because they feared violence."
>
> The difference is just in the verb---"advocated" or "feared." As
Winograd points out, the pronoun "they" in each sentence is officially
ambiguous. Both readings of the pronoun are always legal. Thus, we can
imagine a world in which governmental committees in charge of parade
permits advocate violence in the streets and, for some strange reason,
use this as their pretext for denying a parade permit. But the
natural, reasonable, intelligent reading of the first sentence is that
it's the group that advocated violence, and of the second, that it's
the committee that feared the violence.
>
> Now sentences like this are embedded in a conversation, the computer
must figure out which reading of the pronoun is meant, it is to
respond intelligently. But mere rules of grammar or vocabulary will
not fix the right reading. What fixes the right reading for us is
knowledge about politics, social circumstances, committees and their
attitudes, groups that want to parade, how they tend to behave, and
the like. One must know about the world, in short, to make sense of
such a sentence.
>
> [...]
>
> The only way, it appears, for a computer to disambiguate that
sentence and keep up its end of a conversation that uses that sentence
would be for it to have a much more general ability to respond
intelligently to information about social and political circumstances
and many other topics. Thus, such sentences, by putting a demand on
such abilities, are good quick probes. That is, they test for a wider
competence.

More about "Winograd Schemas" can be found in the paper
"[The Winograd Schema Challenge](http://www.aaai.org/ocs/index.php/KR/KR12/paper/download/4492/4924)"
(PDF) by Levesque, Davis, and Morgenstern (2012).

## Weaker varieties

### Candidate 1

> A computer is intelligent; it wins the World Chess Championship.
>
> That's not a good test, it turns out. Chess prowess has proven to be
an isolatable talent. There are programs today that can play fine
chess but do nothing else. So the quick-probe assumption is false far
the test of playing winning chess.

### Candidate 2

> The computer is intelligent; it solves the Arab-Israeli conflict.
>
> This is surely a more severe test than Turing's. But it has some
defects: passed once, it is unrepeatable; it is slow, no doubt; and it
is not crisply clear what would count as passing it. Here's another
prospect, then:

### Candidate 3

> A computer is intelligent; it succeeds in stealing the British crown
jewels without the use of force or violence.
>
> Now this is better. First, it could be repeated again and again,
though of course each repeat test would presumably be harder, but this
is a feature it shares with the Turing test. Second, the mark of
success is clear: either you've got the jewels to show for your
efforts or you don't. But it is expensive and slow, a socially dubious
caper at best, and no doubt luck would play too great a role.

## Bringsjord's strategies

Selmer Bringsjord, in an article titled
"[If I Were Judge](http://link.springer.com/chapter/10.1007/978-1-4020-6710-5_6),"
in the book
[Parsing the Turing Test](http://link.springer.com/book/10.1007/978-1-4020-6710-5/page/1)
(2009), described some strategies he would take if he believed the
Turing test was valid (which he does not):

### Strategy 1

Require that each contestant pass an array of standardized IQ tests.

### Strategy 2

Give each contestant problems like this one:

> - If there is a king in the hand, then there is an ace, or else if there is not a king in the hand, then there is an ace.
>
> - There is a king in the hand.
>
> - Therefore, what?

The answer is that there is not an ace in the hand. (*I bet you got
that wrong.*)

If the contestant gets the right answer, that probably tells us the
contestant is a human. A computer program, on the other hand, can
easily derive the logically correct answer.

But a very intelligent machine, so intelligent it can appear stupid,
may therefore be able to solve very difficult problems like logical
paradoxes.

### Strategy 3

Give each contestant supposed logical paradoxes, and ask them to solve
the puzzle. Certain paradoxes fool machine reasoning but (very
intelligent) mathematicians can solve them.

### Strategy 4

Finally, if both contestants solve the paradoxes, resort to asking
each contestant to write short stories based on a prompt like, "As
Gregor Samsa awoke one morning from uneasy dreams he found himself
transformed in his bed into a gigantic insect."

![Metamorphosis of Kafka by James LeGros. Acrylic on Watercolor Board.](/images/metamorphosis-of-kafka-james-legros.jpg)

## We have a long way to go

Nobody actually practices with a real Turing test. It's too hard for
the machine. Instead, the yearly
[Loebner Prize](http://www.loebner.net/Prizef/loebner-prize.html)
experiments with a reduced form of this test. The judges simply
estimate how "closely" a computer imitates a human, and judges are not
allowed to attempt trickery (such as typing random symbols) or delve
into deep conversation.

"Computers take the Turing Test in Reading in October 2008 to see if judges believe the machines are human during instant message conversations." ([Source](http://news.bbc.co.uk/2/hi/technology/8249792.stm))

<div style="text-align: center">
<iframe width="480" height="360" src="http://www.youtube.com/embed/e8vZy8a9lSc?rel=0" frameborder="0" allowfullscreen></iframe>
</div>

## The Turing test in culture

Annie Dorsen's [*Hello Hi There*](http://www.anniedorsen.com/showproject.php?id=6) project pairs two chatbots against each other, each trained on text from [Chomsky and Foucault's famous debate](https://www.youtube.com/watch?v=3wfNl2L0Gf8) and the YouTube comments on that video. Each performance is randomize and unique.

<div style="text-align: center">
<iframe width="640" height="360"
src="http://www.youtube.com/embed/3PiwEQQNnBk?rel=0" frameborder="0"
allowfullscreen></iframe>
</div>

<br/>

[Cleverbot](http://www.cleverbot.com/) is one of the better chatbots. A short film was created based on a transcript with Cleverbot.

<div style="text-align: center">
<iframe width="640" height="360" src="http://www.youtube.com/embed/QkNA7sy5M5s?rel=0" frameborder="0" allowfullscreen></iframe>
</div>

<br/>

Consider this test from *Do Androids Dream of Electric Sheep*, which was adapted into the film *Blade Runner*:

> Seated where he could catch the readings on the two gauges of the Voigt-Kampff testing
apparatus, Rick Deckard said, "I'm going to outline a number of social situations. You are to
express your reaction to each as quickly as possible. You will be timed, of course."
>
> "And of course," Rachael said distantly, "my verbal responses won't count. It's solely the
eye-muscle and capillary reaction that you'll use as indices. But I'll answer; I want to go
through this and --- " She broke off. "Go ahead, Mr. Deckard."
>
> Rick, selecting question three, said, "You are given a calfskin wallet on your birthday."
Both gauges immediately registered past the green and onto the red; the needles swung
violently and then subsided.
>
> "I wouldn't accept it," Rachael said. "Also I'd report the person who gave it to me to the
police."
>
> After making a jot of notation Rick continued, turning to the eighth question of the Voigt-
Kampff profile scale. "You have a little boy and he shows you his butterfly collection, including
his killing jar."
>
> "I'd take him to the doctor." Rachael's voice was low but firm. Again the twin gauges
registered, but this time not so far. He made a note of that, too.
>
> "You're sitting watching TV," he continued, "and suddenly you discover a wasp crawling on
your wrist."
>
> Rachael said, "I'd kill it." The gauges, this time, registered almost nothing: only a feeble
and momentary tremor. He noted that and hunted cautiously for the next question.
>
> --- from *Do Androids Dream of Electric Sheep?*, Phillip K. Dick

## Podcasts

### Talking to machines (Radiolab, May 31, 2011)

<div style="text-align: center">
<div class="figure">
<img src="/images/wire_head.jpg" />
</div>
<br/>
<iframe width="474" height="54" frameborder="0" src="http://www.radiolab.org/widgets/ondemand_player/#file=http%3A%2F%2Fwww.radiolab.org%2Faudio%2Fxspf%2F137407%2F;containerClass=radiolab"></iframe>
<br/>
1 hour / <a href="http://www.podtrac.com/pts/redirect.mp3/audio.wnyc.org/radiolab/radiolab053111.mp3">Download</a> / <a href="http://www.radiolab.org/2011/may/31/">Radiolab website for this episode</a> / Image: <a href="http://www.flickr.com/photos/paulmoody/314897848/">Paul Moody</a>
<br/>
</div>

### The Turing Problem (Radiolab, March 19, 2012)

<div style="text-align: center">
<div class="figure">
<img src="/images/turing_sculpture.jpg" />
</div>
<br/>
<iframe width="474" height="54" frameborder="0" src="http://www.radiolab.org/widgets/ondemand_player/#file=http%3A%2F%2Fwww.radiolab.org%2Faudio%2Fxspf%2F193037%2F;containerClass=radiolab"></iframe>
<br/>
23 minutes / <a href="http://www.podtrac.com/pts/redirect.mp3/audio.wnyc.org/radiolab_podcast/radiolab_podcast12turing.mp3">Download</a> / <a href="http://www.radiolab.org/blogs/radiolab-blog/2012/mar/19/turing-problem/">Radiolab website for this episode</a> / Image:
<a href="http://www.flickr.com/photos/ell-r-brown/5118274331/">Elliot Brown</a>
</div>



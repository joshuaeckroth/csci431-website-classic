---
title: Search
layout: note
---

# Search

We can think of AI as having two major approaches: search and pattern recognition. The latter is often called "machine learning." This course is divided into two major parts. The first part focuses on variations of search, while the latter focuses on machine learning.

For much of the history of AI, search was the only effective approach. In fact, it seemed essential to intelligence:

> Problem-solving searches require trial and error in that they
> generally do not go directly to the solution without traversing and
> retracing some blind alleys&#x2014;sometimes many, sometimes few. When a
> person solves a problem without any backtracking whatsoever, we are
> apt to deny that he needed to think at all. We say, "He knew the
> answer," or "he didn't have to think; he did it by rote."
> --- [*Thinking by computers*, Herbert A. Simon](http://digitalcollections.library.cmu.edu/portal/main.jsp?flag=browse&smd=1&awdid=1)

## Why search?

**Why search for the answer if you can just know it instead?**

No matter how an algorithm is coded, it can be reduced to a series of
if-then statements in a loop. The if-then statements can be
represented in a lookup table, where each row in the table is a
different condition. Thus, even a complex search algorithm can be
reduced to a lookup table, assuming one has all the requisite data to
produce such a table.

For example, we could devise a search algorithm that plays good
tic-tac-toe. Or, we can produce a table (with less than 1024 entries)
that describes which move to take depending on the current board
configuration.

Why use a search if we can make a lookup table instead? There are
three reasons: two practical, one intellectual.

### Practical reason 1: space

A lookup table may be too large when fully expanded. A typical chess
game lasts about 40 moves. To represent all possible moves and
counter-moves would require a lookup table with 10<sup>120</sup> entries. This
is, naturally, impossible without some extremely clever encoding
scheme, since the universe is estimated to contain less than 10<sup>81</sup>
atoms.

Using a search algorithm that generates possible moves when requested
avoids this impossible space requirement. This way, the lookup table
is never available in its entirety. Instead, each possible move and
corresponding action are generated as-needed.

### Practical reason 2: unpredictable input

The natural world, unlike chess, does not seem to obey a simple set of
rules. Imagine a robot placed in a random building; the robot has no
way of mapping this building before it arrives there, so it cannot
make a lookup table of all the different movements it can make through
the building.

Also consider a web search engine; there is simply no way to predict
the content and links that webpages will contain as people publish
more and more material. Likewise, there exists an infinite variety of
search queries. Thus, no lookup table relating all possible queries to
ever-changing web pages can be generated.

A lookup table is impossible, yet again. Search is required.

### Intellectual reason: code may have meaning

Lastly, a lookup table tells us nothing about how a problem is
solved. A table that contains all the moves of tic-tac-toe or checkers
or chess gives no insight about how a good game may be played. There
may be reasons certain moves are better than others but the lookup
table does not offer those insights.

A search algorithm, on the other hand, describes intelligent behavior,
assuming the intelligent thing to do is to search. For example, we may
read the Google Search source code and see that a page is ranked more
highly if other highly-ranked pages link to it. The algorithm may not
be appropriate (although Google Search is quite successful, so it
probably is appropriate), but nevertheless the code describes a
certain process that we, as programmers, may find to be meaningful and
possibly intelligent.

## Definition of a search problem

A problem may be solvable by a search technique if the problem has
each of the following features:

- **Initial state:** some description of the agent's starting situation

- **Possible transitions:** the set of actions (such as chess moves) available
  to the agent given the agent's current state, also called "applicable"
actions; the possible transitions depend on the state; in this class, we'll also
attach the state that results from that action in `(action,
resulting-state)` pairs

- **Goal criteria:** some way of finding out if the agent has reached its
  search goal; the function `is_goal(state)` is a boolean function

- **Action cost:** a function that calculates the cost of a particular action
  from a particular state; for example, a driving agent may calculate an action
cost traveling East on I-4 from Orlando for 40 miles to the next waypoint (next
state) be 80 minutes

Of course, each of these components assumes a liberal abstraction away
from most of the details that the agent will be facing in reality. For
example, a driving agent may have a transition model that shows that
driving north on some street results in arriving at the center of
town. Of course, this is a *ceteris paribus* assumption ("everything
else being equal"); if something bad happens, like a flat tire, this
transition model is useless.

## Comparisons of search algorithms

In computer science, we typically compare algorithms based on two
criteria: "time complexity" and "space complexity."

### Time complexity

The time complexity of an algorithm is generally the number of
operations required (e.g., basic CPU operations such as addition,
subtraction, tests for equality, memory reads and writes, etc.).

For example, suppose we have a `min` algorithm that finds the smallest
value in any list. The algorithm checks every element in the list, so
its "time complexity" is $O(n)$ where $O()$ means "on the order of"
and $n$ we'll say is the size of the list. This can also be read
"linear time" because the algorithm requires about $n$ steps (linear),
not $n^2$ steps (quadratic) or $2^n$ steps (exponential). Regardless
how long each step takes, a linear "growth" of the problem (i.e.,
bigger and bigger lists) causes the time to grow linearly.

On the other hand, inefficient sorting algorithms have $O(n^2)$ time
complexity because they compare every element in a list of size $n$
with every other element; this is about $n^2$ comparisons.

### Space complexity

Normally, we can make an algorithm faster by using more memory. We
could, for example, save the answers of some computations to avoid
computing them again. The `min` function has $O(1)$ space complexity
("constant space complexity") because it only uses one or two
variables (the current min, and a pointer to its position in the
list). Some sorting algorithms, on the other hand, have linear
($O(n)$) space complexity because they make a copy of the list as they
sort it.

### Search-specific analysis

For comparing search algorithms in particular, we'll often want to
talk about the following values:

-   $n$, the total number of possible states

-   $b$, the branching factor; this is the maximum number of possible
    actions or branches we might expect from any state in the search
    space.

-   $d$, the depth in the search tree of the least-cost path, i.e., the
    minimum number of steps required to reach the goal

-   $m$, the maximum search depth, if we choose to make it a finite
    number (so that the algorithm might stop looking deeper and instead
    choose to backtrack to an earlier state), or $\infty$ otherwise

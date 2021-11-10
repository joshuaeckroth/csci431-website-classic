---
title: Uninformed search
layout: note
---

# Uninformed search

A search strategy is either "informed" or "uninformed." Uninformed search is a strategy that tries to find a solution without taking into account the cost of each action nor does it prefer to examine more promising actions first. Uninformed search is, therefore, rarely useful, but serves as a good starting point for understanding all the variations of search.

## Overview

We learned in the [Search](../notes/search.html) lecture notes that search
problems have the following components: a starting state, possible
transitions that describes how actions change one
state to another, a goal criteria, and a way of calculating the cost
of each action. We do not use the action cost when executing uninformed search.

The transition model defines a state space, which can be represented
as a directed graph (vertices are states, edges are actions).

For example, consider the 8-puzzle game, which requires that tokens
are shifted around until a particular goal state is reached.

![8-puzzle](../images/8puzzle-simple.png)

Each "state" is a configuration of the puzzle. Each state can be
followed by at most four other states, resulting from moving a
neighboring token left, right, up, or down into the space (thus
shifting the space). If the space is on an edge or in a corner, fewer
than four movements are possible.

## Generic search algorithm

All searches essentially follow the same algorithm:

~~~
1. create an empty list called "closedset"; this list will contain
   states that have been visited

2. create a list called "openset" that contains just the starting
   state; this list contains states that have not been visited but are
   known to exist

3. create an empty map (key/value pairs) called "parents"; this map
   contains the previous state of each state that has been visited

4. while the openset is not empty:

   a. grab a state from the openset (and remove it);
      put it in the closedset (since we're now looking at it)

   b. if that state is the goal, hey we're done!

      i. return a reconstructed path from the goal state to the start
         state (this is easy: recursively grab parent states from the
         "parents" map)

   c. it's not the goal state; for each next state that is accessible
      from here:

       i. if this next state is in the closedset (it has been visited
          before), ignore it

      ii. if this next state is not in the openset, put it in the
          openset and record its parent

   d. (repeat the loop)

5. if the openset is empty and we never found the goal, oops!
~~~

Step `4.a.` is a key step. The "algorithm" above gives no guidance
about how to choose the next state to evaluate. You can imagine that
some choices are better (closer to the goal) than others...

## Random search

A random search, while never practical as far as I know, is
nevertheless interesting to consider as a worst case search. To
program this search, modify step `4.a.` so that a *random* state is
chosen. Given enough time, the goal state should be found, but a
random search will probably take more time (more states are checked)
than any other method.

## Breadth-first search

In breadth-first search (BFS), we want to check all states (which
we'll call "children states") accessible from the previous state (the
"parent state") before we check states accessible from the
children. So if some state is to be checked, say state X, and there
are 15 children of state X, then we will check all of those 15
children before checking any of their children.

Breadth-first search appears to search a tree horizontally before
searching vertically.

To implement BFS, modify step `4.a.` to pick out of the `openset` the
state that was added *earliest* (in time). For example, the children
of a state are checked before the their children, because the children
of the original state are discovered earlier. The `openset` in BFS is
essentially a queue.

Here is an example of BFS operating on the 8-puzzle:

<div style="text-align: center">
<OBJECT CLASSID="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000" 
WIDTH="605" HEIGHT="300" 
CODEBASE="http://active.macromedia.com/flash5/cabs/swflash.cab#version=5,0,0,0">
<PARAM NAME="MOVIE" VALUE="/flash/8puzzle-bfs.swf">
<PARAM NAME="PLAY" VALUE="true">
<PARAM NAME="QUALITY" VALUE="best">
<PARAM NAME="LOOP" VALUE="true">
<EMBED SRC="/flash/8puzzle-bfs.swf" WIDTH="605" HEIGHT="300" PLAY="true" LOOP="true" QUALITY="best" 
PLUGINSPAGE="http://www.macromedia.com/shockwave/download/index.cgi?P1_Prod_Version=ShockwaveFlash"> 
</OBJECT>
<br/>
<a href="../images/8puzzle-bfs.png">View final image</a>
</div>

## Depth-first search

<div style="float: right; width: 145;">
<OBJECT CLASSID="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000" 
WIDTH="145" HEIGHT="800" 
CODEBASE="http://active.macromedia.com/flash5/cabs/swflash.cab#version=5,0,0,0">
<PARAM NAME="MOVIE" VALUE="/flash/8puzzle-dfs.swf">
<PARAM NAME="PLAY" VALUE="true">
<PARAM NAME="QUALITY" VALUE="best">
<PARAM NAME="LOOP" VALUE="true">
<EMBED SRC="/flash/8puzzle-dfs.swf" WIDTH="145" HEIGHT="800" PLAY="true" LOOP="true" QUALITY="best" 
PLUGINSPAGE="http://www.macromedia.com/shockwave/download/index.cgi?P1_Prod_Version=ShockwaveFlash"> 
</OBJECT>
</div>

A trivial change to breadth-first search gives us depth-first search (DFS). For DFS, modify step `4.a.` to pick out of the `openset` the state that was added *last* (in time). So in DFS, the `openset` is essentially a stack. The purpose is to check the a state's first discovered child, and then that child's first child, etc. before checking the original state's second child. DFS appears to search a tree vertically before it searches horizontally.

## Iterative-deepening depth-first search

Depending on the search problem, DFS may go off into
"never-never-land," seemingly never arriving at a goal state, while
say, BFS, arrives at the solution rather quickly. We see this behavior
in the 8-puzzle problem because DFS just keeps trying moves that are
built off prior moves until it either repeats a state (somewhat
unlikely; there are 9! = 362,880 states) or finds the goal. If the
true goal is only five moves away from the starting state, then BFS
will find this goal in less than 1024 checks while DFS may require,
well, 362,880 checks.

To solve the problem of DFS going to "deep" into "never-never-land,"
we can put a limit $m$ on the depth of DFS. Step `4.c.` is modified so
that only states that have depth less than the finite constant $m$ are added to
the `openset`. The depth is calculated as the number of actions or
moves that have been applied to the starting state.

Because it is often difficult to know what the correct depth limit is,
the *iterative-deepening depth-first search* (IDDFS if you like) first
tries DFS with depth limit 1; if no goal state is found, DFS is run
again with depth limit 2; and so on, until the goal state is found.

## Breadth-first versus depth-first search

Breadth-first search is a good choice when you want to evaluate every
possible choice before deciding an action. BFS ensures that the
shortest path to the goal will be found (shortest in terms of number
of moves or number of "hops"), because no shorter path is left
unchecked. However, BFS suffers when, at each state, there is an
enormous number of choices to consider (a high branching factor
$b$).

On the other hand, depth-first search might be better if the solution
is very "deep," such as in mazes.

## Comparison of uninformed search algorithms

Refer to the [search notes](../notes/search.html) (at the bottom) for an
explanation of the variables $n$ (total possible states), $b$
(branch factor), and $d$ (search depth of least-cost solution).


| Metric | Random | Breadth-first | Depth-first | IDDFS |
|--------+---------------+---------------------+-------------------|
| Complete?<br/>(always finds the goal) | Yes        | Yes  | Yes | Yes |
| Optimal?<br/>(always finds shortest path to goal,<br/>when action costs are all equal) | No | Yes       | No   | Yes |
| Time complexity | $O(n)$ | $O(b^d)$ | $O(n)$ | $O(b^d)$ |
| Space complexity | $O(n)$ | $O(b^d)$ | $O(n)$ | $O(b^d)$ |

Some explanation:

- Random: time complexity is $O(n)$ because might need to check up to all nodes to find the goal; space complexity is $O(n)$ because might need to store up to every node in the openset.
- Breadth-first: time complexity is $O(b^d)$ because every node at every level is checked before finding the goal at depth $d$; space complexity is $O(b^d)$ because up to all nodes in the fringe up to level $d$ need to be stored in the openset.
- Depth-first: time complexity is $O(n)$ because might need to check up to every node (like in 8-puzzle if the it starts searching states further and further from the goal); space complexity is $O(n)$ for the same reason; if there is a search depth limit of $m$, then space complexity would be $O(bm)$.
- IDDFS: space and time complexity are, worst case, the same as breadth-first search because with a given depth limit $m$, if IDDFS doesn't find the goal, it eventually searches every node up to depth $m$.



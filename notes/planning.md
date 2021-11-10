---
title: Planning
layout: note
---

# Planning

Planning is another search problem, but it is slightly different than
8-puzzle, path-finding, etc. We use planning rather than simple search when the domain is very large and there are too many states to search with one of the search strategies we've learned previously.

Instead, a planner searches across partial state descriptions. We describe planning problems in a new language, PDDL, rather than an explicit function of possible transitions.

## Motivation

In a planning problem, we typically do not completely describe a state. Rather, we give just partial
descriptions, like `on(monkey, floor), at(monkey, 5, 2)`. There might
be lots of other things in the room besides the monkey, even things relevant to our planning problem, but we don't
want to describe all those other facts for every possible state transition. Breadth-first search,
depth-first search, A\*, etc. would have trouble with these kinds of
states because they are incomplete.

But we can handle these incomplete states by treating them as a planning
problem. The way the planning algorithm works, and the way we describe
planning problems, is slightly different because we want to know how
different actions *add* or *remove* facts from the state; the action does
not describe all the facts of the state that will result.

Here is an example to illustrate the problem BFS/DFS/A\* would face. Suppose we
have 10 airports, 50 planes, and 200 pieces of cargo. All the cargo is at SFO
and needs to be at JFK. Planes are assumed to have infinite capacity. There are
three actions: load cargo, unload cargo, and fly the plane from one airport to
another. Suppose each of the 50 planes can fly to 9 other airports, and that
each of the 200 packages can be loaded on any plane. Then we have
9\*50\*50\*200 possible actions at the start; that's 4.5 million possible
actions, just for the first move.

## Types of planning problems

We will only focus on "classical" planning, although more sophisticated planning problems exist and remain active research.

- Classical: each state is "atomic", like a single node in a graph; the outcome of every action is known; each action takes a single unit of time to complete.
- Temporal: like classical except actions take variable time to complete, so multiple actions may be performed simultaneously; deadlines may be involved.
- Partially-observable: states cannot be fully observed, instead there is a probability of a state having certain properties; effects of actions are not fully known.

## Definition of a classical planning problem

Like the definition of a search problem, a classical planning problem is made up of an initial state, possible actions, and goal criteria. However, unlike the search problems we examined earlier, states in a planning problem are not fully described. Rather, conjunctions of "predicates" like `at(monkey, 5, 2)` or negated predicates like `not(at(monkey, 5, 2))` are used instead to describe a state. When a predicate involves no variables, it is called a "literal."

-   **Initial state:** a conjunction of positive "literals" (no variables), e.g.,
    `on(monkey, floor), at(monkey, 5, 2), at(box, 3,
                       0), on(bananas, box)`

-   **Actions:** a set of possible actions to take. Each action has an action
    name, **relevant variables**, **preconditions**, and **effects**. Think of
an action like a function with arguments. The preconditions say under what
conditions the action is valid; they can refer to the arguments. The effects
say what the result of the action is; they can also refer to the arguments, and
can include positive and negative effects, sometimes separated as "add" effects
and "delete" effects. For example, the `move` action might involve variables
`thing`, `from`, and `to`, have precondition `at(thing, from)` and
postcondition or effect `not(at(thing, from)), at(thing, to)`.

-   **Goal criteria:** another conjunction of literals. Both positive and
    negative literals are allowed. E.g., `on(monkey, box),
                    not(on(bananas, box))`.

{% comment %}
### Typical assumptions

-   Atomic time: Each action is indivisible

-   No concurrent actions are allowed (though actions do not need to be
    ordered with respect to each other in the plan)

-   Deterministic actions: The result of actions are completely
    determined—there is no uncertainty in their effects

-   Agent is the sole cause of change in the world

-   Agent is omniscient: Has complete knowledge of the state of the
    world

-   Closed World Assumption: everything known to be true in the world is
    included in the state description. Anything not listed is false.

(From: <http://people.cs.pitt.edu/~litman/courses/cs2710/lectures/ch10RNa.pdf>)

### Limitations of classical planning

Classical planning considers what to do in what order, but
not any of the following:

- When actions happen and how long they take.
- Limited resources that actions may need.
- Semi-observable environments.
- Dynamic environments.
- Uncertain environments.
- Stochastic (partially random) environments.

## Generic planning algorithm

Forward search, like breadth-first or depth-first search, would try
any action that met the preconditions, and see what
resulted. Eventually, it would find a state that met the goal
criteria. This is a bit slow, however, since BFS and DFS are not
considering **relevant** actions.

It is better to work backwards from the goal. Find out first which
action would put you in the goal state, then figure out which action
is required to meet its preconditions. Go backwards like this until
the preconditions for some action are already met by the starting
state.

Suppose you want to find actions relevant to the state \(g\). Then a
relevant action is one where some of the effects of the action are
elements of \(g\). For example, suppose we want `on(monkey, box)` and
some action like `climb(X, Y)` has as the effect we are looking for if
`X=monkey` and `Y=box`. Then this action would be relevant. We would
look at its preconditions, and meeting those would be the new
goal. Thus, we build the plan backwards, so the final plan needs to be
reversed before we can actually follow it in the real world. (Note, we
also have to be careful that no part of the effects of an action
cancel out some part of our goal.)

    function find-plan(state, goal):
    
      # goal not found
      if(initial-state does not meet goal):
    
        relevant-actions <- Find actions that include part
                            of the goal in their effects
    
        foreach(relevant-action):
    
          if(state meets preconditions-of-action):
    
            # our plan is simply this action itself
            return action
    
          else:
    
            # try to find a plan to achieve this action's preconditions
            partial-plan <- find-plan(state, preconditions-of-action)
    
            if(partial-plan is found):
    
              # we can achieve this action's preconditions; so the new plan
              # is the partial-plan plus this action itself
              return (action + partial-plan)
    
      # no action was relevant or its preconditions could not be met,
      # or we are already at the goal, so return no-plan
      return no-plan

## A philosophical issue: The frame problem

Our actions indicate what effects the actions have, e.g., the "climb"
action in which the monkey climbs on the box results in the monkey
being on the box. But our actions normally do not state all the facts
of the world that don't change. But then how can be sure what exactly
changed and what didn't? Did the box move as the monkey tried to climb
it? How can we be sure? And if we wanted to, how could we list all the
things that do and don't change? This might not matter in a toy
problem, but in the real world it matters a lot.

> The analogy of the stage magician is particularly apt. One is not
> likely to make much progress in figuring out *how* the tricks are done
> by simply sitting attentively in the audience and watching like a
> hawk. Too much is going on out of sight. Better to face the fact that
> one must either rummage around backstage or in the wings, hoping to
> disrupt the performance in telling ways; or, from one's armchair,
> think aphoristically about how the tricks *must* be done, given
> whatever is manifest about the constraints. The frame problem is then
> rather like the unsettling but familiar 'discovery' that so far as
> armchair thought can determine, a certain trick we have just observed
> is flat impossible.
> &#x2014; ["Cognitive Wheels: The frame problem of AI," Daniel C. Dennett](http://web.fc.uaem.mx:8080/~bruno/material/dennet_93_cognitiveWheels.pdf)

> The frame problem is not the problem of induction in disguise. For
> suppose the problem of induction were solved. Suppose&#x2014;perhaps
> miraculously&#x2014;that our agent has solved all its induction problems or
> had them solved by fiat; it believes, then, all the right
> generalizations from its evidence, and associates with all of them the
> appropriate probabilities and conditional probabilities. This agent,
> *ex hypothesi*, believes just what it ought to believe about all
> empirical matters in its ken, including the probabilities of future
> events. It might still have a bad case of the frame problem, for that
> problem concerns how to represent (so it can be *used*) all that
> hard-won empirical information&#x2014;a problem that arises independently of
> the truth value, probability, warranted assertability, or subjective
> certainty of any of it. Even if you have excellent *knowledge* (and
> not mere belief) about the changing world, how can this knowledge be
> represented so that it can be efficaciously brought to bear?
> &#x2014; ["Cognitive Wheels: The frame problem of AI," Daniel C. Dennett](http://web.fc.uaem.mx:8080/~bruno/material/dennet_93_cognitiveWheels.pdf)

{% endcomment %}


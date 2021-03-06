---
title: Prolog unification
layout: note
---

# Prolog unification

When programming in Prolog, we spend a lot of time thinking about how
variables and rules "match" or "are assigned." There are actually two
aspects to this. The first, "unification," regards how terms are
matched and variables assigned to make terms match. The second,
"resolution," is described in
[separate notes](/notes/prolog-resolution.html). Resolution is only
used if rules are involved. You may notice in these notes that no
rules are involved since we are only talking about unification.

## Prolog 'Terms'

Prolog has three kinds of *terms*:

1. Constants like `42` (numbers) and `franklin` (atoms, i.e.,
   lower-case words).

2. Variables like `X` and `Person` (words that start with upper-case).

3. Complex terms like `parent(franklin, bo)` and `baz(X, quux(Y))`.

Two terms *unify* if they can be matched. Two terms can be matched if:

- they are the same term (obviously), or

- they contain variables that can be uniformly instantiated so that the two
  terms without variables are the same. "Uniformly" instantiated means that
each distinct variable gets the same value, e.g., all `X` variables in the term
get the same value.

For example, suppose our knowledge base is:

~~~ prolog
woman(mia).
loves(vincent, angela).
loves(franklin, mia).
~~~

- `mia` and `mia` unify because they are the same.

- `mia` and `X` unify because `X` can be given the value `mia` so
  that the two terms (without variables) are the same.

- `woman(mia)` and `woman(X)` unify because `X` can be set to `mia`
  which results in identical terms.

- `loves(X, mia)` and `loves(vincent, X)` *cannot* unify because
  there is no assignment for `X` (given our knowledge base) that
  makes the two terms identical.

- `loves(X, mia)` and `loves(franklin, X)` also cannot unify (can
  you see why?).

We saw in the [Prolog](/notes/prolog.html) notes that we can "query"
the knowledge base and get, say, all the people who love `mia`. When
we query with `loves(X, mia).` we are asking Prolog to give us all the
values for `X` that unify. These values are, essentially, the people
who love `mia`.

## A more formal definition

`term1` and `term2` unify whenever:

1. If `term1` and `term2` are *constants*, then `term1` and `term2`
   unify if and only if they are the same atom, or the same number.

2. If `term1` is a *variable* and `term2` is any type of term, then
   `term1` and `term2` unify, and `term1` is instantiated to
   `term2`. (And vice versa.) (If they are both variables, they're
   both instantiated to each other, and we say that they share
   values.)

3. If `term1` and `term2` are *complex terms*, they unify if and only
   if:

   a. They have the same *functor* and *arity*. The functor is the
      "function" name (this functor is `foo`: `foo(X, bar)`). The
      arity is the number of arguments for the functor (the arity for
      `foo(X, bar)` is 2).

   b. All of their corresponding arguments unify. *Recursion!*

   c. The variable instantiations are compatible (i.e., the same
      variable is not given two different unifications/values).

4. Two terms unify if and only if they unify for one of the above
   three reasons (there are no reasons left unstated).

## Practice

We'll use the `=` predicate to test if two terms unify. Prolog will
answer "Yes" if they do, as well as any sufficient variable
assignments to make the unification work.

*Do these two terms unify?*

~~~ prolog
?- mia = mia.
~~~

Yes, from rule 1.

*Do these two terms unify?*

~~~ prolog
?- mia = X.
~~~

Yes, from rule 2.

*Do these two terms unify?*

~~~ prolog
?- X = Y.
~~~

Yes, from rule 2.

*Do these two terms unify?*

~~~ prolog
?- k(s(g), Y) = k(X, t(k)).
~~~

Yes, from rule 3 and, in the recursion, from rule 2 in two cases (`X`
set to `s(g)` and `Y` set to `t(k)`).

*Do these two terms unify?*

~~~ prolog
?- k(s(g), Y) = k(s(g, X), Y).
~~~

No, because rule 3 fails in the recursion (in which rule 3 is invoked
again, and the arity of `s(g)` does not match `s(g, X)`).


Much of these notes were adapted from
[Learn Prolog Now!](http://www.learnprolognow.org), a free online
textbook.

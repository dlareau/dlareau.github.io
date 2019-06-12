---
layout: blogpost
title: "Adventures into pizza math"
category: pizza_math
mathjax: true
published: false
---

{% include mathjax.html %}

A tale of a simple pizza wish that falls down a math and optimization rabbit
hole.

#### The Application ####

Don't worry, we'll get to the math soon enough, just have to give some
background first.

All of this started in late August of 2018 after helping one of my friends move
into his new house. My friends and I all help each other out whenever one of us
has to move, usually with the promise of the person moving ordering pizza for
everyone at the end. I'm unfortunately personally against some of the group's
more popular toppings of mushrooms, pineapple, and pepperoni. This usually means
that I either have to have an active voice in the pizza ordering or risk picking
stuff off of a pizza even when we get like 3 different pies. On this particular
day, I was still moving stuff when the order was called in, meaning that I was
greeted with 3 pies where my best option was to pick mushrooms off of one. It
was at that point that I decided something needed to be done.

That afternoon I went home and immediately started writing the "Pizza Solver".
The goal was simple: Take in everyone's preferences and the number of pizzas
desired and output the ideal groupings of people to maximize topping overlap.
After a bit of infrastructure work to get it hosted on my personal server and
register it under a cute domain ending in .pizza it was up and working!

{% include image.html url="/assets/images/blog/pizza_homepage.png"
description="The homepage, clean and simple." %}

{% include image.html url="/assets/images/blog/pizza_spreadsheet.png"
description="The preference input page, a Google sheet." %}

The interface was as simple as the concept. Users would first go to a shared
Google sheet, fill out what they liked (1), didn't care about (0), disliked
(-1), hated (-2), and were allergic to (-3). Users would then go to the
homepage, select by clicking all of the people at the event, the number of
pizzas desired and after hitting "Generate Pizzas" would get a page like this:

{% include image.html url="/assets/images/blog/pizza_output.png"
description="The output" %}

Here you can see that it groups people into pizzas, and shows all the toppings
that everyone likes along with a score for each topping showing exactly how
"liked" it is. It doesn't dictate the pizza each group has to order, but
instead just shows all toppings of shared interest and the people can decide
for themselves what subset of them to get. In this example image, Eric, Jose, and
Peter would all be very happy getting a Pizza with onions, sun dried tomatoes,
and spinach.

Within a few short days I already had a few improvements over the original:
- Reduced clutter by not showing toppings everyone is neutral about
- Changed which set of groups was the "best" by maximizing the minimum of the
group scores rather than the sum of the scores. (Because one group with a great
pizza shouldn't offset another group having a bad pizza)

Those improvements stood unchallenged for almost a year. The website even came
in use a few times during that year as small events needed pizza. But there was
a monster of an implementation detail lurking under the surface waiting till
the next time we helped someone move to rear its head.

#### The Math ####

Lets take a step back and look at some of the math behind the impending issue.
In order to present the best possible grouping, we must first find and score all
possible groupings. Putting scoring aside for a moment, first we have to
generate every possible group. There are a number of ways to go about this, and
I'll present the ones I iterated through in the order I thought of them.

##### The Problem Statement#####

Generate all possible groupings of **n** people into **k** groups where the
groups are as evenly sized as possible. (We don't care about wildly uneven
groups because when ordering pizza you don't split into groups like 6 people, 1
person and 1 person)

###### Solution #1 ######

The simplest way to ensure you have all possible groups is to just take every
possible permutation of the **n** people and then split each permutation into
groups after the fact. For example, 6 people into 3 groups would first become
```
A,B,C,D,E,F
B,A,C,D,E,F
C,A,B,D,E,F
A,C,B,D,E,F
B,C,A,D,E,F
C,B,A,D,E,F
C,B,D,A,E,F
...
```
and then become
```
(A,B) (C,D) (E,F)
(B,A) (C,D) (E,F)
(C,A) (B,D) (E,F)
(A,C) (B,D) (E,F)
(B,C) (A,D) (E,F)
(C,B) (A,D) (E,F)
(C,B) (D,A) (E,F)
...
```
This solution technically works, but as you can even see form this relatively
small example that it generates a bunch of useless duplicate groups. For our
purposes we don't need both

```(A,B) (C,D) (E,F)``` and ```(B,A) (C,D) (E,F)```. (Lines 1 and 2 above)

Just one of them will suffice, which brings us to our second solution.

###### Solution #2 ######

Because we don't care about ordering, we should instead be looking at
combinations instead of permutations. A different way to look at the problem is
to instead select the groups group by group. To do this for 6 people into 3
groups we'd first get every way to choose 2 of the 6 people.

```
(A,B)
(A,C)
(A,D)
(A,E)
(A,F)
(B,C)
(B,D)
...
```

That becomes our first group. For each group in the first set we then apply the
same logic to the remaining letters. So for the group ```(A,B)``` we have
```C,D,E,F``` left over. We again get every way to get choose 2 of the now 4
people and add that group to ```(A,B)```. Again we get something like:

```
(A,B) (C,D)
(A,B) (C,E)
(A,B) (C,F)
(A,B) (D,E)
(A,B) (D,F)
(A,B) (E,F)
```

Finally we do it one last time, this time though it is easy, because we are
choosing 2 people out of a remaining 2 people for each grouping so far there is
only one option. So the above groupings respectively turn into:

```
(A,B) (C,D) (E,F)
(A,B) (C,E) (D,F)
(A,B) (C,F) (D,E)
(A,B) (D,E) (C,F)
(A,B) (D,F) (C,E)
(A,B) (E,F) (C,D)
```

Once we do this for every group that we started with back in step one we have
our list, now with no more confusions between ```(A,B)``` and ```(B,A)```. We
still have a problem though and that is that we are still getting duplicates
in the form of

```(A,B) (C,D) (E,F)``` vs ```(A,B) (E,F) (C,D)```. (Lines 1 and 6 above)

I didn't notice this back when I first wrote it and so as far as I was concerned
this solution was optimal and got left alone for a year.

#### That Lurking Problem ####

So that problem I mentioned earlier... The logic in the program when it was
first written was to generate all of the groups and then go through and score
them, keeping track of the best group as we go and then displaying it at the
end. Some of you reading might have already noticed the problem, but for those
who haven't yet, lets take a look at the numbers behind the two solutions we've
looked at so far.

###### Solution #1's Size ######

The first solution was basically just generating permutations and then grouping
them. There exists $$n!$$ (spoken as "n factorial") ways to permute a set of
**n** elements, and we would have been looking at all of them. Factorials get
big fast, for example $$10! = 3{,}628{,}800$$.

Thankfully I never implemented solution #1, so how about solution #2?

###### Solution #2's Size ######

Solution 2 is a bit more complex but still not too bad. We were just choosing
**g** elements (the number of people in a group, also known as $$\frac{n}{k}$$)
repeatedly until we had nothing left. So we start with $${n \choose
g}$$ (spoken as "n choose g"). Then for each of those we have another $${n-g
\choose g}$$ possibilities this goes on until we have no more elements, so we
can define the number of groupings $$P(n,k)$$ as:

$$ P(n,k) = {n \choose g} * {n-g \choose g} * ... * {g \choose g} $$

Expanding this out using the following formula for combinations

$$ {a \choose b} = \frac{a!}{b!(a-b)!} $$

we get:

$$
\require{enclose}
\begin{eqnarray}
P(n,k) &=& \frac{n!}{g!(n-g)!} * \frac{n-g!}{g!(n-g-g)!} * \frac{n-2g!}{g!
(n-2g-g)!} * ... * \frac{2g!}{2g!(2g-g)!} * \frac{g!}{g!(g-g)!} \nonumber \\
  	   &=& \frac{n!}{g!(n-g)!} * \frac{(n-g)!}{g!(n-2g)!} * \frac{(n-2g)!}{g!
(n-3g)!} * ... * \frac{2g!}{g!(g)!} * \frac{g!}{g!} \nonumber \\
       &=& \frac{n!}{g!\enclose{horizontalstrike}{(n-g)!}} *
       \frac{ \enclose{horizontalstrike}{(n-g)!}}{g! \enclose{horizontalstrike}{(n-2g)!}} *
       \frac{ \enclose{horizontalstrike} {(n-2g)!}}{g! \enclose{horizontalstrike} {(n-3g)!}} *
       ... * \frac{\enclose{horizontalstrike} {2g!}}{g!\enclose{horizontalstrike} {(g)!}} *
       \frac{\enclose{horizontalstrike} {g!}}{g!} \nonumber \\
       &=& \frac{n!}{(g!)^{\frac{n}{g}}} \nonumber \\
 	   &=& \frac{n!}{(\frac{n}{k}!)^k}
\end{eqnarray}

$$

It isn't the prettiest result in the world, but it is immediately clear that
we're doing better than the base $$n!$$ we got from solution 1. In fact, for 10
people in 2 groups, there are only 252 possible groupings according to this
result, much better than 3.6 million!

###### Very Large Numbers ######

There is still a problem though, because we have duplicates with regards to the
ordering of the groups that means that for **k** groups we will have $$k!$$
duplicates of each grouping. This isn't really a problem for a small gathering
where we're ordering two or 3 pizzas, but when everybody gets together to help
a friend move and we're ordering 5 or 6 pizzas it means that each grouping has
720 duplicates. Using the above formula, 18 people into 6 groups gets you
$$ P(18,6) = 137{,}225{,}088{,}000 $$.

One Hundred and Thirty Seven BILLION.

Combine that with the fact that the program was written in python and the
scoring function wasn't perfectly optimized means that there was no way a
request for 18 people and 6 pizzas was ever going to give a solution that day.

#### Fixing It ####

So a number of fixes were implemented immediately to make scoring the groupings
faster:
- Generate common sets such as which toppings a person is okay with once for
each person at the start and not each time.
- Use Numpy to multiply and sum the arrays representing people's scores
- Use memoization to ensure that the score for each group of people is only
computed once.

With those in place, the program is able to score more than 100,000 pizzas per
second, but that still won't allow us to compute all 137 Billion of P(18,6).

###### Solution #3 ######
Which brings us to solution #3. The problem with solution #2 was that it had
duplicates with regards to the ordering of the groups. To fix that we just have
to specify and enforce an ordering of the groups.






\-Dillon
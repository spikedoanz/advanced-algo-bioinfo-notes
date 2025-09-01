> HW1: Estimate the expected number of times you need to toss a unbiased coin
> in order to observe two heads in a row using  a formula  (x = f(x)) explained
> in class.

i used chatgpt to figure out what problem this was. it informed me that
this was an instance of https://en.wikipedia.org/wiki/Absorbing_Markov_chain.

i then used this material on wikipedia as a guide on how to tackle this issue.

--------------------------------------------------------------------------------

Let x be the number of tosses required to see two heads in a row, or HH.
Let p be the probability of seeing a head in a given toss. Vice versa for q.
Since this is an unbiased coin, we know that p == q == 0.5.

Absorbing markov chain problems can be solved by defining a set of recursive
formulas conditioned on 'themselves'. In the case of HH, we can define these
recursive relationships by looking at **what happens with the first toss**:

1. H -> We've made progress! Now we need one more H
2. T -> No progress, we need to start over

Let's define:
- x = E[tosses to get HH starting from nothing]
- y = E[tosses to get HH starting from one H]

**From the starting state (no progress):**
- If we toss H (probability p): we use 1 toss and move to state "one H"
- If we toss T (probability q): we use 1 toss and stay at "no progress"

Therefore: x = 1 + p*y + q*x

**From the "one H" state:**
- If we toss H (probability p): we're done! Used 1 toss total from this state
- If we toss T (probability q): we use 1 toss and go back to "no progress"

Therefore: y = 1 + p*0 + q*x = 1 + q*x

**Solving the system:**
Substituting y = 1 + qx into the first equation:
x = 1 + p(1 + qx) + qx
x = 1 + p + pqx + qx
x = 1 + p + x(pq + q)
x - x(pq + q) = 1 + p
x(1 - pq - q) = 1 + p

Subbing in p == q == 0.5:
x(1 - 0.25 - 0.5) = 1 + 0.5
x(0.25) = 1.5
x = 6

Therefore, we should expect 6 tosses before we see two heads in a row.

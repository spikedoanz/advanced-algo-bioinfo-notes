> 13. Consider the following tree topology T. The value on the edge is the
>     mutation probability p. Can you compute Pr(a = 10, b = 01, c = 11|T, p)?
>       r
>      / \
>   0.2   0.3
>    /     \
>  a=10     u
>          / \
>       0.2   0.1
>        /     \
>     b=01    c=11
>
> 1. What is the maximum agreement subtree for T1 and T2? Is the maximum
>    agreement subtree unique?
> tree T1
>          root
>         /    \
>        /      \
>       /        \
>      /\        /\
>     /  \      /  \
>    1   /\    4    5
>       /  \
>      3    2
>
> tree T2
>          root
>         /    \
>        /      \
>       /        \
>      /\        /\
>     /  \      /  \
>    5   /\    4    2
>       /  \
>      1    3

================================================================================

13.

each node has 4 possible states: 00, 01, 10, 11

the probability calculation is as follows:

Pr(a = 10, b = 01, c = 11|T, p) 
= ∑_r ∑_u (Pr(r) * Pr(a=10|r, 0.2) * Pr(u|r, 0.3) * Pr(b=01|u, 0.2) * Pr(c=11|u, 0.1)

we consider all states for u first :

given u = 00 : 
    Pr(b=01|u=00, 0.2) = 0.8 * 0.2 = 0.16
    Pr(c=11|u=00, 0.1) = 0.1 * 0.1 = 0.01
given u = 01 :
    Pr(b=01|u=01, 0.2) = 0.8 * 0.8 = 0.64
    Pr(c=11|u=01, 0.1) = 0.1 * 0.9 = 0.09
given u = 10 :
    Pr(b=01|u=10, 0.2) = 0.2 * 0.2 = 0.04
    Pr(c=11|u=10, 0.1) = 0.9 * 0.1 = 0.09
given u = 11 :
    Pr(b=01|u=11, 0.2) = 0.2 * 0.8 = 0.16
    Pr(c=11|u=11, 0.1) = 0.9 * 0.9 = 0.81


we consider the likelihood of each state of u :
    L(u=00) = 0.16 * 0.01 = 0.0016
    L(u=01) = 0.64 * 0.09 = 0.0576
    L(u=10) = 0.04 * 0.09 = 0.0036
    L(u=11) = 0.16 * 0.81 = 0.1296

we now consider all states of r :

given r = 00 :
    Pr(a=10|r=00, 0.2) = 0.2 * 0.8 = 0.16
    
    Pr(u=00|r=00, 0.3) = 0.7 * 0.7 = 0.49
    Pr(u=01|r=00, 0.3) = 0.7 * 0.3 = 0.21
    Pr(u=10|r=00, 0.3) = 0.3 * 0.7 = 0.21
    Pr(u=11|r=00, 0.3) = 0.3 * 0.3 = 0.09
    
    L(r=00) = 0.16 * (0.49*0.0016 + 0.21*0.0576 + 0.21*0.0036 + 0.09*0.1296)
            = 0.16 * (0.000784 + 0.012096 + 0.000756 + 0.011664)
            = 0.16 * 0.0253
            = 0.004048

given r = 01 :
    Pr(a=10|r=01, 0.2) = 0.2 * 0.2 = 0.04

    Pr(u=00|r=01, 0.3) = 0.7 * 0.3 = 0.21
    Pr(u=01|r=01, 0.3) = 0.7 * 0.7 = 0.49
    Pr(u=10|r=01, 0.3) = 0.3 * 0.3 = 0.09
    Pr(u=11|r=01, 0.3) = 0.3 * 0.7 = 0.21
    
    L(r=01) = 0.04 * (0.21*0.0016 + 0.49*0.0576 + 0.09*0.0036 + 0.21*0.1296)
            = 0.04 * (0.000336 + 0.028224 + 0.000324 + 0.027216)
            = 0.04 * 0.0561
            = 0.002244

given r = 10 :
    Pr(a=10|r=10, 0.2) = 0.8 * 0.8 = 0.64

    Pr(u=00|r=10, 0.3) = 0.3 * 0.7 = 0.21
    Pr(u=01|r=10, 0.3) = 0.3 * 0.3 = 0.09
    Pr(u=10|r=10, 0.3) = 0.7 * 0.7 = 0.49
    Pr(u=11|r=10, 0.3) = 0.7 * 0.3 = 0.21
    
    L(r=10) = 0.64 * (0.21*0.0016 + 0.09*0.0576 + 0.49*0.0036 + 0.21*0.1296)
            = 0.64 * (0.000336 + 0.005184 + 0.001764 + 0.027216)
            = 0.64 * 0.0345
            = 0.02208

given r = 11 :
    Pr(a=10|r=11, 0.2) = 0.8 * 0.2 = 0.16
    Pr(u=00|r=11, 0.3) = 0.3 * 0.3 = 0.09
    Pr(u=01|r=11, 0.3) = 0.3 * 0.7 = 0.21
    Pr(u=10|r=11, 0.3) = 0.7 * 0.3 = 0.21
    Pr(u=11|r=11, 0.3) = 0.7 * 0.7 = 0.49
    
    L(r=11) = 0.16 * (0.09*0.0016 + 0.21*0.0576 + 0.21*0.0036 + 0.49*0.1296)
            = 0.16 * (0.000144 + 0.012096 + 0.000756 + 0.063504)
            = 0.16 * 0.0765
            = 0.01224

final calculation (assuming uniform prior Pr(r) = 1/4 for all r):
Pr(a=10, b=01, c=11|T, p) = (1/4) * (L(r=00) + L(r=01) + L(r=10) + L(r=11))
                          = (1/4) * (0.004048 + 0.002244 + 0.02208 + 0.01224)
                          = (1/4) * 0.040612
                          = 0.010153

therefore, Pr(a=10, b=01, c=11|T, p) = 0.010153 or about 1.0153%.

================================================================================

1. 

we need to find the maximum agreement subtree (mast) for trees t1 and t2.

first, let's identify the leaf relationships in each tree:

tree t1 structure:
- leaves: {1, 2, 3, 4, 5}
- 1 is alone under left child of left subtree
- 2 and 3 are siblings under left child of left subtree
- 4 and 5 are siblings under right subtree

tree t2 structure:
- leaves: {1, 2, 3, 4, 5}
- 5 is alone under left child of left subtree  
- 1 and 3 are siblings under left child of left subtree
- 4 and 2 are siblings under right subtree

now we check pairwise relationships for conflicts:

checking pair (1,3):
- in t1: 1 and 3 are cousins (different parents in left subtree)
- in t2: 1 and 3 are siblings (same parent)
- conflict detected - cannot both be in mast

checking pair (2,3):
- in t1: 2 and 3 are siblings (same parent)
- in t2: 3 is in left subtree, 2 is in right subtree
- conflict detected - cannot both be in mast

checking pair (4,5):
- in t1: 4 and 5 are siblings (same parent in right subtree)
- in t2: 4 is in right subtree, 5 is in left subtree
- conflict detected - cannot both be in mast

checking pair (2,4):
- in t1: 2 is in left subtree, 4 is in right subtree
- in t2: 2 and 4 are siblings in right subtree
- conflict detected - cannot both be in mast

now checking valid pairs:

checking pair (1,4):
- in t1: 1 is in left subtree, 4 is in right subtree
- in t2: 1 is in left subtree, 4 is in right subtree
- no conflict - valid agreement subtree

checking pair (1,5):
- in t1: 1 is in left subtree, 5 is in right subtree
- in t2: 1 is in left subtree, 5 is in left subtree (but different branches)
- relationships preserved - valid agreement subtree

checking pair (2,5):
- in t1: 2 is in left subtree, 5 is in right subtree  
- in t2: 2 is in right subtree, 5 is in left subtree
- relationships preserved - valid agreement subtree

checking pair (3,4):
- in t1: 3 is in left subtree, 4 is in right subtree
- in t2: 3 is in left subtree, 4 is in right subtree
- no conflict - valid agreement subtree

checking pair (3,5):
- in t1: 3 is in left subtree, 5 is in right subtree
- in t2: 3 is in left subtree, 5 is in left subtree (but different branches)
- relationships preserved - valid agreement subtree

attempting larger subsets (size 3):
given the conflicts identified above, any subset of size 3 or larger will
contain at least one conflicting pair.

final answer:
the maximum agreement subtree has 2 leaves.
the maximum agreement subtree is not unique.
valid masts include: {1,4}, {1,5}, {2,5}, {3,4}, {3,5}

therefore, the mast has size 2 and there are multiple distinct masts of this
maximum size.

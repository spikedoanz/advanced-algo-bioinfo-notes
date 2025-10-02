> 2. Can you solve the large compatibility problem, that is, find the
>    largest set of characters which admit the perfect phylogeny? Can
>    you check if the following matrix has a perfect phylogeny? If
>    yes, can you report the corresponding tree?
> 
> | M  | C1 | C2 | C3 | C4 |
> |----|----|----|----|----|
> | S1 | 0  | 0  | 0  | 1  |
> | S2 | 1  | 1  | 0  | 0  |
> | S3 | 0  | 0  | 0  | 1  |
> | S4 | 0  | 1  | 1  | 0  |
> | S5 | 0  | 1  | 1  | 1  |
--------------------------------------------------------------------------------

we first check all pairs of characters:

# c1 vs c2:
- s1: (0,0)
- s2: (1,1)
- s3: (0,0)
- s4: (0,1)
- s5: (0,1)
- combinations present: (0,0), (1,1), (0,1) - compatible

# c1 vs c3:
- s1: (0,0)
- s2: (1,0)
- s3: (0,0)
- s4: (0,1)
- s5: (0,1)
- combinations present: (0,0), (1,0), (0,1) - compatible

# c1 vs c4:
- s1: (0,1)
- s2: (1,0)
- s3: (0,1)
- s4: (0,0)
- s5: (0,1)
- combinations present: (0,1), (1,0), (0,0) - compatible

# c2 vs c3:
- s1: (0,0)
- s2: (1,0)
- s3: (0,0)
- s4: (1,1)
- s5: (1,1)
- combinations present: (0,0), (1,0), (1,1) - compatible

# c2 vs c4:
- s1: (0,1)
- s2: (1,0)
- s3: (0,1)
- s4: (1,0)
- s5: (1,1)
- combinations present: (0,1), (1,0), (1,1) - compatible

# c3 vs c4:
- s1: (0,1)
- s2: (0,0)
- s3: (0,1)
- s4: (1,0)
- s5: (1,1)
- combinations present: (0,1), (0,0), (1,0), (1,1) - all four! incompatible

since characters c3 and c4 are incompatible (they exhibit all four gamete
combinations), the full matrix does not have a perfect phylogeny.

for the largest compatible subset, we need to remove either c3 or c4.
both choices give us a subset of 3 characters that admits a perfect
phylogeny:
- option 1: {c1, c2, c3}
- option 2: {c1, c2, c4}

the reduced matrix is:
| m  | c1 | c2 | c4 |
|----|----|----|----| 
| s1 | 0  | 0  | 1  |
| s2 | 1  | 1  | 0  |
| s3 | 0  | 0  | 1  |
| s4 | 0  | 1  | 0  |
| s5 | 0  | 1  | 1  |

the perfect phylogeny tree for {c1, c2, c4}:
```
root
|-- c1=1
|   *-- c2=1
|       *-- {s2}
*-- c1=0
    |-- c2=0
    |   *-- c4=1
    |       *-- {s1,s3}
    *-- c2=1
        |-- c4=0
        |   *-- {s4}
        *-- c4=1
            *-- {s5}
```

=> the full matrix does not have a perfect phylogeny because
characters c3 and c4 are incompatible. the largest compatible subset
contains 3 characters (either {c1, c2, c3} or {c1, c2, c4}).

================================================================================

> 3. Consider the following tree topology for taxa {AC, CT, GT, AT}. Can
>    you compute the parsimony length? Also, can you give the correspond-
>    ing labeling for the internal nodes?

> the tree shows taxa {ac, ct, gt, at} with sequences of length 2.
--------------------------------------------------------------------------------

## position 1 (a, c, g, a):

working bottom-up from the leaves:

node v1 (parent of ct and gt):
- ct has 'c', gt has 'g'
- intersection: c ∩ g = ∅
- union: c ∪ g = {c, g}
- cost: 1 (since intersection is empty)

node v2 (parent of v1 and at):
- v1 has {c, g}, at has 'a'
- intersection: {c, g} ∩ a = ∅
- union: {c, g} ∪ a = {a, c, g}
- cost: 1

root (parent of ac and v2):
- ac has 'a', v2 has {a, c, g}
- intersection: a ∩ {a, c, g} = {a}
- union: {a}
- cost: 0

total cost for position 1: 2

## position 2 (c, t, t, t):

node v1 (parent of ct and gt):
- ct has 't', gt has 't'
- intersection: t ∩ t = {t}
- union: {t}
- cost: 0

node v2 (parent of v1 and at):
- v1 has {t}, at has 't'
- intersection: {t} ∩ t = {t}
- union: {t}
- cost: 0

root (parent of ac and v2):
- ac has 'c', v2 has {t}
- intersection: c ∩ {t} = ∅
- union: c ∪ {t} = {c, t}
- cost: 1

total cost for position 2: 1

## final results:

parsimony length = 2 + 1 = 3

most parsimonious labeling for internal nodes:
- v1 (parent of ct, gt): gt
- v2 (parent of v1, at): at  
- root: at

the tree with internal node labels:
at (root)
|-- ac
*-- at (v2)
    |-- gt (v1)
    |   |-- ct
    |   *-- gt
    *-- at


================================================================================

> 7. Can you check if the following matrix has a perfect phylogeny? If yes,
>    can you report the corresponding tree?

| M  | C1 | C2 | C3 |
|----|----|----|----| 
| S1 | 0  | 0  | 1  |
| S2 | 1  | 1  | 0  |
| S3 | 0  | 0  | 1  |
| S4 | 0  | 1  | 0  |
| S5 | 0  | 1  | 1  |

--------------------------------------------------------------------------------

we check all pairs of characters using the four-gamete test:

# c1 vs c2:
- s1: (0,0)
- s2: (1,1)
- s3: (0,0)
- s4: (0,1)
- s5: (0,1)
- combinations present: (0,0), (1,1), (0,1) - compatible 

# c1 vs c3:
- s1: (0,1)
- s2: (1,0)
- s3: (0,1)
- s4: (0,0)
- s5: (0,1)
- combinations present: (0,1), (1,0), (0,0) - compatible 

# c2 vs c3:
- s1: (0,1)
- s2: (1,0)
- s3: (0,1)
- s4: (1,0)
- s5: (1,1)
- combinations present: (0,1), (1,0), (1,1) - compatible 

since all pairs of characters are compatible, the matrix has a perfect phylogeny.

## constructing the perfect phylogeny tree:

the perfect phylogeny tree is:

root
|-- c1=1
|   *-- c2=1
|       *-- {s2}
*-- c1=0
    |-- c2=0
    |   *-- c3=1
    |       *-- {s1, s3}
    *-- c2=1
        |-- c3=0
        |   *-- {s4}
        *-- c3=1
            *-- {s5}

=> yes, the matrix has a perfect phylogeny. the tree above shows that each 
character changes from 0 to 1 at most once along the tree.

> 16. For the following matrix M, is it an ultrametric matrix? Can you construct
>     the corresponding ultrametric tree or the corresponding nearly ultrametric
>     tree?
> 
> |     | S₁ | S₂ | S₃ | S₄ | S₅  |
> |-----|----|----|----|----|-----|
> | S₁  | 0  | 20 | 20 | 20 | 8   |
> | S₂  |    | 0  | 16 | 16 | 20  |
> | S₃  |    |    | 0  | 10 | 20  |
> | S₄  |    |    |    | 0  | 20  |
> | S₅  |    |    |    |    | 0   |
> 
> 
> 17. Is the following matrix additive? If not, give a reason. If yes, give the
>     additive tree.
> 
> |     | S₁ | S₂ | S₃ | S₄ |
> |-----|----|----|----|----|
> | S₁  | 0  | 3  | 8  | 7  |
> | S₂  |    | 0  | 7  | 6  |
> | S₃  |    |    | 0  | 5  |
> | S₄  |    |    |    | 0  |

--------------------------------------------------------------------------------

## problem 16: ultrametric matrix check

first, check if matrix M is ultrametric by verifying the three-point condition:
for any three distinct points i, j, k, at least two of the distances d(i,j),
d(i,k), d(j,k) must be equal, and the third must be no larger.

checking all triplets:
- (S1, S2, S3): d(S1,S2)=20, d(S1,S3)=20,   d(S2,S3)=16 -> two equal (20,20), third smaller 
- (S1, S2, S4): d(S1,S2)=20, d(S1,S4)=20,   d(S2,S4)=16 -> two equal (20,20), third smaller 
- (S1, S2, S5): d(S1,S2)=20, d(S1,S5)=8,    d(S2,S5)=20 -> two equal (20,20), third smaller 
- (S1, S3, S4): d(S1,S3)=20, d(S1,S4)=20,   d(S3,S4)=10 -> two equal (20,20), third smaller 
- (S1, S3, S5): d(S1,S3)=20, d(S1,S5)=8,    d(S3,S5)=20 -> two equal (20,20), third smaller 
- (S1, S4, S5): d(S1,S4)=20, d(S1,S5)=8,    d(S4,S5)=20 -> two equal (20,20), third smaller 
- (S2, S3, S4): d(S2,S3)=16, d(S2,S4)=16,   d(S3,S4)=10 -> two equal (16,16), third smaller 
- (S2, S3, S5): d(S2,S3)=16, d(S2,S5)=20,   d(S3,S5)=20 -> two equal (20,20), third smaller 
- (S2, S4, S5): d(S2,S4)=16, d(S2,S5)=20,   d(S4,S5)=20 -> two equal (20,20), third smaller 
- (S3, S4, S5): d(S3,S4)=10, d(S3,S5)=20,   d(S4,S5)=20 -> two equal (20,20), third smaller 

all triplets satisfy the ultrametric condition -> matrix is ultrametric

constructing ultrametric tree using UPGMA:

step 1: smallest distance d(S1,S5)=8, merge at height 4
step 2: smallest distance d(S3,S4)=10, merge at height 5  
step 3: smallest distance d(S2,{S3,S4})=16, merge at height 8
step 4: merge {S1,S5} with {S2,S3,S4} at height 10

ultrametric tree:
```
        root
       /    \
     [10]   [10]
     /        \
    /          \
   v1          v2
  /  \        /  \
[8]  [8]    [4]  [4]
 |    |      |    |
 S2   u1     S1   S5
     / \
   [5] [5]
    |   |
   S3   S4
```

--------------------------------------------------------------------------------

## problem 17: additive matrix check

check four-point condition: for any four distinct points i,j,k,l, the two
largest of the three sums d(i,j)+d(k,l), d(i,k)+d(j,l), d(i,l)+d(j,k) must be
equal.

checking quartet (S1,S2,S3,S4):
- d(S1,S2) + d(S3,S4) = 3 + 5 = 8
- d(S1,S3) + d(S2,S4) = 8 + 6 = 14  
- d(S1,S4) + d(S2,S3) = 7 + 7 = 14

two largest sums (14,14) are equal → matrix is additive

constructing additive tree using neighbor-joining:

step 1: compute Q-matrix, minimum is Q(1,2)=-28
step 2: join S1 and S2
- branch to S1: v1 = 2
- branch to S2: v2 = 1
- new node u with d(u,S3)=6, d(u,S4)=5
step 3: three nodes {u,S3,S4}, create central node v
- branch v to u: (6+5-5)/2 = 3
- branch v to S3: (6+5-5)/2 = 3  
- branch v to S4: (5+5-6)/2 = 2

additive tree:
```
      v
     /|\
   3/ | \2
   /  |3 \
  u   S3  S4
 / \
2|  |1
 |  |
S1  S2
```

=> yes, the matrix is additive. the tree above shows the additive tree with
edge lengths that reproduce the original distances.

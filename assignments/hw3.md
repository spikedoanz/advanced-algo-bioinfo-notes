> - Problem 1
> Can you deduce the haplotypes for the following four genotypes using
> Clark’s algorithm?
> • G1 = 122101
> • G2 = 210101
> • G3 = 022121
> • G4 = 201121 
> 
> - Problem 2
> Consider the following set of genotypes.
> G1 : 1012
> G2 : 2220
> G3 : 1020
> G4 : 2210
> 
> (a) Every iteration in Clark’s algorithm resolves at least one Gi by in-
> cluding at most 1 new haplotype. Suppose we always try to resolve Gi
> with the smallest index i first. What is the set of haplotypes generated?
> (b) Is the answer in (a) optimal? If not, can we resolve Gi in a different
> order to obtain the optimal solution?

--------------------------------------------------------------------------------

note: i missed the previous lecture so i used an llm (claude opus 4)to explain
clark's algorithm to me. i now know it's a constraint satisfaction algorithm
for resolving what are essentially superpositions of strings. (which is
essentially what the haplotypes encode for). the sources that came up
when i googled 'clark's algorithm bioinfomatics' weren't really helpful.

# problem 1

we first check the heterozygote count of each genotype:
- G1: 2 (index 1 and 2)
- G2: 1 (index 0)
- G3: 3 (index 1 2 4)
- G4: 2 (index 0 4)

only G2 is unambiguous in this instance, we obtain

G2 -> 010101 + 110101

-> pool = __010101 + 110101__

we try G1 next, which can possibly contain:

100101 + 111101
101101 + 110101 (matched with existing pool)

therefore:

G1 -> 101101 + 110101

-> pool = 010101 + 110101 + __101101__

we try G4 next, which can possibly contain

001101 + 101111
001111 + 101101 (match)

G4 -> 001111 + 101101

-> pool = 010101 + 110101 + 101101 + 001111

we try G3 next, which has 4 possible pairs

000101 + 011111
000111 + 011101
001101 + 010111
001111 + 010101 (match!)

G3 -> 001111 + 010101

therefore, the complete haplotype set are:

{010101, 110101, 101101, 001111}

resolution summary:

G1 -> 101101 + 110101
G2 -> 010101 + 110101
G3 -> 001111 + 010101
G4 -> 001111 + 101101

--------------------------------------------------------------------------------
# problem 2

## part (a): resolve in order g1, g2, g3, g4
--------------------------------------------

check heterozygous sites:
- G1 = 1012: position 3 → 1 site
- G2 = 2220: positions 0,1,2 → 3 sites  
- G3 = 1020: position 2 → 1 site
- G4 = 2210: positions 0,1 → 2 sites

__step 1: G1 (unambiguous)__ 
G1 = 1012 → 1010 + 1011 
pool = {1010, 1011}

__step 2: G2__ 
G2 = 2220 has 4 possible pairs:
1. 0000 + 1110
2. 0010 + 1100
3. 0100 + 1010 (match with pool)
4. 0110 + 1000

G2 → 0100 + 1010 pool = {1010, 1011, 0100}

__step 3: G3__ 
G3 = 1020 → 1000 + 1010 (1010 already in pool) 
pool = {1010, 1011, 0100, 1000}

__step 4: g4__ g4 = 2210 has 2 possible pairs:
1. 0010 + 1110
2. 0110 + 1010 (match)

g4 → 0110 + 1010 
pool = {1010, 1011, 0100, 1000, 0110}

=> answer (a): 5 haplotypes = {1010, 1011, 0100, 1000, 0110}

## part (b): find optimal solution
----------------------------------

the solution above uses 5 haplotypes. try different order:

__resolve g1, g3, g4, g2:__

g1 → 1010 + 1011, pool = {1010, 1011}

g3 → 1000 + 1010, pool = {1010, 1011, 1000}

g4 → 0110 + 1010,  pool = {1010, 1011, 1000, 0110}

g2 → 0110 + 1000 (both already in pool!), pool = {1010, 1011, 1000, 0110}

=> answer (b): no, part (a) is not optimal. resolving in order g1, g3, g4, g2
gives only 4 haplotypes = {1010, 1011, 1000, 0110}

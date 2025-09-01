> EC2:  Estimate the expected number of aminoacids before first stop codon
> caused by a frameshift using either a formula- the formula or algorithm should
> be described - In other words, estimate the length of the protein that is
> translated from a random infinite nucleotide sequence

i used claude to search up the formula that might describe the stop codon shift
phenomenon mentioned. this brought me to the following sources:

(1) https://www.biorxiv.org/content/10.1101/067736v5.full
(2) https://pmc.ncbi.nlm.nih.gov/articles/PMC7084103/

by consulting those two sources, here's my answer to the original problem
statement:

--------------------------------------------------------------------------------

When a frameshift mutation occurs (insertion or deletion of nucleotides not
divisible by 3), the reading frame shifts permanently downstream of the
mutation site. This means we start reading a completely different sequence of
codons, which can be modeled as essentially random if we assume the original
nucleotide sequence has uniform distribution.

We first assume that in the infinite nucleotide sequence the following
statistical properties:

a. After the frameshift, we're reading a new sequence of codons that can be treated as random
b. Each nucleotide position has equal probability for A, T, G, or C (1/4 each)
c. Therefore, each of the 64 possible codons has probability 1/64

Since there are 3 stop codons (UAA, UAG, UGA) out of 64 possible codons:

-> Probability of stop codon at any position: p = 3/64
-> Probability of non-stop codon: 1 - p = 61/64

This is a geometric distribution problem: "How many trials until the first success?"

This problem has the formula:

E[X] = 1/p = 1/(3/64) = 64/3 ≈ 21.33 aminoacids 

(technically the answer should be 21.33 - 1 = 20.33, if we don't count the
stop codon itself, since it's not an amino acid)

The answer here (20-21 aminoacids) also lines up with the results found in
sources (1) and (2).

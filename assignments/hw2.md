> HW2 (check recorded lecture 3 recording):
>
>(a)  p_AA = 0.6, p_aa=0.01, p_Aa=0.39 Find probability that the population of
>size 100 is in HWE. 
>
>(b) Given genotype population: AA =100,  Aa =50, aa =50 Based on allele
>frequencies and assuming HWE, what is the expected genotype frequencies?
>Perform x^2 test - do you accept hypothesis that the population is in HWE?

--------------------------------------------------------------------------------

(a) hardy-weinberg equilibrium (HWE) states that genotype frequencies
should follow p^2 + 2pq + q^2 = 1, where p and q are allele frequencies.

first, we extract the allele frequencies from the given genotype frequencies:
- p(A) = p_AA + 0.5 * p_Aa = 0.6 + 0.5 * 0.39 = 0.795
- q(a) = p_aa + 0.5 * p_Aa = 0.01 + 0.5 * 0.39 = 0.205


under HWE, we'd expect:
- AA: p^2 = 0.795^2 ≈ 0.632
- Aa: 2pq = 2 * 0.795 * 0.205 ≈ 0.326
- aa: q^2 = 0.205^2 ≈ 0.042

but we actually have 0.6, 0.39, and 0.01. these don't match the HWE
predictions, so this population is unlikely to be within HWE. the heterozygote
frequency is higher than expected (0.39 vs 0.326).

to obtain the exact probability, we perform a chi-squared goodness of fit test

with a population of 100, we expect to see under HWE:
- AA = 63.2
- Aa = 32.6
- aa = 4.2

-> x^2  = (60-63.2)^2/63.2 + (39-32.6)^2/32.6 + (1-4.2)^2/4.2
-> x^2  = (60-63.2)**2/63.2 + (39-32.6)**2/32.6 + (1-4.2)**2/4.2
        = 0.162 + 1.252 + 2.438 
        = 3.85

with 1 degree of freedom (3 categories, with 1 paramter (allele frequency, if
we know p(A), we also know p(a))), this gives a p value of 0.05.

=> which means that the probability that this population is in HWE is
approximately 5%.

--------------------------------------------------------------------------------

(b) given total individuals = 200

allele frequencies:
- p(A) = (2 * 100 + 50) / (2 * 200) = 250/400 = 0.625
- q(a) = (2 * 50 + 50) / (2 * 200) = 150/400 = 0.375

under HWE, expected frequencies:
- AA: p^2 = 0.625^2 = 0.390625 -> expected count = 0.390625 * 200 = 78.125
- Aa: 2pq = 2 * 0.625 * 0.375 = 0.46875 -> expected count = 0.46875 * 200 = 93.75
- aa: q^2 = 0.375^2 = 0.140625 -> expected count = 0.140625 * 200 = 28.125

x^2 test: x^2 = sum(observed - expected)^2/expected

for AA: (100 - 78.125)^2/78.125 = 6.13 for Aa: (50 - 93.75)^2/93.75 = 20.41 for
aa: (50 - 28.125)^2/28.125 = 17.01

χ^2 = 6.13 + 20.41 + 17.01 = 43.55

with df = 1 (3 genotypes - 1 - 1 for estimating p), the critical value at α =
0.05 is 3.84.

since 43.55 >> 3.84, we strongly reject the hypothesis that the population is
in HWE. the heterozygote deficiency (50 observed vs 93.75 expected) suggests
inbreeding, population substructure, or some other violation of HWE
assumptions.

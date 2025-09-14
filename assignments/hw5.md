> 1. Consider loci 1 and 2. Suppose the allele for locus 1 is either A or a and
>    the allele for locus 2 is either B or b. Suppose A and B are associated such
> that (1) pAB = pApB + D1, (2) pAb = pApb − D2, (3) paB = papB −D3, and (4) pab
> = papb +D4. Can you show that D1 =D2 =D3 =D4?
> 
> 2. Given a set of 6 haplotypes over 11 SNPs, find the
> minimum size subset of tag SNP which will distinguish all haplotypes
> the subset consists of SNPs:_________________
>  0,1,2,3,4,5,6,7,8,9,10
> (0,1,0,1,0,1,0,1,0,1,0)
> (0,1,1,0,1,0,1,0,0,0,0)
> (0,0,0,1,0,1,0,0,1,1,1)
> (1,0,1,1,0,1,0,1,1,0,1)
> (1,0,1,0,1,0,0,1,1,0,1)
> (1,0,0,0,1,0,1,0,1,1,1)
--------------------------------------------------------------------------------

problem 1:
----------

we have 4 original constraints:

1. pAB = pApB + D1
2. pAb = pApb - D2
3. paB = papB - D3
4. pab = papb + D4

we also have:
- that the sum of all haplotype frequencies = 1
- marginal frequency constraints: sum across one locus equals allele frequency

marginal constraint for allele:

5. A: pAB + pAb = pA
6. B: pAB + paB = pB
7. a: paB + pab = pa

substituting 5 into 1 and 2:

->  (pApB + D1) + (pApb - D2) = pA
<=> pApB + pApb + D1 - D2 - pA = 0
<=> pA (pB + pb - 1) + D1 = D2

pB + pb = 1 (sum of haplotype frequencies)

<=> pA * 0 + D1 = D2
=> D1 = D2


substituting 6 into 1 and 3:

-> pApB + D1 + papB - D3 = pB
... exactly the same simplifications as for the steps with allele A
=> D1 = D3

we also have sum constraints: pAB + pAb + paB + pab = 1

this gives us:
  D1 - D2 - D3 + D4 = 0

since D1 = D2 = D3. we can conclude that D4 must also equal the other
three quarters.

therefore, D1 = D2 = D3 = D4

--------------------------------------------------------------------------------

problem 2:
----------

we'll need at least 3 bisections of the data to discern the haplotypes. this is
because ceil(log_2(6)) = 3.

it obviously cannot be 2 splits, because we have 6 haplotypes,
and 2 splits can only at most 4 haplotypes apart.

to avoid finding the bisections by hand, i wrote this python script to
automatically loop through all combinations of 3-snps.

```python
from itertools import combinations
from collections import defaultdict

H0 = [0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0]
H1 = [0, 1, 1, 0, 1, 0, 1, 0, 0, 0, 0]
H2 = [0, 0, 0, 1, 0, 1, 0, 0, 1, 1, 1]
H3 = [1, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1]
H4 = [1, 0, 1, 0, 1, 0, 0, 1, 1, 0, 1]
H5 = [1, 0, 0, 0, 1, 0, 1, 0, 1, 1, 1]

haplotypes = [H0, H1, H2, H3, H4, H5]
hap_names = ['H0', 'H1', 'H2', 'H3', 'H4', 'H5']
indices = range(len(H0))

def test_snp_combination(snp_indices, haplotypes, hap_names):
    signatures = defaultdict(list)
    for i, hap in enumerate(haplotypes):
        signature = tuple(hap[snp] for snp in snp_indices)
        signatures[signature].append(hap_names[i])
    return signatures

print("-" * 60)
print("testing all 3-SNP combinations:\n")

valid_combinations = []
invalid_combinations = []

for snp_combo in combinations(indices, 3):
    signatures = test_snp_combination(snp_combo, haplotypes, hap_names)
    group_sizes = [len(group) for group in signatures.values()]
    max_group_size = max(group_sizes)
    if max_group_size == 1:
        valid_combinations.append((snp_combo, signatures))
    else:
        invalid_combinations.append((snp_combo, signatures))

print(f"Found {len(valid_combinations)} valid 3-SNP combinations")
print(f"Found {len(invalid_combinations)} invalid 3-SNP combinations\n")

if valid_combinations:
    print("VALID COMBINATIONS (all haplotypes distinguished):")
    for combo, sigs in valid_combinations[:3]:
        print(f"\nSNPs {combo}:")
        for sig, haps in sorted(sigs.items()):
            print(f"  {sig}: {haps}")
else:
    print("NO VALID 3-SNP COMBINATIONS FOUND\n")

if valid_combinations:
    print(f"\nMINIMUM TAG SNP SET: 3 SNPs - Example: {valid_combinations[0][0]}")
```


from this script, i've found quite a handful of valid splits, one of which is: {0,3,7}

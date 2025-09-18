> Consider the following two SNPs. • SNP1: Case — 40 A, 160 C, Control — 20 A,
> 180 C, • SNP2: Case — 20 A, 180 C, Control — 10 A, 190 C. Can you compute the
> relative risk and the odds ratio for the two SNPs? Which SNP has a higher
> risk

================================================================================

# snp 1

data:
- cases:    40A, 160C (total = 200 alleles)
- controls: 20A, 180C (total = 200 alleles)

frequenciesa:
- A frequency in cases      = 40/200 = .2
- A frequency in controls   = 20/200 = .1
-> the A allele seems to be the risk allele (more frequent in cases)

relative risk

RR = P(disease | A) / P(disease | C)

using alelle counts:
- P(disease | A) = 40 / (40+20) = 40/60         = 0.667...
- P(disease | C) = 160 / (160+180) = 160/340    = 0.471...

RR = 0.667 / 0.471 = __1.42__

odds ratio:

OR = (A in cases * C in controls) / (C in cases * A in controls)
OR = (40 * 180) / (160 * 20) = 7200/3200 = __2.25__

--------------------------------------------------------------------------------

# snp 2

data:
- cases:    20A, 180C (total = 200 alleles)
- controls: 10A, 190C (total = 200 alleles)

frequencies:
- A frequency in cases      = 20 / 200 = .1
- A frequency in controls   = 10 / 200 = .05
-> the A allele seems to be the risk allele

relative risk:
- P(disease | A) = 20/(20+10) = 20/30       = 0.667
- P(disease | C) = 180/(180+190) = 180/370  = 0.486

RR = 0.667/0.486 = __1.37__

odds ratio:
OR = (20 * 190) / (180 * 10) = 3800/1800 = __2.11__

--------------------------------------------------------------------------------

in summary, each snp has relative risk and odds ratio:
- SNP1: 1.42 and 2.25
- SNP2: 1.37 and 2.11

because SNP 1 has higher scores scores on both metrics, we can conclude that it
has a higher risk association.

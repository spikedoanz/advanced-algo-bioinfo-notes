> Assume that the there is a coding DNA sequence string - you translate each
> codon into amino-acid and can see the resulted first 30 amino-acids (sequence
> A). Also you remove the first nucleotide and also produce the first 30
> amino-acids (sequence B). Can you tell which of two sequences is a valid
> protein beginning (A) and which is a frameshifted garbage (B)? What easy to
> see difference between them? (Hint:   find on-line tools translating dna into
> aminoacids)

when we translate DNA into amino acids, we're basically running a parser on the
string containing the genetic data. the correct reading frame (sequence A),
results in clean output, it will start with a methionine (M), with no stop
codon in the middle of the flow, which makes biological sense. 

but if we frame shift (sequence B), stop codons will start appearing in the middle
of the sequence. using a tool like https://web.expasy.org/translate/, it even
looks like parser errors. (in the tool above, it gets highlighted as '-')

so in short, the stop codons are the obvious tell. if your sequences contain them,
they're probably garbalged data. else, it's likely that it was the correct sequence.

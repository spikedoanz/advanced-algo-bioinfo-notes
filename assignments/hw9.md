================================================================================
> 2. Suppose the following set of sites are known to be bound by the tran-
> scription factor NFkB:
> AGGAAATG, GGAAATGCCG, AGGAAATG, GGAATTCC, GAAATG, GGAAAACC,
> ATGGAAATGAT, GGAAATCCCG, GGAAATTCCA, GGAAATTCCC, GGAAATTCCG.
> Can you align them by packing spaces to the beginning and the end of
> each sequence? Then, can you report the corresponding logo? (Sequence
> logo can be found in http://weblogo.berkeley.edu/logo.cgi.)
--------------------------------------------------------------------------------

step 1: analyze the sequence

1.    AGGAAATG (8 bp)
2.    GGAAATGCCG (10 bp)
3.    AGGAAATG (8 bp)
4.    GGAATTCC (8 bp)
5.    GAAATG (6 bp)
6.    GGAAAACC (8 bp)
7.    ATGGAAATGAT (11 bp)
8.    GGAAATCCCG (10 bp)
9.    GGAAATTCCA (10 bp)
10.   GGAAATTCCC (10 bp)
11.   GGAAATTCCG (10 bp)

step 2: identify core motif

"GAA" is shared by most sequences
"GGAA", "GGAAAT" and "GGAAATT" are also common
-> the consensus appears to be around "GAA"


step 3: align sequences

we align based on the GAA pattern

---AGGAAATG----
----GGAAATGCCG-
---AGGAAATG----
----GGAATTCC---
-----GAAATG----
----GGAAAACC---
--ATGGAAATGAT--
----GGAAATCCCG-
----GGAAATTCCA-
----GGAAATTCCC-
----GGAAATTCCG-

=> the corresponding logo is in the file hw9problem2.png
- positions 1-4: empty
- positions 5-6: strong G
- positions 7-8: strong A
- positions 9: preference for A
- positions 10: preference for T
- position 11: equal among GCT
- position 12: preference for C
- position 13: preference for C
- position 14: small preference for G
- position 15-...:mostly gaps


================================================================================
> 3. For each of the following cases, design a positional weight matrix that
> gives a high score for the motif.
> (a) The motif equals TATAAT.
> (b) The motif has five nucleotides where the first position equals A and
> the third position equals either C or G.
> (c) The motif is either TATAAT or CATCGT
--------------------------------------------------------------------------------

a. motif equals TATAAT:

- each correct nucleotide at each position gets a high positive score
- incorrect nucleotides get a negative score

Position:    1    2    3    4    5    6
    A       -5   10   -5   10   10   -5
    C       -5   -5   -5   -5   -5   -5
    G       -5   -5   -5   -5   -5   -5
    T       10   -5   10   -5   -5   10


b. motif has five nucleotides where the first position equals A and the third
position equals either C or G:

- position 1: only A scores high
- position 3: both C and G score high equally
- position 2,4,5: all nucleotides score equally (small positive to show no penalty)

Position:    1    2    3    4    5
    A       10    1   -5    1    1
    C       -5    1    5    1    1
    G       -5    1    5    1    1
    T       -5    1   -5    1    1


c. motif is either TATAAT or CATCGT:

- position 1: T or C (both get high scores)
- position 2: A (both motifs have A)
- position 3: T (both motifs have T)
- position 4: A or C (from TATAAT and CATCGT respectively)
- position 5: A or G (from TATAAT and CATCGT respectively)
- position 6: T (both motifs have T)

Position:    1    2    3    4    5    6
    A       -5   10   -5    5    5   -5
    C        5   -5   -5    5   -5   -5
    G       -5   -5   -5   -5    5   -5
    T        5   -5   10   -5   -5   10

================================================================================
> 7. Given a sequence S of length n, the aim is to find an (l, d)-motif which
> occurs the most frequently in S.
> (a) Propose an algorithm which finds an (l, 0)-motif in O(n) time.
> (b) Propose an algorithm which finds an (l, 1)-motif in O(|Σ|n2 log n)
> time, where Σ is the alphabet size (for DNA, |Σ| = 4).
--------------------------------------------------------------------------------

the (l,d) motif is a substring of length l that appears multiple times in S,
where each occurrence can have at most d mismatches from the motif.

a. propose an algorithm which finds an (l, 0)-motif in O(n) time:

- for d=0, we need exact matches
-> we can use a hash table to store all substrings of length l in S

```python
def find_l_0_motif(S, l):
    n = len(S)
    if l > n:
        return None
    
    # hash table to count occurrences of each l-length substring
    count = {} # assume this is O(1) on fetches
    max_count = 0
    best_motif = None
    
    # slide through all l-length substrings
    for i in range(n - l + 1):
        substring = S[i:i+l]
        
        if substring not in count:
            count[substring] = 0
        count[substring] += 1
        
        # track the most frequent
        if count[substring] > max_count:
            max_count = count[substring]
            best_motif = substring
    
    return best_motif, max_count
```


b. propose an algorithm which finds an (l, 1)-motif in O(|Σ|n2 log n) time:

```python
def find_l_1_motif(S, l, alphabet):
    n = len(S)
    # step 1: Extract all length-l substrings
    substrings = []
    for i in range(n - l + 1):
        substrings.append(S[i:i+l])
    # step 2: Sort them lexicographically - O(n log n)
    sorted_substrings = sorted(substrings)
    # step 3: For each substring, count matches with at most 1 mismatch
    best_motif = None
    best_count = 0
    # use a set to avoid counting the same motif multiple times
    checked = set()
    
    for substring in substrings:
        if substring in checked:
            continue
        checked.add(substring)
        count = 0
        # count exact matches using binary search
        count += count_occurrences(sorted_substrings, substring)
        # generate and count all 1-mismatch variants
        for i in range(l):
            for c in alphabet:
                if c != substring[i]:
                    # create variant with one substitution
                    variant = substring[:i] + c + substring[i+1:]
                    count += count_occurrences(sorted_substrings, variant)
        if count > best_count:
            best_count = count
            best_motif = substring
    return best_motif, best_count

def count_occurrences(sorted_list, target):
    left = binary_search_left(sorted_list, target)
    if left == len(sorted_list) or sorted_list[left] != target:
        return 0
    right = binary_search_right(sorted_list, target)
    return right - left

def binary_search_left(arr, target):
    left, right = 0, len(arr)
    while left < right:
        mid = (left + right) // 2
        if arr[mid] < target:
            left = mid + 1
        else:
            right = mid
    return left

def binary_search_right(arr, target):
    left, right = 0, len(arr)
    while left < right:
        mid = (left + right) // 2
        if arr[mid] <= target:
            left = mid + 1
        else:
            right = mid
    return left
```

- extract substrings: O(n) substrings of length l
- sort: O(n log n) comparisons, each taking O(l) time
- for each unique substring (at most n):
    Generate O(l·|Σ|) variants
    Each variant requires binary search: O(log n)
    Total per substring: O(l·|Σ|·log n)
- overall: O(n) × O(l·|Σ|·log n) = O(|Σ|·n·l·log n)

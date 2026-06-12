---
layout: post
title: "Where in the Genome Does DNA Replication Begin?"
date: 2019-05-01
description: ""
tags: BioInfo Python
categories: BioInfo
redirect_from:
  - /posts/eb5da1c8/
---

## 1.1 A Journey of a Thousand Miles…

Genome replication

Replication begins in a genomic region called the replication origin (denoted ori) and is performed by molecular copy machines called DNA polymerases.

```
Finding Origin of Replication Problem:   
 Input: A DNA string Genome.   
 Output: The location of ori in Genome.
```

## 1.2 Hidden Messages in the Replication Origin

### DnaA boxes

Hidden Message Problem: Find a “hidden message” in the replication origin.  
 Input: A string Text.  
 Output: A hidden message in Text.

### Hidden messages in “The Gold-Bug”

The problem just like the encryped messages in the gold-bug.

### Counting words

```
PatternCount(Text, Pattern)
    count ← 0
    for i ← 0 to |Text| − |Pattern|
        if Text(i, |Pattern|) = Pattern
            count ← count + 1
    return count
```

```python
ori = open('v_cholerae_oric.txt', 'r')
Text = ori.read()
Pattern = 'TGATCA'
def PatternCount(Text, Pattern):
    count = 0
    for i in range(len(Text)-len(Pattern)+1):
        if Text[i:i+len(Pattern)] == Pattern:
            count = count + 1
    return count
PatternCount(Text, Pattern)
```

```
8
```

#### The Frequent Words Problem

#### Frequent words in Vibrio cholerae

```
    FrequentWords(Text, k)
        FrequentPatterns ← an empty set
        for i ← 0 to |Text| − k
            Pattern ← the k-mer Text(i, k)
            Count(i) ← PatternCount(Text, Pattern)
        maxCount ← maximum value in array Count
        for i ← 0 to |Text| − k
            if Count(i) = maxCount
                add Text(i, k) to FrequentPatterns
        remove duplicates from FrequentPatterns
        return FrequentPatterns```

```python
k = 3
Text = 'CGATATATCCATAG'
def FrequencyMap(Text, k):
    freq = {}
    n = len(Text)
    for i in range(n-k+1):
        Pattern = Text[i:i+k]
        freq[Pattern] = 0
        for i in range (n-k+1):
            if Text[i:i+k] == Pattern:
                freq[Pattern] = freq[Pattern] + 1
    return freq
print(FrequencyMap(Text, k))
```

```
{'CGA': 1, 'GAT': 1, 'ATA': 3, 'TAT': 2, 'ATC': 1, 'TCC': 1, 'CCA': 1, 'CAT': 1, 'TAG': 1}
```

```python
def FrequentWords(Text, k):
    words = []
    freq = FrequencyMap(Text, k)
    m = max(freq.values())
    for key in freq:
        if freq[key] == m:
            words.append(key)
    return words
k = 4
Text = 'ACGTTGCATGTCGCATGATGCATGAGAGCT'
FrequentWords(Text, k)
```

```
['GCAT', 'CATG']
```

```python
# Input:  A string Text and an integer k
# Output: A list containing all most frequent k-mers in Text
def FrequentWords(Text, k):
    words = []
    freq = FrequencyMap(Text, k)
    m = max(freq.values())
    for key in freq:
        if freq[key] == m:
            words.append(key)
    return words
# Copy your FrequencyMap() function here.
def FrequencyMap(Text, k):
    freq = {}
    n = len(Text)
    for i in range(n-k+1):
        Pattern = Text[i:i+k]
        freq[Pattern] = 0
        for i in range (n-k+1):
            if Text[i:i+k] == Pattern:
                freq[Pattern] = freq[Pattern] + 1
    return freq

f = open('v_cholerae_oric.txt', 'r')
ori = f.read()
Text = 'ACGTTGCATGTCGCATGATGCATGAGAGCT'
k = 10
FrequentWords(ori, k)

```

```
['CTCTTGATCA', 'TCTTGATCAT']
```

```python
f.close()
```

```python
f = open('v_cholerae_oric.txt', 'r')
ori = f.read()
print(ori)
f.close()
```

```
ATCAATGATCAACGTAAGCTTCTAAGCATGATCAAGGTGCTCACACAGTTTATCCACAACCTGAGTGGATGACATCAAGATAGGTCGTTGTATCTCCTTCCTCTCGTACTCTCATGACCACGGAAAGATGATCAAGAGAGGATGATTTCTTGGCCATATCGCAATGAATACTTGTGACTTGTGCTTCCAATTGACATCTTCAGCGCCATATTGCGCTGGCCAAGGTGACGGAGCGGGATTACGAAAGCATGATCATGGCTGTTGTTCTGTTTATCTTGTTTTGACTGAGACTTGTTAGGATAGACGGTTTTTCATCACTGACTAGCCAAAGCCTTACTCTGCCTGACATCGACCGTAAATTGATAATGAATTTACATGCTTCCGCGACGATTTACCTCTTGATCATCGATCCGATTGAAGATCTTCAATTGTTAATTCTCTTGCCTCGACTCATAGCCATGATGAGCTCTTGATCATGTTTCCTTAACCCTCTATTTTTTACGGAAGAATGATCAAGCTGCTGCTCTTGATCATCGTTTC
```

## 1.3 Some Hidden Messages are More Surprising than Others

```python
def Reverse(Pattern):
    rev = ""
    for char in Pattern:
        rev += Pattern[::-1]
        return rev
    
Pattern = 'AAAACCCGGT'
Reverse(Pattern)
```

```
'TGGCCCAAAA'
```

```python
Pattern = "ACGT"
rev = ""
for i in range(len(Pattern)-1):
    print(i)
   

    
```

```
0
1
2
```

```python
#else if 
def Complement(Pattern):
    com = ""
    for i in range(len(Pattern)):
        if Pattern[i] == "A":
            com += "T"
        elif Pattern[i] == "T":
            com += "A"
        elif Pattern[i] == "C":
            com += "G"
        elif Pattern[i] == "G":
            com += "C"
    return com

Pattern = "AAAACCCGGT"
Complement(Pattern)
            
```

```
'TTTTGGGCCA'
```

```python
def Complement(Pattern):
    basepairs = {"A":"T", "G":"C", "C":"G", "T":"A"}
    comp = ""
    for base in Pattern:
        comp += basepairs.get(base)
    return comp
Pattern = "AAAACCCGGT"
Complement(Pattern)
```

```
'TTTTGGGCCA'
```

```python
# Input:  A DNA string Pattern
# Output: The reverse complement of Pattern
def ReverseComplement(Pattern):   
    return Reverse(Complement(Pattern))
# Copy your Reverse() function here.
def Reverse(Pattern):
    rev = ""
    for char in Pattern:
        rev += Pattern[::-1]
        return rev
# Copy your Complement() function here.
def Complement(Pattern):
    basepairs = {"A":"T", "G":"C", "C":"G", "T":"A"}
    comp = ""
    for base in Pattern:
        comp += basepairs.get(base)
    return comp
Pattern = "AAAACCCGGT"
ReverseComplement(Pattern)
```

```
'ACCGGGTTTT'
```

```python
def PatternMatching(Pattern, Genome):
    positions = [] # output variable
    # your code here
    for i in range(len(Genome)-len(Pattern)+1):
        if Genome[i:i+len(Pattern)] == Pattern:
            positions.append(i)
    
    return positions
Pattern = "ATAT"
Genome = "GATATATGCATATACTT"
PatternMatching(Pattern, Genome)
```

```
[1, 3, 9]
```

```python
def PatternMatching(Pattern, Genome):
    positions = [] # output variable
    # your code here
    for i in range(len(Genome)-len(Pattern)+1):
        if Genome[i:i+len(Pattern)] == Pattern:
            positions.append(i)
    
    return positions
f = open("Vibrio_cholerae.txt", "r")
Genome = f.read()
Pattern = "CTTGATCAT"
PatternMatching(Pattern, Genome)
```

```
[60039,
 98409,
 129189,
 152283,
 152354,
 152411,
 163207,
 197028,
 200160,
 357976,
 376771,
 392723,
 532935,
 600085,
 622755,
 1065555]
```

```python
f.close()
```

## 1.4 An Explosion of Hidden Messages

#### Looking for hidden messages in multiple genomes

```python
ori = open('t_petrophila_oriC.txt', 'r')
Text = ori.read()
Pattern = 'ATGATCAAG'
def PatternCount(Text, Pattern):
    count = 0
    for i in range(len(Text)-len(Pattern)+1):
        if Text[i:i+len(Pattern)] == Pattern:
            count = count + 1
    return count
PatternCount(Text, Pattern)
```

```
0
```

```python
# Copy your PatternCount function below here
def PatternCount(Text, Pattern):
    count = 0
    for i in range(len(Text)-len(Pattern)+1):
        if Text[i:i+len(Pattern)] == Pattern:
            count = count + 1
    return count

# On the following line, create a variable called Text that is equal to the oriC region from T petrophila
Text = "AACTCTATACCTCCTTTTTGTCGAATTTGTGTGATTTATAGAGAAAATCTTATTAACTGAAACTAAAATGGTAGGTTTGGTGGTAGGTTTTGTGTACATTTTGTAGTATCTGATTTTTAATTACATACCGTATATTGTATTAAATTGACGAACAATTGCATGGAATTGAATATATGCAAAACAAACCTACCACCAAACTCTGTATTGACCATTTTAGGACAACTTCAGGGTGGTAGGTTTCTGAAGCTCTCATCAATAGACTATTTTAGTCTTTACAAACAATATTACCGTTCAGATTCAAGATTCTACAACGCTGTTTTAATGGGCGTTGCAGAAAACTTACCACCTAAAATCCAGTATCCAAGCCGATTTCAGAGAAACCTACCACTTACCTACCACTTACCTACCACCCGGGTGGTAAGTTGCAGACATTATTAAAAACCTCATCAGAAGCTTGTTCAAAAATTTCAATACTCGAAACCTACCACCTGCGTCCCCTATTATTTACTACTACTAATAATAGCAGTATAATTGATCTGA"

# On the following line, create a variable called count_1 that is equal to the number of times
# that "ATGATCAAG" occurs in Text.
Pattern1 = 'ATGATCAAG'

# On the following line, create a variable called count_2 that is equal to the number of times
# that "CTTGATCAT" occurs in Text. 
Pattern2 = 'ATGATCAAG'

# Finally, print the sum of count_1 and count_2
print(PatternCount(Text, Pattern1)+PatternCount(Text, Pattern1))
```

```
0
```

## Exercise

```python
Text = "CGCGATACGTTACATACATGATAGACCGCGCGCGATCATATCGCGATTATC"
Pattern = 'CGCG'
def PatternCount(Text, Pattern):
    count = 0
    for i in range(len(Text)-len(Pattern)+1):
        if Text[i:i+len(Pattern)] == Pattern:
            count = count + 1
    return count
PatternCount(Text, Pattern)
```

```
5
```

# Selection scanning

Selection scanning is the process of identifying genomic regions that have been under selection.
It is a powerful tool to understand the genetic basis of adaptation and to identify candidate genes that are responsible for adaptation.

## Site frequency spectrum (SFS)

Site frequency spectrum (SFS), also known as allele frequency spectrum (AFS), is a histogram of the number of sites in a population that have a given allele frequency.
It is a powerful tool to infer demographic history and selection.

## Statistics


| Statistics | Description                           | Reference            |
| ---------- | ------------------------------------- | -------------------- |
| EHH        | Extended Haplotype Homozygosity       | |
| iHS        | Integrated Haplotype Score            | |
| XP-EHH     | Cross-population EHH                  | |
| nSL        | Number of segregating sites by length | @@ferrer-admetlla2014 |
| XP-nSL     | Cross-population nSL                  | @@szpiech2021         |

### Tajima's D

Tajima's D is a measure of the difference between the number of segregating sites and the average number of nucleotide differences in a sample.

### EHH and iHS

### XP-EHH

### nSL

We organize phased data as an $ n \times S_n $ matrix $\mathbf{H}$ with rows corresponding to the $n$ sampled haplotypes and columns corresponding to the $S_n$ segregating sites, with $H_{ik}=1$ if the $i$th haplotype carries the derived allele at the $k$th segregating site, and 0 otherwise.
For each segregating site, we define the following sets of haplotypes carrying the ancestral and derived alleles:
$$\begin{align}
A(k) &= \{i : H_{ik} = 0\} \\
D(k) &= \{i : H_{ik} = 1\}
\end{align}$$
and let $n_A(k)$ and $n_D(k)$ denote the sizes of these respective sets.
We let $p_k$ be the position, in units of recombination distance, of the $k$th segregating site.
It will be useful to refer to single nucleotide polymorphisms (SNPs) by their recombination position, rather than ordinal position in $\mathbf{H}$, so we let $H_{i,r_1:r_2}$ denote the row vector corresponding to segregating sites of the $i$th haplotype which lie in the open interval $(r_1, r_2)$ For haplotypes $i$ and $j$, we define $L_{ij}$ to be as follows:

$$
    L_{ij} = \max\{r - l : x \in (p_l, p_r), H_{i, p_l:p_r} \stackrel{ibs}{=} H_{j, p_l:p_r} \}.
$$

This is the number of consecutive segregating sites, in the interval containing x, over which haplotypes $i$ and $j$ are identical by state (IBS). At the $k$th segregating site, our statistic is defined in terms of the mean value of $L_{ij}$ over pairs of haplotypes which either both carry the ancestral or derived allele:

$$\begin{align}
SL_A(k) &= \frac{2 \sum_{i < j \in A(k)} L_{ij}(p_k)}{n_A(k)(n_A(k)-1)} \\
SL_D(k) &= \frac{2 \sum_{i < j \in D(k)} L_{ij}(p_k)}{n_D(k)(n_D(k)-1)}
\end{align}$$

Finally, $nS_L$ is defined in a manner analogous to $iHS$ by taking the log ratio of ancestral and derived statistics:

$$\begin{align}
unstandardized nS_L(k) &= \ln(\frac{SL_A(k)}{SL_D(k)}) \\
nS_L(k) &= \frac{unstandardized nS_L(k) - \mu}{\sigma}
\end{align}$$

```python
import numpy as np

def nSL(H):
    n, S = H.shape
    nSL = np.zeros(S)
    for k in range(S):
        A = np.where(H[:, k] == 0)[0]
        D = np.where(H[:, k] == 1)[0]
        nA = len(A)
        nD = len(D)
        if nA > 1:
            SLA = 2 * np.sum([np.max([np.sum(H[i, p1:p2] == H[j, p1:p2]) for p1, p2 in zip(np.where(H[i] != H[j])[0][:-1], np.where(H[i] != H[j])[0][1:])]) for i in A for j in A if i < j]) / (nA * (nA - 1))
        else:
            SLA = 0
        if nD > 1:
            SLD = 2 * np.sum([np.max([np.sum(H[i, p1:p2] == H[j, p1:p2]) for p1, p2 in zip(np.where(H[i] != H[j])[0][:-1], np.where(H[i] != H[j])[0][1:])]) for i in D for j in D if i < j]) / (nD * (nD - 1))
        else:
            SLD = 0
        nSL[k] = np.log(SLA/SLD)
    nSL = (nSL - np.mean(nSL)) / np.std(nSL)
    return nSL
```

### XP-nSL

## Softwares

| Software | Description | Reference |
| -------- | ----------- | --------- |
| Sweep    | Sweep™ allows large-scale analysis of haplotype structure in genomes for the primary purpose of detecting evidence of natural selection. Primarily, it uses the Long Range Haplotype (LRH) test to look for alleles of high frequency with long-range linkage disequilibrium (LD), which suggest the haplotype rapidly rose to high frequency before recombination could break down associations with nearby markers (Nature 419(6909): 832-7). Sweep takes phased genotype data as input, detects all haplotype blocks in that data, and then determines the frequency and long-range LD for each allele in each block. | @@sabeti2002 |
| selscan  | A software package for detecting recent positive selection from patterns of linkage disequilibrium | @@szpiech2024 |

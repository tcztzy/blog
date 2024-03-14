# Data Structure

Data structure is the fundamental of computer science. It is the foundation of
algorithm and software development. In bioinformatics, data structure is also
important. It is the key to efficient data processing and analysis. In this section, we will discuss the data structure used in bioinformatics.

If you choose a wrong data structure, you may end up with a slow and inefficient
program, or even worse, a wrong result.

| File format | Description           |
| ----------- | --------------------- |
| FASTA/FASTQ | Sequence data         |
| SAM/BAM     | Alignment data        |
| VCF/BCF     | Variant data          |
| BED         | Genomic interval data |
| GFF/GTF     | Gene annotation data  |
| MSA         | Multiple sequence alignment |

## Structured and unstructured data

Structured data is data that is organized in a specific way. It is often in tabular format, and can be easily processed and analyzed.
Unstructured data is data that is not organized in a specific way. It is difficult to process and analyze.
In bioinformatics, structured data is often used to represent sequence, alignment, variant, and genomic interval data. Unstructured data is often used to represent gene annotation, protein structure, and multiple sequence alignment data.

### Anndata

Personally, I will introduce the `anndata` package, which is a structured data format for single-cell genomics.
The design of `anndata` is good for bioinformatics data, and it is easy to use and efficient.

Typically, we have a tabular data, each row represents a sample (e.g. cell, individual), and each column represents a feature (e.g. gene, variant).
We also have serialized data for each sample and feature.

### tskit

The `tskit` package is a structured data format for tree sequence data. It is designed for efficient storage and analysis of genealogical data.

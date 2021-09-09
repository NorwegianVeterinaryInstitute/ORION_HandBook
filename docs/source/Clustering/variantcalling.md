# SNPs and variant calling

## What is SNPs and variant calling?

Genomic variants are polymorphic sites within segments that are “identical by
descent”, i.e. are genomic regions or positions which originate from a common
ancestor, but differ between the different samples/isolates/species at study.
Such differences can correspond to single-nucleotide polymorphisms
([SNPs](https://en.wikipedia.org/wiki/Single-nucleotide_polymorphism)),
insertions or deletions ([INDELs[](https://en.wikipedia.org/wiki/Indel)), copy
number variations ([CNVs](https://en.wikipedia.org/wiki/Copy_number_variation)),
[duplications](https://en.wikipedia.org/wiki/Gene_duplication),
[translocations](https://en.wikipedia.org/wiki/Chromosomal_translocation) or
[inversions](https://en.wikipedia.org/wiki/Chromosomal_translocation). All these
types of variants are extremely relevant for comparative genomics analyses.
Nevertheless, given the higher rate of point mutations and their lower
complexity, SNPs are the most commonly used variants in comparative genomics.
SNP or variant calling corresponds to the identification of each of these
polymorphisms in the dataset, which is normally coupled with additional
downstream filtering steps to remove regions that can bias the clustering of the
different samples, such as recombination-prone regions, specific homoplasic
sites or SNPs associated with antibiotic resistance. The relevance and impact on
the analysis of these additional filtering steps is contingent on the species
(or lineages) under evaluation.

## SNP calling by mapping

SNP-calling by mapping (i.e,. mapping the reads against a reference genome
sequence)  implies the choice of an adequate reference sequence (see species
sections for details).  This approach has the advantage of being able to use the
read coverage depths, or the proportion of mixed alleles to calculate the
confidence with which a given polymorphism is called ([Olson et al.
2014](https://www.frontiersin.org/articles/10.3389/fgene.2015.00235/full)).
Variant calling results are usually output in [VCF
format](https://samtools.github.io/hts-specs/VCFv4.2.pdf), which indicates for
each variable position the information relative to the respective coordinates in
the reference, the reference allele, the alternative allele (single nucleotide
for SNPs, multiple nucleotides for INDELs), and other parameters. A posterior
variant filtration step is always recommended. For that, the minimum number of
reads that mapped to the reference, the proportion of reads that differ from the
reference, the base sequencing quality, as well the proportion of mixed alleles
can be used (eg. as used in [Snippy](https://github.com/tseemann/snippy), and
the underlying tool [Freebayes](https://github.com/ekg/freebayes)). Although
SNP-calling is performed independently for each sample, the ultimate goal of
this step is to  obtain a multi-sample SNP alignment/matrix. This can be
achieved as far as all samples were compared against the same reference
sequence. In this case, some pipelines, such as Snippy, offer the possibility to
easily combine (and filter) SNP data from multiple samples, providing all the
necessary files for subsequent clustering/phylogenetic analyses. Noteworthy,
these tools can additionally provide useful functionalities, such as consensus
sequence generation and SNP annotation, which may be relevant at several levels
beyond the clustering (e.g., rapid detection of mutations of interest, etc).

NOTE: It is important to read the recommended guidelines of each variant caller
before setting all the parameters. The values that work for one program may not
be the best for another onei.


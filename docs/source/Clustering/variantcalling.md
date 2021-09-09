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
be the best for another one.

## SNP calling by multiple alignment 

SNP calling by multiple alignment intends to produce core multiple alignments
for subsequent clustering/phylogenetic analyses. This method takes  assembled
genomes of multiple samples as input, and generates a “core” alignment, in which
the core is defined as the proportion of the genome that is common to all
isolates included in the analysis. For this reason, the choice of the dataset
will greatly influence the resolution of downstream phylogenetics, i.e., a
highly diverse dataset tends to yield shorter core alignment, thus reducing the
discriminatory power among closely related isolates, since there is less core
genome to gather SNPs from.  Although several programs are available for genome
alignment (e.g., [Mauve](http://darlinglab.org/mauve/mauve.html),
[Muscle](https://www.drive5.com/muscle/)), further steps of SNP
filtering/masking are usually needed. As such, there are a few solutions that
integrate alignment, SNP filtering and even phylogenetics. For instance,
[Harvest](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0524-x)
is a suite that allows the quick analysis of thousands of sequences, enabling
variant calling, recombination detection, and phylogenetic tree visualization.
It integrates
[Parsnp](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0524-x),
which uses short sequences of the genome that are unique and shared in all the
genomes (Maximal unique matches: MUMs) under study and thereafter extend the
area of the alignment recursively across all the genomes (Locally collinear
blocks LCNs). Aligned nucleotides (and gaps) which are not unique at position X
across samples that are defined as variants. Exporting the multiplement
(multi-fasta) or as variant VCF format requires a reference as coordinate system
(by default it is chosen as the first reference in the alignment). The reference
cannot contain gaps, so if some of the isolates have sequences that are not
represented in the references, those will not be included in the output,
therefore, according to which reference that is used, there might be small
variation in what is given as output with an otherwise identical dataset. 

Note: it is possible to create an MSA of the whole genome (ie. with
[progressiveMauve](http://darlinglab.org/mauve/user-guide/progressivemauve.html)),
however further processing is challenging as most softwares do not handle
multiple-alignments formats where the number of sequences aligned is not
identical. If you are working with an epidemiologic group, the samples are
assumed to be very closely related and therefore even a core-alignment with
Parsnp will represent a substantial fraction of the genome size.


## SNP calling using kmers

K-mer-based SNP calling methods rely on the comparison of
[k-mers](https://en.wikipedia.org/wiki/K-mer) between different samples in order
to detect and identify polymorphic positions and subsequently perform
clustering/phylogenetic analysis. For this reason, these methods can be used on
assembled genomes or directly on the genome sequencing reads. Programs able to
perform all the analysis from k-mer definition to clustering of multiple samples
have been developed, such as
[SKA](https://www.biorxiv.org/content/10.1101/453142v1.full) and
[Ksnp3[(https://academic.oup.com/bioinformatics/article/31/17/2877/183216).
Briefly, each sequence is sliced into k-mers of a specified odd-length and each
k-mer is then compared between the different samples searching for their
differences. In both programs a table of common k-mers allowing one central
difference is the basis to compare samples and reported SNPs result from the
central differences of k-mers. Because of this definition it is not possible to
detect variants composed of successive SNPs, and k-mer-based SNP calling loses
power with increased sample variability. As these k-mer comparisons may be
performed in the absence of an assembled genome, SNPs can be provided without
coordinates. Nevertheless, both programs have the option of mapping back k-mers
to an input reference genome which gives the position of the SNPs. Of note,
Ksnp3 provides the possibility to download genome annotations from GenBank.

## hqSNP vs non-hqSNPs

“All SNPs are equal, but some SNPs are more equal than others”. hqSNPs (high
quality) are SNPs usually detected by a combination of methods, usually two, and
where methods reported congruent SNPs, that were not flagged as problematic by
the quality filters of each method (robust SNPs). There might be some variations
in the variants found by different methods, according to the detection criteria
of each particular method. This can e.g. arise because multiple alignment is not
perfect, alternative local alignments may be equally possible and therefore
different alternative variants can be detected by the different methods.
Therefore, MSA-based and mapping-based methods are likely to detect a set of
variants that is not totally overlapping. For further explanation, a good
overview of the different methods can be found in this paper ([Olson N.D et al.
2015](https://www.frontiersin.org/articles/10.3389/fgene.2015.00235/full)).
Algorithms underlying those methods are explained here, and ([Canzar, S. and
Salzberg S.L. 2015](https://ieeexplore.ieee.org/document/7244195)) and some
tutorials online from the [Broad Institute can be found
here](https://www.broadinstitute.org/partnerships/education/broade/best-practices-variant-calling-gatk-1).

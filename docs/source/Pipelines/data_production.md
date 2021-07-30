# Data Production

## Reference-based vs _de novo_ genome assembly

Once data has been preprocessed, the reads can be analysed further. To this end,
we need to “solve the puzzle” and understand to which genomic region a read may
correspond. This usually proceeds via one of two pathways: via mapping to a
reference genome or via _de novo_ genome assembly. In cases where the desired
output can be acquired via mapping in some way or shape, that is often preferred
since genome assembly is a computationally demanding process. However, that
should be balanced against the subsequent use. Anecdotal results suggest that
mapping methods might give more variants for cgMLST, and thus result in
artificial inflation of allele differences between isolates. 

## Assembly and annotation

### What is an assembly

After sequencing, the genome is available in the form of sequenced reads, and
these can be used to create an assembly of the genome. An assembly is a
reconstruction of the genome, in that the actual genome being sequenced is in
itself an unobservable entity. In the assembly process, the reads stemming from
the sequencing process are aligned and merged with the aim of producing a
consensus sequence of the genome. 

The end result of an assembly is a fasta file containing the reconstructed
genome sequence. The assembly is likely to be fragmented, at least if the input
data was Illumina reads due to their short insert size, which [influences the
ability to solve genomic
repeats](https://www.illumina.com/Documents/products/technotes/technote_denovo_assembly_ecoli.pdf)
(see also the [Sequencing technologies](../Seq_tech/sequencing_tech.md)
section). The individual parts of the genome that could be reconstructed without
any issue will be present as contigs - contiguous sequences. Some assembly tools
analyze the read data further and try to organize contigs to make scaffolds. In
a scaffold, the contigs are in the order that the assembler thinks they should
be in, and there will be Ns present as place holders between the contigs to show
how far apart the assembler thinks the contigs are. The assemblers create
scaffolds by examining the read data and use the pairing information to order
the contigs into scaffolds and to estimate what the distance between the contigs
might be. There would then be scaffolds present in the fasta file. Please note,
some assemblers have a default setting for the minimum gap in a scaffold length.

### Estimating genome coverage

For assembly, it is important to have reads covering all bases, and in
sufficient quantity. In order to assess if this is the case, it is possible to
calculate the approximate coverage of the sequenced genome before an assembly is
created. For this calculation, an estimate of how long the “real” genome is
likely to be is needed. Frequently, the length of a closely related reference
genome can be used.

Coverage = (number of reads * read length) / estimated genome length

Example:  
_Listeria monocytogenes_ genome length: 2.944 Mbp  
Number of reads: 1 400 000 (paired-end)  
Read length: 150 bp  
Coverage = (1 400 000 * 2 *150) / 2 944 000 = 143  

I.e. the expected coverage for this genome is 143. This is frequently written as 143x coverage.

For assemblies from Illumina data, it is commonly recommended to have a coverage
between 50x and 100x. Assembly software commonly does better with higher
coverage, but there can be deterioration in the results with coverage above 100x
or so since for most de Bruijn graph assemblers (for instance SPAdes), higher
coverage can complicate and break apart the assembly graph.

### How does the assembly process work

There are two main types of methods in use today for assembly. The two types are
Overlap-Layout-Consensus (OLC), and de Bruijn-based methods ([check this
paper](https://academic.oup.com/bfg/article/11/1/25/191455)). OLC methods are
more frequently used with longer reads, and was the commonly used method in the
first wave of sequencing, when reads were from 400-1000 bp long. With the advent
of short-read sequencing (i.e. 36-300 bp long reads), de Bruijn based methods
came to the forefront. OLC methods are again becoming more widespread due to
long-read sequencing becoming available.

Both methods use graphs to create the assembly. The two main features of a graph
are nodes and edges. Nodes are often depicted as circles, with the edges being
lines between the circles. The main difference between the two methods is how
reads are used to build the graph. In OLC methods, the reads are assigned to the
nodes in the graph. All reads are then compared all-against-all to discover
overlap. If there is sufficient overlap between two reads, an edge will be
created between the two nodes. This represents the overlap between the two
reads. The assembly is then created by walking along this graph and in the
process creating contigs. An OLC graph will contain as many nodes as there are
reads in the read set. 

In de Bruijn-based methods, the reads are chopped up into subsequences of length
k - these shorter pieces are called k-mers. This cutting into k-mers happens by
shifting a window of size k base by base along the reads, so that each k-mer
from a read will have an overlap of length k-1 with the preceding and the
following k-mer. The graph is built by assigning each k-mer to a node, and if
two k-mers have an overlap of k-1, an edge will be created between the two
nodes. Contigs are again created by walking along the graph and finding paths in
it that become contigs. A de Bruijn graph will have as many nodes as there are
unique k-mers in the read set. Therefore, a critical step is the choice of the
value of k. If k is small, there will be many connections between the nodes in
the graph, i.e. many overlaps between k-mers will be found. However, this
increases the chance of nodes and edges being introduced in the graph due to
overlap between random k-mers, and this can contribute to the assembly
fragmentation due to the graph becoming very entangled. If k is too long, the
chances of detecting overlapping sequences decreases, and this can also lead to
assembly fragmentation. As an attempt to get a good compromise between these
factors, several assembly programs (e.g. SPAdes) have implemented a system in
which different k-mer sizes are used iteratively and in the end a combined
genome assembly is generated.

The main difference between the two methods lies then in how the reads are being
used to build the graph. These differences have as their main consequence how
the complexity of the graphs increases. While OLC graphs do not depend on the
k-mers but on the number of reads, they tend to increase complexity with
increased read coverage. By opposite, de Bruijn graphs deal very well with the
high coverage of NGS data (because it does not imply an increase in the number
of nodes), but the size and complexity of the target genome (e.g. presence of
repetitive regions) may have a great impact on the performance, as will also
sequencing errors.

### Assumptions made in the assembly process

There are certain assumptions that are made when performing assemblies. The main
assumptions are:

**All bases are sequenced**: it is assumed that all bases in a genome are
present in the reads from that genome. If not, that region will naturally not be
present in the assembly, and it will lead to breaks in the assembly. Several
studies have reported some bias in the sequencing data, which can be related,
for example, to the read starting position, the GC content, or the protocol of
library preparation ([check this
paper](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0157033#pone.0157033.ref005)).

**Sufficient depth of coverage**:  it is assumed that there are a sufficient
number of reads that cover each base in the genome, this reflects the minimum
number of times that a base has been sequenced. Many of the assembly methods
actively use evenness of coverage when trying to resolve repeats.

**Errors are random**: it is assumed that any sequencing errors appear randomly
in the reads. If they are, it is likely that these errors will be eliminated in
the assembly process, either by error correction processes, or simply by the
other reads from that region forming a consensus that eliminates the error. If
they are not random, they can form an alternate contig, thus giving rise to two
contigs from the same region. Errors may have great impact in de Bruijn graphs
because they contribute to the increase in the number of nodes and edges. These
issues can be alleviated by good QC analysis and trimming during data
preprocessing.

### The influence of read length

Read length is a determining factor on the outcome of an assembly process. This
is due to the fact that in an assembly process it is not possible to resolve
repeats that are longer than the read length. This is exemplified in the
[section about paired-end sequencing](../Seq_tech/sequencing_tech.md#Paired-end-sequencing). 
This is also known as Ukkonen’s condition, and for a deep dive into
that, [please read this
blogpost](https://liorpachter.wordpress.com/2013/10/08/ukkonens-condition-for-assembly/).
This is the main reason why long read sequencing has been gaining ground the
last years, longer reads give assemblies with fewer contigs. For microbial genomes it is not uncommon for long read data to result in fully closed genomes.

### Some commonly used assembly programs

The amount of sequencing assembly tools increased drastically with the advent of second generation sequencing instruments. The first assemblers that were available were primarily Overlap-Layout-Consensus tools, such as [Newbler](https://en.wikipedia.org/wiki/Newbler) and [Celera](http://wgs-assembler.sourceforge.net/wiki/index.php), both now discontinued. These were used for Sanger sequencing and for sequences from 454 machines, which were generally 400-1000 bp long. With the advent of Illumina sequencing, whose first reads were 36 bp long, de Bruijn based methods came to the forefront. This development was started by the [velvet software package](https://en.wikipedia.org/wiki/Velvet_assembler), which uses a fixed k-mer size for assembly. After the release of velvet in 2008, many different assemblers were created and got varying levels of use (for an early review, [see this paper](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0017915). In 2012 the program [SPAdes](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3342519/)  was released, this tool uses different k-mer sizes (and other tricks too), which means that it frequently produces more contiguous assemblies than velvet does. This program gradually took over as the main assembler for microbial data.

For short read data, there are today four tools in common use, three of which involve SPAdes in some way. The first is naturally SPAdes itself. Then there is the [software package shovill](https://github.com/tseemann/shovill) that uses SPAdes as its assembly component. Shovill does downsampling of the data to avoid overloading the assembly graph, and also includes trimming, so it is a good choice for a one-stop-shop assembler. It is also known to be fast, which increases its usefulness for bulk analysis. [The tool Unicycler](https://github.com/rrwick/Unicycler) also uses SPAdes in its internals, and works as a SPAdes optimizer when only used on Illumina data. Unicycler is also a hybrid assembler, and can thus be used in cases where both long and short read data is available. Last but not least, there is [SKESA](https://github.com/ncbi/SKESA) which was created by the NCBI. This assembler has as its goal to be a bit conservative and rather break up at repeats to avoid mis-assemblies, and to be fast. 

PacBio was the first of the 3rd generation platforms that came on the market with long single cell reads. With long reads, OLC methods again came to the forefront. The tools that came into common use were frequently modifications and adaptations of previous OLC software, such as [canu](https://github.com/marbl/canu) which is a fork of Celera. Today, for PacBio the most commonly used assemblers are [HGAP](https://github.com/PacificBiosciences/Bioinformatics-Training/wiki/HGAP), which was developed by Pacbio, and also canu. Oxford Nanopore, the most commonly used tools are Unicycler and canu. 

For more on what tools are in use, [see this
paper](https://www.frontiersin.org/articles/10.3389/fcimb.2020.527102/full).

### Assembly quality evaluation

Once a genome has been assembled, the assembly has to be evaluated to see how good it is. It is common to evaluate this on three different features:

**Completeness**: Completeness shows to what extent the entirety of the genome has been captured in the assembly. This can be difficult to quantify, since each new genome is a novel entity unto itself. However, this can be estimated by examining to what extent genes that so far seem universally present in a specific type of genome can be recovered from the assembly. This can be done with tools such as [CheckM](https://ecogenomics.github.io/CheckM/) or [BUSCO](https://busco.ezlab.org). The latter gives an estimate of how many of a set of expected genes are either found in a complete form, a fragmented form, or not found at all. 

Another measure of completeness is how the reconstructed genome length compares to the expected genome length. This can be challenging for genomes of species like _Escherichia coli_, where the known span of genome lengths vary with approximately 1M bases. 

Another alternative is the comparison of the k-mers present in the final genome assembly with the k-mers present in the trimmed and cleaned fastq files with programs like [KAT](https://kat.readthedocs.io/en/latest/). Such an approach can give an idea not only of the missing portions of that particular genome, but also of the presence of non-collapsed repetitive regions in the assembly. 

**Contiguity**: Contiguity shows to what extent the assembly process is capable of knitting together the reads into a contiguous sequence. The aim is to have as few and as long contigs as possible, while avoiding mis-assemblies. Contiguity is frequently measured as N50. This value is the length of the longest contig where the contigs longer than this contig in total contains 50% or more of the assembled bases. 

Example of what N50 is:  
Let’s say an assembly has 7 contigs, and they have these lengths:  
120, 170, 320, 550, 750, 760, 850

The total length is 3520, and the length halfway point here is 1760. Thus, the
N50 becomes the contig length which, when counting from the longest to the
shortest, tips over 1760 bases. In this case that is 750 - the contigs with a
length of 750 and longer in total contain more than 50% of the bases of the
assembly.

A variant of this is the LG50 or L50. In this case the length of the assembly in
the calculation above is replaced by an estimate of how long the genome should
be. More on these measures, and other similar measures are available
[here](https://en.wikipedia.org/wiki/N50,_L50,_and_related_statistics).

**Correctness**: Correctness shows to what extent the bases and their order in the
assembly reflect what is in the sequenced genome. This is per definition
impossible to truly measure since the actual sequenced genome is not a directly
observable entity. Common errors that can be looked for are mis-joins, repeat
compression or expansions as well as indels. Such errors can either be detected
by comparing to a reference (with for instance [QUAST](https://github.com/ablab/quast)), or by doing an internal
comparison between the reads and the genome assembled from those reads (as done
by [REAPR](https://genomebiology.biomedcentral.com/articles/10.1186/gb-2013-14-5-r47) or the nuc-suite of tools). 

### Genome annotation 

DNA or genome annotation is the process of identifying the location of functional regions in DNA / genomes sequences ([Wikipedia](https://en.wikipedia.org/wiki/DNA_annotation)) and subsequently designating a function to this region. Functional regions can consist of both coding regions and non-coding regions, and they can be identified using a variety of tools that are trained to detect  rRNA, tRNA, non-coding RNA, protein coding genes, CRISPR regions and more. The input for this process is a fasta file containing the DNA sequence and which the annotation tools use to identify the location of various functional regions. That information can be stored inside a General Feature Format ([GFF](https://en.wikipedia.org/wiki/General_feature_format)) file or in a Genbank / EMBL / DDBJ format file. The former only contains information on the location of functional regions, but does not contain the DNA sequence nor the translation of protein coding genes. A Genbank file (or EMBL / DDBJ) contains the complete genome sequence, as well as the location of the coding regions with the translation of those regions when applicable (e.g. Protein coding genes).
Specialized algorithms exist to predict the presence of each type of functional region. This can happen in one of two main ways: either through _de novo_ gene prediction, or through homology searches. Both of these methods have one thing in common: they both presuppose the availability of already annotated genes that may be present in the genome that is being examined. With the amount of sequencing done today, such a data set is often available. However, in situations when new species, or possibly even new genuses are being examined, this can be an issue.

In either case, the data that is available is then used to predict the functional regions in the genome at hand. If prediction is done directly via homology searches, this commonly proceeds through blast searches where the available genes are searched for in the genome. If prediction is done _de novo_, the available data set is instead used to train a model that is subsequently used to search the genome for genes. This is the tactic employed by [Glimmer](http://ccb.jhu.edu/software/glimmer/index.shtml) and [Prodigal](https://github.com/hyattpd/Prodigal), which are two of the more commonly used prokaryotic gene finding tools. These tools extract a wide range of information from their training sets to determine protein coding regions such as: The presence of start and stop codons usage, ribosomal binding site (RBS) motif, GC content bias, hexamer coding bias etc. _De novo_ gene finding tools frequently come with default training models. However, since these factors can differ from species to species, a species specific training file can be created from other annotated genomes from that species and used for prediction for new genomes from that species. 

Once the various types of genomic features have been identified, they have to be assigned a function. For some types of regions the functional assignment is baked into the finding tool. For instance, for finding tRNAs, the fact that the found regions are tRNAs are a given since that is what was searched for. Functional assignment is predominantly an issue when it comes to assigning a function to proteins. If homology searches were used for gene prediction, the gene function is frequently then “lifted” from the search onto the found gene. If _de novo_ methods have been used, this functional assignment is then a separate step, commonly involving homology searches using blast. In either case, this highlights the need for a well curated and a well selected database for these searches. 

For command line prokaryotic genome annotation, the most commonly used tool today is likely [PROKKA](https://github.com/tseemann/prokka). This tool uses prodigal for gene prediction, along with other specialist tools for finding rRNAs, tRNAs and other genomic features. For functional assignment, this tool does several different kinds of searches in a hierarchical manner. First a core set of curated and included with the program databases is searched using blast. If a match is found, then the function is lifted over. If the user wants to, it is possible to add their own core database to this set of annotated databases. Next, for the genes who did not gain a function through this step, a different kind of search using profiles is done, using [HMMER3](https://github.com/EddyRivasLab/hmmer). This program allows for more distant searches than blast. In addition, the [PROKKA](https://github.com/tseemann/prokka) program allows a user to supply their own annotated proteins via the “-proteins” option. 

Another commonly used tool is the web based [RAST](https://rast.nmpdr.org/) system. RAST has as its core a set of subsystems, which are functionally related proteins, and these proteins have a “FIGfam” associated with them, which is a gene family which have been curated by human experts in the [FIG group](http://www.thefig.info/). When doing genome annotation, RAST starts out by annotating some specialist types of genes first. Then, it uses GLIMMER do do ab initio gene prediction, these are then used to find the 30 most closely phylogenetically related genomes. In addition, k-mer searches are done towards all of the subsystems in RAST to find genes that seem to be present in the genomes. These subsystems, together with the subsystems in the 30 most related genomes are then used to train a GLIMMER model, and the genome is then searched with this model. Genes that are not annotated in this process are blast-ed against the 30 most related genomes and annotated that way.  

Genome annotation is a complex business, and many methods and tools exist. Only two of the available tools have been mentioned here. [This paper](https://pubmed.ncbi.nlm.nih.gov/32962098/) goes into depth about gene prediction and annotation, including how these processes work for eukaryotic genomes. That paper also includes information on genome visualization, and tools for assigning more high level functions.


## Sequence read mapping

### How mapping works

Mapping is used for many different purposes, such as contamination removal, SNP
calling, and for finding specific genes such as through MLST typing and
serotyping. Mapping is the process by which reads are placed onto a reference
sequence. This sequence can represent the whole-genome of one or multiple
organisms (_de novo_ assembled or retrieved from public databases), multiple
genes, or any other DNA sequence of interest. During mapping a read is matched
up with a location on a genome provided the read is identical or nearly
identical to the sequence in that location. Consequently, mapping is only
appropriate when it is presumed that the reads are very similar to the
reference. Due to this, mapping is rarely done with long read data due to the
error profile of long reads. For long reads, alignment processes such as blast
are often used instead. 

The results of mapping are output in a [SAM or a BAM (Binary
SAM)](https://samtools.github.io/hts-specs/SAMv1.pdf) format, which specifies
the coordinates in the reference sequence where the similarity between the read
and the reference sequence is the highest, together with other relevant
information about the read mapping. For instance, mapped reads commonly receive
a mapping score detailing how well it mapped. However, the interpretation of
that score varies widely with the tool used for mapping. It should be noted that
since Illumina reads are quite short, it is possible that a read might have two
or more equally well fitting locations on the genome. These reads are then
called “multimapping” reads. The fact that they are multimapping should be
evident in the output. The “CIGAR string” is also included, which is a shorthand
description of how much of the read mapped, and how many mismatches there were.
For paired-end data it also includes information about the mapping
characteristics of the other read in the pair. 

During mapping the reads might end up being “clipped”, either hard or soft clipped. This will be evident in the output and can be seen in the CIGAR string.
With hard clipping, the parts of the read that did not match are removed from
the read, while in soft clipping the clipped region will be present, but will be
masked so that other downstream tools don’t use that part. As read mapping can
be done using any DNA sequence as a reference, this strategy can be used for
contamination checking and filtering, in that it can be used to figure out if a
certain contaminant (e.g. PhiX genome) is present (for instance, any remaining
PhiX reads will map to the PhiX reference sequence). If so, the reads associated
with the contaminant can be removed. In cases such as MLST finding and serotype
finding, where the main focus is a specific set of target genes (see [MLST
section](../Typing/MLST.md)), the reads are commonly mapped to a database of sequences comprising
the genes of interest and not the whole genome sequence. The reads that then map
to a reference sequence (a MLST sequence, a serotype gene, an AMR gene etc),
will show what gene is present in the data. After mapping, SNP calling (see [SNP
calling section](../Clustering/snp_calling.md)) can highlight any nucleotidic differences between the reads and
the reference, being useful to determine SNPs (and INDELs) across the genome
when a whole-genome reference is used, or to determine allele-specific variation
in the MLST, AMR or serotyping analysis. 

It is important to note that read mapping can be performed for multiple samples
towards the same reference (single sequence or a set of sequences, often
referred to as a database). Therefore, for downstream analysis all the regions
of interest will be indirectly aligned between the different samples. I.e.,
position X in sample A corresponds to position X in sample B, and any
information relative to that position can be compared without the need of a
multi-sequence alignment.

There are many mapping tools available today. However, among the ones more
commonly used are [BWA](https://sourceforge.net/projects/bio-bwa/) and
[Bowtie](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml). In addition,
BBMap from the [BBTools](https://jgi.doe.gov/data-and-tools/bbtools/) package is
a popular choice. Read mapping results (BAM files) can be visualized with
so-called genome browsers, e.g.
[IGV](http://software.broadinstitute.org/software/igv/), where the user can have
a visual idea of the genomic features of a given sample or even multiple samples
as long as their reads were mapped to the same reference.

### How to choose a reference genome?

A “reference” allows for creating a coordinate system (the reference map) that
can be used to compare samples at each position. This reference map can be used
for producing multiple-alignments and variants files required for downstream
analyses. A reference genome is usually chosen because the genome is complete,
annotated and the sequence has been validated. The reference sequence  is
usually chosen as a representative of the species/or taxa under study. This
choice strongly influences the precision of the SNP calling tools, and should be
chosen to be “as similar as possible” (closely related) to the isolates under
study ([Bush et al. 2020](https://academic.oup.com/gigascience/article/9/2/giaa007/5728470)). A good source are genomes from refseq. Be also aware
of whether the genome contains plasmids.

If a reference from a specific strain or sequence type is needed,
[Enterobase](http://enterobase.warwick.ac.uk) offers options for searching for
specific genomes. Note some options are only available for logged in users. In
Enterobase, organisms of interest can be selected, such as _Salmonella, E. coli,
Streptococcus_, and others. After selecting a species, specific strains can be
searched for using the search fuctions “search strains” or “find STs”. For
sequence type searchers, for some species the schema then has to be selected.
Data can subsequently be filtered in the resulting table to get isolates from
specific continents, matrices, year, etc. The data can also be downloaded (see
the Data dropdown menu) if there is a wish to filter the data in separate
programs such as R or excel. Note: Make sure that the experimental data, on the
right of the separator, is presenting the wanted information, these will be
downloaded with the other info. Several types of experimental data, including
MLST and cgMLST data is available.  

As an alternative (or if a good genome assembly is not yet available for the
species that is being studied), genome assembly of the samples at hand can be
done (see [_de novo_ genome assembly section](#Assembly-and-annotation)), and one of these can be selected as
a reference. This genome should preferably be the one that appears as the most
complete, i.e high N50, few contigs, etc. Fast clustering, for instance using
[popPUNK](https://poppunk.readthedocs.io/en/latest/) can be done to figure out
which ones of the samples are at hand would be “equally related”, i.e. a
centroid in the similarity space of the samples at hand.

## BLAST - sequence search
Basic Local Alignment Search Tool ([BLAST](https://en.wikipedia.org/wiki/BLAST_(biotechnology))) is a method (and a program) that allows searching in sequence databases. These databases can contain whole-genome sequences, a set of genes or proteins, or any other DNA sequences of interest. The method takes in one or several query sequences (e.g. the predicted protein-coding genes of a genome assembly, check [_de novo_ genome assembly section](#Assembly-and-annotation)), and tries to align them in the sequences of the provided database (e.g. the nucleotide sequence database of NCBI). When it finds corresponding matches (similar sequences), it reports the name of the match, the respective percentage of identity, length of the alignment, query coverage, e-value, and other important scores. It is worth noting that these matches may be partial, both on the query side and the database side. That is, if searching with a 100 bp query sequence, it is not given that the matching region will cover the entire 100 bp query sequence. This is important when using it to search for genes. Therefore, it is important to post-process the results to be able to infer homology relationships from the alignment. The BLAST tool enables the user to set criteria on the results, such as lower values for e-value, query coverage, etc, which will reduce the number of reported hits. BLAST can be used to align nucleotide to nucleotide sequences (BLASTn), protein to protein (BLASTp), protein to nucleotide (tBLASTn) or nucleotide to protein (BLASTx). 

BLAST is commonly available online as a tool on sites offering access to sequence data. The most well known site is the [NCBI website](https://blast.ncbi.nlm.nih.gov/Blast.cgi). BLAST can also be downloaded and installed as a [command line tool on Windows, Linux and Mac](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=Download). For local BLAST a database has to be generated beforehand. This database can be any set of sequences/genome(s) of interest. Public databases (e.g. non-redundant database or uniprot database), are available for download in this [ftp](https://ftp.ncbi.nlm.nih.gov/blast/db/).

**Reciprocal Best Hits** (RBH) are a common proxy for orthology in comparative
genomics. A RBH is defined as when two sequences, each from its own genome, find
the other as the best scoring match when searched for in the other genome. That
is, if a BLAST search is done between the set of genes from genome A towards a
database comprising the genes from genome B, and vice-versa, and genes A1 and B1
are the best hit of each other in both cases, they are RBHs. 

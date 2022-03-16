# cgMLST

Core genome multi-locus sequence typing is an extension of the original
seven-loci MLST method ([Maiden et al.
2013](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3980634/), [Lüth and al.
2018](https://www.sciencedirect.com/science/article/pii/S092422441730540X)).
Conceptually speaking cgMLST works in the same way as MLST, however, many more
genes/loci are being used. For instance, one popular set of genes that is used
as a schema for _Escherichia coli_ consists of 2,513 genes. As for 7-gene MLST,
there are different sources for the schemas. Schemas are defined as a set of
loci/genes and their respective alleles. There are also different tools in use
for finding the alleles which might not always produce perfectly comparable
results. One notable difference between 7-gene MLST and cgMLST is that there is
frequently no sequence type. Since so many genes are used, and since there are
so many alleles possible for each gene, translating that into a sequence type
label becomes difficult. cgMLST is thus primarily used as basis to compute
pairwise distance measures matrices based on the number of shared alleles (eg.
hamming distance), distance measures can then be used for clustering. However,
recently methods have appeared that do allow for assigning a sequence type, this
is described below.

## Schemas and nomenclature servers
As with 7-gene MLST, a schema is needed for doing cgMLST. Schemes provide a list
of loci (including an identifier), the set of alleles (including sequence for
the allele) that are defined for each locus as well as an allele identifier.
Schemes are designed for each bacterial pathogen and therefore cannot be used
for a species it has not been designed for. Several schemes might have been
designed for specific species. In such cases,  the allele identifier of the
different schemes will not be directly comparable even for alleles that might be
included in both schemes ([Uelze et al.
2020](https://link.springer.com/article/10.1186/s42522-020-0010-1)). 

The process of typing with cgMLST works similarly as it does for MLST. The
alleles in the schema are searched for in the genome. If an allele is found, its
locus id ID and allele number is logged for the genome. However, the two
processes differ when it comes to handling novel allele variants. For MLST, it
is common to submit the allele to a nomenclature server, where it will be given
a centrally assigned number. For cgMLST this process may happen locally, i.e.
within the system of whomever is using the tool.  

Database servers give access to schemas and allow for synchronisation of alleles
designations when new alleles are added to the schemes, and synchronisation or
submitting of newly discovered alleles to the scheme. The more commonly used
servers  are:

- [Enterobase](https://enterobase.warwick.ac.uk/)
- [PubMLST](https://pubmlst.org/)
- [ChewBBACA online: Chewie-NS](https://chewbbaca.online/)
- [Ridom SeqSphere](https://www.cgmlst.org/ncs)
- [BIGSdb Pasteur Institute](https://bigsdb.pasteur.fr/)

When new alleles for a locus in a schema are discovered, the allele sequence is
added to the scheme and is given a numerical ID. This number is commonly
attributed sequentially. Analyzing isolates that contain new alleles in a
different order will lead to differences in attribution of allele ID numbers for
the same allele. Therefore, the numbering of cgMLST typing might not be
comparable between laboratories that are keeping local typing databases, even
for laboratories that use the same scheme, due to possible divergence of allele
numbering after local database initiation ([Deneke et
al.2021](https://www.frontiersin.org/articles/10.3389/fmicb.2021.649517)), unless local
databases are in constant synchronisation with nomenclature servers. Therefore
there is a growing interest in developing hash-based cgMLST. Hash-based cgMLST
transforms the typed alleles sequences into a hashID (a compressed
representation of the sequence in form of a string). Due to the way hashes work,
this means that each allele will have an unique identifier This allows direct
sharing of typing results that are independent of allele numbering and thus
directly comparable between laboratories without relying on centralised and
curated nomenclature servers ([Eyre et al.
2019](https://journals.asm.org/doi/10.1128/JCM.01037-19), [Deneke et
al.2021](https://www.frontiersin.org/articles/10.3389/fmicb.2021.649517)). Thus hash-based
cgMLST typing is as such not a new sequence typing method but a new way to allow
optimization of data exchange.

## cgMLST resources
cgMLST software generally speaking works in the same way as MLST methods do: the
software compares the sequencing data for an isolate, either in the form of
reads or an assembly, to a set of alleles. If an allele is located in the
sequencing data, it is recorded as found in that isolate. Similarly to MLST,
there are two main approaches to finding cgMLST alleles, either based on using
BLAST on an assembly, or using the reads directly somehow against an allele
database. Another variable is whether the tool is available as a stand-alone
installable tool, or whether it is web-based. The [xMLST tools](mlst_typing.md)
page contains information about several commonly used tools. 

## Factors to consider

### How is allele calling performed? 
The nature of the starting material used for cgMLST typing, ie. reads or draft
assemblies influences how the calling process and therefore which algorithms for
calling can be used. 

### Assembly based methods
Loci defined by a cgMLST scheme usually are delimited by a start and stop
codons, eg. coding units. The size coding genes and thus of alleles might exceed
the read lengths obtained by NGS. This is most likely why most cgMLST typing
tools are assembly based. 

Verifying that start-stop codons are recovered prior to allele typing ensures
that single gene units are compared to the scheme. However, failure to detect
some loci may occur if there is a lack of a proper start-stop codon due to
genome mis-assembly or assembly fragmentation, where eg. the start and stop
codons might occur on different contigs or be frame shifted. Most software used
for cgMLST typing flag loci for which there are potential loci matches but from
which compliance with the start-stop codon condition failed. This quality
assurance control might provide an indication of poor typing quality due to
insufficient assembly quality, particularly if many loci are flagged as such.
Those flags are usually visible in the summary table or can be output as a
separate file. Note that new alleles in ChewBBACA are flagged as NEW-xx the
first time it is encountered, the “NEW-” part must be removed as well as other
indicative flags prior to computing distances matrices. 

BLAST based calling methods are usually used for assembly based cgMLST typing.
Allele calling using BLAST methods employs the similarity of the sequences both
in alignment and size (length), with a predefined threshold criteria for allele
calling. Performance is generally optimized for example by using a hierarchical
blast search strategy, in several passes. It can for instance allow for rapidly
selecting CDS that perfectly match scheme alleles, which can be followed by a
similarity search for the remaining CDS, thereby determining if new alleles
should be called or if loci must be considered as missing ([Silva et al.
2018](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5885018/)). Alleles are
usually considered as missing if they differ from a given length and
similarity/homology threshold to the previously identified alleles, eg. within
98% of identity and 98% of the total length of a known allele. This implies that
if not all the allelic diversity has been recovered during scheme creation, some
loci might be flagged as missing while they would have been found during
reanalysis at a later stage when the database had been augmented. This, because
the nomenclature allele database has been populated with increasingly divergent
alleles, as illustrated in  [Deneke et
al. (2021)](https://www.frontiersin.org/articles/10.3389/fmicb.2021.649517).

### Read based methods
MLST callers (eg. reviewed in [Page and al.
2017](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000124))
that employ reads as input might be used for cgMLST based typing. MLST callers
that use this approach map the reads to a set of reference alleles, and evaluate
the “stack” or pileup of reads that map to each allele and use this to determine
the type (eg. MOST: [Tewolde et al
2016](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4991843/), SRT2: [Inouye et
al.
2014](https://genomemedicine.biomedcentral.com/articles/10.1186/s13073-014-0090-6)).
The frequency of variants in the pileup are often used to control for potential
contamination and/or ambiguous allele matches. Read mapping with targeted local
assembly of reads mapped to the alleles of the schemes prior to typing allows
for verifying if alleles in the isolate are complete. This is an approach that
has been developed in ARIBA: [Hunt et al.
2017](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5695208/)). However, MLST
callers that use read mapping approaches usually require substantial compute
resources when large cgMLST schemes are employed. Therefore, alternative tools,
designed to specifically handle the large cgMLST schemes might be better suited
to the task ([Feijao et al.
2018](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000146)).
Kmer based methods allow rapid and low compute resource demand in comparison to
mapping based typing methods. They allow for comparing the kmer composition of
the alleles in the schemes that are transformed into a hash database, to the
kmer composition of the reads. The general idea is that an allele is typed when
a representative allele of scheme at a given locus maximizes the number of kmers
that is also recovered in the reads. There are different variations of kmer
typing algorithm , eg. kmer indexing and counting of kmers at the middle of the
reads ([Gupta et al.
2016](https://academic.oup.com/bioinformatics/article/33/1/119/2525695?login=true))
and kmer voting ([Feijao et al.
2018](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000146))

### Nomenclature storage
Nomenclature is hosted on web servers. It is possible to download schemes for
local usage, however, synchronisation of eventual new discovered alleles that
are called locally is not always straightforward. Some nomenclature servers
allow for directly synchronizing schemes (eg. Chewie-NS) while other offer the
possibility to submit new alleles via API (eg. BIGsdb), while other appear to
have disabled the possibility to synchronize schemes or submit new allele calls
via API, in which case the only alternative to update those schemes would be by
running the analyses directly through their platform (eg. Enterobase).
Consequently, choice of analysis tool might also be influenced by local
constraints and aim, eg. If the aim is to analyse data locally, using a
nomenclature server that allows continuous synchronisation could be considered,
or optionally hash-cgMLST solutions to share data with other labs if needed
could be adopted. 

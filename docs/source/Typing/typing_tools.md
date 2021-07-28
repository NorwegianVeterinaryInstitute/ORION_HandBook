# xMLST typing tools

This page lists several tools that are used for MLST and cgMLST finding. Some
tools do both, while some are specific for either.

## MLST and cgMLST tools

### BIGSdb software and database
The Bacterial Isolate Genome Sequence
[(BIGSdb)](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-11-595) is a software that offers a large range of pathogen population analyses.
BIGSdb is hosted by [PubMLST](https://pubmlst.org/), a website that allows
access to curated open-access databases of many microbial species (Jolley et al
2018).  PubMLST also serves as nomenclature server for both MLST and cgMLST.
cgMLST analyses are not available for the whole range of species, due to a lack
of scheme developpement for many species. PubMLST comes with a RESTful
Application Programming Interface that allows querying, retrieval,
synchronisation and submission of allele and profile definitions from and to
BIGSdb.  Several web services and software tools (Enterobase, Bionumerics,
SeqSquere+, CLC, MLST-CGE, MOST, GoSeqIt, MLSTcheck, mlst, SRST2, stringMLST,
MLStar, Krocus, Smartgene) rely on tools that utilise data hosted by PubMLST
(Table 2 in Jolley et al. 2018). In cases where PubMLST is not the authoritative
database for a typing scheme developed for a specific species, eg. Escherichia
sp., the scheme is synchronized with the authoritative database, eg. Enterobase.

BIGSdb can be used through the PubMLST interface. Sequences must be uploaded to
a public repository or the website. Upon website upload, they can be kept
private until eg. publication. The website interface allows to launch analyses.
Synchronisation to the nomenclature server is administered by BIGSdb. Moreover,
it is also possible to install the software locally. An Application programming
interface (API) allows different tools to interact with the databases hosted at
PubMLST, eg. for synchronizing allele definition and nomenclature, and
submitting new alleles to curators (the documentation is available at
https://bigsdb.readthedocs.io/en/latest/). 

Typing is based on an assembled/draft genomes using BLAST query against the
database that contains the scheme definition. To optimize efficiency, the BLAST
query is limited to alleles that are representative of a set of similar alleles
at each locus, also called “exemplar alleles”. “Exemplar alleles” represent all
alleles that are within 10% sequence identity of all known alleles for each
locus previously identified. Alleles are identified by exact match and scheme
fields are returned. Best matches are reported for other alleles, and
differences with the best match are reported. New alleles must be within 98%
identity and 98% of the total length of a known allele, contain start and a
terminal in-frame single stop codon. Finally, BIGSdb allows computing pairwise
distance matrices and performs single-linkage clustering, allowing to define
clusters at a defined allelic-difference threshold (Jolley et al 2018).

### Enterobase
EnteroBase is an integrated software environment for enteric bacteria population
structure analysis, which is accessible through their website. Enterobase offers
online resources for typing, incl. cgMLST typing ([Zhou et al.
2019](https://www.biorxiv.org/content/10.1101/613554v3)). Currently different
typing schemes are implemented for [8 different bacterial
species](https://enterobase.warwick.ac.uk/). Enterobase also hosts the
nomenclature schemes and offers the possibility to download those schemes
(alleles and STs profiles). However,  the possibility of synchronizing schemes
stored locally via API seems to have been removed. Sequencing data (raw reads)
must be uploaded to the website or to public repositories. It is also possible
to provide assembly data by using a local installation of enterobase for
assembly (see [local
enterobase](https://local-enterobase.readthedocs.io/en/latest/)). As per today,
raw reads are kept private but assemblies can be kept private but are made
available to Enterobase developers (see [Enterobase terms of
use](https://enterobase.readthedocs.io/en/latest/enterobase-terms-of-use.html) &
[GDPR](https://enterobase.readthedocs.io/en/latest/GDPR.html)) also it is
encouraged to make your data publicly available at once. Typing is done on
assembled genomes using a combined strategy using BLAST and USearch ([see
description
here](https://enterobase.readthedocs.io/en/latest/pipelines/backend-pipeline-nomenclature.html)).
It appears that only alleles that fully match alleles predefined in the scheme,
while potential new alleles, partial alleles and duplicated alleles are flagged
with a negative tag. cgMLST typing results can be run through HierCC, a
multilevel HIERarchical Clustering of CgMLST that allows finding optimal
thresholds for performing cluster assignment ([Zhou et al.
2021](https://academic.oup.com/bioinformatics/advance-article/doi/10.1093/bioinformatics/btab234/6212647)).
Visualisation of clusters can be used with Minimum spanning tree (grapeTree
implementation, [Zhou et al. 2018](https://genome.cshlp.org/content/28/9/1395)).


### Bionumerics
Bionumerics is proprietary software that is installed locally that performs both
MLST and cgMLST typing on assemblies and/or on reads.  Typing schemes can be
retrieved from nomenclature servers, incl. BIGSdb or Enterobase. Automatic
scheme synchronisation as well as automated submission of new alleles is
supported. Users also have the possibility to define their own
schemes/sub-schemes. Allele mapping tool allows conversion of alleles ID tags
between schemes that share identical alleles but use a different nomenclature
system. Quality criteria for allele calling and automatic submission to the
nomenclature database are adjustable. Default settings appear to be imported
from predefined nomenclature databases. New alleles can be automatically
submitted to the reference database, following either default nomenclature
database settings (e.g. requirement of start/stop codon for alleles within
coding regions, excluding premature stop codons, using a minimum homology
threshold of 85% and allow a maximum number of gaps of 999 to to define new
alleles) or by adjusting those settings at convenience. 

Assembly based typing uses a BLAST approach to identify matching alleles to a
reference (Blast Allele Finder). Typically one reference allele sequence is
used, but in some cases (ie. different uses of frames several references can be
defined.  Default parameters for allele calling are defined by the database
allele curator. Settings are adjustable at convenience, incl. BLAST word size,
minimum gap similarity and allowance of gapped alignment. Alleles are typed when
a 100% sequence identity id found with a pre-existing allele, potential new
alleles that satisfy the automated submission criteria are flagged as
“tentative”, in which case the automatic submission process is initiated. If and
when the new-allele is accepted, then the flagg status changes to “accepted”. If
a potential allele does not satisfy the automatic submission criteria, it is
flagged as “closest match: x” where x is the reference sequence to which the
potential allele has the highest sequence identity (SI), in which case SI is
also provided. Because full CDSs delimited by start/stop codons are required for
allele typing (default parameter), it is possible that some alleles are missed
for genes that overlap between contigs.

The assembly free (reads-based) calling method is kmer based. Adjustable
settings are: kmer word size, minimum coverage, minimum forward and reverse
coverage. This method should theoretically allow detection of all alleles
present in the sample. Missing loci are expected to be truly missing (at the
defined settings). Multi-copy loci are typed as separate allele calls. All
alleles passing the defined quality criteria are used for detection. A 100%
sequence identity (SI) is required for allele calling. Partial matches are not
further considered for calling, however SI to the best matching allele is
registered. Keyword coverage (the number of keywords found by the algorithm for
the allele or allele with lowest number when multiple alleles have been found
for a locus) is provided.

Both typing methods, at the assembly and reads level are seen as complementary,
as it is expected that some drawbacks from each method are compensated. When
both methods are used, a consensus call is performed for all loci. In case of
ambiguity, choice is given to retain the allele with the lowest common allele ID
or to be defined as absent. Summary table can be manually filtered for
inspection. 

Hierarchical clustering and basic phylogenetics tools and minimum spanning tree
visualisation are also available in Bionumerics.  

### SeqShere+
Seqsphere + is a proprietary analysis software that is installed locally. It
allows MSLT and cgMLST scheme creation or typing using predefined MLST and
cgMLST. It can use predefined schemas from PubMLST cgMLST typing schemes are
hosted on a [Nomenclature server](https://www.cgmlst.org/ncs), this server is
also publicly available. Sparse documentation makes it difficult to assess in
detail how the tool works, but it appears that all samples that enter the
database are automatically compared to previously existing samples, and close
matches are indicated. Typing is performed on assemblies using a BLAST approach.
A tagging system allows to indicate potential alleles that failed calling and
potential new alleles. Phylogenetic tools, minimum spanning tree, an epi curve
and GIS mapping are available for visualisation and helping interpreting of
typing results. 

## cgMLST only

### chewBBACA
[chewBBACA](https://github.com/B-UMMI/chewBBACA) ([Silva et al.
2018](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000166))
is a locally installable command line based software developed for scheme
creation, evaluation and cgMLST/wgMLST typing. A nomenclature server
[chewie-NS](https://chewbbaca.online/), that can be accessed with REST API and
allows users to synchronize schemas from chewBBACA has recently been developed
([Mamede et al. 2021](https://academic.oup.com/nar/article/49/D1/D660/5929238)).
As per today, schemes for [10 bacterial species](https://chewbbaca.online/stats)
are available at/via chewie-NS. The analysis parameters that are required to
ensure compliance with the parameters used at scheme creation are associated,
stored and synchronized through chewie-NS. The server also allows database
snapshots to allow reproducibility of analyses: re-analyzing using a scheme as
it was in a previous analysis. 

ChewBBACA typing is done on assembled genomes (complete or drafts). Genes (CDSs)
are predicted using a [Prodigal](https://github.com/hyattpd/Prodigal) ([Hyatt et
al. 2020](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2848648/)) training file.
CDSs that are 100% identical to alleles present in the schemes are typed. The
remaining CDS are compared to the two most divergent alleles at each loci of the
scheme, using BLASTP score ratio (BSR) ([Rasko et al.
2005](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC545078/)). This to detect
alleles that are divergent at the nucleotide level but similar at the amino
acids level. Size validation step filtering (+-20%) allows identification of
valid alleles, new alleles or absence of alleles, and allows for tagging of CDSs
that do not fulfill the selection criteria to be considered as valid alleles eg.
paralogous CDSs, partial matches (see [chewBBACA
wiki](https://github.com/B-UMMI/chewBBACA/wiki/2.-Allele-Calling#allele-call-statistics-output-results_statisticstsv)).
This advanced tagging system allows detection of potential assemblies quality
issues, and also can allow detection of loci that are problematic in a
predefined scheme. The typing table can after removal of flags and after
cropping of the “NEW-” string from the flag for new alleles can be used to
compute the pairwise distance matrix that will serve as clustering basis. A
recently  developed pipeline:
[ChewieSnake](https://gitlab.com/bfr_bioinformatics/chewieSnake/blob/master/README.md)
([Deneke et
al.2021](https://www.frontiersin.org/articles/10.3389/fmicb.2021.649517/full))
allows to automate the full process of cgMLST typing, from draft assemblies (or
reads that are assembled with ), typing with ChewBBACA, reconstructing of the
pairwise allelelic distance matrix, reconstruction of a phylogenetic tree using
single linkage clustering, cluster membership assignment according to a
user-determined distance threshold. It also automatically produces a typing
report. Allele typing is reported in the form of hash-ID as this software has
been designed to allow direct comparison of alleles between laboratories while
bypassing the needs for a centralised Nomenclature server. 


### MentaLIST
[MentaLIST](https://github.com/WGS-TB/MentaLiST)
([Feijao2018](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000146))
is a command line multilocus typing software that has been developed to allow
rapid cgMLST/wgMLST typing directly from reads using limited compute resources.
It allows fetching schemes stored at PubMLST, Enterobase and from seqsphere+
Nomenclature server ([www.cgmlst.org](http://www.cgmlst.org)) or installing any
custom scheme. A kmer data-base is created from the chosen scheme. Typing is
effectuated by kmer voting. The idea is that all alleles in the scheme that
contain kmers present in the reads receive a vote. Typing is therefore performed
by “electing” alleles that received the most votes at each loci
([MentaLIST](https://github.com/WGS-TB/MentaLiST),
[Feijao2018](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000146)).
In case of equality, a random allele is chosen among the best candidates. Novel
alleles are detected given a maximum number of mutations to existing alleles
(default 6) at a minimum coverage (default 10X). Mutation positions for new
alleles are given using the closest allele of the scheme as reference, their
locus and sequence is given in an output file (fasta format), which can be used
to separately propose scheme updates (eg. via API to the nomenclature servers).
A python script is provided to select alleles and update the locally stored
scheme/database. It is necessary to rerun analyses to obtain results with the
updated scheme. An allele is considered missing when there is no allele at this
locus having a length coverage above 50% to any possible alleles of the scheme.
“Special cases”: novel alleles and potential alleles that are not typed: eg.
such as incomplete allele length coverage ([50-100%]), potential multiple
alleles are flagged and can be output in a separate file. Allele typing results
can be used separately for further cluster analysis.

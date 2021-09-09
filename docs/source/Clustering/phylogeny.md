# Phylogenetic analysis

## Introduction: History and purpose 

Phylogenetics is the study of relationships between organisms based on common
ancestry (vertical descendance). Historically, phylogenetics was developed to
contribute to taxonomical classification, as it was expected that species
classification into genera, families or superior order would be made on the
basis of shared common ancestry. Therefore the first phylogenetic studies
attempted to reconstruct relatedness relationships based on matrices of shared
morphological characters. The field of phylogenetics thereafter evolved to
molecular methods, ie. with the first evolutionary studies of allozymes.
Phylogenetics methods have evolved in parallel with the development of sanger
sequencing and next generation sequencing, with the wishful/idealistic idea that
being able to use a larger amount of character states (ie. nucleotides present
at each position of the genome) would provide the utmost possible resolution
when determining relationships between organisms. The ability of delineating and
identifying isolates belonging to groups of highly related pathogens using NGS
molecular phylogenetics has become an invaluable tool in epidemiological
surveillance ([Rife et al.
2017](https://ghrp.biomedcentral.com/articles/10.1186/s41256-017-0034-y)) and
outbreak investigations and can contribute to better understanding of the
factors driving the emergence and spread of infectious diseases, either at macro
or micro temporal and geographic scales. In this regard, phylogenomics is
nowadays frequently employed in bacterial epidemiology. However, it is not
employed as first intended: to evaluate the relationships between species. Most
of the focus of phylogenetics in epidemiology is on reconstructing
“genealogies'' within populations, lines of descent from most recent common
ancestor (eg. determining the source of a food-borne pathogen outbreak).

## Terms 

In molecular phylogenetics, **homology** is defined as a similarity between
sequences due to the sharing of an ancestral sequence. Sequence homology can
thus arise by duplication events of an ancestral sequence, or by vertical
descent (eg. divergence from an ancestor during speciation), also called
**orthology**. In phylogenetics reconstruction methods, the hierarchical
relationships between taxa are derived by comparison of sequence/loci that are
assumed to be orthologous.

The positions in a **multiple sequence alignment (MSA)** used for phylogenetics
analysis are thus assumed to be orthologous. **Gaps** (or indels: insertions and
deletions) are artificially introduced markers to allow alignment of sequences
or sequence portions that differ in length. 

Multiple sequence alignments can be extracted from a **whole genome alignment
(WGA)**, however, note that due to genome reorganisation, and the complexity of
the alignment, the resulting MSA is a concatenated set of several alignment of
supposedly orthologous sequences. (See SNP and variant calling section).

**Single nucleotide polymorphisms (SNPs)** are the representation of the
variants loci/positions in MSA.

**Taxon (pl. taxa)**: term derived from taxonomy to represent a group of
organisms sharing an identical taxonomic ranking (eg. species, genus, family,
etc …) 

**Operational taxonomic unit (OTU)**: a group of organisms under study, (ie.
species, population, clonal lineage, family, …). The concept of OTU is most
convenient in phylogenetics, as it allows for defining groups of organisms we
are referring to without prior knowledge of their taxonomic level. 

**Clusters in phylogenetics**: Clusters are aggregates of similar isolates. The
concept of cluster allows to define a group of things with similar properties.
In molecular epidemiology, clusters can be defined eg. based on pairwise
distance measures), where pairwise distance thresholds (cutoffs) often are used
to determine which isolates belong to a specific cluster. In phylogenetics,
defined clusters MUST be **monophyletic**.  

A **monophyletic group (or clade)** is a group where all OTUs that form this
group are linked by a single ancestor (decipited by a single node), and all the
descendants of this ancestor belong to this singular group. The monophyletic
concept is often used to describe the relations of the OTU to each other in
phylogenetics. It contrasts with the concept of **paraphyletic group**, which
allows describing OTU groups sharing a common ancestor but where not all
descendants are included in the group. [See this
figure](https://www.mun.ca/biology/scarr/Taxon_types.htm) for descriptive terms
of OTU grouping. 

A **lineage** is a line of descent, including all the ancestors and all the
descendants (leaves/tips), from the most ancient ancestor that defines the
lineage. 

**Phylogenetic trees** are tree-like graphs (non-cyclic) that are used to
visualise the reconstructed relationships between organisms. The **topology of
the tree** (ie. the branching pattern of the tree) is expected to reflect how
OTUs are related to each other. Reading and interpreting phylogenetic trees is
not always as straightforward as it seems ([Baum
2008](https://www.nature.com/scitable/topicpage/reading-a-phylogenetic-tree-the-meaning-of-41956/),
[Gregory
2008](https://evolution-outreach.biomedcentral.com/articles/10.1007/s12052-008-0035-x)).
Here we only present some few of the several terms and concepts that are
available to interpret phylogenetic trees and describe relatedness among OTUs.
In short, each ancestor (depicted at nodes of the tree) are expected to have
two, and only two (bifurcating trees) descendants represented at the tips (also
called terminal nodes or leaves). The **most recent common ancestor (MRCA)** is
the term used to describe the ancestor that is most recent to all OTU we are
referring to. When phylogenetic reconstruction methods allow to evaluate the
support of the splits (one ancestor to two descendants), and when the support of
the split is low, the branching pattern of the tree is not well resolved. This
could be visualised as [polytomies](https://en.wikipedia.org/wiki/Polytomy) (or
**multifurcation**: when one ancestor diverged into more than two descendants).
Note that in most commonly used phylogenetics inference, tips always are the
isolates under study, and ancestors are always reconstructed (inferred), ie.
ancestors can never be sampled, they are purely a reconstruction of ancestry of
your isolates. 

Note that when we are speaking about the succession of ancestors, we assume a
direction of evolution in time, this implies that the phylogenetic tree is
**rooted**. The root of the tree allows for providing a direction (the order of
splitting events) on the tree. However, when the tree is **unrooted** (not
rooted) the order of the branching pattern of the nodes is not defined (ie. we
do not know which node is the ancestor of which node).  

A specific terminology is used to describe the different types of trees. A
**dendrogram** is a bifurcating graph tree that represents a hierarchical
structure but does not necessarily represent evolutionary relationships, it is
basically a generic term for tree-graphs. A **cladogram** is a dendrogram where
the hierarchical structure indicates a common ancestry.  Branch lengths do not
provide indications about evolutionary distance between OTUs. A **phylogram** is
a phylogenetic tree where the topology indicates the ancestry history and the
branch length represents the amount of evolution (or evolutionary distances)
between OTUs. **Ultrametric** trees are trees where all branches have equal
length to the root. Beware that those ultrametric trees must be reconstructed
under the assumption of a **molecular clock**, and that all tips are
contemporary isolates. Ultrametric trees are very sensitive to deviations of
those assumptions, in which case the branch lengths may not indicate the real
amount of evolution of OTUs since their last MRCA. Ultrametric trees are
generally poorly adapted to represent evolutionary relationships of rapidly
evolving organisms with short generation times, where lineages may evolve at
different rates, most particularly if you mix contemporary isolates to isolates
previously stored in the freezer for many years.  **Additive trees** are trees
where the branch length represents the amount of evolution, but do not require
the assumption of molecular clock (note that ultrametric trees are a particular
case of additive trees).

The **molecular clock hypothesis** is the assumption that sequence divergence
occurs at the same pace among the studied lineages, and therefore that the
genetic distance is proportional to time elapsed since divergence from MRCA. 

**Phylogenetics and phylogenomics derived terms**: The joint study of phylogeny
and population genetics has given rise to the term of **Phylodynamics**. In
epidemiology, this can be defined as “the study of the interaction between
epidemiological and evolutionary processes within and among pathogen
populations” ([Rife et al.
2017](https://ghrp.biomedcentral.com/articles/10.1186/s41256-017-0034-y)).
**Phylogeography** is the study of spatial arrangements of genealogical lineages
within and among conspecific populations and closely related species.” (Avise
2010 in [Avise 2016](https://www.pnas.org/content/113/29/7957)).


## Examples of usages of phylogenies in molecular epidemiology

### Detecting and investigating outbreaks
Finding the source of some food-born pathogen causing an outbreak can be
challenging. A patient might have consumed food originating from diverse origin,
and the usage of preprocessed ingredients entering in each individual meal
composition might be nearly impossible to trace back. [Hoffmann et al.
(2016)](https://academic.oup.com/jid/article/213/4/502/2459204) provided an
example where Maximum likelihood (ML) phylogenetic analysis of WGS data of a
preselected set of isolates (geolocated isolates: outbreak isolates,
environmental isolates and historical isolates) that were identified as similar
by PFGE, allowed to pitpoint toward the most probable origin of Salmonella
Bareilly outbreak. The pathogen responsible for the USA outbreak, was associated
with tuna imported from a Indian fishery. They also demonstrated that the method
had a high resolution to distinguish between geographically distinct lineages,
which showed the high potential of those methods to monitor evolution and
transmission routes of either food or environmental pathogens to new
niches/hosts.

[Chen et al. (2016)](https://aem.asm.org/content/82/20/6258) presented an
interesting case of distance based phylogeny (using cgMLST data) of Listeria
monocytogenes outbreaks. They demonstrated that in somes cases, it is necessary
to investigate the hierarchical levels of population structure sequentially,
first by identifying the main lineages, and thereafter refining analysis by
working within lineages. This to successfully discriminate between isolates
belonging to closely related outbreaks.

### Tracking transmission routes of pathogens at different geographic scales 

Pathogen transmission can be studied at different geographic scales: from
worldwide patterns of strain dissemination to direct transmission events eg.
between hosts (see [Croucher and Didelot
2015](https://www.sciencedirect.com/science/article/pii/S1369527414001635)). At
intercontinental scales, the focus is mainly on detecting changes in the global
population structure of the pathogen, which can affect the epidemiology of the
disease associated to the pathogen, or can eg. help pinpoint possible routes of
transmission (eg. through food import) and can contribute to narrowing the area
of where epidemiological investigation should be directed. At a microgeographic
scale, transmission routes can help identify reservoirs of persistence in the
environment (eg. food processing) and contribute to improvement of routines and
disinfection practices. 


#### Understanding evolution, spread and transmission routes of antimicrobial resistance

AMR strains have been associated with increasing usage of antimicrobials
worldwide. Usage of antimicrobial induces a selection pressure on the bacterial
pathogens, which can lead to change in strain population structure (eg.
population replacement of some lineages by others) and transform the
epidemiology of the disease. Phylogenetic analysis can contribute to the
understanding of the evolution and spread of resistant phenotypes ([Klemm and
Dougan
2016](https://www.sciencedirect.com/science/article/pii/S1931312816301512?via%3Dihub)).
[Wong et al. (2015)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4921243/)
identified inter and intracontinental transmission of multidrug resistant (MDR)
Salmonella typhi H58 clades. The H58 clade emergence was identified as recent
(~30 years ago). They identified multiple transmission events between Asia and
Africa and demonstrated that mutations in a region of GyrA, involved in
quinolone resistance, evolved independently on several occasions. An indication
that selection at this gene was driven by the geographical pattern of antibiotic
usage. Moreover, the expansion of the H58 lineage leads to replacement of other
S.typhi strains, and therefore is likely to transform the epidemiology of
disease, which justifies the necessity for long term surveillance of this
pathogen. This was further supported by the increasing number of reported MDR
resistant cases, which coincided with the identification of previously
unrecognized ongoing outbreak. 

#### Evaluating effectiveness of interventions and actions to fight persistence or reintroduction of pathogens from local reservoirs at a microgeographic scale 

Phylogenetic analysis at a microgeographic scale has been used in combination
with contact tracing of patients to support hospital infection control of
nosocomial strains of Carbapenems resistant Klebsiella pneumonia strains. This
allowed to identify potential reservoirs of infection ([Cella et al.
2017](https://www.nature.com/articles/s41598-017-03581-4)). The authors
reconstructed a time-scaled phylogeny and inferred the geographical location of
ancestral lineages through Bayesian phylogeography. Their results indicated that
the ancestor of the strain could have been introduced at the hospital as early
as 6 years previously to their study, indicating that the bacteria was likely
transported in the different parts of the hospital by employees, and that some
strains might have been maintained at reservoirs related to ie. endoscopic
procedures. This type of study can help detect which procedures and routines
need to be improved, and where intervention measures lack effectiveness. 

[Fagerlund and al. (2020)](https://aem.asm.org/content/86/14/e00579-20) studied
the genetic diversity of Listeria monocytogenes ST9 lineage, and showed that
gradually refining their analysis (cgMLST, wgMLST and SNP data), first focusing
on the whole ST9 lineage and then on Norwegian clones allowed to increase the
discriminatory power of the analyses while providing a background for
interpretation of the analyses. Using time-scaled analysis, they were able to
estimate the timing of emergence of the two Norwegian subclones that belonged to
several meat processing plants. This showed that the emergence of the two
Norwegian clades occurred relatively recently (95% HPD 1970-1991, and
1992-2004). Their study highlights that deep sampling is critical for studies
aiming at finding the origin of bacterial contamination in food products.
Moreover they provide a rich example of the challenges related to the
interpretation of contamination routes, cases of multiple introduction events
and persistence within production facilities when isolates are closely related. 

### Improving risk assessment, risk management and assessment of risk prevention measures
The risk associated with exposure to pathogens from a single species might vary
between lineages, i.e., a subset of strains from a bacterial pathogen might be
more likely to induce disease than other strains ([Rantisou et al.
2018](https://www.sciencedirect.com/science/article/pii/S0168160517305007)).
Some phenotypes might confer a higher risk, eg. resistance to antimicrobials,
ability to synthetize toxins, ability to grow in specific niches such as
determined by pH or specific hosts. Those specific phenotypes might be shared
within lineages but some might also be acquired through horizontal transfer,
gene gain and loss. The risk of invasive disease might also be associated to
host factors (eg. [Klemm and Dougan 2016) and to the evolution mechanisms of the
pathogens. 

Here three examples are provided on the possible contribution of phylogenetics analysis for these situations. 

#### Risk prevention
As mentioned previously,phylogenetic analyses at a microgeographic scale [ Cella
et al. 2017](https://www.nature.com/articles/s41598-017-03581-4) example), can
be used to assess whether intervention measures against a pathogen are effective
and allow adjustment those measures. 

#### Understanding host-pathogen interaction, pathogen evolution Within-host
diversity, within-host evolution and within-host niche adaptation has been
observed in bacterial pathogens ([Ailloud et al.
2019](https://www.nature.com/articles/s41467-019-10050-1)). Within-host
evolution is particularly relevant in regard to the development of antimicrobial
resistance, modifications of virulence, host-niche adaptation and for host to
host transmission studies (reviewed in [Didelot et al.
2016](https://www.nature.com/articles/nrmicro.2015.13)).  Phylogenetics can
contribute to elucidating the evolutionary mechanisms allowing host shifts in
pathogens. Such host shifts are a threat to food safety and public heaths, and
have been associated with acquisition of genetic material required for survival
into the new host-species in Staphylococcus aureus ([Ridchardson et al.
2018](https://researchonline.lshtm.ac.uk/id/eprint/4648677/1/Gene%20exchange%20drives%20the%20ecological%20success_GREEN%20AAM.pdf)).


#### Risk prevention by flagging phenotypes associated to specific lineages, contributions of phylogenetics to gene-phenotype association

Phylogenetic comparative methods can help study the pattern of phenotypic traits
that are epidemiologically relevant. Indeed, phylogenetics can contribute to the
ability to discriminate between phenotypes that are associated to specific
lineages from those under control of genes that are shared among several
lineages. This can eg. be used to flag some lineages as presenting a higher risk
than others. Moreover, phylogenetic based methods can be eg. employed to
evaluate the heritability of virulence traits ([Hassler et al.
2020](https://www.tandfonline.com/doi/abs/10.1080/01621459.2020.1799812?journalCode=uasa20)),
which can provide an estimate of the strength of the risk associated with a
trait. 

Phylogenetics also contribute to the identification of gene-phenotype
associations. [Genome-Wide Association Studies
(GWAS)](https://en.wikipedia.org/wiki/Genome-wide_association_study) have been
employed to evaluate the association between phenotype and the presence of
specific SNPs or genes in bacterial pathogens and pathogen lineages, in the hope
that candidate genes discovered might be responsible for the observed phenotype.
To disentangle candidates identified through lineage effects (due to
linkage-disequilibrium: LD) from the candidates with likely phenotypic effect,
population structure needs to be accounted for. This is particularly important
as LD between genes is particularly strong in bacteria, due to their clonal
population structure as well as to the physical linkage of genes. The population
structure can be deduced from phylogenetic trees and incorporated into bacterial
GWAS analyses (eg. [Lees et al.
2020](https://journals.asm.org/doi/full/10.1128/mBio.01344-20)), or directly
incorporated within the GWAS analysis (eg. [Collins and Didelot
2018](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005958),
[Saund and Snitkin
2020](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005958)).


### Providing population dynamics estimates to support epidemiological modeling 

Phylodynamics (field combining phylogenetics and population genetics a common
analysis framework has been used to estimate epidemiological parameters (eg.
effective reproduction numbers) of Mycobacterium tuberculosis ([Kühnert et al.
2018](https://www.sciencedirect.com/science/article/pii/S1755436517301068)),
(eg. duration parameters) to assist modeling of demographic and epidemiological
processes ([Saunier et al.
2016](https://www.biorxiv.org/content/10.1101/050211v1.abstract), [Saulnier et
al.
2017](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005416),
[Volz and Silveroni
2018](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1006546),
[Baele and al.
2018](https://www.sciencedirect.com/science/article/pii/S187962571830066X)).

## A short overview of phylogenetic reconstruction methods and considerations

### Phylogenetic reconstruction methods

#### Distance based methods

In **Distance based methods**, any distance measure (eg. similarity between
sequences, hamming distances between shared alleles at cgMLST, computed from a
MSA/WGA employing an evolutionary model, ANI: Average nucleotide identity
distances, distances based on shared k-mer approaches as used in alignment free
phylogenetic methods) that is assumed to be minimal when organisms are closely
related, can be used as the basis for phylogenetic tree reconstruction. The
distance matrix of pairwise dissimilarities is used to perform a hierarchical
clustering (e.g. UPGMA: Unweighted pair group method with arithmetic means, NJ:
Neighbor joining) which leads to obtaining a single tree.

#### Character state phylogenetic methods

**Character state phylogenetic methods** require a multiple alignment of
orthologous DNA sequences/genomes. “Nucleotide states” (A,C,G,T and depending on
the model used, indels: “-”) at each position (column) of the multiple alignment
might either be ignored (ie. considered as missing data) or analyzed
independently. 

##### Maximum parsimony

**Maximum parsimony** method aims at reconstructing a phylogenetic tree whose
topology minimizes the number of character state changes in the tree, since the
last common ancestor. This method does not allow explicit substitution modeling
to compute the parsimony criteria (neither allow for multiple substitutions).
Those implicit assumptions might be unrealistic ([Kapli et al.
2020](https://www.nature.com/articles/s41576-020-0233-0)). No further details
concerning this method will be provided as it is not frequently employed in
bacterial phylogenetics, but it is described in many introduction-level
phylogenetics books (eg. [chap 8 in Lemey et al.
2009](https://www.cambridge.org/core/books/phylogenetic-handbook/A9D63A454E76A5EBCCF1119B3C56D766)),
for those interested. 

##### Statistical phylogenetics methods

**Statistical phylogenetics methods**, ie. **Maximum likelihood methods (ML)**
and *Bayesian methods** (or approximation of those), use nucleotide states at
each position of the multiple sequence/genome alignment to reconstruct
phylogenetic trees. A genetic distance is estimated according to an evolutionary
model during phylogenetic inference. A set of trees within possible trees (the
tree space) is evaluated.  

In **ML methods** the likelihood optimality criterion allows for assessing which
tree in the tree space is an “optimal” tree. Because the set of all possible
trees is often very large given the number of isolates under study, it is not
computationally possible to evaluate all possible trees. Algorithms are designed
to explore the tree space in search of the best tree: the tree topology that has
the highest likelihood to have given rise to the data (MSA/WGA) given the chosen
evolutionary model. However there is no guarantee that they will find the
absolute best tree among all the possible trees. 

**Bayesian methods** allow estimating the probability distribution of trees and
model parameters, and provide estimates of the confidence of inferred
relationships (clades), estimates of the evolutionary hypotheses (the
evolutionary model distribution) and the data through the posterior (posterior
probability distribution). Bayesian methods require specification of prior
belief on the evolutionary model parameters and are the most computationally
intensive, due to the modalities of the exploration of the “tree space” through
sampling and updating of the model parameters with MCMC ([Markov chain Monte
Carlo](https://en.wikipedia.org/wiki/Markov_chain_Monte_Carlo)). They are more
complex to implement than ML methods, computationally heavier and are so far
rarely used in molecular epidemiology for routine surveillance of bacterial
outbreaks. Bayesian phylogenetics provides a statistical framework for
hypothesis testing and allow to incorporate a variety of data types into the
phylogenetic modelling (eg. sampling locations, sampling dates that will allow
calibrating an evolutionary timeline) and are therefore quite powerful analysis
methods. 

### Some major assumptions to be aware of and to take into consideration  

One major assumption of phylogenetics methods is that it describes the vertical
evolution of the OTU under study. Genomes evolve through different mechanisms,
and this implies that the different sections of the genome, following the
specificities of their evolutionary mechanisms (and when those evolution events
occurred) might not have the same evolutionary history (ie. do not point to the
same ancestral lineage: eg. case of recombinant sequences, nor to the same
timeline of evolution to the rest of the genome: eg. case of evolution by gene
duplication). Therefore, it is important that phylogenetic reconstruction
originates from the comparison of orthologous sequences. cgMLST schemes appear
to be designed such as the phylogenetic noise introduced by recombination is
minimal, if the recombinant signal is only counted once (eg. in [Neumann et al.
2019](https://jcm.asm.org/content/57/3/e01686-18)) but his might still be rather
problematic for species with high recombination rates. Detecting and discarding
recombinant sequences for methods employing MSA as input data (eg. [Whaley et
al. 2018](https://www.nature.com/articles/s41598-018-33622-5)) is the most
commonly use approach, also this is not without consequences and
recombination-aware methods are being developed (see eg. [Vaughan et al.
2017](https://academic.oup.com/genetics/article/205/2/857/6066433?login=true)).

Genetic distances can be obtained from MSA by explicitly specifying sequence
evolutionary models, as eg. done for statistical phylogenetics methods.
Evolutionary models allow to make different assumptions about the evolutionary
process of the sequences, eg. the rates of substitutions from one nucleotide to
another, difference of rates of evolutions between different sites in the
genome, and can allow to include different evolution rates for the different
lineages ([Lemey et al.
2009](https://books.google.no/books/about/The_Phylogenetic_Handbook.html?id=DeD_lQ-kBPQC&printsec=frontcover&source=kp_read_button&redir_esc=y#v=onepage&q&f=false)).

More complex models (with more parameters eg. different rates of substitutions
for each nucleotide change) than simpler models are not always necessary to
provide better phylogenetic reconstruction (see eg. [Kelchner and Thomas
2007](https://moodle.umontpellier.fr/pluginfile.php/923225/mod_resource/content/1/Kelchner~2007-TREE.pdf)).

Interpreting phylogenetic trees requires having an idea of how confident we are in the different lineages obtained during phylogenetic analysis. Support attributed to the groups by resampling techniques (eg. bootstrapping) are frequently used in ML methods. Confidence is assessed directly from the posterior for Bayesian phylogenetic methods. Moreover, robustness of trees inferred by different methods, might be an additional indicator of the strength of the phylogenetic signal.  

### Which method should I choose? 

**Choosing a method depends on the biological question you want an answer to,
and to the level of similarity between your sequences.** 

Distance based phylogenetic methods are less computationally intensive than
statistical phylogenetic methods, and might be a good choice if you have a large
amount of samples to analyse. This is particularly important since the number of
possible tree topologies increase rapidly with increasing number of studied OTU,
in which case statistical phylogenetic methods might be too demanding of compute
resources. Distance based methods produce a single tree. It is possible to
access the confidence in the inferred clades by calculating support values using
eg. resampling methods such as bootstrapping (see eg. [Efron et al.
1996](https://www.pnas.org/content/93/23/13429)), on the character or loci used
to calculate the distance matrix. 

Maximum likelihood (ML) are with distance based methods the most commonly used
phylogenetic reconstruction methods used in bacterial molecular epidemiology.
For distantly related isolates, MSA from concatenated genes are better suited
than MSA obtained from WGA of collinear sequences or from SNP typing using a
closely related sequence as coordinate system. This is due to the complexity of
WGA alignment when organisms are too dissimilar due to the. abundance of gene
duplications, genome reorganisation events, and if sequences are too divergent.
See e.g., [Kapli et al. 2020](https://www.nature.com/articles/s41576-020-0233-0)
for a comprehensive overview of phylogenomic methods for distantly related OTUs,
as well as considerations for method choice. Distantly related isolates usually
belong to different serogroups, relatedness is higher for isolates belonging to
identical sequence type or clonal complexes. Closely related isolates are eg.
outbreak isolates. 

Note that MSA only represents a fraction of size of the aligned genomes.
Therefore the ability to discriminate between clusters of related individuals
will not only depend on the quality of the MSA, but also on the fraction of the
genome that is compared (that is common to all isolates: core). Different
methods can be used sequentially, to gain additional resolution (new MSA) for
subsets of closely related isolates. 

Note that software that provide different MSA or SNP typing approaches might be
optimized for different types of analyses, and different amounts of divergence
between isolates under study.

## What do you need to be able to reconstruct phylogenetic trees with WGS data?

For distance based methods a pairwise distance matrix is needed, eg. from
alignment-free methods that allow computation of distances based on kmer/word
frequencies, or from a MSA/WGA. 

For statistical phylogenetics a MSA/WGA/MultipleSNP alignment is needed, eg.
concatenated from a set of gene alignments or a whole genome alignment. 

### Workflow for phylogenetic reconstruction with distance based methods 

#### Obtaining a pairwise distance matrix

A pairwise distance matrix can be obtained from a multiple alignment, or by any
other measure where the distance is assumed to represent the amount of evolution
between isolates, eg. as perform for alignment free phylogenetic reconstruction
where the distance is estimated by kmer difference counts or spaced words
matches (see eg. [Röhling et al.
2020](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0228070),
[Morgenstern
2019](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0228070))

#### Phylogenetic tree building

UPGMA (unweighted pair group method with arithmetic mean) produces ultrametric
trees, where all OTUs are equally distant to the root. UPGMA assumes that all
lineages evolve at the same rate: molecular clock and that all OTU have been
sampled at the same time. While this method is still relatively frequently used,
this is likely not the best choice for pathogen surveillance datasets. It is
therefore not presented here. (For an overview of principle see any phylogenetic
textbook or review such as eg. at [Sharma et
2018](https://link.springer.com/chapter/10.1007/978-981-10-8198-9_50)). 

The most frequently used distance method to reconstruct phylogenetic trees is
the neighbor-joining method (NJ). NJ does not assume a molecular clock and
produces a single unrooted tree  ([Saitou and Nei
1987](https://pubmed.ncbi.nlm.nih.gov/3447015/)). The NJ principle is to build
the phylogenetic tree iteratively, starting from a star topology and by creating
nodes joining OTU with the smallest pairwise branch length and by minimizing the
sum of branch length in the tree. At each node created, the distance between the
taxa in the node and other OTU is calculated. This is repeated until all OTU are
joined by bifurcating nodes (see eg. for a detailed process using 4 OTU [DeSalle
and Rosenfeld
2013])(https://books.google.no/books/about/Phylogenomics.html?id=IAcPBAAAQBAJ&redir_esc=y)).


#### Evaluating clade confidence

Clades can be evaluated using Bootstrapping, as mentioned elsewhere in this
handbook.

## Workflow for MSA/WGA/MSA-SNP methods

### Obtaining a multiple alignment (MA: MSA/WGA/MA-SNP)

One critical assumption is that at each position of the multiple alignment (MA),
the characters are assumed to have evolved from a common ancestor (homology) and
have diverged from the same ancestral sequence (ie. vertically: orthology).
Depending on the nature (gene, SNPs, collinear regions) of the MA,  different
preprocessing such as removal of recombination between homologous segments
methods might be employed prior to phylogenetic reconstruction (see eg. [Kapli
et al. 2020](https://www.nature.com/articles/s41576-020-0233-0)). There are
different strategies to obtain a multiple alignment from WGS data based on
either 

- The set of presumed orthologous genes that are present in all isolates are
  extracted from genome annotations, and specialized databases (eg. described in
  [Kapli et al. 2020](https://www.nature.com/articles/s41576-020-0233-0)). A
  multiple sequence alignment is performed for each gene individually. In
  bacterial surveillance, alignments of all the genes are generally concatenated
  in a single MSA/WGA for phylogenetic reconstruction, eg. by exporting the core
  gene alignment using
  [Roary](https://github.com/microgenomics/tutorials/blob/master/pangenome.md)
  ([Page et al.
  2015](https://academic.oup.com/bioinformatics/article/31/22/3691/240757)).
  Alternatively, it is possible to reconstruct one phylogenetic tree per gene
  and “reconcile” the obtained set of phylogenies in a single tree using
  supertree methods (see eg. [Boussau and Scornavacca
  2020](https://hal.archives-ouvertes.fr/hal-02535529/document), and [Kapli et
  al. 2020](https://www.nature.com/articles/s41576-020-0233-0)). 

- Whole genome multiple alignment is a complex computing problem, this due to
  eg. genome rearrangement ([Henning and Nielselt
  2019](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6612806/), [Dewey
  2019](https://link.springer.com/protocol/10.1007%2F978-1-4939-9074-0_4)). A
  strategy that is frequently employed is the “hierarchical” multiple alignment
  of collinear blocks (segments of the compared genomes that do not contain
  rearrangements)  or a “local” alignment of parts of the genomes that are later
  merged as multiple alignments ([Darling et al.
  2004](https://pubmed.ncbi.nlm.nih.gov/15231754/), [Darling et al.
  2010](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0011147)).
  Whole genome alignment contains information about genome synteny, and
  typically includes pangenomes. The core MA must be extracted from pangenome
  WGA for phylogenetic analysis. MSA/WGA can be either directly obtained (eg.
  [ParSNP](https://github.com/marbl/parsnp), [Treangen et al.
  2014](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0524-x))
  or extracted by concatenating the several collinear blocks that were common
  (core) in all genomes under study (eg. from extracting the core from a WGA
  alignment file output from Mauve/progressiveMauve aligner ([Darling et al.
  2004](https://pubmed.ncbi.nlm.nih.gov/15231754/), [Darling et al.
  2010](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0011147))
  with biopython script or with eg., with harvesttools ([Treangen et al.
  2014](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0524-x)).
  

- Multiple SNP alignment can be obtained when an identical reference is used to
  type SNPs for all isolates under study. The reference serves as a coordinate
  system, therefore a multiple SNP alignment can be reconstructed by
  concatenating all the SNPs at all the different coordinates of the reference.
  This can eg. be done with [Snippy](https://github.com/tseemann/snippy).  

### 5.2.2 Ensuring that aligned sequences are orthologous 

During WGA building, recombinants from homologous regions might be included in
the alignment. Those regions must be either deleted or masked (hidden) from the
alignment used in phylogenetic reconstruction because those sites are not
inherited by vertical descent (non orthologous). The methods developed to detect
recombinant loci (see eg, [Lai and Loerger
2018](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2456-z))
are not universally applicable to all multiple alignments. The methods that use
sliding window where positional information of SNPs is crucial to detect
hotspots of SNPs that are then considered as recombinants (eg. Gubbins
([Croucher et al. 2015](https://academic.oup.com/nar/article/43/3/e15/2410982)),
ClonalFrameML ([Didelot and Wilson
2015](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004041)))
are not applicable for detection of recombinants in MA from concatenated genes
because the order of genes is arbitrary and intergenic regions are not present.
Moreover some methods have been developed to work with relatively closely
related isolates (within lineages), eg. ClonalFrameML and Gubbins. Other methods
might be better adapted when working with more distantly related isolates within
a species (eg. [fastGear](https://mostowylab.com/news/fastgear) [Mostowy etal.
2017](http://Mostowy2017)).  

### 5.2.3 Defining an evolutionary model of the sequences (Modeling evolution)

Statistical phylogenetic methods aim at modeling the process of evolution that
is evidenced by the SNPs seen between taxa. Therefore it is necessary to provide
a evolutionary model, which is a representation of the sequence evolutionary
process: the change in character/nucleotide over time in orthologous sequences
belonging to two taxa that diverged from a most recent common ancestor (MRCA),
to perform phylogenetic inference with statistical phylogenetic methods. 

Each evolutionary model is composed of a set of sub-models that represent the
different components or biological characteristics that are relevant to describe
the characteristics of the sequence evolution.  A “minimum evolutionary model”
that might be realistic enough to represent sequence evolution for a set of OTUs
can be composed of a nucleotide substitution model and a model of heterogeneity
rate among sites. Below these are described, as are also several additional
models which when used in conjunction with the  “minimum evolutionary model” can
provide a means to increase the realisms of the evolutionary process modeling. 

#### Which evolutionary model should I choose? 

Choosing an evolutionary model might be a daunting task. Therefore, a strategy
for “choosing” the model, is actually to perform phylogenetic inference with
several models and then evaluate the fit of the model to the data. Fortunately,
model testing is implemented and automated in several phylogenetic softwares,
thus this does not require you to manually perform several analyses. 

Generally, when reconstructing phylogenies of isolates that are very closely
related, you can expect that the best fit evolutionary model will be more simple
(less parameters) than when you reconstruct phylogeny of distantly related OTU
([Lemey et al.
2009](https://books.google.no/books/about/The_Phylogenetic_Handbook.html?id=DeD_lQ-kBPQC&printsec=frontcover&source=kp_read_button&redir_esc=y#v=onepage&q&f=false)).
This can eg. be explained because you are less likely to have to model multiple
substitutions events and because the sequence nucleotide frequencies are likely
to be nearly identical among the isolates unders study. 

#### Nucleotide substitution models

##### What is a substitution model: 

Substitutions models are one of the major components of the sequence
evolutionary model. Substitution models are a statistical description of how
nucleotides evolve from the MRCA to another during sequence evolution; they
provide the probability of change of each base into another base  (eg. describe
the probability of A becoming T over time). For amino-acid substitution models
please see phylogenetic books).

Nucleotide substitutions are usually modeled as a random event (ie. occurring
randomly at one nucleotide location within your MA). Nucleotide sites are
assumed to evolve independently of each other. Through phylogenetic inference,
evolution can be modelled step wise (discrete time) or continuously (continuous
time, eg. Bayesian methods). Herein we only use “time step” to present the
general idea of those methods. At each time step, each site evolves or not,
independently from other sites. At each time step, the nucleotide substitution
probabilities remain unchanged (time homogeneity assumption). A very good
introduction on substitution models can be found here: ([Lecture primer by Paul
Lewis - Part 1](https://www.youtube.com/watch?v=1r4z0YJq580)). 

The relation between an observed nucleotide change and the “true” evolutionary
distance is not one to one, because some types of base changes may be more
likely than others. This can be due to a bias in nucleotide composition, or a
bias in base biochemical properties that favors some types of nucleotide changes
being more probable than others, thus having less evolutionary weight than other
changes.  Other reasons of the absence of one to one relationship between
evolutionary distance and observed nucleotide changes are the occurrence of
multiple substitutions events, where only the final state is observed (eg: A ->
T -> G), or the occurrence of back mutations (eg: A -> T -> A) or convergence
(eg. A -> T and C->T) where sequence evolution did not leave an observable
footprint in the sequences under comparison. Reversal and multiple substitutions
are more likely if organisms have diverged a long time ago. 

##### Frequently employed substitution models 

The most frequently employed substitution models belong to a family of models
called time reversible models (REV). The general time reversible model (GTR) can
be seen as the most complex (most parameters) of the REV model family. 

The most simple REV model is called the **Jukes and Cantor model (JC69)**.  JC69
assumes equal probability of change of each nucleotide to one-another and equal
equilibrium frequencies of each nucleotide, i.e. 0.25 of each. The slightly more
complex model **Kimura two-parameter mode (K2P or K80)** introduced different
rates of changes for transitions and transversions, as transitions are more
frequent than transversion during evolution. The **GTR model** is composed of
different rates of changes for the different nucleotides and different
equilibrium nucleotides frequencies (see eg. review in [Arenas
2015](https://www.frontiersin.org/articles/10.3389/fgene.2015.00319/full)  and a
figure
[here](https://www.semanticscholar.org/paper/What%27s-in-a-character-DeSalle/313ab4728900e96d7eaff5c8db8fe30f1f702afb/figure/5)
for the relations between different REV models.) All GTR models, and submodels
(nested models) assume that the relative frequencies of each nucleotide are at
equilibrium. This means that relative nucleotide frequencies do not change in
the course of evolution (also called stationary).

Note that if a MA-SNP is used it might be necessary to provide the number of
invariant positions for each nucleotide. This is required to compute the
relative nucleotide frequencies of the dataset. 

Note: that non-REV models exist. They allow providing a direction of evolution,
but those are so far not frequently encountered (see eg. [Williams et al.
2015](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4571574/), [Woodhams et al.,
2015](https://doi.org/10.1093/sysbio/syv021)) in molecular epidemiology
phylogenetic inference of bacterial pathogens.
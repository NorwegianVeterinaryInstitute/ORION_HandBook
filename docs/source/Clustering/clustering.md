# Clustering of xMLST data

Once typing information from xMLST methods have been obtained, it is quite
common to cluster isolates on their profiles. In order to be able to do
clustering, a pairwise distance matrix of allelic differences has to be
obtained. It is usually calculated from the [hamming
distances](https://en.wikipedia.org/wiki/Hamming_distance), the number of
pairwise allelic differences between isolates. Missing loci in one or both
isolates are commonly omitted from the distance calculation.  Dissimilarity
matrices are obtained from normalized distances matrices (scaling the values of
the distance matrix to the interval [0-1]). Calculating distances matrices is
often integrated in the workflow provided by commercial tools and analyses web
platforms. The tools section below describes other tools that may be used.

## Commonly used clustering methods for (cg)MLST data

Clustering of xMLST data is used to classify groups that are more similar to
each other than to other groups. Because it is assumed that the isolates that
group together are more closely related, it is expected that if a distance
measure makes it possible to to separate between very similar isolates (i.e. it
gives high resolution), it can be used to identify isolates belonging to a
single (sub)lineage or to a single outbreak.  

[Agglomerative hierarchical
clustering](https://en.wikipedia.org/wiki/Hierarchical_clustering) is used to
group isolates based on their similarity, and by extension, it is assumed that
highly similar isolates are closely related. Compute requirements of
hierarchical clustering methods are generally low, when compared to phylogenetic
inference, and therefore it is possible to analyze a large number of isolates.
Hierarchical clustering algorithms work iteratively, combining groups that are
more similar to each other at each step, starting by considering each isolate as
a single group. The type of linkage indicates how the distances between groups
are (re)calculated at each iteration. Good introductions to agglomerative
hierarchical clustering and linkage types can be found in [Chap1 in Machine
Learning with R, the tidyverse and
mlr](https://livebook.manning.com/book/machine-learning-for-mortals-mere-and-otherwise/chapter-17/43)
and in the book  [Practical Guide to cluster analysis in
R](https://xsliulab.github.io/Workshop/week10/r-cluster-book.pdf). 

In short: **Single linkage** appears to be the most frequently used linkage type
when doing hierarchical clustering with cgMLST.  In this linkage method, the
distance between groups is the smallest distance between two isolates in the two
groups. Single linkage might have been chosen as the method of choice for
surveillance, as it produces long clusters that may better reflect clonal
expansion of bacterial pathogens. In **average linkage** (equivalent to
[UPGMA](https://drive5.com/usearch/manual/linkage.html)), the distance between
groups is calculated as the mean distance of all members of each group to all
members of the other group. In **centroid linkage**, the central point of each
group is calculated, and this centre is used as distance between groups.
**Complete linkage** produces more compact groups as the distance between
clusters is defined as the maximal distance between all pairs of elements
belonging to each group. **Neighbor joining** is also a type of hierarchical
clustering that is frequently used to reconstruct phylogenetic trees (unrooted
tree with a topology that minimizes the total tree length, see phylogenetics
section). 

Clustering can also be based on [Minimum-spanning trees
(MST)](https://www.statisticshowto.com/minimum-spanning-tree/). MST is a type of
tree graph that connects isolates by the shortest possible distance, pairwise
distances representing the dissimilarity between isolates, that is frequently
used to represent population structure in epidemiology ([Salipante and Hall
2011](https://journals.asm.org/doi/full/10.1128/JCM.00919-11)). Distance
thresholds are used to delineate between clusters. Recently, [Zhou et al.
(2020)](https://www.biorxiv.org/content/10.1101/2020.11.25.397539v1) developed a
hierarchical clustering method for cgMLST data, that calculates and uses a MST
to assign bacterial genomes in real-time to the different stable hierarchical
levels of population structure of bacterial pathogens that have been previously
identified using a seeding dataset of representative bacterial genomes. 

It is important to consider that using different distance metrics and different
linkage types or different clustering methods may produce different grouping
hierarchies. Because it is assumed that the similarity was representative of the
relatedness between individuals, this can therefore lead to different
representation of the relationships between individuals, see eg. the different
hierarchical structure when the same data used with different clustering methods
are visualized with [dendrograms: image
15](https://www.displayr.com/what-is-dendrogram/) in a [Hierarchical clustering
presentation by Shawn Hopkins](https://slideplayer.com/slide/9336538/). Note
that the uncertainty associated to this hierarchical clustering reconstruction
is rarely evaluated, neither for linkage based clustering nor MST clustering,
while this could (and probably should) be done by eg. using bootstrapping
methods (see eg [Salipante and Hall
2011](https://journals.asm.org/doi/full/10.1128/JCM.00919-11), [Yu et al.
2019](https://link.springer.com/article/10.1007/s00180-018-0830-y))

Moreover, while the clustering provides an indication of the hierarchies of
groups of individuals, it does not indicate at which level of the hierarchical
structure individuals can be considered as belonging to a single outbreak
cluster. Using a distance threshold or cutoff value is frequently employed for
this purpose. The clustering threshold can be defined on data with known
epidemiological links using a longitudinal study (as done for SNPs in [Walker et
al.
2013](https://www.sciencedirect.com/science/article/pii/S1473309912702773?via%3Dihub)).
Unfortunately it appears that might not possible to define an universal cutoff
value that would allow to successfully discriminate between epidemiology related
VS non related clusters in a single analysis (eg. [Henri et al.
2017](https://www.frontiersin.org/articles/10.3389/fmicb.2017.02351/full),
[Chen et al. 2016](https://aem.asm.org/content/82/20/6258)), and methods that
allow comparison of workflows might be used to assess one's ability to produce
concordant results with other institutions (see [Coipan et al.
2020](https://europepmc.org/article/med/32101514)). 


Note: Many other and/or less traditional clustering methods can be employed in
surveillance and to define lineages. An example of such use is presented in
[PopPUNK](https://github.com/johnlees/PopPUNK) [(Lees et al.
2019](https://genome.cshlp.org/content/29/2/304)). PopPUNK employs density-based
clustering (DBSCAN/HDBSCAN) of core and accessory distances computed by Minhash
sketching ([Broder 1997](https://ieeexplore.ieee.org/abstract/document/666900)).


## Visualisation of clustering

The results of the hierarchical clustering (eg. exported as nexus file) can
usually be visualised with MST or dendrograms/phylogenetic trees graphical
viewers eg. [FigTree](http://tree.bio.ed.ac.uk/software/figtree/) or
[GrapeTree](https://github.com/achtman-lab/GrapeTree) ([Zhou et al.
2018](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6120633/) provide a list of
software that are convenient for visualising results given a large amount of
isolates). Commercial softwares such as Seqsphere+ or Bionumerics and
web-platforms such as Enterobase provide integrated tools to visualize your
results. Libraries available in programming languages such as R or python are
also good alternatives, and can be conveniently used if you wish to produce
non-standard graphs to better suit your needs. 

## Tools (non exhaustive list) - See also species specific tools

**Allele calling - assembly based**
- [chewBBACA](https://github.com/B-UMMI/chewBBACA) ([Silva et al. 2018](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000166))
- [chewieSnake](https://gitlab.com/bfr_bioinformatics/chewieSnake/blob/master/README.md) ([Deneke et al.2021](https://www.frontiersin.org/articles/10.3389/fmicb.2021.649517/full)) - hash-cgMLST (allele calling pipeline with Chewbbaca, allelic distance matrix computation, clustering and report)
- Bionumerics (commercial)
- Seqsphere (commercial)
- [LOCUST](https://sourceforge.net/projects/locustyper/) ([Brinkac et al. 2017](https://academic.oup.com/bioinformatics/article/33/11/1725/2953249)) (BLAST based) 


**Allele calling - sort-read-based**
- [ARIBA](https://github.com/sanger-pathogens/ariba) ([Hunt et al. 2017](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000131)) (combined mapping/alignment with local assembly, although not specifically designed for cgMLST purpose)
- [MentaLIST](https://github.com/sc0tfree/mentalist) ([Feijao2018](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000146)) (kmer based)
- [stringMLST](http://jordan.biology.gatech.edu/page/software/stringMLST/) ([Gupta et al. 2017](https://academic.oup.com/bioinformatics/article/33/1/119/2525695?login=true)) (kmer based)
- [MOST](https://github.com/phe-bioinformatics/MOST) ([Tewolde et al 2016](http://v)) (mapping based)
- [SRST2](http://katholt.github.io/srst2/) ([Inouye et al. 2014](https://genomemedicine.biomedcentral.com/articles/10.1186/s13073-014-0090-6)) (mapping based)



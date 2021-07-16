# Escherichia coli analysis

Escherichia coli are gram-negative bacteria which may reside in the intestinal
tract of most warm-blooded animals contributing to a healthy microbiota.
However, some of these bacteria have a pathogenic behavior, and may be
transmitted by contaminated water or food. E. coli are divided into six
different pathotypes, from which phage-encoded Shiga toxin-producing E. coli
(STEC) (also known as Verocytotoxin-producing E. coli (VTEC)) are the ones most
commonly associated with foodborne outbreaks
([CDC](https://www.cdc.gov/ecoli/general/index.html)). Indeed, Shiga toxins
(Stx) are thought to be the key virulence factors for STEC infections ([Gyles,
2007](https://pubmed.ncbi.nlm.nih.gov/17085726/)). STEC represents the third
most relevant human foodborne bacterial pathogen, just behind Campylobacter and
Salmonella ([EFSA (2019)](https://www.efsa.europa.eu/en/efsajournal/pub/6406)).
[Amesquita-Lopez et al.
(2018)](https://www.sciencedirect.com/science/article/pii/S1684118217301445#bib1)
revises the possible routes of STEC transmission, classification, virulence
factors and antimicrobial resistance. 

Considering the relevance of STEC for human health, different methods have been
applied in order to determine their diversity and associate these features to
pathogenic traits.  E. coli serotyping is based on somatic surface (O-antigens)
and flagellum (H-antigens) antigens, and so far more than 400 STEC serotypes
have been identified ([Amesquita-Lopez
2018](https://www.sciencedirect.com/science/article/pii/S1684118217301445#bib1)).
Moreover, these serotypes are also divided into pathotypes (from A to E),
according to their association to outbreaks and [hemolytic-uremic
syndrome](https://en.wikipedia.org/wiki/Hemolytic%E2%80%93uremic_syndrome)
([Karmali et al. 2003](https://pubmed.ncbi.nlm.nih.gov/14605120/)). STEC O157:H7
serotype belongs to the pathotype A and is responsible for the majority of
outbreaks. For this reason, it is the main focus of many studies
([Amesquita-Lopez
2018](https://www.sciencedirect.com/science/article/pii/S1684118217301445#bib1)).
However, in recent years the epidemiology of this disease has been shifting with
the increasing number of cases of non-O157:H7 STEC infections ([Shen et al.
2015](https://pubmed.ncbi.nlm.nih.gov/25998811/), [Lang et al.
2019](https://jcm.asm.org/content/jcm/early/2019/07/26/JCM.00768-19.full.pdf)).
Similar to what happens with other species, STEC serotyping can be
time-consuming and have limited discriminatory power for epidemiological
studies. Therefore, molecular typing methods have been developed and are also
used to assess STEC diversity.

## Typing methods
STEC molecular typing is an evolving field, constantly seeking for the best typing method. A good typing method is not only highly discriminatory, but also reproducible and automated. STEC molecular typing can be performed through:

- Pulsed Field Gel Electrophoresis (PFGE)   
  PFGE is a fragment length restriction analysis that has long been considered
  the most discriminatory typing method for STEC in the pre-WGS era
  ([Amesquita-Lopez
  2018](https://www.sciencedirect.com/science/article/pii/S1684118217301445#bib1)).
  This is currently the “gold-standard” for
  [PulseNet](https://www.cdc.gov/pulsenet/index.html) network, and has been used
  by public health authorities and food regulators for outbreak investigations.
  Several studies have suggested that combination of PFGE with other typing
  methods may increase the discriminatory power and be useful to determine
  outbreak infection’s sources ([Amesquita-Lopez
  2018](https://www.sciencedirect.com/science/article/pii/S1684118217301445#bib1)).

- MLVA (Multiple locus variable tandem repeat analysis)   
  Multiple Locus Variable Number of Tandem Repeats Analysis is a PCR-based
  typing method, which is the second major typing tool used by the PulseNet
  network (before WGS). This method is fast and might also be able to
  differentiate fast-evolving bacteria with a similar PFGE profile. Therefore,
  MLVA has been used to complement PFGE results, thus providing a useful
  resource during outbreaks ([Parsons et al.
  2016](https://pubmed.ncbi.nlm.nih.gov/27148176/)).

- MLST   
  As for other bacteria, MLST methods based on 7 locus have been developed for
  E. coli. Two protocols have been established; one specifically developed for
  STEC (aspC, clpX, fadD, icdA, lysP, mdh, and uidA;
  http://shigatox.net/new/tools/ecmlst.html) and one developed for a more
  general approach for E. coli (adk, fumC, gyrB, icd, mdh, recA and purA; [Wirth
  et al.
  2006](https://onlinelibrary.wiley.com/doi/10.1111/j.1365-2958.2006.05172.x)).
  MLST can provide faster results when compared to PFGE, and it is highly
  reproducible.

- WGS  
  With the advent of NGS technologies, WGS was shown to be useful for STEC
  outbreak investigation ([Parsons et al.
  2016](https://pubmed.ncbi.nlm.nih.gov/27148176/)). By providing information at
  the genomic level, WGS allows not only a highly discriminatory typing (cgMLST,
  wgMLST and SNP-typing), but also to establish the backward compatibility with
  previously mentioned molecular typing methods, as the in silico serotyping and
  7-loci MLST. For this reason, these methods will tend to continue to be used.
  Furthermore, it allows the analysis of specific genes, such as virulence
  factors and antimicrobial resistance genes. Genetic clustering using WGS can
  be performed on any distance measure (eg. issued from allelic differences
  detected using cgMLST typing) or evolutionary-model based clustering (ie.
  phylogenetics) relying on variants/SNPs detection.
  [PulseNet](https://www.cdc.gov/pulsenet/pathogens/wgs.html) network is making
  efforts to implement WGS as a routine tool to replace PFGE and MLVA. 

## “One Health” surveillance and WGS of STEC
The identification of infection sources is essential for outbreak monitoring.
Hence, an integrated analysis of clinical, food and veterinary samples relying
on the concept of One Health is the key to achieve a good surveillance system.
As shown
[here](https://www.cdc.gov/listeria/surveillance/whole-genome-sequencing.html)
by PulseNet network, the high discriminatory power of WGS increases the chances
to find the bacterial source of infection, and possibly reduces the time that it
takes. Indeed, WGS analysis has proven to be an effective way to determine the
genetic clustering of STEC isolates, as well as the source of infections
([Parsons et al. 2016](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4828450/),
[Jenkins et al. 2019[(https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6352002/),
[Nouws et al. 2020](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7466227/),
[Joensen et al. 2014])(https://pubmed.ncbi.nlm.nih.gov/24574290/), [Chattaway et
al. 2016](https://pubmed.ncbi.nlm.nih.gov/26973632/)). For instance, in England
and Denmark WGS-based STEC surveillance has been implemented with success
([Parsons et al. 2016](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4828450/),
[Dallman et al.
2021)[(https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000544?crawler=true),
however this has mainly focused on STEC from patients. Nevertheless, WGS-based
STEC surveillance at the EU level has been proposed to be delayed until the
technological transition has been made for listeriosis ([ECDC
roadmap[(https://www.ecdc.europa.eu/en/publications-data/ecdc-roadmap-integration-molecular-typing-and-genomic-typing-european-level)).

## WGS lab protocol

### DNA extraction
Before DNA extraction, STEC is cultured in the laboratory. Commonly used media
for STEC include tryptic soy broth, E. coli broth and buffered peptone water
([Amezquita-Lopes et al.
2018](https://www.sciencedirect.com/science/article/pii/S1684118217301445#bib1))
as well as more specific growth media. Regarding DNA extraction, there is not a
standard protocol or kit that is used, but a protocol directed towards
Gram-negative bacteria will be recommended.

### Sequencing technology
There is not a prefered WGS technology to sequence STEC. Similar to other
fields, Illumina paired-end reads represent the most commonly used strategy. Due
to the number of samples that can be handled at a single run and the possible
higher read size, MiSeq sequencing machines seem to be the choice for the
majority of the labs. 

## Bioinformatics protocol

### Mapping or assembly
The first step to perform when receiving the sequencing data , is to evaluate
the sequencing quality and perform trimming and cleaning of the reads (see [Data
preprocessing](../Pipelines/data_preprocessing.md)). 

The cleaned sequence data can then be used for downstream analysis following one
of two approaches (or both in parallel, check [Data
production][../Pipelines/data_production.md]): 
- De novo genome assembly of the sample(s),
- Read mapping of each sample on a reference sequence (obtained from a database
  or by de novo genome assembly of one of your samples.

It is important to note that both approaches have advantages and disadvantages.
The decision on which of them to follow should be made according to what is more
appropriate for the data at hand, and the purpose of the analyses. De novo
genome assembly of all sequenced isolates followed by their annotation seems to
be a common approach in studies including STEC genomes. A commonly used de novo
genome assembler for STEC is [SPAdes](https://cab.spbu.ru/software/spades/)
([Iramiot et al.
2020](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0231852),
[Reid et al.
2020](https://www.frontiersin.org/articles/10.3389/fmicb.2019.03050/full),
[Sonda et al.
2018](https://aricjournal.biomedcentral.com/articles/10.1186/s13756-018-0361-x)).
It performs very well and is freely available. There are command-line pipelines,
such as INNUca, which incorporate these programs and provide the opportunity to
automatically perform all the analyses from quality control to genome assembly. 
If a platform with predefined pipelines (and that usually does not require
bioinformatics skills) is preferred,
[Enterobase[(https://enterobase.readthedocs.io/en/latest/) is available for 
E. coli. As for read mapping, [BWA](http://bio-bwa.sourceforge.net) is a
commonly used approach ([Holmes et al.
2015](https://jcm.asm.org/content/53/11/3565), [Iramiot et al.
2020](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0231852),
[Parsons et al. 2016](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4828450/),
[Dallman et al.
2021](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000544?crawler=true)).
However, as mentioned before, these represent commonly used approaches, and not
recommendations. Thus, other methodologies, pipelines or even platforms may be
used.


### Choosing a reference genome
Should an analysis require the use of a reference genome, the choice of the
reference genome is a crucial step. Analyses relying on read-mapping approaches
might be strongly influenced by reference choice, as the genetic distance
between  the reference and the sample may influence the performance of
downstream steps, namely SNPs/INDELs calling ([Pightling et al.
2014](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0104579),
[Pightling et al.
2015](https://bmcresnotes.biomedcentral.com/articles/10.1186/s13104-015-1689-4)).
This reference can be picked from the samples (after genome assembly), or from a
public database.  .[Enterobase[(https://enterobase.readthedocs.io/en/latest/) is
a good site for choosing a reference for this species.

### Serotyping
Besides the wet-lab approach for serotype determination of STEC samples, in
silico approaches using WGS data can also be performed ([Joensen et al.
2015](https://jcm.asm.org/content/53/8/2410), [Ingle et al.
2016](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5343136/)).
[SRST2](https://github.com/katholt/srst2) can be used to determine serotyping
without the need of de novo genome assembly, by comparing the genomic reads
directly to the database ([Ingle et al.
2016](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5343136/)).
[SeroTypeFinder](https://cge.cbs.dtu.dk/services/SerotypeFinder/) is another
alternative for in silico determination of E. coli serotype, requiring
sequencing reads or genome assembly as input.
[Bionumerics](https://www.applied-maths.com/bionumerics) (using the database
from SeroTypeFinder), [Enterobase](https://enterobase.readthedocs.io/en/latest/)
is an examploe of of a platform where this function is available.

### Getting SNPs
Analysis of SNPs is a frequently used approach for the analysis of STEC samples
[(Parsons et al. 2016](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4828450/)). 

How to detect SNPs is described earlier. Briefly, there are three different approaches.

- Perform de novo genome assembly of each sample and then align
  their genomic sequences. 
- Use a reference genome where the reads of all the samples will be mapped, and
  then use a variant-calling pipeline to determine the polymorphic positions.
  [CFSAN SNP](https://snp-pipeline.readthedocs.io/en/latest/) is a commonly used
  pipeline which performs both processes (read mapping and variant calling).
  [Snippy](https://github.com/tseemann/snippy) and
  [SNVPhyl](https://snvphyl.readthedocs.io/en/latest/user/input/#input) are also
  commonly used alternatives for STEC analyses.
- Determine the polymorphic positions in the sample by analyzing the k-mer
  pattern using
  [kSNP](https://academic.oup.com/bioinformatics/article/31/17/2877/183216). For
  this approach either the genome assembly or the genomic reads must be
  provided. This is not a commonly used approach for STEC analyses.


### Getting alleles and allele differences

The allele sequences of the samples can be retrieved by:

- Replacing the nucleotide of the reference genome by the observed alternative
  allele, and then retrieve the sequence of each gene
  of interest considering the genome annotation of the reference.
- Obtaining the de novo genome assembly of each sample, and performing the
  respective genome annotation. [Prokka](https://github.com/tseemann/prokka) is acommonly used program for STEC.
- Some allele callers, such as [chewBBACA](https://github.com/B-UMMI/chewBBACA),
  provide locus-specific alignments in an automated manner, being a good option
  to determine the allelic profile of samples. 

It is important to note that nowadays there are several platforms which can
automatically do all this analysis. One of the more commonly used for E.coli 
is [Enterobase](https://enterobase.readthedocs.io/en/latest/index.html), and
also [Bionumerics](https://www.applied-maths.com/bionumerics). These platforms
provide assembly, serotyping and allele calling. Several of these platforms are
mentioned in the [xMLST](../Clustering/xMLST.md) section.


### Allele based typing
Allele-based typing consists of retrieving clustering information considering
the different alleles present in a population for a given set of genes (e.g. the
core genome). Therefore, if the tool that is being used for allele finding does
not automatically update its background database itself, it is paramount that a
new database is downloaded before starting the analysis. 

With the advent of WGS, the 7-loci based MLST approach was broadened to the use
of a cgMLST or a wgMLST approach. In this context, there is a public cgMLST
scheme which has been used in STEC analysis considering an allele-based
approach. This scheme comprises [2,513
loci[(https://www.cgmlst.org/ncs/schema/5064703/) and is available in the most
commonly used platforms, such as
[EnteroBase](https://enterobase.readthedocs.io/en/latest/pipelines/salmonella-statistics.html)
and [Ridom SeqSphere+](https://www.ridom.de/seqsphere/). Noteworthy, although
the scheme used by the platforms is the same, their allele calling is
independent, and therefore there may be some nomenclature incompatibilities
between the different platforms. 

### SNP based typing
A SNP-based approach relies on the comparison of SNPs in a population. This
strategy can be seen as an alternative to the allele-based approach, but many
studies actually perform both of them and assess the overlap of the results.
Although for the majority of important bacterial pathogens WGS-based typing is
performed following an allele-based approach, in the case of STEC SNP-based
typing is frequently used. For instance, Public Health England has performed
WGS-based STEC surveillance for a long time following a well established
pipeline ([PHEnix](https://github.com/phe-bioinformatics/PHEnix)) for
surveillance and outbreak detection ([Dallman et al.
2021](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000544?crawler=true),
[Dallman et al. 2015](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4542925/)).
This pipeline relies mostly on variant-calling with
[GATK](https://gatk.broadinstitute.org/hc/en-us) after read-mapping with
[BWA-MEM](http://bio-bwa.sourceforge.net/bwa.shtml), followed by clustering
analysis with [SnapperDB](https://pubmed.ncbi.nlm.nih.gov/29659710/).

Examples of other available pipelines for SNP-based typing are: 

- Center for Food Safety and Applied Nutrition
  ([CFSAN](https://snp-pipeline.readthedocs.io/en/latest/)) HqSNPs pipeline
- [Lyve-SET](https://github.com/lskatz/Lyve-SET) pipeline HqSNPs typing 
- [SNV-Phy](https://snvphyl.readthedocs.io/en/latest/)l (Canadian Public Health
  Agency)  

### Outbreak definition
As defined by the World Health Organization, “a disease outbreak is the
occurrence of cases of disease in excess of what would normally be expected in a
defined community, geographical area or season” . WGS data provides a high
discriminatory power allowing clustering of different isolates (from different
geographical areas, and clinical, animal or environmental sources) according to
their genomic similarity. This contributes not only to an earlier detection of
outbreaks and determination of contamination sources, but also to the detection
of more outbreaks, as has been reported by
[PulseNet](https://www.cdc.gov/listeria/surveillance/whole-genome-sequencing.html)
network for Listeria. It is difficult to establish a clear cluster outbreak
definition, a threshold at which we decide whether two isolates belong to the
same genetic cluster, thus linking two cases of infection. Previous studies have
shown that outbreak-related isolates differ in up to five SNPs in the whole
genome, and therefore this is a commonly used threshold to determine an
outbreak-related cluster ([Dallman et al.
2021](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000544?crawler=true),
[Holmes et al. 2018](https://jcm.asm.org/content/56/3/e01388-17#ref-35),
[Dallman et al. 2015](https://academic.oup.com/cid/article/61/3/305/491349)).


### Virulence and AMR
Several genes are important for E. coli ability to cause infection and are
medically relevant and many of these are associated to different pathogroups.
Relevant virulence-associated genes for STEC are [different stx
subtypes](http://www.fao.org/3/CA0032EN/ca0032en.pdf) (stx1a, stx2a, stx2d) and
other virulence associated genes such as eae and aggR (ref) while Extra
intestinal E. coli (ExPEC) other virulence genes such as pap, fimH, sfa, iha,
hlyA, cnf1 or sat are of importance (eg. [Hung et al.
2019](https://www.sciencedirect.com/science/article/pii/S168411821830433X?via%3Dihub),
[Wang et al.
2009](https://www.clinicalmicrobiologyandinfection.com/article/S1198-743X(14)60399-2/fulltext),
[Rodríguez-Villodres et al.
2019](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6947626/#B12-jcm-08-02118)).
As stx subtypes might be highly similar a specific database has been created
associated with
[VirulenceFinder](https://cge.cbs.dtu.dk/services/VirulenceFinder/). Natural
evolution, horizontal transfer of antimicrobial resistant elements as well as
the use of antibiotics  have contributed to the emergence of multi-drug
resistant isolates, and this has become a worrying issue that is increasingly
observed ([Poirel et al. 2018](https://pubmed.ncbi.nlm.nih.gov/30003866/)). Of
particular concern is the acquisition of genes conferring resistance to
broad-spectrum cephalosporins, carbapenems aminoglycosides, and
(fluoro)quinolones ([Poirel et al.
2018](https://pubmed.ncbi.nlm.nih.gov/30003866/)). For this reason, monitoring
of virulence- and antimicrobial resistance-related genes is of great relevance
to determine the best way of action in the presence of a case of infection or
even an outbreak. As mentioned in the “Virulome and
Resistome'' section, where more details can be found, this is performed by
comparing the genome to a database comprising a set of genes of interest.
Examples of predefined resistome databases are mentioned in the same section.
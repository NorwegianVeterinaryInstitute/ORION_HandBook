# Virulence and AMR Detection

## Finding methods

Disease surveillance has as its ultimate goal the decrease of human (and animal) illness. 
This is done not only by the rapid detection and control of disease outbreaks, for which WGS 
typing methods represent a relevant technological advance (see [Serotyping section](serotyping.md))
, but also by the identification of phenotypically-relevant markers (and their changes at the 
population level), such as virulence- or antimicrobial resistance-associated genes. Therefore, 
the analysis of the virulome (complete set of virulence genes) and the resistome (complete set of
antimicrobial resistance genes) is of extreme relevance in the context of surveillance and outbreak
control.

Differences at the genome level involving point mutations or presence/absence of certain loci may 
have great impact in pathogens' behavior, and consequently in the disease. For example, presence of 
_tetO_ and point mutations in _gyrA_ have been associated with increased resistance to tetracyclines 
and fluoroquinolones in _Campylobacter jejuni_ 
([Fiedoruk et al. 2019](https://gutpathogens.biomedcentral.com/articles/10.1186/s13099-019-0313-x)). 
Moreover, specific genes, such as those involved in the adhesion to human cells or those related to 
the efflux of certain molecules, have been particularly associated in many microorganisms with virulence 
and antimicrobial resistance, respectively 
([Poimenidou et al. 2018](https://www.frontiersin.org/articles/10.3389/fmicb.2018.01103/full#B4), 
[Anbazhagan et al. 2019](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6511633/), 
[Vieira et al. 2017](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5666138/)). 
These genomic features can be acquired not only by vertical evolution, but also by 
[horizontal gene transfer](https://en.wikipedia.org/wiki/Horizontal_gene_transfer). For instance, the 
existence of [plasmids](https://en.wikipedia.org/wiki/Plasmid) and 
[transposable elements](https://en.wikipedia.org/wiki/Transposable_element) allows the interchange of 
genetic material between distantly related lineages (reviewed in 
[Gyles and Boerlin, 2014](https://journals.sagepub.com/doi/pdf/10.1177/0300985813511131)), 
thus contributing to the introduction and expansion of new virulence- or resistance-related phenotypes 
in some lineages. This may contribute to the emergence of different phenotypes which may impact, for 
example, the pathogenic behavior and the host range. Therefore, there is a need for constant surveillance 
of the resistome and the virulome in bacterial pathogens.

Similarly to what occurs with molecular typing, virulome and resistome analysis relies on the assessment 
of the presence of genetic traits (specific genes or mutations) which have previously been associated with 
relevant phenotypes. In the pre-WGS era, this search could be performed, for example, by amplification and 
detection of specific target genes. Such an approach could be particularly challenging for presence of 
unexpected genomic changes which prevent the amplification of the region of interest, or by the presence of 
horizontally transferred genes which would not be detected. By providing information at the whole-genome level, 
WGS overpasses these drawbacks as information is expected to be provided independently of the genetic 
variability of the sample. With WGS data, the identification of genes/alleles of particular interest can be 
performed by the comparison of the genome of the sample with a database comprising precisely the set of genes of 
interest. In the particular case of the virulome and the resistome, there are public databases where those sets 
of genes are already available and programs which automatically perform this search.


## Database resources

Several databases exist for both antimicrobial resistance-associated genes and mutations and virulence genes. 
These differ in their content and curation procedures, and may therefore produce different outputs when used 
within the same tool. Some databases have species-specific subdatasets, such as the PointFinder and VirulenceFinder 
databases. Other databases have more comprehensive content, such as MEGARes, CARD, and VFDB. A user should be cautious 
when selecting a database, and have knowledge about their limitations and content, as it is only possible to identify 
the genes/mutations that are present in the database.  Examples of predefined resistome databases for bacteria include:
  
- [Bacterial Antimicrobial Resistance Reference Gene Database](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA313047)
- [Bacterial Antimicrobial Resistance Reference Gene Database](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA313047)
- [The Comprehensive Antibiotic Resistance database (CARD)](https://card.mcmaster.ca)
- [ResFinder](https://bitbucket.org/genomicepidemiology/resfinder_db/src/master/)
- [PointFinder](https://bitbucket.org/genomicepidemiology/pointfinder_db/src/master/) (detection of chromosomal point 
  mutations associated to resistance)
- [MEGARes](https://megares.meglab.org)


Examples of predefined virulome databases for bacteria include:

- [Virulence Factor Database (VFDB)](http://www.mgc.ac.cn/VFs/main.htm)
- [Virulence Finder](https://bitbucket.org/genomicepidemiology/virulencefinder/src/master/)
- [VirulenceDB](https://microscope.readthedocs.io/en/stable/content/compgenomics/virulence.html#what-is-virulencedb)
- [PathogenFinder](https://cge.cbs.dtu.dk/services/PathogenFinder/)


## Tools
[ResFinder](https://cge.cbs.dtu.dk/services/ResFinder/), [PathogenFinder](https://cge.cbs.dtu.dk/services/PathogenFinder/) 
and [VirulenceFinder](https://cge.cbs.dtu.dk/services/VirulenceFinder/) are associated with user-friendly web-based 
interfaces, which have the same name as the database, for the search of genes of interest. [
ResFinder](https://cge.cbs.dtu.dk/services/ResFinder/) has the option to search for both acquired resistance genes, 
as well as resistance-associated chromosomal mutations. The above tools also exist as command-line tools, which can be 
implemented into workflows and pipelines. While these web- or command line- based programs rely on their respective 
databases, other programs have been developed to perform a broader search for the genes of interest by integrating several 
of the above-mentioned databases. Examples of such programs are [ABRicate](https://github.com/tseemann/abricate), 
[ARIBA](https://github.com/sanger-pathogens/ariba) and 
[AMRFinderPlus](https://www.ncbi.nlm.nih.gov/pathogens/antimicrobial-resistance/AMRFinder/). Moreover, 
[ABRicate](https://github.com/tseemann/abricate) and [ARIBA](https://github.com/sanger-pathogens/ariba) allow you to 
create your own database. Of note, the majority of these programs rely on sequence alignment, using for example BLAST, 
and only accept fasta sequences as input. Exceptions to this are [PathogenFinder](https://cge.cbs.dtu.dk/services/PathogenFinder/), 
which applies prediction models to determine the pathogenic nature of the isolate, and the most recent versions of 
[ResFinder](https://cge.cbs.dtu.dk/services/ResFinder/) and 
[PointFinder](https://bitbucket.org/genomicepidemiology/pointfinder_db/src/master/), which have incorporated 
[KMA](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2336-6) allowing the k-mer based alignment 
of genomic reads (no need for genome assembly) on the database, and [ARIBA](https://github.com/sanger-pathogens/ariba) which 
relies on a read mapping approach using paired-end reads to identify the genes of interest.


## Interpretation of results

Regardless of the tool, the main output provided by this kind of analysis is the  presence/absence of gene of interest 
or mutations (i.e., genotype) and their potential impact on  the phenotype (e.g., increased virulence, antibiotic resistance). 
This output is usually provided in tabular format (e.g., text files, which are useful for automated report generation and 
downstream applications), in combination with additional output files for better data visualization and interpretation (e.g., 
interactive QC color codes, graphics, etc).  This is true for both the online and command-line versions of the tools, where the 
command-line version often has the option to produce additional output files. Interpretation of the different reports can be 
difficult for the general user, especially for tools that have extensive quality control of the genes/variants predicted, e.g. 
ARIBA. Handling such reports usually requires an in-depth knowledge of how the tool works, and knowledge of its sub-constituents. 
This may not be viable for the everyday user. Therefore, learning how to interpret such reports may be a huge hindrance for many 
that want to use these tools. For example, ARIBA may produce reports that scale several hundred rows of data for a single isolate. 
This is due to the extensive quality control of each gene and/or variant identified, where ARIBA supplies a “flag” to describe the 
success or failure of the process. Each flag has its own interpretation, which the user needs to be aware of to interpret the results 
correctly. Reports of such scale are therefore not meant for in-depth human reading, but rather for automatic handling and 
interpretation by set rules. This is already supplied with ARIBA, as it can interpret and summarise the results from several isolates 
with one line of code.

Due to the differences in output reports, comparing results across tools may be a difficult task. The 
[hAMRonization](https://github.com/pha4ge/hAMRonization) tool addresses the issue of comparing results from several AMR gene-finding 
tools. hAMRonization is a parser tool that combines the output of several AMR gene-finding tools and generates a standardised AMR gene 
report, easing interpretation and comparison of tools.

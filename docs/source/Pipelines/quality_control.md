# Quality control and preprocessing

## Fastqc / Multiqc analysis
After sequence data is delivered to the analyst / researcher it first needs to
be checked to assure that the data is of good enough quality to work with. This
is mostly done by performing an analysis with the program
[Fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/). The
software Fastqc summarizes the fastq file data, and displays information about
read length, average quality score along the read, GC-content, number of
ambiguous bases, the presence of sequencing adapters, and various other
parameters useful to determine the quality of the raw sequence data. The
program [Multiqc](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5039924/) can be
used to combine the output of multiple fastqc output files, or many other
programs, so that many datasets can be inspected simultaneously.

## Controlling contamination
Besides general inspection of the data, it is also wise to check for possible contaminants present in the sequence data files. Sequence data can contain exogenous sequences (generally at low frequency) derived from contaminants introduced during either the DNA extraction or the library prep phases. This is mostly of serious concern when working with small amounts of input material and when using PCR amplification ([Salter et al., 2014](https://bmcbiol.biomedcentral.com/articles/10.1186/s12915-014-0087-z#Sec1); [Drengenes et al., 2019](https://bmcmicrobiol.biomedcentral.com/articles/10.1186/s12866-019-1560-1)). In all cases, it is advisable to remove contaminating sequences from the sequence data.

The origins of the microbial contaminants can be diverse and they are found in ultrapure water systems, molecular biology kits or laboratory reagents ([Salter et al., 2014](https://bmcbiol.biomedcentral.com/articles/10.1186/s12915-014-0087-z)). In addition, some experimental procedures deliberately add control DNA to improve throughput or for normalization purposes so different samples can be compared. For example, the Illumina sequencing platform uses the genome of the phage PhiX ([Sanger et al., 1977](https://pubmed.ncbi.nlm.nih.gov/870828/)). as a control in the sequencing run. It is included for quality and calibrations purposes, but when not detected in the sequence data it can contaminate such data with far reaching consequences ([Mukherjee et al., 2015](https://environmentalmicrobiome.biomedcentral.com/articles/10.1186/1944-3277-10-18)). Additional sources for contaminating data can be human sequences due to laboratory contamination, or because the sample was associated with host tissue (as in the case of metagenomic experiments).  In labs where DNA extraction of other species is performed on a large scale, it is possible that DNA fragments of other species can contaminate the samples when DNA extraction is done without measures to prevent such contamination.

In addition to contamination due to laboratory methods, contaminants can also be present due to entirely natural causes. In the case of whole genome sequencing, contaminants are often due to pure cultures containing an additional bacterial species or the culture is a different species than expected.

Contamination is commonly detected by either:
- comparing the sequence data to a
reference genome and calculating a distance measure as done by the program
[Mash](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4915045/),
- by mapping the reads to the human or other relevant genomes,
- or by classifying the reads against a database
containing reference genomes and identifying if there are reads that do not belong to the target species. This is often done with tools from metagenomics research such as [Kraken2](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6883579/),
[Centrifuge](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5131823/), etc.

Contamination can be removed via mapping or classification of reads to either a reference genome (e.g. PhiX or Homo sapiens) or a dedicated reference database (see for instance this publication: [Bush et al., 2020](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000393)). Reads that match are then removed and it is assumed that the remaining reads are clean from contamination. Assembled microbial genomes can / should also be screened for the presence of contaminating sequences, for instance the genome of the Phage phiX readily assembles as one contig when the Phix sequences were not removed before assembly. This can also be done by screening the contig sequences using blast or other approaches ([Mukherjee et al., 2015](https://environmentalmicrobiome.biomedcentral.com/articles/10.1186/1944-3277-10-18)).

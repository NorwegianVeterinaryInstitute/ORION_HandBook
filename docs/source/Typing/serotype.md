# Serotyping
Serotyping has traditionally played an essential role in determining species and
subspecies, and has been used for epidemiologic classification down to
subspecies level. The method is based on serological typing of the  cell surface
antigens of the bacteria. A serotype (syn. serovar: [International Code of
Nomenclature of Prokaryotes,
2019](https://www.microbiologyresearch.org/content/journal/ijsem/10.1099/ijsem.0.000778),
p134) corresponds to  the combination of surface structures or antigens. This
has been proved to be an effective way of discriminating groups of bacteria,
with some serotypes being host specific and others associated with virulence
intensity (high/mild)
([CDC](https://www.cdc.gov/salmonella/reportspubs/salmonella-atlas/serotyping-importance.html)).
Moreover, further research experiments have associated serotypes to particular
features such as pathological properties, susceptibility to antimicrobials and
niche distribution (eg. [Ørskov, F. and Ørskov, I.
1992](https://cdnsciencepub.com/doi/abs/10.1139/m92-115), [Yang, X. et al.
2015](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4567320/) [Lee, S. et al.
2018](https://mbio.asm.org/content/9/2/e00396-18.short), [Zoz, F. et al.
2017](https://www.sciencedirect.com/science/article/abs/pii/S0168160517300715)).

Traditional serotyping (wet lab) relies on the detection of cell surface
antigens by agglutination assays using species-specific antibodies (see the
Species specific sections for which ones). Serotyping has been used in
epidemiology since 1960 in the wet-lab to detect Salmonella outbreaks, and as
per today more than 2,500 have been described in this species. As the expression
of surface structures of each pathogen are coded in their genome, molecular
typing methods based on the detection/amplification of certain alleles or DNA
sequences have been developed (eg. [Beaubrun et al.
2012](https://pubmed.ncbi.nlm.nih.gov/22608224/), [Borucki et al.
2003](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC309009/), [Iguchi et al.
2015](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4508431/)). The advent of WGS
technologies brought a higher discriminatory power for genetic clustering
without losing the ability to link genomic information to previously available
knowledge. This has led to the implementation of a gradual technological
transition and to the need of using WGS data for serotyping. Some studies have
compared traditional serotyping with WGS based serotyping (egr:
[Salmonella](https://www.frontiersin.org/articles/10.3389/fmicb.2019.02554/full),
[Escherichia
coli](https://www.frontiersin.org/articles/10.3389/fmicb.2016.00644/full), and
[Listeria
monocytogenes](https://www.sciencedirect.com/science/article/pii/S0168165616313487).

Whole genome based serotyping can be done in different ways:
- By emulating laboratory methods such as presence/absence DNA-fragments
  detection PCR. 
- By detecting alleles within a set of antigen-genes loci (serotyping performed
  like MLST finding).  
- By specific genes identification, by either mapping or BLAST searches towards
  serotype determinants.

## Serotyping by in-silico PCR
When marker genes are associated to at set specific antigens are defined, it is
possible to determine serogroups based on the presence/ absence of the PCR
amplification pattern of a combination of specific gene markers (eg. [Doumith et
al. 2004](https://jcm.asm.org/content/42/8/3819)). PCR based serotyping can be
bioinformatically emulated (ePCR, in silico PCR), and serotypes can thus be
inferred from whole genome sequencing data. In such cases presence / absence of
genes can be detected using blast in conjunction with a set of rules determining
when to consider a match presence or not (Eg. as performed on assemblies in
[LisSero](https://github.com/MDU-PHL/LisSero) for ePCR serotyping of Listeria
monocytogenes, or In Silico PCR for fliC and filB alleles of the H antigens for
Salmonella serotyping with assemblies in
[SeqSero1](https://jcm.asm.org/content/53/5/1685)). 
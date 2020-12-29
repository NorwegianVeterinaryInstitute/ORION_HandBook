# xMLST methods
MLST (multi locus sequence typing) was first developed
[in 1998 for N. meningitidis](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC19708/).
The idea is to select a set of loci in the genome, and get the alleles in each
genome for these loci. Typing is then done by seeing what isolates have which
combination of alleles for each locus.

## Schema
With MLST, the focus is on a subset of genes or loci that are known to be
present in most, if not all strains of that species, but which are also known
to have some sequence variation. The loci selected for use in MLST constitute
the schema for that species. Commonly, for the original type of MLST, the number
of genes chosen was 7. These are commonly housekeeping genes. There are several
extensions of this that have come in later years, among them core genome MLST
(cgMLST) and ribosomal MLST (rMLST). The main difference between the methods is
in the criteria for how loci are included in the schema.

## Allele and nomenclature
For each gene or locus in the schema, it is possible to have different sequence
variants, or alleles. The different variants that have been observed can be
collected in a database. Each observed allele for a gene can in this database
be given a label, commonly a number. It is important to realize that these
labels or numbers are attributed sequentially when detected, but do NOT provide
any indication of relatedness or similarity between the alleles.

For the original “7-gene” type of MLST, several international nomenclature
databases with alleles have been established. With access to such nomenclature
databases, it is possible to ensure that all alleles have a unique number. This
means that if using the same schema and the same database, two institutions can
exchange information and know that they are referring to the same alleles.

## Profile and sequence type
Each isolate can be typed by finding the sequence for each of the loci the
schema. Once the sequence is found, it is compared to known alleles for that
locus. This is usually done by comparing to alleles downloaded or otherwise
accessed from the nomenclature server. If it is identical to an allele from
the nomenclature database, the allele number for that locus is assigned to that
isolate. If not, the allele is commonly uploaded to the server, which then
assigns it a new number. The set of identifiers for an isolate is called it’s
profile. The profile is commonly collapsed into a sequence type number, where
each ST represents a unique combination of alleles for each locus.

Provided that the allele numbers and sequence type numbers are assigned by the
same central nomenclature server, sequence types can be compared between
institutions. Some institutions, like EFSA, can under certain circumstances
allow organizations to submit sequence types, thus avoiding the need for
uploading the full sequence.  

## Typing/Nomenclature databases

There are three main MLST nomenclature/database servers.  
* https://pubmlst.org/
* https://bigsdb.pasteur.fr/
* https://enterobase.warwick.ac.uk/


It is important to realize that these work independently from each other. A
sequence type only makes sense provided it is known which system has been used.

## MLST finding methods

There are two main strategies for finding MLST genes.

* Assembly strategy: in this case the genomes are first assembled. Next, the
allele set included in the typing database is used to search the genome,
[commonly using BLAST](blast page). The results are subsequently post-processed
to get the allele and then compared to a profile database to assign ST numbers.

* Mapping strategy: in this case, the reads for each isolate is mapped against
the allele typing database. Next, those reads are collected and assembled into
genes. These are then compared to the alleles in the database, and allele and
ST numbers are assigned.

## MLST software
There are many tools for doing MLST from both reads and assemblies available. It is important to realize that even though they might use the same schema, they might not give the same results. [A review of various MLST tools and their results can be found in this paper.](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000124)


## cgMLST

cgMLST is an extension of the original seven-loci MLST method. Conceptually speaking it works in the same way as MLST. The main difference lies in how the
schema is established, and how many loci are included. Since cgMLST schemas
commonly include thousands or more genes, it is more common to use cgMSLT
more as a way of measuring differences between genomes, than to do typing as
such. However,  


## cgMLST nomenclature servers

* https://pubmlst.org/
* https://bigsdb.pasteur.fr/
* https://enterobase.warwick.ac.uk
* https://chewbbaca.online/

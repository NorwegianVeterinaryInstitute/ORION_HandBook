# Sequence file formats

Sequencers output their data in different formats according to what technology they are. Illumina sequencers output fastq-files, while Nanopore output their files in the Fast5 format. Pacbio however outputs their results in the BAM format.

## Illumina - Fastq files
Fastq files are text files containing the biological sequence data produced by a sequencing machine. The “FASTQ format” is used to represent sequence data: a nucleotide sequence together with associated quality scores (for each base). The fastq file format is a standard format, consisting of 4 lines for each sequence:

- Line 1 starts with @, and is followed by an identifier. The identifier can be designed as the user wished, but in most cases it contains the sequencing machine ID, the sequencing run ID, the sequencing date, and a unique ID for the sequence.
- Line 2 is the raw sequence data. This section can be wrapped over multiple lines.
- Line 3 begins with a +, and can optionally contain the same information as line 1. This line is to indicate when the raw sequence in line 2 has stopped.
- Line 4 contains the Phred quality score information which is encoded using the ASCII characters 33 to 126.

Fastq files are usually compressed allowing storage of the same information while using less storage space. Compression softwares such as: gzip, bzip are standardly used. The compressed format is indicated by the following extensions: “.fastq.gz” or “.fq.gz”. Most modern applications are able to extract the data from gzip compressed datasets and process the data for further use.

For paired-end data the fastq files come in pairs: “SAMPLE_R1.fastq.gz” and “SAMPLE_R2.fastq.gz” are the forward and the reverse reads files.

## Illumina sequence architecture
The sequences produced by illumina sequencers consist of several parts, which is dependent on the experimental design. For a simple shotgun sequencing experiment, the sequence contains the shredded DNA fragment to which sequencing adapters are ligated. In contrast an amplicon sequencing experiment with multiple samples, contains the amplicon sequence as well as the amplification primers, a heterogeneity spacer (needed to make the library more complex), and a barcode or index to separate the samples. At the end it contains the sequencing adapters (see for instance [Figure 1 in this article](https://microbiomejournal.biomedcentral.com/articles/10.1186/2049-2618-2-6)).

The experimental design therefore dictates how the sequences are handled bioinformatically after delivery of sequencing data. The Illumina machine software will use the indexes to group sequences in samples and it can be set up to remove the adapter sequences. For most sequences this means that one adapter sequence is removed. But the other adapter might be present as well:  depending on the length of the sequenced fragment and how many bases were sequenced, therefore the later needs to be removed by the user of the data.

## Nanopore - Fast5 files
Fast5 files are used for storing the output from Nanopore sequencing machines. These files are based on HDF5 file format. A fast5 file contains three sources of information: raw sequence data in picoampere, the event-level data, and base-level data. In addition, the fast5 files can also contain configuration data, based on the pipelines used to process the fast5 file, and summary data.

The event-level data is an aggregate of the raw data that on average describes the signal that belongs to one nucleotide ([for a more detailed explanation see here](http://simpsonlab.github.io/2017/02/27/packing_fast5/)).

The base-level data is the fastq information of each base with the corresponding quality value and stored in a compressed manner. The quality scores inside the fast5 format are capped at a maximum score of 31. That means that quality scores higher than 31 are [set to 31](http://simpsonlab.github.io/2017/02/27/packing_fast5/).

## Nanopore sequence architecture
Nanopore sequencing produces sequences that contain the DNA fragment with ligated to its ends sequencing adapters. In the case of multiple samples, barcodes are first ligated to the DNA fragments before sequencing adapters are ligated to the barcodes.

## Pacbio - BAM files
The sequencer from Pacific biosciences will output the sequence data in a Binary Alignment Map file, or BAM file. Such files are binary, compressed, and they are a record-oriented container format for raw or aligned sequence reads [Pacbio BAM file format](https://pacbiofileformats.readthedocs.io/en/10.0/BAM.html). The uncompressed BAM files are called [Sequence alignment map (SAM)](https://en.wikipedia.org/wiki/SAM_(file_format)) files, which are text files that contain alignment information of sequences against a reference sequence. A difference with “regular” BAM files, is that the Pacbio BAM files can contain information in the [header](https://pacbiofileformats.readthedocs.io/en/10.0/BAM.html) on the sequencing machine used, the sequencing kit, barcodes etc.
Since the Pacbio sequencer can produce different kinds of reads, the BAM files are named accordingly. e.g. a file with unaligned ccs reads: “FileName.ccs.bam”, and aligned ccs reads are : “FileName.aligned_ccs.bam”.  The sequences in the BAM files can be exported to FASTQ or FASTA formatted files.


## Pacbio sequence architecture
With Pacbio sequencing DNA fragments are end-repaired and special sequencing adapters are ligated to the ends (see [Figure 1 in this paper](https://www.nature.com/articles/s41587-019-0217-9)). The structure of the sequencing adapters allows for repeated sequencing of both strands since a circular template molecule is created. The sequencing of such fragments then generates sequences that consist of both strands of the original fragment separated by the adapter sequence. The reads generated using such a strategy are called circular consensus sequences (CCS) and using dedicated tools these sequences are then transformed into a high quality sequence. The amount of times that a single sequence passes the polymerase, determines the sequencing quality after data processing. For instance, four passes will give a read with a Phred Quality score of 20 (99 % accuracy), while nine passes will give a quality score of 30 (99,9 % accuracy) ([Amarasinghe et al., 2020](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-020-1935-5)).

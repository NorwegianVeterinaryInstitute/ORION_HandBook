# Storage and Compute Infrastructures

## Storage

### Package format
Commonly, when data is delivered by the sequencing facility, they will come in
what is called a [“tar”](https://en.wikipedia.org/wiki/Tar_(computing)) format.
This is a way of grouping files into one package. Note, as opposed to the “zip”
format, files in a tar archive are only packaged into one file. Files that are
in the archive may or may not be compressed, but that is done independently of
the packaging. Files inside of such an archive are commonly compressed with a
tool called [“gzip”](https://en.wikipedia.org/wiki/Gzip).

Note: commonly the tools to unpack a tar archive are not available on a windows
machine. These tools are available on linux and in the terminal on Macs (Mac
systems are linux based). However, on windows the terminal program [Git
Bash](https://gitforwindows.org/) does contain these tools, in case there is a
need for unpacking on a windows machine.

To unpack a tar file the following command can be used:

`tar -xvf mypackage.tar`

The `-x` means extract, the `-v` means show me the progress on the screen and
`-f` means the filename of the archive is given on the command line.

Once an archive file has been unpackaged, there will likely be a folder or a
directory present on your computer filled with files ending in “.gz”. This
indicates that your sequencing files are compressed, most likely using the tool
mentioned above. Many sequence analysis tools are able to work with compressed
files, thus these can be left as is. If not, the “gzip” tool can be used to
unpack the files. In true linux fashion, however, the command for unpacking
these files is not “gzip”, it is “gunzip”.

### Space
Sequencing data can consume quite a bit of space. Generally speaking, one set of
Illumina paired end read files for one isolate will take up about 0.5-1GB of
space. However, in the course of processing this is commonly likely to expand
somewhere between 5-10 times the original space of the raw data. As is described
later, the analysis of the data mostly consists of processing the files, and
then storing the results as a new set of files. Hence, it is likely that this
process will produce somewhere between 5-10 different sets of derived data. The
space consumed by these derived files are likely to shrink by each step, but
many of these processing steps will not reduce the file size drastically.

Here are some size estimates from an assembly pipeline consisting of commonly
used tools. Reads here means the raw untrimmed data from the sequencer. Work
folder here indicates the size of the files produced by the pipeline, i.e.
trimmed files, bam files used for polishing etc. These do not necessarily need
to be kept. Results indicates the size of the output that would be used further
on, i.e. assemblies, annotation files, antibiotic resistance results, etc. These
data are likely to be kept and used onwards.

| #isolates | Reads  | Results | Work   | Total  |
|-----------|--------|---------|--------|--------|
| 10        | 5 Gb   | 750 Mb  | 10 Gb  | 15 Gb  |
| 100       | 40 Gb  | 10 Gb   | 100 Gb | 150 Gb |
| 500       | 200 Gb | 50 Gb   | 500 Gb | 750 Gb |

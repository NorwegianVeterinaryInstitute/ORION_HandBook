#Workflow managers 

## What is a workflow manager 

As is described in [Data Production], a bioinformatics analysis pipeline
commonly consists of many tools chained after each other, each tool providing
input to the next step in the process. This means that an analysis can consist
of many steps, each with their own inputs and options. Running these analyses by
hand can be time consuming and error prone. To help with this, several so-called
workflow managers or engines have been developed. These are tools that allow for
creating a script for your analysis, detailing all of the steps. Many people
write this up in bash the first time they try to do this. However, with bash the
person writing it will have to figure out where all of the files are, and also
take care of the error handling. In addition, in many cases analyses will have
to be done on a compute cluster, and that adds another layer of complexity that
workflow managers can sort out on their own. 

There are several tools to manage workflows/pipelines available. In this section
some of the major players will be described. 

## Nextflow

[Nextflow](https://nextflow.io/) is a domain specific language
[DSL](https://en.wikipedia.org/wiki/Domain-specific_language) created
specifically for handing bioinformatics analyses. This is a programming language
that allows the user to create pipelines connecting many tools together.

The central entity in Nextflow is a process. A process is akin to a function, in
that it takes in a set of input data, and produces output. Output is produced by
the process executing something on the input, for instance running SPAdes on a
read set to produce an assembly. Data input and output to a process is handled
via [non-blocking unidirectional FIFO
queues](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)). A data
set is put into the input queue of a process, and the process will then pick
that data set out of the queue and process it. The output will then be put into
a separate output channel, which then can be used as an input channel by a
different process. In this way processes can be chained together to create a
pipeline. 

The channel system also takes care of file handling. Nextflow operates with the
concept of a “work” directory. For each run of a process on a specific data set,
a specific directory is set up in the work directory to deal with the data
needed and produced by that process. The input data to that process is
“softlinked” in from its current location into that directory.
[Softlinking](https://en.wikipedia.org/wiki/Symbolic_link) is a way of making
“shortcuts” from one location in the file system to another.  In this case, the
input data to that process is softlinked into the process directory in such a
way that it looks like it is in that directory. The output data from that
process is stored in the processis directory. Any processes working on the
output data further downstream in the pipeline will then softlink to the
output data in its current work directory location. Thus, most of the data that
is produced by a pipeline will be found in the “work” directory. Data that
should be viewable by the user at the end of the run can be tagged in the
process by the “publishdir” directive. These data will then be available in the
directory specified by the “publishdir” directive. 

Due to the way processes are set up, it is also possible to have conditional
executions of parts of the pipeline. This allows for evaluating results before
proceeding with the analyses. In addition, it allows the user to have one
complete pipeline, and depending on user input and user options only parts of
the pipeline will be run. 

Another benefit of Nextflow is that it is able to run on High Performance
Computing systems. In practice this means that Nextflow will produce a batch
file for each run of a process, and that file will then be submitted to the
queueing system. Nextflow will then check in with the system and see if
processes are running well or not. If a process does not complete well, it can
be auto-restarted. If a process still won’t produce satisfactory results, the
rest of the pipeline will  either not be run and the pipeline will terminate, or
the particular step is ignored and there is no further processing of the dataset
that failed. 

Since a lot of scientific software tools can be difficult to install on local or
HPC systems, it might be challenging to build a pipeline in nextflow using
several tools, each with their own installation requirements. To circumvent this
Nextflow can works with  with a variety of systems such as both
[conda](https://docs.conda.io/en/latest/) environments or with container
systemss ([Docker](https://www.docker.com/resources/what-container),
[Singularity](https://sylabs.io/guides/3.0/user-guide/index.html), etc) both
singularity and docker). These systems can make installation of software easier
since the installed software is isolated and independent from the software
installed locally or on a cluster. In addition, containers can make pipelines
more reproducible, since the used software version can easily be installed on a
different computing system. Nextflow can be pointed to software, available
online as a conda environment or a container, required for a single or multiple
processes and nextflow will automatically install the required software needed
for a process before starting the analysis. 


## Snakemake 

[Snakemake](https://snakemake.readthedocs.io/en/stable/index.html) is another
workflow manager that functions in a similar manner as nextflow. A main
difference to nextflow is that Snakemake uses a Python based syntax for
programming pipelines. Other than that Snakemake uses rules that describe each
of the steps in a pipeline. These rules also contain which input files to use
and what to do with the output files. One difference with nextflow is that
Snakemake is set-up via conda, and to run snakemake it is required to start a
conda environment. 

An interesting part of Snakemake is that workflow creation can be checked with a
code quality checker which helps the creater to improve the readability and
stimulates best practices when writting code. In a similar way to nextflow,
Snakemake can be run on a local computer as well as on a HPC cluster or the
Amazon cloud.
 
## Galaxy

Galaxy is a web based, user friendly, scientific workflow platform for analyses
especially for researchers who want to analyse their data using bioinformatics
tools within a graphical interface. Programming knowledge is not needed to
upload data, run analyses and export the results. However, it is also possible
to use Galaxy as a pure workflow manager, without the graphical interface.  

Most of the known bioinformatics tools can be installed through Galaxy toolshed,
tools repository for galaxy. New tools also can be added without any complex
technical steps. Each new tool needs a tool definition file (xml) where input
data, parameters, output and tool location are defined. Galaxy uses this file to
produce the user interface for the tool, execute the tool and display the
results.  Galaxy also comes with visualization tools to visualize data and the
results. Galaxy recommends to use conda package manager as the best practice to
manage the tool dependencies for each tool which can be configured in
galaxy.config file. 

Each user can have username and password. Using a galaxy without a username and
password is also possible. Galaxy history section keeps track of all the
analyses done by each user. Users can not see other users' history if they are
not shared with them.  These analyses can be easily re-run and also exported to
another galaxy to reproduce.

Galaxy allows users to create workflows easily using a simple user interface.
Workflows can use high performance computing to analyse big/high throughput
data. Workflows can be exported from one instance of Galaxy and imported to
another instance manually. Thus, Galaxy makes the reproducibility of analyses
easier.

Galaxy is an open source software implemented in the Python programming
language. Galaxy has a very active developers’ community which actively adds new
features a few times a year. Galaxy can be installed in a user laptop for a
single user use or in a high performance computing server for a multiuser
purpose. Docker containers and Ansible playbooks are also used to deploy galaxy
easily. Popular database management systems such as MySQL, PostGres can be used
by Galaxy to store the user, data and analysis details. 

Galaxy can be configured to use
[slurm](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) to make use of
high performance clusters. Galaxy comes with a remote job running system called
Pulsar. Using pulsar Galaxy jobs can be sent to remote computing resources and
get back the results. Transport of data, tool information and other metadata can
be done using [RabbitMQ](https://en.wikipedia.org/wiki/RabbitMQ).

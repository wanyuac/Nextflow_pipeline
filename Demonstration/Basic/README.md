# Nextflow scripts for basic tasks

This repository contains short scripts for pipelines performing simple tasks.

<br/>

**Table of Content**

- [First pipeline (PL\_1)](#PL1)
- [Second pipeline: multiple input files (PL2)](#PL2)
- [Options of Nextflow](#options)

<br/>

## 1. First pipeline
<a name = "PL1"></a>

This script implements a simple pipeline, which is composed of a single process `pbs_job` and runs on an HPC through the PBS. Users need three files to run this pipeline: `pbs_job.nf`, `nextflow.config`, and the input file `demo1.fasta`. The command to run this pipeline is:

```bash
nextflow run pbs_job.nf -profile pbs_shifter

N E X T F L O W  ~  version 19.01.0
Launching `pbs_job.nf` [backstabbing_banach] - revision: c018187b0f
[warm up] executor > pbs
[c2/48ff7a] Submitted process > basic_io (1)
```

A work directory `work` and a log file `.nextflow.log` are produced by Nextflow. The only output file `name.txt` is generated in the directory `work`. A hidden file `.command.run` is the script automatically generated from the pipeline script `pbs_job.nf` and the pipeline configuration file `nextflow.config` and submitted to PBS by Nextflow. In this script, the configuration `-lselect=1:ncpus=1:mem=1gb` is mandatorily required by the ICL's HPC.

<br/>

## 2. Second pipeline: multiple input files (PL2)

<a name = "PL2"></a>

In this example, the pipeline takes as input multiple FASTA files and generate an output file for each FASTA file. All the output files are created under the same output folder. This example shows how to apply a process to multiple input files in parallel.

```bash
nextflow run multiple_inputs.nf -profile pbs_shifter

N E X T F L O W  ~  version 19.01.0
Launching `multiple_inputs.nf` [grave_gilbert] - revision: a74b249e8d
[warm up] executor > pbs
[09/91674f] Submitted process > basic_io (5)
[e6/3f8436] Submitted process > basic_io (4)
[20/588bb4] Submitted process > basic_io (3)
[f7/01399a] Submitted process > basic_io (2)
[57/692345] Submitted process > basic_io (1)
```

<br/>

## Appendix. Options of Nextflow
<a name = "options"></a>

**Options of `nextflow`**

```bash
nextflow -h
Usage: nextflow [options] COMMAND [arg...]

Options:
  -C
     Use the specified configuration file(s) overriding any defaults
  -D
     Set JVM properties
  -bg
     Execute nextflow in background
  -c, -config
     Add the specified file to configuration set
  -d, -dockerize
     Launch nextflow via Docker (experimental)
  -h
     Print this help
  -log
     Set nextflow log file path
  -q, -quiet
     Do not print information messages
  -syslog
     Send logs to syslog server (eg. localhost:514)
  -v, -version
     Print the program version

Commands:
  clean         Clean up project cache and work directories
  clone         Clone a project into a folder
  cloud         Manage Nextflow clusters in the cloud
  config        Print a project configuration
  drop          Delete the local copy of a project
  help          Print the usage help for a command
  info          Print project and system runtime information
  kuberun       Execute a workflow in a Kubernetes cluster (experimental)
  list          List all downloaded projects
  log           Print executions log and runtime info
  pull          Download or update a project
  run           Execute a pipeline project
  self-update   Update nextflow runtime to the latest available version
  view          View project script file(s)
```



**Options of `nextflow run`**

```bash
nextflow run -h
Execute a pipeline project
Usage: run [options] Project name or repository url
  Options:
    -E
       Exports all current system environment
       Default: false
    -bucket-dir
       Remote bucket where intermediate result files are stored
    -cache
       Enable/disable processes caching
       Default: true
    -dump-channels
       Dump channels for debugging purpose
    -dump-hashes
       Dump task hash keys for debugging purpose
       Default: false
    -e.
       Add the specified variable to execution environment
       Syntax: -e.key=value
       Default: {}
    -h, -help
       Print the command usage
       Default: false
    -hub
       Service hub where the project is hosted
    -latest
       Pull latest changes before run
       Default: false
    -lib
       Library extension path
    -name
       Assign a mnemonic name to the a pipeline run
    -offline
       Do not check for remote project updates
       Default: false
    -params-file
       Load script parameters from a JSON/YAML file
    -process.
       Set process options
       Syntax: -process.key=value
       Default: {}
    -profile
       Choose a configuration profile
    -qs, -queue-size
       Max number of processes that can be executed in parallel by each executor
    -resume
       Execute the script using the cached results, useful to continue
       executions that was stopped by an error
    -r, -revision
       Revision of the project to run (either a git branch, tag or commit SHA
       number)
    -test
       Test a script function with the name specified
    -user
       Private repository user name
    -with-conda
       Use the specified Conda environment package or file (must end with
       .yml|.yaml suffix)
    -with-dag
       Create pipeline DAG file
    -with-docker
       Enable process execution in a Docker container
    -N, -with-notification
       Send a notification email on workflow completion to the specified
       recipients
    -with-report
       Create processes execution html report
    -with-singularity
       Enable process execution in a Singularity container
    -with-timeline
       Create processes execution timeline file
    -with-trace
       Create processes execution tracing file
    -with-weblog
       Send workflow status messages via HTTP to target URL
    -without-docker
       Disable process execution with Docker
       Default: false
    -w, -work-dir
       Directory where intermediate result files are stored
```

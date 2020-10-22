# Single-cell Variant Calling via Integer Linear Programming (scVILP)
**single-cell Variant-calling by Integer Linear Programming (scVILP)** is a new approach to mutation calling in single cells with Perfect Phylogeny assumption using Integer Linear Programming formulations. scVILP jointly calls mutations for each cell and estimates the Perfect Phylogeny of those cells in the presence of allelic dropouts and missing data. 
It is possible for the user to investigate the violations of infinite-sites assumption on the inference by setting an upper bound on the number of violations 
## Contents
* [Getting started](#getting-started)
  - [Prerequisites](#prerequisites)
* [Required inputs](#required-inputs)
* [Running scVILP](#running-scvilp)
  - [Identify the candidate loci](#identify-the-candidate-loci)
  - [Run the variant caller](#run-the-variant-caller)
* [Outputs](#outputs)
* [Contact](#contact)

## Getting started

### Obtaining scVILP (and PerfectPhy)

The easiest way to obtain scVILP including a copy of PerfectPhy is to use:

```
git clone https://github.com/mae6/scVILP.git
```

**PerfectPhy** is used to reconstruct the Perfect Phylogeny. The original software can be found [here](https://csiflabs.cs.ucdavis.edu/~gusfield/software.html), but we also provide a version in the scripts directory of this repository.

### Installing dependencies

scVILP depends on a number of python modules and uses the Gurobi optimizer.
The easiest way to install all those dependencies is via (bio)conda.
For quick install instructions, see: https://bioconda.github.io/user/install.html

Once you have set this up, you can use the file `scvilp_conda.yaml` to install those dependencies:

```
cd scVILP
conda env create -f scvilp_conda.yaml
```

This creates an environment called `scvilp` that you can activate with:

```
conda activate scvilp
```

Before using scvilp as specified below, you will further have to obtain a license to use it and install that license on the machine on which you want to run scvilp (with the `scvilp` environment activated and using the command provided with the license).
For academic purposes, you can for example obtain a free license:
https://www.gurobi.com/downloads/end-user-license-agreement-academic/

**[PAUP](http://phylosolutions.com/paup-test/)** - to visualize the phylogenetic tree using the Newick output file, you can further download and install PAUP.


## Required inputs
* The input data of scVILP is the output of sequence alignment in [mpileup](http://www.htslib.org/doc/samtools-mpileup.html) format
* At least the number of cells is required, or a file containing the cell names which is optional, in case the cell names are not avaialble, they are named as *cell k* where *k* is the index of the cell
## Running scVILP
### Identify the candidate loci
First, run one of the following commmands to identify the candidate mutation loci
1- With the number of cells:
```
python loci_identify.py -in ovarian.mpileup -out ./output.mpileup -n 370 -ms 2 -nmc 3 
```
2- Or, using a text file containing the cell names to run this code:
```
python loci_identify.py -in ovarian.mpileup -out ./output,mpileup -names cellNames.txt -ms 2 -nmc 3
```
At this step, the user needs to select the loci on which they are performing the analysis. The parameters are as follows:
* *in*: path to the input file
* *out*: path to the output file
* *ms*: at each cell and genomic loci, this parameter requires a minimum of *ms* variant counts 
* *nmc*: at each genomic loci, this parameter requires at least *n* cells to have the minimum number of variants (*m*)

### Run the variant caller 
To run the optimizer, enter the following command:
```
python scVILP_main.py -in <path to the mpileup file> -names <path to the cell names> -out <path to the output directory>
```
To see the other options:
```
python scVILP_main.py --help
```
## Outputs
Running the main code, generates two files in the output directory specified by the user:
* A VCF file named snv.vcf describing the inferred genotypes for all the cells
* A Nexus file named *phylogeny.nex* containing the Newick string of the Perfect Phylogeny with leaves labeled by cell names
  - **Note**: Our method generates the phylogenetic tree in Newick format only when there is no violations of infinite-sites assumption. Before running scVILP, please specify the path to the directory of PerfectPhy in scVILP_main.py, the default path to PerfectPhy directory is the same where the scripts are.
## Contact
Please feel free to contact edrisi@rice.edu if you have any questions


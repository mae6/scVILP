# Single-cell Variant Calling via Integer Linear Programming (scVILP)
**single-cell Variant-calling by Integer Linear Programming (scVILP)** is a new approach to mutation calling in single cells with Perfect Phylogeny assumption using Integer Linear Programming formulations. scVILP jointly calls mutations for each cell and estimates the Perfect Phylogeny of those cells in the presence of allelic dropouts and missing data. 
scVILP is scalable to high number of cells and mutations by introducing a novel super-tree algorithm which could be run parallelly on multiple processors. 
## Getting started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.
## Running scVILP
### Inputs
* The input data of scVILP is the output of sequence alignment in [mpileup](http://www.htslib.org/doc/samtools-mpileup.html) format
* At least the number of cells is required, or a file containing the cell names which is optional, in case the cell names are not avaialble, they are named as *cell k* where *k* is the index of the cell
### Running the pipeline step by step
#### Filtering the candidate loci
```
python loci_filter.py -in ovarian.mpileup -out ./output.mpileup -n 370 -ms 2 -nmc 3 
```
Or 
```
python loci_filter.py -in ovarian.mpileup -out ./output,mpileup -names cellNames.txt -ms 2 -nmc 3
```
At this step, the user needs to select the loci on which they are performing the analysis. The parameters are as follows:
* *in*: path to the input file
* *out*: path to the output file
* *ms*: at each cell and genomic loci, this parameter requires a minimum of *ms* variant counts 
* *nmc*: at each genomic loci, this parameter requires at least *n* cells to have the minimum number of variants (*m*)


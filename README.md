# Single-cell Variant Calling via Integer Linear Programming (scVILP)
**single-cell Variant-calling by Integer Linear Programming (scVILP)** is a new approach to mutation calling in single cells with Perfect Phylogeny assumption using Integer Linear Programming formulations. scVILP jointly calls mutations for each cell and estimates the Perfect Phylogeny of those cells in the presence of allelic dropouts and missing data. 
scVILP is scalable to high number of cells and mutations by introducing a novel super-tree algorithm which could be run parallelly on multiple processors. 
## Getting started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.
## Running scVILP
### Inputs
* The input data of scVILP is the output of sequence alignment in [mpileup](http://www.htslib.org/doc/samtools-mpileup.html) format
* The list of the cell names is optional, in case the cell names are not avaialble, they are named as cellK where K is the index of the cell

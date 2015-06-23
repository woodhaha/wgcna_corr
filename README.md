# wgcna_corr
Using Weighted Gene Coexpression Network Analysis (WGNCA) to analyze microarray data for correlations between gene modules (groups of genes with similar expression profiles) and phenotypes.

# Soft Thresholding Parameter
```bash
Rscript thresholding_parameters.R --cel_path=/path/to/cel/files --out=/directory/to/save/plots/and/RData
```
This script should be used to set the hyperparameters to build the gene co-expression network. Essentially, a several soft thresholding parameters $k$ are tested to determine which parameters cause the resulting network to best approximate a scale-free network. It has been shown that biological networks (and many other networks such as social networks) exhibit a scale-free (also known as power law) topology.

_Important output to keep:_ Thresholding parameter $k$ and ExpressionSet object saved as an RData file. These will be used in downstream analyses.

# Defining Gene Modules

```bash
Rscript generate_modules.R --eset=/path/to/expressionset/Rdata/file --soft_thresh_k=integer --out_dir=/directory/to/save/plots/and/module/assignment
```

This script will generate gene -> gene module assignment by building a network, clustering into a dendrogram, and using DynamicTreeCut to slice the dendrogram branches into module assignments. A tab-delimited text file will be produced that maps genes to fine-grained modules and to larger modules (by combining modules with eigengene correlation >80%).

_Important output to keep:_ Gene module assignments and ExpressionSet object (from thresholding_parameters.R). These will be used to determine module eigengenes to correlate with phenotypes.

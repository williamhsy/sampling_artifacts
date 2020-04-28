# Sampling time-dependent artifacts in single-cell genomics studies

This repository contains all the scripts, notebooks and reports to reproduce the scRNA-seq analysis of our paper ["Sampling time-dependent artifacts in single-cell genomics studies"](https://www.biorxiv.org/content/10.1101/2020.01.15.897066v1), published in Genome Biology in 2020. Here, we describe how to access the data, the most important packages and versions used, and how to navigate the directories and files in this repository.

## Data

All the raw data (fastqs) and expression matrices are available at the Gene Expression Omnibus (GEO) under [GSE132065](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE132065). The data in this project can be broadly divided into 5 subprojects:

- [Smart-seq2](https://www.nature.com/articles/nprot.2014.006): includes a total of 4 96-well plates, with ids P2568, P2664, P2671 and P2672.
- [10X scRNA-seq](https://www.10xgenomics.com/products/single-cell/) data for Peripheral Blood Mononuclear Cells (PBMC): divided into two batches, which we named "JULIA_03" (cDNA libraries: AH9225 and AH9226, hashtag oligonucleotide (HTO) libraries: AH9223 and AH9224) and "JULIA_04" (cDNA libraries: AI0101 and AI0102, HTO libraries: AI0099 and AI0100).
- 10X scRNA-seq data for Chronic Lymphocytic Leukemia (CLL) cells: a total of 5 libraries, which are named after a combination of the donor id ("1220", "1472", "1892") and the temperature ("4ºC" or room temperature (RT)): 1220_RT, 1472_RT, 1892_RT, 1472_4C and 1892_RT.
- 10X scRNA-seq data for T-cell activation experiment (see methods): "Tcell_activation_day0_rep1", "Tcell_activation_day2_rep1", "Tcell_activation_day0_rep2" and "Tcell_activation_day1_rep2".
- [10X scATAC-seq](https://www.10xgenomics.com/products/single-cell-atac/) data for PBMC.
- 10X scATAC-seq data for CLL.


### Fastqs

As described in the paper, we multiplexed several sampling times into the same 10X Chip Channel using the [cell hashing](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-018-1603-1) technology. To map the fastqs to the reference genome to obtain the single-cell gene expression matrices, we followed the ["Feature Barcoding Analysis"](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/feature-bc-analysis) pipeline from [cellranger](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/what-is-cell-ranger). This is an example of a cellranger run we used to map one of the libraries:

```{bash}
cellranger count --libraries libraries.csv --feature-ref feature_reference.csv --id 1472_RT --chemistry SC3Pv3 --expect-cells 5000 --localcores 12 --localmem 64 --transcriptome eference/human/refdata-cellranger-GRCh38-3.0.0/;
```

As you can see, a key input in this command is the feature_reference.csv which, according to 10X, "declares the set of Feature Barcoding reagents in use in the experiment. For each unique Feature Barcode used, this file declares a feature name and identifier, the unique Feature Barcode sequence associated with this reagent, and a pattern indicating how to extract the Feature Barcode sequence from the read sequence". This files can be easily created from the file "GSE132065_conditions_10X.tsv", available in both this GitHub repository and in GEO.


### Expression matrices
A total of 3 files per library are needed to reconstruct the full expression matrix:

1. barcodes*.tsv.gz: corresponds to the cell barcodes (column names).
2. features*.tsv.gz: corresponds to the gene/condition identifiers (row names). Moreover, it contains a columns that ideantifes genes ("Gene Expression") and experimental conditions ("Antibody Capture").
3. matrix*mtx.gz: expression matrix in sparse format.


To makes things easier, you can also access the matrices and several intermediate Seurat objects (saved as .rds) [here](https://drive.google.com/drive/folders/1ZST33kPXpc0f1Qs3NJ1fJ-A4IU313PFs?usp=sharing).


## Package versions

These are the versions of the most important packages used throughout all the analysis:

CRAN:

* [tidyverse 1.3.0](https://cran.r-project.org/web/packages/tidyverse/vignettes/paper.html)
* [Seurat 3.1.4](https://www.cell.com/cell/fulltext/S0092-8674(19)30559-8?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS0092867419305598%3Fshowall%3Dtrue)

Bioconductor:

* [Scater 1.10.1](https://academic.oup.com/bioinformatics/article/33/8/1179/2907823)
* [Scran 1.10.2](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-0947-7)
* [GOstats 2.48.0](https://academic.oup.com/bioinformatics/article/23/2/257/204776)

**Note**: Two months before compiling the notebooks to release them together with the paper, we updated most Bioconductor packages. Thus, some versions reported in the sessionInfo() of the notebooks might be slightly different to the ones used to produce the figures of the article.


## File system and name scheme


* 1-PBMC:
* 2-CLL:
* 3-T_cell_activation:
* 4-Revision:

reports VS notebooks VS bin VS data




https://drive.google.com/drive/folders/1ZST33kPXpc0f1Qs3NJ1fJ-A4IU313PFs?usp=sharing
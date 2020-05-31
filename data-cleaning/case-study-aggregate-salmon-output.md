# 🎉 Case Study: Aggregate Salmon Quant

In the [last case study](../python-and-unix-system/case-study-mapping-bulk-rna-seq-reads-with-salmon.md), we went through the whole process of mapping 16 bulk RNA-seq samples with salmon, and we got 16 transcript-level quantification tables for each sample. In this page, we want to aggregate the transcript-level counts into gene-level counts \([the reason is described in this paper](https://f1000research.com/articles/4-1521/v1)\) for further Differentially Expressed Gene \(DEG\) analysis. In order to do so, we will use a R package called "tximport".

For coding, you will learn two things in this case study:

1. More examples of manipulating table using pandas;
2. How to integrate R seamlessly include some open-box R packages into python. 

## Step 1. Prepare transcript2gene map

[See Jupyter Notebook](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/DevFBProject/AggSalmon/Step%201%20-%20Prepare%20transcript2gene%20map.ipynb)

In this notebook, we will use the GENCODE GTF file to extract informations related to next step. The same GTF file is used in salmon index when I prepare the data. **It is IMPORTANT to keep using the same reference \(e.g., genome FASTA, gene annotation GTF\) throughout your single project.**

We will extract gene\_id for each transcript\_id from the GTF, then save them into another table.

### Step 2. Transcript Quant To Gene Quant

[See Jupyter Notebook](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/DevFBProject/AggSalmon/Step%202%20-%20Transcript%20Quant%20Into%20Gene%20Quant.ipynb)

In this notebook, we will use the R package "tximport" to aggregate transcript quant into gene quant for each sample. This step also provides an example how we can combine R and python in the same notebook, taking advantages from both world!

I also created one large table in the end for the whole dataset, which contains all samples' gene-level information. This is the start point of all our future analysis, just a 6Mb CSV table.


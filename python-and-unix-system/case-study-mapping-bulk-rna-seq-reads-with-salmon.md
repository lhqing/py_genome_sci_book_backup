# 🎉 Case Study: Mapping bulk RNA-seq reads with salmon

In this book, we will use a bulk RNA-seq data from mouse developing forebrain as an example. In the github repo, I already provided [quantified salmon tables](https://github.com/lhqing/py_genome_sci_book/tree/master/data/DevFB). In this page, we will use a small subset of the data to reproduce the these `salmon quant` tables using exact process.

## How to follow this case study?

1. [Download or update github repository](../work-environment/git-and-github.md#clone-github-repository-of-this-book), the files for this case study located in `py_genome_sci_book/analysis/salmon_demo`
2. The analysis contain four main steps, each associated with a jupyter notebook in that directory
3. On github, you can see the executed version of these notebooks, you should be able to execute each of them in your local environment, and check the content with online version.

{% hint style="info" %}
I prepared 25 small FASTQ files \(only contain 10,000 reads in each for demo purpose\) for this demo. The reduced file size allows you go through all of these steps in about 30 min.
{% endhint %}

## Main Steps and Notebooks

### Step 1. Create Salmon Index

[See notebook here](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/salmon_demo/step1.create_salmon_index.ipynb).

In this step, we will create salmon index for the mouse GENCODE transcriptome annotation. 

### Step 2. Prepare Input FASTQ files

[See notebook here.](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/salmon_demo/step2.PrepareMetadata.ipynb)

In this step, we will go through these 25 FASTQ files, rename them via soft-link with meaningful names, and create a metadata table for them.

### Step 3. Trim FASTQ

[See notebook here.](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/salmon_demo/step3.fastqTrimAndQC.ipynb)

In this step, we will trim the FASTQ using trim\_galore. These step generate a new set of 25 trimmed FASTQ files so we will also update the metadata table.

### Step 4. Salmon mapping

[See notebook here.](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/salmon_demo/step4.mapping.ipynb)

In this step, we will use salmon quant to quantify the 25 trimmed FASTQ files into 16 salmon quant tables. These tables has same layout as the one provided in our[ real dataset](https://github.com/lhqing/py_genome_sci_book/tree/master/data/DevFB), but the numbers are mostly zero, because here we used a much smaller FASTQ files as input. For any further analysis, please refer to the [real dataset](https://github.com/lhqing/py_genome_sci_book/tree/master/data/DevFB).

### My suggestions:

1. When doing analysis, keep your file organized into sub-directory;
2. Always associate your data files with a metadata table locating besides them, include all necessary informations in that metadata table;
3. Document all steps into Jupyter Notebook, or at least some files with your commands for each step. Doing analysis is just like doing wet lab experiment 🧪, we need to write down what we did📘📝


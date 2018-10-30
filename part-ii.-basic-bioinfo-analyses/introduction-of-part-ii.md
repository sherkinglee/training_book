# Introduction of PART II

{% hint style="info" %}
**写在前面的话**

我们将通过实际的例子，也就是Case Study，来进行生物信息分析的教学和训练。这样的学习更加有目的性，也更加有趣，但是不足的地方是教学的内容会不够完备。
{% endhint %}

## Work with a computing server remotely <a id="1"></a>

1. [ssh](../part-i-basic-skills/2.linux.md#4-setup-ssh-key) and ssh keys
2. nohub, screen or tmux

> **More Reading**
>
> &lt;&lt;Bioinformatics Data Skills&gt;&gt;
>
> 4\) Working with Remote Machines

## Let's start a real case

{% hint style="info" %}
**Identify novel exRNA biomarkers for cancer diagnosis**
{% endhint %}

### Outline:

1. Basics
   1. **Pre-processing**, **Mapping, Annotation** and **QC**. 
   2. **Expression Matrix**
   3. **Differential Expression Analysis and Clustering**
2. Advanced
   1. **Normalization**
   2. **Imputation**
   3. **Control Data**
   4. **Extension**

### a\) Background Introduction

* [PPT](../getting-startted.md#learning-materials):  0. Introduction of exRNA-seq.pdf \(view on-line only, not downloadable\)
* [Teaching Video](../getting-startted.md#learning-materials): Week V - Part II. 0. Intr to exRNA-seq.mov

### b\) Understand your data

**Type of RNA-seq**

* **Default:** \(whole cell poly-A\) RNA-seq  \(&gt;200nt\)
* **Other types:**
  * small RNA-seq  \(&lt;50nt\)
  * total RNA-seq \(ribosome removed\) \(&gt;200nt\)
  * nonpolyA RNA-seq \(ribosome removed\) \(&gt;200nt\)
* [**Different cell localizations**](5.control-data.md#local)**:**
  * nuc. \(total\) 
  * chromosome \(total\) 
  * cyto. \(poly-A\) 
* **Single cell RNA-seq**
* **exRNA-seq**
  * cell free/MV/exosome/RNP
  * small/long

**So what RNA-seq we are mapping and analyzing?**

* Sequencing machine ?
* Single-strand V.S. Paired-end ?
* Strand specific ?
* Size selection ?
* Poly-A enriched or total \(ribosome removed\) ?
* Cellular localization ?

### c\) Organize your data

[**Data format**](https://genome.ucsc.edu/FAQ/FAQformat.html)**:**

* fasta
* fastaq
* gff/gtf
* bam
* bed
* bigwig

**Shared dirs/data:**

```text
cd  #go to my home
ln -s /BioII/lulab_b/shared/genomes  .   #shared reference genome sequeunces and annotations
ln -s /BioII/lulab_b/shared/shared_scripts  .  #shared scripts in Lu Lab
ln -s /BioII/lulab_b/shared/projects/exRNA  shared_exRNA_projects   #shared projects' files
```

* ~/genomes/human\_hg38
  * sequences/ \#sequences of reference genome \(fasta format\)
  * index/ \# indexed genome sequences
  * gtf/   \#annotation of reference genome 

**Make your own project dir:**

```bash
cd # go to my home
vim .bashrc # see my example in /home/john/.bashrc (and /home/john/shortcuts)
mkdir github

mkdir -p ~/projects/exRNA
cd ~/projects/exRNA

alias mkpr="mkdir -p {data/mapped,scripts,analysis}"  # you can put this in your ~/.bashrc
mkpr
```

### d\) Get the software ready

[Install bioinformatics software in Linux \(centos\)](https://github.com/lulab/training/wiki/cnode)

## Video

### a\) Introduction exRNA-seq

[@Youtube](https://youtu.be/ovSVpqcDB8o)

[@Bilibili](https://player.bilibili.com/player.html?aid=30591172&cid=53394108&page=1)

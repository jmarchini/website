## Software

This page contains links to software packages that were developed by our group.

If you have questions use the [[OXSTATGEN MAIL LIST]](https://www.jiscmail.ac.uk/cgi-bin/webadmin?A0=OXSTATGEN), and post a question there.

**Some of these programs are licenced for academic use only. Please read the [[LICENCE]](licence.md)**


### Tensor and Matrix Decomposition
#### SDA4D
A program for sparse Bayesian 4D tensor decomposition

Christopher Gill and Jonathan Marchini (2020) Four-Dimensional Sparse Bayesian Tensor Decomposition for Gene Expression Data [[bioRxiv]](https://www.biorxiv.org/content/10.1101/2020.11.30.403907v1)

[[Source code and documentation]](https://github.com/marchinilab/SDA4D)

#### SDA
A program for sparse Bayesian matrix and tensor decomposition.

Victoria Hore, Ana Viñuela, Alfonso Buil, Julian Knight, Mark I McCarthy, Kerrin Small, Jonathan Marchini. Tensor decomposition for multi-tissue gene expression experiments. Nature Genetics 10.1038/ng.3624 [[Journal]](http://www.nature.com/ng/journal/vaop/ncurrent/full/ng.3624.html)

[[Executables and documentation]](https://www.dropbox.com/sh/chek4jkr28qnbrj/AABbHEVX_Ct70Dl54rKNKr6ra?dl=0) [[Licence]](licence.md)
#### FastICA
R package that implements the FastICA algorithm. This is now hosted on CRAN and maintained by others.

[[R package]](https://cran.r-project.org/web/packages/fastICA/index.html)

### GxE Interactions

#### LEMMA
LEMMA (Linear Environment Mixed Model Analysis) is a whole genome wide regression method for flexible modeling of gene-environment interactions in large datasets such as the UK Biobank.

The method estimates a linear combination of environmental variables,
called an environmental score (ES), that interacts with genetic
markers throughout the genome, and provides a readily interpretable
way to examine the combined effect of many environmental
variables. The ES can be used both to estimate the proportion of
phenotypic variance attributable to GxE effects, and also to test for
GxE effects at genetic variants across the genome.

Matthew Kerin and Jonathan Marchini (2020) Inferring
Gene-by-Environment Interactions with a Bayesian Whole-Genome
Regression Model. American Journal of Human Genetics
[[Journal]](https://www.cell.com/ajhg/fulltext/S0002-9297(20)30277-9)

[[Documentation and Source Code]](https://mkerin.github.io/LEMMA/) (freely available under an MIT licence)

#### GPLEMMA

GPLEMMA (Gaussian Prior Linear Environment Mixed Model Analysis) is a non-linear randomized Haseman-Elston regression method for flexible modeling of gene-environment interactions in large datasets such as the UK Biobank.

The method simultaneously estimates a linear combination of environmental variables, called an environmental score (ES), that interacts with genetic markers throughout the genome, and it’s associated heritability. Estimation of the ES provides a readily interpretable way to examine the combined effect of many environmental variables.

Matthew Kerin and Jonathan Marchini (2020) Non-linear randomized
Haseman-Elston regression for estimation of gene-environment
heritability. Bioinformatics
[[Journal]](https://academic.oup.com/bioinformatics/advance-article/doi/10.1093/bioinformatics/btaa1079/6050717)

The GPLEMMA method is implemented as an option in the LEMMA code

[[Documentation and Source Code]](https://mkerin.github.io/LEMMA/) (freely available under an MIT licence)

### Imputation

#### IMPUTE 5

IMPUTE 5 is a genotype imputation method that can scale to reference panels with millions of samples. This method continues to refine the observation made in the IMPUTE2  method, that accuracy is optimized via use of a custom subset of haplotypes when imputing each individual. It achieves fast, accurate, and memory-efficient imputation by selecting haplotypes using the Positional Burrows Wheeler Transform (PBWT). By using the PBWT data structure at genotyped markers, IMPUTE 5 identifies locally best matching haplotypes and long identical by state segments. The method then uses the selected haplotypes as conditioning states within the IMPUTE model.

IMPUTE5 is up to 30x faster than MINIMAC4 and up to 3x faster than
BEAGLE5.1

S. Rubinacci, O. Delaneau, J. Marchini (2019) Genotype imputation using the Positional Burrows Wheeler Transform PLoS Genetics [[Journal]](https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1009049) 

IMPUTE 5 is **freely available for academic use only**. To see rules for non-academic use see the [[Licence]](licence.md) (also included with each software download).

[[Binary executables and documentation]](https://www.dropbox.com/sh/mwnceyhir8yze2j/AADbzP6QuAFPrj0Z9_I1RSmla?dl=0)

#### IMPUTE 4

A program for efficient genotype imputation. IMPUTE 4 implements the haploid imputation options included in IMPUTE 2, but is much faster and more memory efficient. It was written to impute genotypes for the UK Biobank dataset that consists of genetic data on ~500,000 individuals

IMPUTE 4 is **freely available for academic use only**. To see rules for non-academic use see the [[Licence]](licence.md) (also included with each software download).

[[Binary executables and documentation]](https://www.dropbox.com/sh/k6b34fzw9w4s8bg/AAA65aF5l2oj_AT9iDLgKCv9a?dl=0)

#### IMPUTE 2
a program for genotype imputation and phasing in genome-wide
association studies and fine-mapping  studies based on a dense set of
marker data (such as 1000 Genomes Project haplotypes)

IMPUTE 2 is **freely available for academic use only**. To see rules for non-academic use see the [[Licence]](licence.md) (also included with each software download).

[[Software and Documentation]](https://mathgen.stats.ox.ac.uk/impute/impute_v2.html)

#### MVNCALL
a program for genotype calling and phasing using next-generation sequencing reads and a haplotype scaffold.

[[Software and Documentation]](http://mathgen.stats.ox.ac.uk/genetics_software/mvncall/mvncall.html)

MVNCALL is **freely available for academic use only**. To see rules for non-academic use see the [[Licence]](licence.md) (also included with each software download).

### Haplotype estimation

#### SHAPEIT 4
a program for accurate and efficient phasing of very large genetic datasets

[[Software and Documentation]](https://odelaneau.github.io/shapeit4/) [[Paper]]([[Journal]](https://www.nature.com/articles/s41467-019-13225-y))

#### SHAPEIT 3
a program for accurate and efficient phasing of very large genetic datasets. It was used to phase the 500,000 individuals as part of the UK Biobank dataset.

SHAPEIT3 introduces several important extensions to the vanilla SHAPEIT algorithm to enable this scalability:

 - a fast clustering routine to identify conditioning haplotypes in sub-quadratic time
 - early stopping of the HMM when perfect haplotype matches are found
 - a redesigned MCMC routine for better performance

[[Software and Documentation]](shapeit3.md) [[Paper]]([[Journal]](http://www.nature.com/articles/ng.3583))

#### SHAPEIT 2
a program for accurate and efficient phasing of genetic datasets

[[Software and Documentation]](https://mathgen.stats.ox.ac.uk/genetics_software/shapeit/shapeit.html) [[Paper]](http://www.nature.com/nmeth/journal/v10/n1/full/nmeth.2307.html)

SHAPEIT2 is **freely available for academic use only**. See the [[SHAPEIT2 website]](https://mathgen.stats.ox.ac.uk/genetics_software/shapeit/shapeit.html) for more details.


#### PHASING SERVER
A service for accurately phasing sequenced samples using large haplotype reference panels, such as the Haplotype Reference Consortium dataset.

[[Website]](https://phasingserver.stats.ox.ac.uk/) [[Paper]](http://bioinformatics.oxfordjournals.org/content/early/2016/02/27/bioinformatics.btw065.abstract?keytype=ref&ijkey=NicAjSqI9E6y0xG)

#### DUOHMM
a program that works together with SHAPEIT to produce accurate inference of haplotypes in pedigrees, estimate recombination events and detect genotyping errors.

[[Source code]](https://github.com/jaredo/duohmm) [[Documentation]](https://mathgen.stats.ox.ac.uk/genetics_software/duohmm/duohmm.html)

### Association testing

#### BGENIE
a program for multiple trait GWAS focussed on the BGEN format files used to store the UK Biobank genetic data on ~500,000 individuals.
[[Software]](https://www.dropbox.com/home/Oxford/software/software_webpages/bgenie) [[Documentation]](bgenie.md)
[[Paper]](https://www.nature.com/articles/s41586-018-0571-7)

BGENIE is **freely available for academic use only**. 

#### SNPTEST
a program for Frequentist and Bayesian tests of SNP association with binary (case-control) and quantitative phenotypes that takes genotype uncertainty into account.

[[Software and Documentation]](https://www.well.ox.ac.uk/~gav/snptest/)

SNPTEST is **freely available for academic use only**. To see rules for non-academic use see the [[Licence]](licence.md) (also included with each software download).

#### SBAT
A program for Sparse Bayesian Association Testing that can fit multi-trait linear mixed models.

[[Software]](https://www.dropbox.com/home/Oxford/software/software_webpages/sbat)

SBAT is **freely available for academic use only*

#### META
A program to carryout meta-analysis of genetic studies.

[[Software and Documentation]](https://mathgen.stats.ox.ac.uk/genetics_software/meta/meta.html)

#### GENECLUSTER
A program for location and detection of unobserved causal loci in fine-mapping experiments and genome-wide association studies.

[[Software and Documentation]](https://mathgen.stats.ox.ac.uk/genetics_software/genecluster/gc.html)

####  PHENIX
PHENIX (PHENotype Imputation eXpediated) is a method for imputing missing phenotypes where samples have an arbitrary level of relatedness. The method can also be used for dimensionality reduction of multiple traits in related samples. The resulting latent traits can be tested as phenotypes, and can result in an increase in power.

[[Software and Documentation]](https://www.dropbox.com/home/Oxford/software/software_webpages/phenix)

####  HAPGEN
A program to simulate case control datasets at linked SNP markers conditional upon a set of known haplotypes.

[[Software and Documentation]](http://mathgen.stats.ox.ac.uk/genetics_software/hapgen/hapgen2.html)

####  GWAPOWER
An R package for assessing the power of genome-wide association studies using commercially available genotyping chips. The package encapsulates extensive simulation results generated by our program HAPGEN and described fully in the paper

[[Software and Documentation]](https://www.dropbox.com/s/nl76sh64jv0qa8h/GWApower_1.1.tar.gz?dl=0)

####  Oxford Brain Imaging Genetics (BIG) server
A [PheWeb browser](https://github.com/statgen/pheweb/) for 3,144 GWAS of brain imaging derived phenotypes in the UK Biobank, based on Elliott, L. et al (2018)

[[Browser]](http://big.stats.ox.ac.uk/)
### Population structure

####  MULTIMIX
A program for admixture deconvolution using multiple (i.e. > 2) phased or unphased ancestral panels.

[[Software and Documentation]](https://jmarchini.org/multimix/)

MULTIMIX is **freely available for academic use only**. To see rules for non-academic use see the [[Licence]](licence.md) (also included with each software download).

###  GWAS Quality Control 

#### QCTOOL
A program for carrying out SNP and sample quality control (QC) for genome-wide association studies

[[Software and Documentation]](https://www.well.ox.ac.uk/~gav/qctool/#overview)

#### GTOOL
A program for (a) generating subsets of genotype data, and (b) converting genotype data between the PED file format and the FILE FORMAT used by SNPTEST and IMPUTE.

[[Software and Documentation]](https://www.well.ox.ac.uk/~cfreeman/software/gwas/gtool.html)

### Genotype calling

#### CHIAMANTE
A joint genotype calling algorithm for array and sequence data. This method can be used to call genotype from just array data.

[[Software and Documentation]]()

#### CHIAMO
A genotype calling algorithm for multi-cohort studies.

[[Software and Documentation]](https://mathgen.stats.ox.ac.uk/genetics_software/chiamo/chiamo.html)

### Brain Imaging

#### AnalyzeFMRI

An R package for visualisation and analysis of FMRI data

[[Software and Documentation]](https://cran.r-project.org/web/packages/AnalyzeFMRI/)






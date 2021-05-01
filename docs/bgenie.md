## Overview


A program for efficient GWAS for multiple continuous traits and PHEWAS with many features designed and optimized for large scale analysis:

 - BGENIE is built upon the [BGEN](https://enkre.net/cgi-bin/code/bgen/dir?ci=trunk) library. It takes BGEN files as input and avoids repeated decompression and conversion of these files when analyzing multiple continuous phenotypes.
 - It was written for the analysis of the UK Biobank dataset (which is stored in the  [BGEN v1.2 file format](https://www.well.ox.ac.uk/~gav/bgen_format/)). This dataset consists of genetic data on ~500,000 individuals, ~93 Million autosomal variants and thousands of phenotypes.
 - It works with indexed BGEN files yielding fast access for any (group of) SNPs. This feature facilitates very fast PHEWAS.
- BGENIE uses the Eigen matrix library and OpenMP to carry out as many of the linear algebra operations in parallel as possible. For example, estimation of effect sizes of large numbers of SNPs can be carried out in parallel using matrix operations, and indexing of missing data values is used to allow for fast estimation of standard errors.
 - It has built in functionality to apply PCA or ICA (using the fastICA algorithm) to multiple phenotypes and use the resulting transformed phenotypes for testing via GWAS.


## Basic Usage:
BGENIE performs a linear association test between SNP/phenotype pairs in the provided data. A basic command to run GWAS on all the phenotypes is:
```
bgenie --bgen example.bgen --pheno example.pheno --out example.out
```
If you wish to specify a range of SNPs specified by position (useful if you wish to split the genome up into multiple jobs) you can use the –range option, for example:
```
bgenie --bgen example.bgen --pheno example.pheno --out example.out --range 22 20000000 21000000
```

If you wish to analyse just a single SNP you can select it using the –rsid option, for example:
```
bgenie --bgen example.bgen --pheno example.pheno --out example.out --rsid rs573069994
```
## Full options list

### Input options

**--bgen <file.bgen\>** (Required) The BGEN file containing the genetic data for the subjects in the analysis must be specified by the file <file.bgen>. It helps to have the BGEN file indexed (i.e produce a BGI file), which allows efficient PHEWAS and ranged based operations. See tools QCTOOL and BGENIX for more information about these sorts of files.

**--pheno <file.pheno\>** (Required) The phenotypes for the subjects in the study must be specified by the file <file.pheno> . This must be a space separated file, wherein the first line is a header line specifying the names of each phenotype as a space separated list, and the remaining lines specifying the values of the phenotypes for each subject. The subjects must be presented in the same order that they are found in the BGEN file. If a SAMPLE file has been provided to accompany the BGEN files, then this order can be found by examining the SAMPLE file. Alternatively, if the subject IDs are present in the BGEN file, then they can be found using the qctool software, with the command qctool -g example.bgen -os example.sample (in some datasets, such as UK BIOBANK, the subject IDs are stripped from the BGEN files, in which case an accompanying SAMPLE file must be relied upon). Missing values must be encoded by the code -999, or the code specified by the argument to the --miss parameter. An example phenotype file is provided in the following listing:

Height(in)  Weight(lbs)  
58 115  
59 117  
60 120   
61 123  
62 -999  


In this example phenotype file, the height and weight are given for 5 subjects, and the 5-th subject has a missing weight measurement.

**--covar <file.cov\>** Specifies that covariates to be removed from the analysis are read from the file file.cov. The format of this file is the same as that for the phenotype file: it is space separated and the first line is a header specifying the names of the covariates. The remaining lines specify the values of the covariates for the subjects (the subjects must be ordered in the same order as they are given in the phenotype file). As for the phenotype file, the code -999 must be used to specify missing covariates (this code can be modified by using the --miss parameter).

Covariates are removed by replacing each phenotype by the residuals found after a multilinear regression between the phenotype and all of the covariates (with the intercept fit). Each subject with at least one missing covariate will be dropped from the analysis.

**--miss <int\>** This option can be used to change the code for missing values in the phenotype file file.pheno and covariate file file.cov to the integer value of int. The default value of is \-999.

### Output file options

**--out <file.out\>** (Required argument.) This parameter specifies the output file. The results of the analysis will be saved in the file file.out.gz, with gzip compression. This is a compressed space separated file. The first line of the output file is a header giving the column names for each column in the file. The first 7 columns provide information about the SNP. These columns are as follows:

The chromosome on which the SNP resides.  
The name of the SNP (rsid).  
The position of the SNP.  
The character code for the first allele (a string).  
The character code for the second allele (a string).  
The allele frequency of the second allele (if the second allele is the minor allele, this is the MAF).  
The information score of the SNP (the quality of imputation).  

For the remaining columns, the results of the linear association test are provided in groups of three columns per phenotype. In these remaining columns, the beta coefficient, standard error and t-statistic for the linear association are provided.

In the regression model we code the first and second alleles as 0 and 1 respectively, so the beta coefficient refers to the effect of having an extra copy of the second allele.

An example of the first 10 columns of an uncompressed ouput file are provided in the following listing:

chr rsid pos a_0 a_1 af info pheno1_beta pheno1_se pheno1_t ...  
22 22:16050075:A:G 16050075 A G 0.0001 1 0.00067749 0.01008 0.067215 ...  
22 22:16050115:G:A 16050115 G A 0.00545 1 -0.00022679 0.010577 -0.021441 ...  
22 22:16050213:C:T 16050213 C T 0.00635 1 -0.0053945 0.010732 -0.50266 ...  
22 22:16050319:C:T 16050319 C T 0.00115 1 -0.0072811 0.010548 -0.69025 ...  
22 22:16050527:C:A 16050527 C A 0.00045 1 -0.010907 0.011428 -0.95444 ...  
22 22:16050568:C:A 16050568 C A 0.00025 1 -0.0024885 0.011269 -0.22083 ...  
22 22:16050607:G:A 16050607 G A 0.0006 1 0.013246 0.010527 1.2583 ...  
22 22:16050627:G:T 16050627 G T 0.0004 1 -0.00043928 0.01008 -0.04358 ...  
...  

Here, ellipses indicate that the file extends rightwards and downwards. This listing implies, for example, that the t-statistic for the association between the SNP with name 22:16050075:A:G and the first phenotype is 0.067215. The 8th to 13th column of this same example output file are as follows:

... pheno1_beta pheno1_se pheno1_t pheno2_beta pheno2_se pheno2_t ...  
... 0.00067749 0.01008 0.067215 0.02078 0.0098946 2.1001 ...  
... -0.00022679 0.010577 -0.021441 -0.009898 0.010385 -0.95313 ...  
... -0.0053945 0.010732 -0.50266 -0.026902 0.010628 -2.5312 ...  
... -0.0072811 0.010548 -0.69025 0.014004 0.010612 1.3196 ...  
... -0.010907 0.011428 -0.95444 -0.00078519 0.011221 -0.069973 ...  
... -0.0024885 0.011269 -0.22083 -0.014114 0.011064 -1.2757 ...  
... 0.013246 0.010527 1.2583 0.01656 0.010336 1.6022 ...  
... -0.00043928 0.01008 -0.04358 -0.032021 0.011422 -2.8034 ...  
...

This listing shows the results of the association test for the first and second phenotype. Note that subject IDs and family IDs must not be included in this file. Instead, they are inferred from the BGEN file.

**--pvals** By default, the p-values for the association tests are not provided in the output file, as they can be inferred by the beta coefficient and the t-statistic. If this output is desired, the --pvals  parameter may be provided, in which case the output file will include four consecutive columns for each phenotype. The first three are as described above (beta coefficient, standard error and t-statistic), and the fourth is the -log10 p-value of the association.

If this parameter is provided, then in the example listings shown for the –out parameter above, columns 8 to 11 of the output file will be as follows:

... pheno1_beta pheno1_se pheno1_t pheno1_p ...  
... 0.00067749 0.01008 0.067215 0.02392 ...  
... -0.00022679 0.010577 -0.021441 0.0074933 ...  
... -0.0053945 0.010732 -0.50266 0.21097 ...  
... -0.0072811 0.010548 -0.69025 0.30975 ...  
... -0.010907 0.011428 -0.95444 0.46866 ...  
... -0.0024885 0.011269 -0.22083 0.083424 ...  
... 0.013246 0.010527 1.2583 0.68125 ...  
... -0.00043928 0.01008 -0.04358 0.015365 ...  
...

The remaining columns are provided in groups of four for each phenotype.

**--dosage <file\>** If this flag is provided, the dosage for each SNP/sample pair is written to the provided file.

**--dump_phenotypes**  This option specifies that phenotypes are written to a file. The file name will have the same name as that specified by –out with the suffix .phenos This is useful for understanding the results of ICA and PCA flags, and also missingness filters.

### Filtering options

**--exc\_missing\_inds** If this parameter is provided, then all subjects with at least one missing phenotype value will be removed from the analysis.

**--include_pheno <pheno.cov\>** If this parameter is provided, then only phenotypes listed in the file pheno.cov will be analysed. This file must contain one phenotype name per line, and the phenotype names must match the names of the phenotypes provided in the header line of the phenotype file.

**--range <chr> <start\_pos\> <end\_pos\>** This option restricts analysis to SNPs falling in the range to (measured in basepairs) on the chromosome <chr>. The index BGI file for the argument <start_pos> to <end_pos> .The BGEN index file file.bgi must exist for this option to work. Also, the chromosome name must match exactly the chromosome name given in the BGEN file (i.e. if the BGEN file names chromosome 1 as 01, then must be 01to specify chromosome 1.)

**--rsid <rsid\>** If this parameter is provided, then a PHEWAS is performed on the SNP named . The format of the output file is the same as that specified for the parameter --out, except it will only have two lines: the first line will be headers and the second line will be the corresponding values for the PHEWAS against the specified SNP.

**--include\_rsids <file\>** This option allows you to specify a list of RS IDs and then analysis if only run at this markers. The file should contain one RS ID per line.

### Runtime options

**--thread <n\>** This option controls the number of threads used by BGENIE will be given to <n>. By default, the number of threads is found by examining the OpenMP environment defaults.

**--chunk <n\>** BGENIE processes the genetic data in chunks. To specify the size of the chunk (in SNPs), this parameter may be provided, and the size of the chunk will be set to <n>. The value of should be large enough to avoid thread overhead, but small enough to allow RAM usage to not be exceeded. The default value of 256 works for most conditions.

### Phenotype and genotype transformations

**--scale\_phenotypes** By default, beta and se for each marker tested are computed without normalizing phenotypes or genotypes. Phenotypes can be scaled by including this flag. This does not affect p-values or t-statistics.

**--scale\_genotypes** By default, beta and se for each marker tested are computed without normalizing phenotypes or genotypes. Genotypes can be scaled by including this flag. This does not affect p-values or t-statistics.

**--pca\_only <var\>** If this option is provided, then the phenotypes will be replaced by the score matrix found by conducting a PCA on the entire set of phenotypes. The score matrix will be restricted to the top principal components that explain the proportion <var> of the variance (i.e.<var>  must be a real number in the interval (0, 1], and the score matrix used in the analysis will explain 100*<var>% of the variance in the phenotypes).

**--pca\_plus <var\>** This parameter is similar to --pca_only, except in addition to the score matrix, analysis will also be performed on all of the untransformed phenotypes. The score matrix will be horizontally concatenated by the phenotype file, and the linear test will be performed between each column of the resulting matrix and all of the SNPs. The identity of the columns in the resulting output file will be clear by the header line.

**--pca\_scale\_phenotypes** By default, the PCA operations described above do not rescale the phenotypes before they are applied. This makes sense if all of the phenotypes in the phenotype file have identical units. If rescaling is required before application of PCA, then this option should be used.

**--ica\_only <k\>** If this parameter is provided, then the phenotypes will be replaced by an ICA transformation in which the projections of the phenotypes onto the top <k> independent components are considered for analysis. This is done using the fastICA algorithm. <k> must be a positive integer, less than or equal to the number of phenotypes presented.

**--ica\_plus <k\>** This parameter is similar to --ica_only, but like --pca_plus it horizontally concatenates the untransformed phenotypes with the ICA transformation specified above.

### Miscellaneous

**--version** Print information about the version of BGENIE used.

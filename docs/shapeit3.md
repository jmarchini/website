## Basic Usage

SHAPEIT3 commands are very similar to SHAPEIT2, with a few additional arguments to enable its fast scaling. Simply enabling the --fast flag should be sufficient for most users:
```
shapeit3 -B example/gwas -M genetic_map.txt -O out --threads 2 --cluster-size 500
```
A full list of arguments are listed below. In addition to the standard SHAPEIT2 parameters, SHAPEIT3 has the following arguments:

| Option | Description |
| --- |   |
|–fast |Turn on fast mode. Greater speed with a small decrease in| accuracy. (suitable for N>10,000)|
|–cluster-size arg |cluster size for fast conditioning haplotype search. We have found 4000 provides a good tradeoff|
|–early-stopping |do not perform HMM calculations when perfect matches are found with conditioning haplotypes|



## Full list of options

### Basic options:

| Option | Description |
|  |   |
|-H [ –help ]  | Produce help message.|
| –seed arg (=1484822686) | Seed of the random number generator.|
| -T [ –thread ] arg (=1) | Number of thread used for phasing.|
| -L [ –output-log ] arg (=shapeit_date_time_UUID.log) | Log file containing a duplicate of the screen output.|

### Subsetting options:

| Option | Description |
|  |   |
|–exclude-snp arg |File containing all the positions of the SNPs to exclude in input/output  files.|
|–include-snp arg |File containing all the positions of the SNPs to
include in input/output files.|
|–exclude-ind arg |File containing all the ID of the individuals to exclude in input/output  files.|
|–include-ind arg | File containing all the ID of the individuals to include in input/output
files.|
|–input-from arg (=0) |First physical position to consider in  input files.|
|–input-to arg (=1000000000) |Last physical position to consider in input file.|

### Input files options:

| Option | Description |
|  |   |
| -B [ –input-bed ] arg | Unphased genotypes in Plink BED/BIM/FAM format.|
| -M [ –input-map ] arg |Genetic map in HapMap format.|
|-G [ –input-gen ] arg | Unphased genotypes in Impute2 GEN/SAMPLE format.|
| –input-thr arg (=0.9) |Probability threshold used to call a genotype in GEN file.|
|-R [ –input-ref ] arg | Reference set of haplotypes in HAPS/SAMPLE format.|

### MCMC options:

| Option | Description |
|  |   |
|–burn arg (=7) |Number of burn-in MCMC iterations.|
|–prune arg (=8) |Number of pruning MCMC iterations.|
|–main arg (=20) |Number of main MCMC iterations.|

### Model options:

| Option | Description |
|  |   |
|-c [ –cluster_burn ] arg (=1) | Frequency of clustering in burnin  iterations.|
|-S [ –states ] arg (=100) | Number of hidden states used for  phasing.|
| –effective-size arg (=15000) | Effective size of the population.|
|–rho arg (=0.0004) |Constant recombination rate.|
|–fast |Turn on fast mode. Greater speed with a small decrease in accuracy. (suitable
for N>10,000)|
|–cluster-size arg |cluster size for fast conditioning haplotype
| search. Accuracy and computation time will increase with this value. We have found 4000 provides a good tradeoff|
|–early-stopping |do not perform HMM calculations when perfect matches are found with conditioning haplotypes|
|-W [ –window ] arg (=2) |Mean size of the windows in which conditioning haplotypes are defined.|

### Output file options:

| Option | Description |
|  |   |
|-O [ –output-max ] arg | Phased haplotypes in Impute2 format.|


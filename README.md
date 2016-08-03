# ngsDist

`ngsDist` is a program to estimate pairwise genetic distances directly, taking the uncertainty of genotype's assignation into account. It does so by avoiding genotype calling and using genotype likelihoods or posterior probabilities.

### Citation

`ngsDist` was published in 2015 at [Biological Journal of the Linnean Society](http://onlinelibrary.wiley.com/doi/10.1111/bij.12511/abstract), so please cite it if you use it in your work:

    Vieira FG, Lassalle F, Korneliussen TS, Fumagalli M
    Improving the estimation of genetic distances from Next-Generation Sequencing data
    Biological Journal of the Linnean Society (2015) doi: 10.1111/bij.12511

### Installation

`ngsDist` can be easily installed but has some external dependencies:

* `zlib`: v1.2.7 tested on Debian 7.8 (wheezy)
* `gsl` : v1.15 tested on Debian 7.8 (wheezy)
* `md5sum`: only needed for `make test`

To install the entire package just download the source code:

    % git clone https://github.com/fgvieira/ngsDist.git

To install these tools just run:

    % cd ngsDist
    % make
    % make test

Executables are built into the main directory. If you wish to clean all binaries and intermediate files:

    % make clean

### Usage

    % ./ngsDist [options] --geno /path/to/input/file --n_ind INT --n_sites INT --out /path/to/output/file

#### Parameters
* `--geno FILE`: input file with genotypes, genotype likelihoods or genotype posterior probabilities.
* `--n_ind INT`: sample size (number of individuals).
* `--n_sites INT`: number of sites in input file.
* `--tot_sites INT`: total number of sites in dataset.
* `--labels FILE`: labels, one per line, of the input sequences.
* `--probs`: is the input genotype probabilities (likelihoods or posteriors)?
* `--log_scale`: Ii the input in log-scale?.
* `--call_geno`: call genotypes before running analyses.
* `--N_thresh DOUBLE`: minimum threshold to consider site; missing data if otherwise (assumes -call_geno) 
* `--call_thresh DOUBLE`: minimum threshold to call genotype; left as is if otherwise (assumes -call_geno)
* `--pairwise_del`: pairwise deletion of missing data.
* `--alt_het_dist`: use heterozygote distance of 0.5 (instead of 0).
* `--indep_geno`: assume independence between genotypes?
* `--n_boot_rep INT`: number of bootstrap replicates [0].
* `--boot_block_size INT`: block size for bootstrapping [1].
* `--out FILE`: output file name.
* `--n_threads INT`: number of threads to use. [1]
* `--version`: prints program version and exits.
* `--verbose INT`: selects verbosity level. [1]
* `--seed INT`: random number generator seed (only for the bootstrap analysis).

### Input data
As input, `ngsDist` accepts both genotypes, genotype likelihoods (GP) or genotype posterior probabilities (GP). Genotypes must be input as gziped TSV with one row per site and one column per individual (__n_sites\*n_ind__) and genotypes coded as [-1, 0, 1, 2].
As for GL and GP, `ngsDist` accepts both gzipd TSV and binary formats, but with 3 columns per individual (__3\*n_sites\*n_ind__) and, in the case of the binary, the GL/GP coded as doubles

### Thread pool
The thread pool	implementation was adapted from Mathias Brossard's and is freely available from:
https://github.com/mbrossard/threadpool

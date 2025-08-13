# GLOOME: Gain Loss Mapping Engine  
*A bioinformatics tool for analyzing gene gain and loss events during evolution*

GLOOME provides evolutionary analysis of presence and absence profiles (phyletic patterns). These patterns are assumed to result from gain and loss dynamics along a phylogenetic tree. Examples of characters represented by phyletic patterns include:

- Restriction sites  
- Gene families  
- Introns  
- Indels

The primary purpose of the GLOOME server is to accurately infer **branch-specific** and **site-specific** gain and loss events. This inference is based on a **stochastic mapping approach**, using evolutionary models that accurately reflect the underlying biological processes.

## Features

- Support for various evolutionary models  
- Gain and loss inference using **stochastic mapping** or **maximum parsimony**  
- Estimation of gain/loss rates per character  
- Advanced optimization options  
- Likelihood and parsimony-based output

A **full user manual** is included in the release:  
**`GLOOME.CoPAP.gainLoss.Manual.pdf`**

This manual provides comprehensive guidance on installation, input formats, command-line usage, interpretation of results, and troubleshooting.

---

## Installation

### Requirements

- UNIX/Linux system  
- GNU Compiler (gcc/g++)

### Steps

1. Download the latest release: `gainLoss.tar.zip`

2. Unzip and untar the archive:
   
   ```bash
   unzip gainLoss.tar.zip
   tar -xvf gainLoss.tar```

This will create the following directory structure:


```
libs/phylogeny
programs/gainLoss
```

### Build Option 1: Using Makefiles

3. Compile the **phylogeny** library:

   ```bash
   cd libs/phylogeny
   make
   ```

4. Compile the `gainLoss` program:

   ```bash
   cd ../../programs/gainLoss
   make
   ```


This will generate an executable called `gainLoss` in the `programs/gainLoss/` directory.

### Build Option 2: Manual Compilation (If Makefiles Fail)

1. Move the phylogeny source files:

   ```bash
   mv libs/phylogeny/* programs/gainLoss/
   ```

2. Compile the program:

   ```bash
   cd programs/gainLoss
   g++ -O3 -o gainLoss *.cpp
   ```

   The compiled binary will reside in `programs/gainLoss/`.

---

## Program Execution

Run the program using:

```bash
gainLoss <paramFileName>
```

The required argument is a **parameter file**, which specifies:

* A 0/1 phyletic pattern file (FASTA format)
* Optionally: A tree file (Newick format)
* Other optional configuration parameters (in case if not provided default parameters will be used)

---

## Parameter File Example

Below is an example of the contents of a `paramFileName` used to configure a run of `gainLoss`:

```ini
######## gainLoss Parameters file ########

### Required (FASTA)
_seqFile   /<Path>/msaFile.aln

### Recommended (Newick format)
_treeFile  /<Path>/usrTreeFile

### Evolutionary Model Options
_rateDistributionType       GAMMA
_minNumOfOnes               1
_minNumOfZeros              0

### Additional Output Options
_costMatrixGainLossRatio    1           # Parsimony
_calculateRate4site         1           # Likelihood-based output per site
_calculeGainLoss4site       1

### Advanced Optimization Settings
_logValue                   4
_performOptimizations       1
_optimizationLevel          VVlow
_numberOfRateCategories     3
_numberOfGainCategories     3
_numberOfLossCategories     3
```

---

## Input File Formats

* ***seqFile*** (required): Binary sequence file in **FASTA** format using 0/1 encoding
* ***treeFile*** (optional but recommended): Tree in **Newick** format

If `_treeFile` is not provided, only default or basic analyses will be run.

---

## Notes

* Only `_seqFile` is strictly required to run the program
* If no other parameters are provided, default values will be used
* Providing a `_treeFile` improves accuracy of gain/loss event estimation

---

## Contact

For issues, questions, or contributions, please open an issue on the repository or contact the maintainer.

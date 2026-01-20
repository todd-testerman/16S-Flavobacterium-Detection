# 16S rRNA Flavobacterium Detection

A computational workflow for 16S rRNA gene sequencing analysis focused on Flavobacterium detection using QIIME2 and R.

## Overview

This repository contains the analysis pipeline and visualization code used for 16S rRNA microbiome sequencing analysis. The workflow processes paired-end Illumina sequencing data to identify and visualize bacterial communities, with a focus on Flavobacterium detection.

## Repository Structure

```
16S-Flavobacterium-Detection/
├── scripts/
│   └── qiime2_analysis_pipeline.sh    # Main QIIME2 processing pipeline
├── docs/
│   └── R_analysis_barplots.html       # R Markdown analysis and visualizations
├── .gitignore
└── README.md
```

## Workflow

### 1. QIIME2 Processing Pipeline

The shell script (`scripts/qiime2_analysis_pipeline.sh`) performs the following steps:

1. **Import**: Imports paired-end FASTQ files from Illumina sequencing
2. **Denoise**: Uses DADA2 for quality filtering, denoising, and chimera removal
3. **Taxonomy Assignment**: Classifies sequences using the GreenGenes (gg-13-8-99) database with a naive Bayes classifier
4. **Output Generation**: Produces feature tables, representative sequences, and taxonomy assignments

**Key Parameters Used:**
- Trim positions: 0 (left), 250 (right) for both forward and reverse reads
- Training reads: 400,000
- Chimera detection: min fold parent over abundance = 1.5
- Taxonomy confidence: 0.8 (80%)

### 2. R Statistical Analysis

The R Markdown document (`docs/R_analysis_barplots.html`) contains:

- Import of QIIME2 output files into R using phyloseq
- Data pre-processing and normalization
- Taxonomic barplot visualizations using ggplot2
- Publication-ready figures

**View the R analysis document:** [HTML Preview](https://htmlpreview.github.io/?https://github.com/todd-testerman/16S-Flavobacterium-Detection/blob/main/docs/R_analysis_barplots.html)

## Requirements

### QIIME2 Pipeline
- QIIME2 (version 2019.1 or compatible)
- GreenGenes classifier (gg-13-8-99-515-806-nb-classifier.qza)
- Silva classifier (optional: silva-132-99-515-806-nb-classifier.qza)

### R Analysis
- R (version 3.6+)
- phyloseq
- ggplot2

## Usage

### Running the QIIME2 Pipeline

```bash
# Activate QIIME2 environment
source activate qiime2-2019.1

# Navigate to your working directory
cd /path/to/your/data

# Run the pipeline
bash /path/to/scripts/qiime2_analysis_pipeline.sh
```

The script will prompt you for:
1. **FASTQ directory**: Path to the folder containing your paired-end FASTQ files
2. **Map file**: Path to your sample metadata file (.txt)
3. **Sampling depth**: Rarefaction depth for diversity analyses

### Input Data Requirements

- Paired-end Illumina FASTQ files (e.g., `*_L001_R1_001.fastq.gz`)
- Sample metadata file in QIIME2-compatible format
- Files should be in a single directory without subdirectories

### Output Files

The pipeline generates:
- `demux-paired-end.qza` - Imported sequences
- `table.qza` - Feature table (ASV counts)
- `rep-seqs.qza` - Representative sequences
- `denoising-stats.qza` - DADA2 statistics
- `taxonomy-gg.qza` - GreenGenes taxonomy assignments

## Reference Databases

This workflow uses the V4 region (515-806) of the 16S rRNA gene with:

- **GreenGenes**: gg-13-8-99 at 99% identity
- **Silva** (optional): SILVA 132 at 99% identity

Classifiers can be downloaded from the [QIIME2 Data Resources](https://docs.qiime2.org/2019.1/data-resources/) page.

## Contact

For questions or issues, please contact:

**Todd Testerman**
Email: todd.testerman@uconn.edu

## License

This project is provided for academic and research purposes.

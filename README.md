<div align="center">
    <a href="#readme"><img src="./docs/img/PaintSHOP-logo.png" width="200"></a>
</div>

# PaintSHOP Pipeline - Memory-Optimized Fork

This is a memory-efficient fork of the [original PaintSHOP_pipeline](https://github.com/beliveau-lab/PaintSHOP_pipeline) that modifies the `parse_pairwise.py` script to use streaming processing instead of loading entire files into memory.

## Key Changes

- **Streaming Processing**: The modified `parse_pairwise.py` reads:
  - File 1: 4 lines at a time (standard FASTQ format)
  - File 2: 1 line at a time
- **Memory Efficiency**: Processes and writes results in batches, significantly reducing memory usage for large files
- **Same Output**: Produces identical results to the original implementation
- **Additional Dependency**: Requires the `re` module (standard library)

## Why Use This Fork?

This fork is ideal if you're:
- Processing large FASTQ files that exceed available memory
- Running the pipeline on systems with limited RAM
- Working with multiple samples in parallel

## Installation

Same as the original pipeline, with no additional external dependencies (uses Python's built-in `re` module).

---

# PaintSHOP Pipeline

[![Snakemake](./docs/img/snakemake.svg)](https://snakemake.readthedocs.io)
[![DOI](./docs/img/preprint.svg)](https://doi.org/10.1101/2020.07.05.188797)

## Overview

[PaintSHOP](https://www.biorxiv.org/content/10.1101/2020.07.05.188797v1) is a technology that enables the interactive design of oligonucleotide FISH experiments at genome and transcriptome-scale and is comprised of two components:

1. A scalable machine learning pipeline for probe specifity prediction

2. An interactive Shiny web application for probe design

This repository contains the Snakemake workflow for the machine learning pipeline and the full software stack needed to design probes for additional genomes not already hosted on the web application.

## Installation

1. Make sure you have [conda](https://docs.conda.io/en/latest/miniconda.html) installed. 

2. Install Mamba to facilitate snakemake installation, as recommended in the [Snakemake docs](https://snakemake.readthedocs.io/en/stable/getting_started/installation.html#installation-via-conda-mamba).

```
$ conda install -n base -c conda-forge mamba
```

3. Clone this repo, then create and activate the provided [environment](./environment.yml):

```
$ git clone https://github.com/beliveau-lab/PaintSHOP_pipeline.git \
    && cd PaintSHOP_pipeline/ \
    && mamba env create -f environment.yml \
    && conda activate paintshop_snakemake
```

## Running the pipeline

A complete example is included to test the pipeline installation. To run the pipeline on the included sample files: 

```
$ cd example_run/ && ./run_pipeline.sh
```

When this example is run, pipeline output will be generated [here](./example_run/pipeline_output/). Expected outputs are provided [here](./example_run/expected_pipeline_output) for comparison. 

To run the pipeline on your own data, update the file paths in [config.yml](./example_run/config.yml) with the paths to your
genome assembly files. For more information on input and output files, see the [documentation](#documentation).

This pipeline is implemented using [Snakemake](https://snakemake.readthedocs.io/en/stable/index.html), and distributed according to [best practices](https://snakemake.readthedocs.io/en/stable/snakefiles/deployment.html). If you are new to Snakemake, the [tutorial](https://snakemake.readthedocs.io/en/stable/tutorial/tutorial.html) is a great place to get started to learn more.

![PaintSHOP Pipeline](../../raw/master/docs/img/pipeline.svg)

## Documentation

Additional information is available in the docs:

* [Input file specification](./docs/pipeline_input.md)
* [Output file specification](./docs/pipeline_output.md)
* [Description of pipeline steps](./docs/pipeline_steps.md)

## Questions

If you have questions or issues, please [open an issue](../../issues/new) on GitHub.

## Citation

For usage of the pipeline and/or web application, please cite according to the enclosed [citation.bib](./docs/citation.bib).

## License

We provide this open source software without any warranty under the [MIT license](https://opensource.org/licenses/MIT).

# DIRT Batch Processor for 2D Root Images

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Docker](https://img.shields.io/badge/Docker-Enabled-blue.svg)
![Bash](https://img.shields.io/badge/Language-Bash-green.svg)

A lightweight batch-processing workflow for running **DIRT (Digital Imaging of Root Traits)** on chile pepper root images using the official Docker image from the Computational Plant Science Lab, The University of Arizona. This workflow is designed for plant breeders using **Docker Desktop with WSL integration** and enables high-throughput root phenotyping without installing DIRT or its dependencies locally.

---

## Features

- Processes all `.JPG` images located in the `images/` directory
- Automatically creates organized output directories for each image
- Uses the official `computationalplantscience/dirt` Docker image
- Generates image-specific DIRT outputs
- Eliminates the need to install Python, graph-tool, or DIRT dependencies locally
- Suitable for high-throughput chile pepper root phenotyping

---

## Project Structure

```text
dirt-batch-root-analysis/
├── images/
│   └── *.JPG
├── results/
├── scripts/
│   └── run_dirt_batch.sh
├── README.md
```

---

## Prerequisites

### 1. Install Docker Desktop

Download and install Docker Desktop:

https://www.docker.com/products/docker-desktop/

During installation:

- Enable WSL 2 integration
- Enable integration with your Linux distribution
- Restart Docker Desktop if prompted

Verify Docker is available inside WSL:

```bash
docker --version
docker run hello-world
```

### 2. Download the DIRT Docker Image

Pull the official DIRT container:

```bash
docker pull computationalplantscience/dirt:latest
```

This only needs to be done once.

---

## Installation

Clone this repository:

```bash
git clone https://github.com/EhtishamSK/Pheno-Roots.git
cd dirt-batch-root-analysis
```

Make the batch-processing script executable:

```bash
chmod +x scripts/run_dirt_batch.sh
```

Place all root images in the `images/` directory.

Example:

```text
images/
├── 25C001.JPG
├── 25C002.JPG
├── 25C003.JPG
└── ...
```

---

## Usage

Navigate to the scripts directory:

```bash
cd scripts
```

Run the batch processor:

```bash
./run_dirt_batch.sh
```

The script will automatically:

1. Detect all `.JPG` images in the `images/` directory.
2. Create a dedicated results folder for each image.
3. Launch the DIRT Docker container.
4. Extract root traits.

---

## DIRT Parameters

The script executes DIRT using the following parameters:

```text
1 1.0 1 1 1 25.4 0 0 0
```

These correspond to the standard DIRT processing settings used by the Docker image.

If desired, these values can be modified directly within `scripts/run_dirt_batch.sh`.

---

## Output

After processing, the directory structure will resemble:

```text
results/
├── 25C001/
│   ├── 1/
│   ├── Mask/
│   ├── Crown/
│   └── Lateral/
│
├── 25C002/
│   ├── 1/
│   ├── Mask/
│   ├── Crown/
│   └── Lateral/
│
└── ...
```
## Example Workflow

```bash
git clone https://github.com/YOUR_USERNAME/Pheno-Roots-analysis.git

cd dirt-batch-root-analysis

docker pull computationalplantscience/dirt:latest

chmod +x scripts/run_dirt_batch.sh

cp /path/to/root_images/*.JPG images/

cd scripts

./run_dirt_batch.sh
```

After completion:

```text
results/      # Image-specific DIRT outputs
```
## Example Input and Output

### Input Image (Raw Root System)

<img src="raw_image.JPG" width="450">

This is the raw root image prepared for DIRT analysis (clean background, clearly visible root architecture).

---

### Output Image (DIRT Processed)

<img src="analyzed_image.png" width="450">

This is the output after DIRT processing showing segmented root structure and extracted phenotypic traits.

## Applications

This workflow can be used for:

- Root phenotyping in chile pepper breeding programs
- Root architecture analysis
- Quantitative trait extraction
- Genome-wide association studies (GWAS)
- Genomic prediction and breeding applications
- High-throughput root image processing

---

## Acknowledgments

- DIRT (Digital Imaging of Root Traits)
- Computational Plant Science Lab
- The DIRT development team for providing the Docker-based analysis pipeline

## References

This work builds on the open-source DIRT platform:

- Das, A., Schneider, H., Burridge, J. et al. *Digital imaging of root traits (DIRT): a high-throughput computing and collaboration platform for field-based root phenomics*. Plant Methods 11, 51 (2015).  
  https://doi.org/10.1186/s13007-015-0093-3

- Computational Plant Science Platform (official site):  
  https://computational-plant-science.org/joomla5/

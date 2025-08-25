# Learning REST with Ensembl

This mini-project is a hands-on tutorial for learning how to use a **REST API** in bioinformatics.  
It focuses on the [Ensembl REST API](https://rest.ensembl.org/), which provides programmatic access to genes, transcripts, sequences, and species information.

The tutorial is implemented as an **R Markdown document** (`ensembl_rest_tutorial.Rmd`) with embedded **Bash** and **R** code chunks.

---

## What you will learn

- What a **REST API** is and how it works in bioinformatics
- How to send HTTP requests with `curl` (Bash)
- How to parse **JSON** and **FASTA** responses in R
- How to:
  - Look up a gene by symbol
  - Fetch genomic sequences and coding sequences
  - Explore transcripts of a gene
  - Query genomic regions for overlapping genes
  - List available species in Ensembl
  - Automate batch queries (symbols → Ensembl IDs → FASTA)

---

## Requirements

- **R (≥ 4.0)**
- **R packages:**
  - [`jsonlite`](https://cran.r-project.org/package=jsonlite)
  - [`readr`](https://cran.r-project.org/package=readr)
- **Command-line tools:**
  - `curl` (default on macOS/Linux, available on Windows via Git Bash)
  - [`jq`](https://stedolan.github.io/jq/) (optional, for pretty-printing JSON)

Install R dependencies:

```r
install.packages(c("jsonlite", "readr"))
```

## Project structure

```
.
├── ensembl_rest_tutorial.Rmd   # Main R Markdown tutorial
├── README.md                   # This file
├── data/                       # JSON responses from batch lookups
├── fasta_genomic/              # Genomic FASTA files for multiple genes
├── brca1.json                  # Example JSON for BRCA1
├── BRCA1_genomic.fasta         # Example FASTA sequence for BRCA1

```

## Example output

Example BRCA1 metadata (from brca1.json):

```json
{
  "id": "ENSG00000012048",
  "display_name": "BRCA1",
  "seq_region_name": "17",
  "start": 43044295,
  "end": 43125482,
  "strand": 1
}


```

Example FASTA header (from BRCA1_genomic.fasta):

```{shell}
>ENSG00000012048 BRCA1
ATG...


```

## Notes


- expand=1 is a query parameter that includes transcripts and exons in the response.

- Always set the Accept header to control output format (application/json or text/x-fasta).

- Be polite with the API: insert short delays (sleep 0.2) in loops.

- Record Ensembl release/version for reproducibility.

- For large projects, integrate these steps into Snakemake or targets workflows.




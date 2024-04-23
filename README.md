# GWAS SumStats Tools
___

GWAS SumStats Tools is a versatile toolkit created to simplify the processing, validation, and formatting of GWAS summary statistics files intended for submission to the GWAS catalog. This toolkit provides a variety of features designed for efficiency and ease of use.

## Features
1. Reading: Preview a GWAS summary statistics data file, extract headers, metadata, or specific field-value pairs from the metadata.
2. Formatting: Convert tubular sumstats files to GWAS catalog standard format (gwas-ssf), with options for spliting fields, renaming fields, reordering, convert -log (P-value) to normal P-values, handling missing values efficiently and removing comments.
3. Metadata Generation: Automatically generate metadata for a data file from a submission form or create metadata from the GWAS Catalog (for internal use).
4. Validation: Validate the integrity of a summary statistic file using a dynamically generated schema.

## Quick Start

### User-friendly interface
If you prefer a user-friendly interface for formatting or validating your data, you can use our online tool. This interface allows you to quickly format or validate individual files with a size limit of 2 GB, all without the need for command-line usage. Simply click on the link below to access the tool and upload your data directly from your local computer:

[GWAS SumStats Tools Online Interface - format and validation](https://ebispot.github.io/gwas-sumstat-format-was/)

> [!TIP|style:callout]
> Please note that this interface works with **a single file only** and has a file size limitation of  <span style="font-size:1.2em;">**2 GB** </span>. 

For instructions on how to use the user-friendly interface, please visit our UI Guide Page (Link to be provided).

### Command Line
However, if you require full access to all functions, or if you need to process larger files or multiple files simultaneously, we recommend using the command-line interface. Please follow the instructions provided here to install and use the command-line tools.

Installation requirements:

Python >= 3.9 and <3.12

If you have a different Python version installed on your local computer and encounter compatibility issues, you can create a virtual environment with Python 3.9 and please follow the instruction [here]()

#### Local Installation with pip
```bash
$ pip3 install gwas-sumstats-tools
```

#### Run with Docker
You can also run GWAS SumStats Tools using Docker:
```bash
$ docker run -it -v ${PWD}:/application ebispot/gwas-sumstats-tools:latest
```

----
Copyright © EMBL-EBI 2024 | EMBL-EBI is an Outstation of the [European Molecular Biology Laboratory](https://www.embl.org/) | [Terms of use](https://www.ebi.ac.uk/about/terms-of-use) | [Data Preservation Statement](https://www.ebi.ac.uk/long-term-data-preservation)

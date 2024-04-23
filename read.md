# Read
---
The Read tool is specifically designed to provide a comprehensive preview of GWAS summary statistics data files or metadata. It offers functionality to extract headers from GWAS summary statistics data files or extract specific fields from the metadata.

## Usage
<span style="font-size:1.5em;">`gwas-ssf read file [options]`</span>

## Options
| Options | short name | type | Default value | Description |
|:--------|:----------:|:----:|:-------------:|:------------|
|`--help`| `-h` |Boolean|False|Display help message|
|`--get_header`|`-h` |Boolean|False|Return the headers of the file|
|`--meta-in`| |Path|filename-meta.yaml|Specify a metadata file to read in,defaulting to filename-meta.yaml|
|`--get-all-metadata`|`-M`|Boolean|False|Return all metadata|
|`--get-metadata`|`-m`|List| None| Get metadata for the specified fields e.g. `-m genomeAssembly -m isHarmonised`|


## Examples


----
Copyright © EMBL-EBI 2024 | EMBL-EBI is an Outstation of the [European Molecular Biology Laboratory](https://www.embl.org/) | [Terms of use](https://www.ebi.ac.uk/about/terms-of-use) | [Data Preservation Statement](https://www.ebi.ac.uk/long-term-data-preservation)

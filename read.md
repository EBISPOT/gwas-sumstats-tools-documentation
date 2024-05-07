# Read
---
The Read tool is specifically designed to provide a comprehensive preview of GWAS summary statistics data files or metadata. It offers functionality to extract headers from GWAS summary statistics data files or extract specific fields from the metadata.

## Usage
<span style="font-size:1.5em;">`gwas-ssf read file [options]`</span>

## Options
| Options | short name | type | Default value | Description |
|:--------|:----------:|:----:|:-------------:|:------------|
|`--help`| `-h` |Boolean|False|Display help message|
|`--get_header`|`-h` |Boolean|False|Return the first five rows of the file|
|`--meta-in`| |Path|filename-meta.yaml|Specify a metadata file to read in,defaulting to filename-meta.yaml|
|`--get-all-metadata`|`-M`|Boolean|False|Return all metadata in the metadata file|
|`--get-metadata`|`-m`|List| None| Get metadata for the specified fields e.g. `-m genome_assembly -m is_harmonised`|


## Examples
Suppose you have a file named `gwas_sumstats.txt` that you want to preview the data, metadata yaml file or extract specific fields from the meta-yaml file `gwas_sumstats.txt-meta.yaml`:

1. Previewing the data (first five rows of the input file.)
```bash
gwas-ssf read gwas_sumstats.txt --get_header
```

<details>
<summary>output</summary>

```text
#-------- SUMSTATS DATA PREVIEW --------#
+------------+--------------------+---------------+--------------+------------+----------------+-------------------------+----------+
| chromosome | base_pair_location | effect_allele | other_allele | beta       | standard_error | effect_allele_frequency | p_value  |
+============+====================+===============+==============+============+================+=========================+==========+
| 1          | 930158             | T             | C            | -0.192142  | 0.364216       | 8.57396e-06             | 0.597811 |
+------------+--------------------+---------------+--------------+------------+----------------+-------------------------+----------+
| 1          | 930165             | A             | G            |-0.0217538  | 0.15844        | 4.53193e-05             | 0.890793 |
+------------+--------------------+---------------+--------------+------------+----------------+-------------------------+----------+
| 1          | 930204             | A             | G            |0.105264    | 0.161247       | 4.40944e-05             | 0.513879 |
+------------+--------------------+---------------+--------------+------------+----------------+-------------------------+----------+
| 1          | 930215             | G             | A            |0.0819067   | 0.257544       | 1.71478e-05             | 0.750462 |
+------------+--------------------+---------------+--------------+------------+----------------+-------------------------+----------+
| 1          | 930245             | A             | G            |0.252748    | 0.227135       | 2.20551e-05             | 0.265808 |
+------------+--------------------+---------------+--------------+------------+----------------+-------------------------+----------+
```
</details>



2. Previewing all fields in the meta-yaml files, `gwas_sumstats.txt-meta.yaml`, which is located in the same directory where your code is being executed:
```bash
gwas-ssf read gwas_sumstats.txt --get-all-metadata
```

3. Assume you need to extract specific fields (genome_assembly and harmonisation status) from the meta-yaml file `gwas_sumstats.txt-meta.yaml`, which is located in a **different** directory where your code is being executed:
```bash
gwas-ssf read gwas_sumstats.txt --meta-in $path_to_the_metadata_yaml --get-metadata genome_assembly -m is_harmonised
```
output:
```bash
#-------- SUMSTATS METADATA --------#
genome_assembly: GRCh37
is_harmonised: false
```
----
Copyright © EMBL-EBI 2024 | EMBL-EBI is an Outstation of the [European Molecular Biology Laboratory](https://www.embl.org/) | [Terms of use](https://www.ebi.ac.uk/about/terms-of-use) | [Data Preservation Statement](https://www.ebi.ac.uk/long-term-data-preservation)

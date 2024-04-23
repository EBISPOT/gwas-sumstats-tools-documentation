# Format
---
The Format tool is designed to facilitate the formatting of any summary statistics files into the GWAS catalog standard format ([gwas-ssf](https://github.com/EBISPOT/gwas-summary-statistics-standard)). This documentation provides a guide on how to use the `gwas-ssf format` in terminal.

## Usage
<span style="font-size:1.5em;">`gwas-ssf format file [options]`</span>

## Options
| Options | short name | type | Default value | Description |
|:--------|:----------:|:----:|:-------------:|:------------|
|`--help`| `-h` |Boolean|False|Display help message, providing guidance on how to use the tool and its various functionalities. It's a handy feature for users who may be unfamiliar with the tool or need a quick reference on its usage.|

**Options for reading the input file**

| Options | short name | type | Default value | Description |
|:--------|:----------:|:----:|:-------------:|:------------|
|`--delimiter`|`-h` |Text|"\t" for .tsv, "," for .csv and " " for .txt|Specify the delimiter in the file, if not specified, we can automatically detect the delimiter as whitespace if your is *.txt file, or comma if your is *.csv file; or tab if your is *.tsv.gz file. Otherwise, please specify the delimiter which can help to recognise the column correctly|
|`--remove_comments`|`-r`|Text|None|Remove the comments in the file|

**Options for generateing configure file**

| Options | short name | type | Default value | Description |
|:--------|:----------:|:----:|:-------------:|:------------|
|`--generate_config`|`-g` |Boolean|False|To generate the configure file for the file needed to be formatted|
|`--config_out`| |Path|None|Specify the configure json output file|

**Options for applying configure file**

| Options | short name | type | Default value | Description |
|:--------|:----------:|:----:|:-------------:|:------------|
|`--apply_config`|`-a` |Boolean|False|Apply the given configure file to the file|
|`--test_config`|`-t` |Boolean|False|Test the given configure file to the first 5 rows of the file|
|`--config_in`| |Path|None|Specify a configure json file to read in|
|`--ss_out`|`-o`|Path|None|Output sumstats file|
|`--analysis_software`|`-f`|Text|None|Specify the analysis software used for generating the summary statistic data|
|`--minimal2standard`|`-s` |Boolean|False|Try to convert a valid, minimally formatted file to the standard format. This assumes the file at least has `p_value` combined with rsid in `variant_id` field or `chromosome` and `base_pair_location`. Validity of the new file is not guaranteed because mandatory data could be missing from the original file. Please use '\t' for tab, ',' for comma, and for whitespace|

**Options for batchly applying configure file**

| Options | short name | type | Default value | Description |
|:--------|:----------:|:----:|:-------------:|:------------|
|`--batch_apply`|`-b` |Boolean|False|Batchly apply configure files to the corresponding files|
|`--lsf`| |Boolean|False|Running the batch process via subitting jobs via LSF|
|`--slurm`| |Boolean|False|Running the batch process via subitting job via Slurm|


## Examples
Suppose you have a file named `GCST12345.txt` that needs to be formatted into the GWAS Sum Stats Formatter (gwas-ssf) format.

### 1. To generate a configuration file:
```bash
gwas-ssf format GCST12345.txt --generate_config --config_out GCST12345.json
```
If your file contains comments at the beginning, which may interfere with header recognition, you can remove them using the --remove_comments option:
```bash
gwas-ssf format GCST12345.txt --generate_config --config_out GCST12345.json --remove_comments "#" 
```
Failure to recognize the correct separator can indeed lead to header recognition issues. By default, the format assumes whitespace as the separator for files with "txt" as suffix. However, if the actual delimiter in `GCST12345.txt` is tab, you can specify it using the --delimiter option as follows:
```bash
gwas-ssf format GCST12345.txt --generate_config --config_out GCST12345.json --remove_comments "#" --delimiter "\t"
```
This command ensures that the formatter correctly identifies correct delimiter, allowing for accurate header recognition during the formatting process. Adjust the options as needed to match the specific requirements of your input file.

### 2. Apply a configured file to a summary statistics file:
#### 2.1. Testing the configured file with the first 5 rows of your input file and previewing the result:
```bash
gwas-ssf format GCST12345.txt --test_config  --config_in GCST12345.json
```
Since the --remove_comments and --delimiter options are already specified in the `GCST12345.json` file, there is no need to specify them again here.
#### 2.2 Applying the configured file to the entire file:
```bash
gwas-ssf format GCST12345.txt --apply_config  --config_in GCST12345.json -o GCST12345_formatted.tsv
```
These commands allow you to test and apply the configuration stored in GCST12345.json to the summary statistics file GCST12345.txt, generating a formatted output file named GCST12345_formatted.tsv. Adjust the options as needed to match your specific configuration and file requirements.

### 3. Format a sumstat file use pre-defined configure
We provide pre-defined configuration files tailored for outputs from specific software packages. Currently, we support configurations for `REGENIE` and `BOLT-LMM`. Support for `METAL` and `SNPtest` configurations will be available soon.

To apply a pre-defined configuration for "REGENIE" to your `GCST12345.txt` file and generate a formatted output file named `GCST12345_formatted.tsv`, you can use the following command:

```bash
gwas-ssf format GCST12345.txt  --apply_config --analysis_software "REGENIE" -o GCST12345_formatted.tsv
```
This command ensures that the formatting process aligns with the specific output format of the "REGENIE" software, simplifying the data processing workflow. Adjust the options as needed based on the software used for generating your summary statistics file.

### 4. Apply a configure file to a list of files 
When dealing with multiple studies in the same format within a publication, you can streamline the formatting process by generating a single configuration file and applying it to all studies.
```bash
gwas-ssf format to_format_list.tsv --apply_config --batch_apply --analysis_software "REGENIE" 
```
The `to_format_list.tsv` file is a tab-separated file containing two columns: the full path of the input file in the first column, and the full path of the corresponding output file in the second column. Here's an example format:

```tsv
path_to_GCST12341.txt path_to_GCST12341_formatted.tsv
path_to_GCST12342.txt path_to_GCST12342_formatted.tsv
path_to_GCST12343.txt path_to_GCST12343_formatted.tsv
.......
```
* How to generate to_format_list.tsv file?
You can easily create the to_format_list.tsv file by preparing your data in a Google Sheets document. Once your data is entered, follow these steps:
  - Go to the "File" menu and select "Download".
  - Choose "Tab-separated values (.tsv)" from the available options.
This will download your spreadsheet as a TSV file to your computer, ready to be used as to_format_list.tsv.

### 5. Batchly apply a configuration file to a list of files on HPC
If your input files are large or if you have a large number of files to process, it's recommended to utilize High-Performance Computing (HPC) resources for efficient data processing. The gwas-ssf format provides direct data submission via Slurm or LSF. If you use other job scheduling tools, please reach out to us, and we'll be happy to add support for them.

```bash
gwas-ssf format to_format_list.tsv --apply_config --batch_apply --config_in GCST12345.json --slurm
```
Each input file in the list will be submitted as an independent job to run, allowing for parallel processing and efficient utilization of HPC resources. Adjust the options as needed based on your specific requirements and job scheduling system.

## How to format gwas sumstat files
**Step 1**: Determine if your input file is larger than 3GB or if you have more than one file to process.
  
  - If yes, proceed to Step 2.
  - If no, consider using the [GWAS SumStats Tools Online Interface - format and validation](https://ebispot.github.io/gwas-sumstat-format-was/) for formatting and validation.

**Step 2**: Identify if your GWAS summary statistics data is generated by `REGENIE`, `BOLT-LMM`, `METAL`, or `SNPtest`.
  - If yes, use the following command to apply a pre-defined configuration for the specified software:
    ```bash
    gwas-ssf format GCST12345.txt  --apply_config --analysis_software "REGENIE" -o GCST12345_formatted.tsv
    ```
  - If no, proceed to Step 3.

**Step 3**: Generate a configuration file based on one input file.
  ```bash
    gwas-ssf format GCST12345.txt --generate_config --config_out GCST12345.json --remove_comments "#" 
 ```
**Step 4**: Edit the configuration file.
- Refer to [How to edit configure file]()

**Step 5**: Test the configuration file on the selected input file.
```bash
gwas-ssf format GCST12345.txt --test_config  --config_in GCST12345.json
```
**Step 6**: Determine if you plan to batch process multiple input files.
  - If yes, proceed to Step 7.
  - If no, use the following command to apply the configuration to the input file:
  ```bash
  gwas-ssf format GCST12345.txt --apply_config  --config_in GCST12345.json -o GCST12345_formatted.tsv
  ```
**Step 7**: Decide if you plan to submit jobs on LSF or Slurm.
  - If yes, use the following command to submit jobs using Slurm:
  ```bash
  gwas-ssf format to_format_list.tsv --apply_config --batch_apply --config_in GCST12345.json --slurm
  ```
  - no
  If no, you can contact us for assistance or submit one job to process all your input files.

----
Copyright © EMBL-EBI 2024 | EMBL-EBI is an Outstation of the [European Molecular Biology Laboratory](https://www.embl.org/) | [Terms of use](https://www.ebi.ac.uk/about/terms-of-use) | [Data Preservation Statement](https://www.ebi.ac.uk/long-term-data-preservation)

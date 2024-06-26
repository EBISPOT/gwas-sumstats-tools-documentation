# SSF-morph
____
This guide provides instructions on how to use the GWAS summary statistics online formatting and validation tool - [SSF-morph](https://ebispot.github.io/gwas-sumstats-tools-ssf-morph/). You can use this tool to either
- **Format** (Steps 1 to 4) your summary statistics files into the GWAS Catalog standard format, as specified by the [gwas-ssf](https://github.com/EBISPOT/gwas-summary-statistics-standard) schema, or to 
- **Validate** (Step 5) whether your files adhere to this standard format.

>[!ATTENTION|style:callout]
>This interface requires a **chromium browser** (Google Chrome, Microsoft Edge) that supports the [File System Access API](https://developer.chrome.com/docs/capabilities/web-apis/file-system-access).

>[!ATTENTION|style:callout]
>Please note that this interface works with **a single file only** and has a file size limitation of **2 GB**. 

## Format Steps:

### Step 1: Select the input file:
   1. Click the `Grant Permission` button to give the browser read and write access to a specific folder.
   2. Click the `Select Input File` button to choose your input file from the authorized folder.
   3. The message `<your file> is selected` confirms that the file has been successfully selected.

### Step 2: Prepare the configuration file:
   The configuration template is generated from the input file. This template serves as a blueprint for configuring the formatting options. Please review the example configuration template provided [here](edit_config?id=summary). There are three ways to input the configuration file:
   
   - Method 1: Select the appropriate analysis software from the `Analysis Software` dropdown menu if your data is generated by `REGENIE`, `BOLT-LMM`,`SNPtest` or `SAIGE`.

   - Method 2: Click the `Generate` button to create a configuration template file based on the selected input file. The generated file will appear in the text box under the `Configure` section. 

   - Method 3: Copy and paste your own configuration file into the text box under the `Configure` section.

### Step 3: Tailor and test the configuration file:
1. Please ensure that the text box in the Configure section is not empty.
2. Click on `Show Your Input Data` button and/or `Show Example Data` button to compare the differences and adjust your configuration as necessary.
3. To further tailor the configuration file to better suit your needs, please refer to [these instructions](edit_config) on how to modify the configuration.
4. Click the `Test` button to apply the configuration to the first **FIVE** rows of your selected input file. This action generates a formatted preview output displayed under the `Your Output` section. This approach is particularly time-saving for large input files.

### Step 4: Apply configuration file and download the formatted result:
Once you are satisfied with your configuration and test result, please click the `Apply` button to apply the configuration to the entire input file and download the formatted output. You will have the option to choose the destination and name for your formatted output file. This selection will overwrite the `outFileSuffix` specified in your configuration.


## Validate Steps:

Please note:
 - The UI validation function operates independently from the formatting function and can be used separately. 
 - Unlike the CLI validation, this tool does not allow forcing acceptance of zero P-values or adjustments based on the minimum number of rows. The minimum required number of rows is set at 100,000 to pass the validation.

### Step 5: Select the input file:
   1. Click the `Grant Permission` button to give the browser read and write access to a specific folder.
   2. Click the `Select Input File` button to choose your input file from the authorized folder. Once the file is successfully selected, a confirmation message, `<your file> is selected for validation`, will appear.
   3. The message `<your file> is selected` confirms that the file has been successfully selected.
   4. Click `Validate the selected file` to begin validation. The validation results will be displayed in the box below.

----
Copyright © EMBL-EBI 2024 | EMBL-EBI is an Outstation of the [European Molecular Biology Laboratory](https://www.embl.org/) | [Terms of use](https://www.ebi.ac.uk/about/terms-of-use) | [Data Preservation Statement](https://www.ebi.ac.uk/long-term-data-preservation)

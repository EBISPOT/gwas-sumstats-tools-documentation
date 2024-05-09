# How to Edit the Configuration
----
## Configuration Overview
The configuration file serves as a blueprint for the formatting options. It includes options for output file settings and column-specific formatting operations. Users can customize field separators, column splitting, renaming, finding and replacing values, and more based on requirements.

While using the CLI, configurations are managed within the `filename.json` file. On the UI, however, configurations are accessible in a text box, allowing users to easily customize settings without the need to open and edit JSON files

<details>
<summary>Here is an example of the JSON configuration template</summary>

```json
{
    "fileConfig": {
        "outFileSuffix": null,
        "convertNegLog10Pvalue": false,
        "fieldSeparator": " ",
        "naValue": null,
        "removeComments": null,
    },
    "columnConfig": {
        "split": [
            {
                "field": "SNP",
                "separator": null,
                "capture": null,
                "new_field": null,
                "include_original": null
            },
            {
                "field": "A1",
                "separator": null,
                "capture": null,
                "new_field": null,
                "include_original": null
            },
            {
                "field": "A2",
                "separator": null,
                "capture": null,
                "new_field": null,
                "include_original": null
            },
            {
                "field": "freq",
                "separator": null,
                "capture": null,
                "new_field": null,
                "include_original": null
            },
            {
                "field": "b",
                "separator": null,
                "capture": null,
                "new_field": null,
                "include_original": null
            },
            {
                "field": "se",
                "separator": null,
                "capture": null,
                "new_field": null,
                "include_original": null
            },
            {
                "field": "p",
                "separator": null,
                "capture": null,
                "new_field": null,
                "include_original": null
            },
            {
                "field": "N_cases",
                "separator": null,
                "capture": null,
                "new_field": null,
                "include_original": null
            },
            {
                "field": "N_controls",
                "separator": null,
                "capture": null,
                "new_field": null,
                "include_original": null
            }
        ],
        "edit": [
            {
                "field": "SNP",
                "rename": "variant_id",
                "find": null,
                "replace": null,
                "extract": null
            },
            {
                "field": "",
                "rename": "",
                "find": null,
                "replace": null,
                "extract": null
            },
            {
                "field": "A1",
                "rename": "effect_allele",
                "find": null,
                "replace": null,
                "extract": null
            },
            {
                "field": "A2",
                "rename": "other_allele",
                "find": null,
                "replace": null,
                "extract": null
            },
            {
                "field": "freq",
                "rename": "effect_allele_frequency",
                "find": null,
                "replace": null,
                "extract": null
            },
            {
                "field": "b",
                "rename": "beta",
                "find": null,
                "replace": null,
                "extract": null
            },
            {
                "field": "se",
                "rename": "standard_error",
                "find": null,
                "replace": null,
                "extract": null
            },
            {
                "field": "p",
                "rename": "p_value",
                "find": null,
                "replace": null,
                "extract": null
            },
            {
                "field": "N_cases",
                "rename": "n_cas",
                "find": null,
                "replace": null,
                "extract": null
            },
            {
                "field": "N_controls",
                "rename": "n_con",
                "find": null,
                "replace": null,
                "extract": null
            }
        ]
    }
}
```
</details>

The configurations comprises two primary sections: `fileConfig` and `columnConfig`. The columnConfig section further encompasses two subsections: `split` and `edit`. 

The `fileConfig` settings are applied to the input file first, followed by modifications from the `split` and then the `edit` subsections.

### fileConfig Section:
  - `outFileSuffix`: Specifies the suffix for the output file. It is currently set to null. To name your formatted file as `filename_formatted.tsv`, specify the suffix in your configuration as shown below:
    ```json
     "outFileSuffix":"_formatted"
     ```
  - `convertNegLog10Pvalue`: Specifies whether to convert negative log10 p-values into p-values and it is set to false defautly. To enable this conversion, adjust your settings as follows:
    ```json
     "convertNegLog10Pvalue":true
     ```
  - `fieldSeparator`: Defines the field separator for reading the input file. It is same to the `--delimiter` in the command line. If not specified, we can automatically detect the delimiter as whitespace if your is *.txt file, or comma if your is *.csv file; or tab if your is *.tsv file. Otherwise, please specify the delimiter which can help to recognise the column correctly.To specify a tab as the separator, use:
     ```json
     "fieldSeparator":"\t"
     ```
  - `removeComments`: The `removeComments` field in the JSON config acts like the `--remove_comments` command-line option. Setting it to a character or string, like "#", removes lines starting with that character or string from the input file. For example, to remove lines that begin with `#`, effectively eliminating comments or metadata for a cleaner output, use:
     ```json
     "removeComments":"#"
     ```
  - `naValue`: Different software may represent missing values in various ways. The naValue parameter allows you to convert your specified missing value representation into the GWAS-SSF standard `#NA`.
    ```json
     "naValue":"Nan"
     ```


### columnConfig Section:

#### `split` Subsection:

This subsection specifies how to split certain columns in the input file. For each column, it contains:

  - `field`: Specifies the name of the column to be split.
  - `separator`: Defines the delimiter used to split the column. New columns created from the split will be name  as specified in the `new_field`.
  - `capture`: Utilizes a regular expression to extrac  specific patterns from the field into multiple ne  columns. These resulting columns are named according the values specified in `new_field`.
  - `new_field`: Names the new fields created afte  splitting.
  - `include_original`: Determines whether to retain the original column after the spliting. By default, th  original field is omitted after the operation.

      * <details>
        <summary>Separator example</summary>

        **Input**:
        | SNP | rsid | EA |
        |-----|-------|---------|
        | chr11:88249377 | rs11020170_T_C  | T   |
        | chr1:60320992 | rs116406626_A_G  | A   |
        | chr2:18069070 | rs763680312_T_C  | T   |
        | chr8:135908647 | rs11992603_A_G  | A   |

        **JSON config**:
        ```json
        "field": "SNP",
        "separator": ":",
        "capture": null,
        "new_field": ["chromosome","base_pair_location"],
        "include_original": true
        ```
        **Output**:
        | SNP | rsid | EA |chromosome|base_pair_location|
        |-----|-------|---------|----|------------------|
        | chr11:88249377 | rs11020170_T_C  | T   |chr11 |88249377 |
        | chr1:60320992 | rs116406626_A_G  | A   |chr1| 60320992 |
        | chr2:18069070 | rs763680312_T_C  | T   |chr2 |18069070 |
        | chr8:135908647 | rs11992603_A_G  | A   |chr8| 135908647 |
        </details>
      * <details>
        <summary>Capture example</summary>

        **Input**:
        | SNP | rsid | EA |chromosome|base_pair_location|
        |-----|-------|---------|----|------------------|
        | chr11:88249377 | rs11020170_T_C  | T   |chr11 |88249377 |
        | chr1:60320992 | rs116406626_A_G  | A   |chr1| 60320992 |
        | chr2:18069070 | rs763680312_T_C  | T   |chr2 |18069070 |
        | chr8:135908647 | rs11992603_A_G  | A   |chr8| 135908647 |

        **JSON config**:
        ```json
        "field": "rsid",
        "separator": null,
        "capture": "(rs[0-9]+)_([A,T,C,G])_([A,T,C,G])",
        "new_field": ["rsid","effect_allele","other_allele"],
        "include_original": false
        ```
        **Output**:
        | SNP | EA |chromosome|base_pair_location| rsid | effect_allele| other_allele |
        |-----|---------|----|------------------|-----|-----|----|
        | chr11:88249377 |T   |chr11 |88249377 |rs11020170 | T | C  |
        | chr1:60320992 |A   |chr1| 60320992 |rs116406626 |A | G|
        | chr2:18069070 |T   |chr2 |18069070 |rs763680312| T |C |
        | chr8:135908647 |A   |chr8| 135908647 |rs11992603 |A |G |

        >[!TIP|style:callout]
        > If you're new to regex, [Regex101](https://regex101.com/) is a highly recommended online tool for testing and debugging regular expressions. It offers detailed explanations of each component of your regex and tests your patterns against sample texts for easy understanding. Additionally, there are numerous [regex cheat sheet](https://cheatography.com/davechild/cheat-sheets/regular-expressions/) available online that provide a handy quick-start guide to familiarize yourself with the basics.
        </details>

#### `edit` Subsection:
This subsection specifies editing operations to be performed on certain columns.Each entry contains:
- `field`: The name of the column to edit.
- `rename`: Specifies the new name for the column.
- `find`: Specifies a pattern to find within the column.
- `replace`: Specifies a pattern to replace within the  column.
- `extract`: Specifies a pattern to extract from thcolumn.
    * <details>
      <summary>Find and replace example</summary>

      **Input**:
      | SNP | EA |chromosome|base_pair_locatiorsid |  effect_allele|other_allele |
      |-----|----|---------|-----------------------|-------------|------------|
      | chr11:88249377 |T   |chr11 |88249377    rs11020170 |     T | C  |
      | chr1:60320992 |A   |CHR1| 60320992    rs116406626 |    A | G|
      | chr2:18069070 |T   |chr2 |18069070    rs763680312|     T |C |
      | chr8:135908647 |A   |CHR8| 135908647     rs11992603 |    A |G |
      
      **JSON config**:
       ```json
      "field": "chromosome",
      "rename": "chromosome",
      "find": "chr|CHR",
      "replace": "",
      "extract": null
       ```
      
      **Output**:
      | SNP | EA |chromosome|base_pair_location| rsi  effect_allele| other_allele |
      |-----|---------|----|------------------|--------  ----|------|
      | chr11:88249377 |T   |11 |88249377| rs11020170 |     T | C  |
      | chr1:60320992 |A   |1| 60320992 |rs116406626|A |     G|
      | chr2:18069070 |T   |2 |18069070 |rs763680312 |T |    C |
      | chr8:135908647 |A   |8| 135908647 |rs11992603  A |    G |
      
      
      When utilizing the find and replace function, please note that it will modify values within the columns but  not within the headers. For instance, if you attemp  to replace `chr` in the column headers, the header `chromosome` will remain unchanged. Pleas use the `rename` function to change the header.

      >[!NOTE|style:callout]
      > Please use "find and replace" together. To remove      any character, enter `""` (an empty string) in the      replace field, rather than leaving it as `null`.      
      </details>

    
    * <details>
      <summary>Extract example</summary>
      
      **Input**:
      | chromosome| base_pair_location | rsid |effect_allele| other_allele |
      |-----------|--------------------|------|-------------|-------------|
      | 11| 88249377 | rs11020170_T_C  | T   | C|
      | 1 | 60320992 | rs116406626_A_G  | A   | G|
      | 2 | 18069070 | rs763680312_T_C  | T   | C|
      | 8 |135908647 | rs11992603_A_G  | A   | G|
      
      **JSON config**:
       ```json
      "field": "rsid",
      "rename": "variant_id",
      "find": null,
      "replace": null,
      "extract": "rs"
       ```
      
      **Output**:
       | chromosome| base_pair_location | variant_id |effect_allele|other_allele |
      |-----|-------|-------------|-------------|------|
      | 11| 88249377 | rs11020170 | T   | C|
      | 1| 60320992 | rs116406626  | A   | G|
      | 2| 18069070 | rs763680312 | T   | C|
      | 8|135908647 | rs11992603  | A   | G|
      
      </details>

## Additional Functions
Beyond formatting the input file according to the configuration file, the format tool also applies several default settings to every summary statistic:

1. Reorder the mandatory columns in your dataset to match the GWAS-SSF specified sequence: 
```text
chromosome, base_pair_location, effect_allele, other_allele, effect (beta/odds ratio/hazard ratio), standard_error, effect_allele_frequency, pval (or negativelog10Pvalue). 
```
Arrange any additional columns in their original input order.
2. Filling Missing Fields: If any mandatory column is missing from the input file, the format tool will automatically add this column and populate all its values with `#NA`.
3. Convert NA Values: The tool converts any 'NA' or 'None' values with `#NA`, ensuring data consistency.

----
Copyright © EMBL-EBI 2024 | EMBL-EBI is an Outstation of the [European Molecular Biology Laboratory](https://www.embl.org/) | [Terms of use](https://www.ebi.ac.uk/about/terms-of-use) | [Data Preservation Statement](https://www.ebi.ac.uk/long-term-data-preservation)

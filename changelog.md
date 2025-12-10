# Changelog

### 2.7.1 -> 3.0.0 [breaking]

#### General changes

- Introcuded a specific, limited character set for `Poseidon_ID`s and `Group_Name`s (in the .janno file, the .ssf file, and the genotype data): The ASCII characters `A-Za-z0-9_-.`.
- Allowed another genotype data format next to (binary) PLINK and EIGENSTRAT: the Variant Call Format (VCF).
- Specified a mechanism to store genotype data in a more space-efficient gzipped form.

#### Clarifications

- Clarified the exact meaning of a `Poseidon_ID` and the entity in genotype and context data it represents.
- Clarified the suitability of the Poseidon standard for non-human data: `[Poseidon] is geared towards human data, but is to a large extent species-agnostic and can be used to track archaeogenetic data also of non-human species.`
- Clarified that text files in Poseidon packages should use Unix-style line endings.

#### Changes to the `POSEIDON.yml` file

- Added the optional section `licence` with the fields `name` and `file` to specify a data licence for a package.
- Added two optional fields within the `genotypeData` structure:
  - `referenceGenomeAssembly`, the reference genome name of the reference genome used, e.g. GRCh37
  - `referenceGenomeAssemblyURL`, the reference assembly accession URL from a public database, such as NCBI or Ensembl
- Modified the definition of the `genoFile` and `snpFile` fields to cover the case of gzipped data, for which the respective file names must end with `*.gz`.

#### Changes to the `.janno` file

##### Replaced columns

- Replaced `Source_Tissue` with `Source_Material` and `Source_Material_Note`.

##### Added columns

- Added a column for the sampled `Species`, to make the schema more explicitly species-agnostic.
- Added a `Custodian_Institution` column that documents the institution that curated the sampled remains at the time of sampling, with name, city and country.
- Added four list columns to describe the cultural eras and archaeological cultures a sample is associated with: `Cultural_Era` + `Cultural_Era_URL` and `Archaeological_Culture` + `Archaeological_Culture_URL`.
- Added the columns `Chromosomal_Anomalies` and `Chromosomal_Anomalies_Note` for genetic anomalies on the chromosome level detected for the sample. This includes extra, missing or irregual portions of chromosomal DNA like in gonosomal and autosomal aneuploidies. `Chromosomal_Anomalies` is not limited to a specific set of options, but a common notation is recommended (e.g. `XXY`, `XYY`, `XXX`, `X0`, `Trisomy21`, `Trisomy18`).

##### Changed columns

- Introcuded a specific, limited character set for the `Poseidon_ID` and `Group_Name` column: The ASCII characters `A-Za-z0-9_-.`.
- Adjusted the definition of the `Group_Name` column. The role of population labels as general analysis labels was emphasised, and the original recommendation for the geographic-temporal nomenclature proposed by Eisenmann et al. 2018 toned down.
- Made the `Collection_ID` column a list column that allows multiple entries separated by `;`.
- Removed `ReferenceGenome` as an option for the `Capture_Type` column and further clarified its definition.
- Changed the scaling of the columns `Endogenous` and `Damage` from percent (0-100) to fractions (0-1).
- Allowed multiple values in the `Damage` column for estimates per library.
- Slightly adjusted the definitions of `MT_Haplogroup` and `Y_Haplogroup` to better account for non-human data.

##### Removed columns

- Removed all explicitly defined `_Note` columns. The schema allows arbitrary additional columns since v2.2.0; a specification of free-text fields is not necessary.

#### Changes to the `.ssf` file

##### Added columns

- Added a `submitted_md5` column, which records the md5sum of the file in the `submitted_ftp` column.

### 2.7.0 -> 2.7.1 [not breaking]

Only changes to the definition of the Sequencing Source File (`.ssf`):

- The `poseidon_IDs` column was made not mandatory.
- The `sample_accession` column was made not mandatory and the entries do not have to be unique any more within one package.
- The `secondary_sample_accession` also lost the uniqueness constraint.

Beyond that also some small adjustments to the variable definition/description of the `.ssf` columns `udg`, `library_built`, `library_name` and `run_accession`. The latter will probably be unique in most Poseidon packages, but duplicates are possible under rare circumstances.

### 2.6.0 -> 2.7.0 [not breaking]

- Added the Sequencing Source File (`.ssf`) to the Poseidon package definition.
- Added the column `Country_ISO` to the .janno file definition.
- Added the list column `Library_Names` to the .janno file definition.
- Replaced the option `other` by `mixed` in the `Library_Built` .janno column. Although this is technically a breaking change, we will not treat 2.7.0 as breaking. We assume this only affects few packages.

### 2.5.0 -> 2.6.0 [not breaking]

- Made the *contributor* field in the POSEIDON.yml file optional. We strongly recommend to keep this information in published packages, but for private packages or in computational pipelines it can be omitted now.
- Added the optional subfield *orcid* to the contributor field of the POSEIDON.yml file. A unique identifier for authors as provided by the [ORCID](https://info.orcid.org/what-is-orcid) is very valuable.
- Added new possibly entries for the *Capture_Type* field in the .janno file: `ArborComplete`, `ArborPrimePlus`, `ArborAncestralPlus`, `TwistAncientDNA`

### 2.4.0 -> 2.5.0 [breaking]

Only adds changes to the .janno file -- these are pretty significant, though. Please check [the documentation](janno_details.md) for details on how to use the new columns.

- Renamed multiple columns
  - *Individual_ID* -> *Poseidon_ID*
  - *No_of_Libraries* -> *Nr_Libraries*
  - *Data_Type* -> *Capture_Type*
  - *Nr_autosomal_SNPs* -> *Nr_SNPs*
  - *Publication_Status* -> *Publication*
  - *Coverage_1240K* -> *Coverage_on_Target_SNPs* (this change also implies a small semantic change in the meaning of this column)
- Added a new column to specify details about the absolute dating information
  - *Date_Note*
- Added a new set of columns to represent biological relationships among samples/individuals
  - *Alternative_IDs*
  - *Relation_To*
  - *Relation_Type*
  - *Relation_Degree*
  - *Relation_Note*
- Replaced the previous, pretty limited solution to document contamination estimates with a more flexible set of columns. That means the following columns were removed: *X_Contam*, *X_Contam_Stderr*, *MT_Contam*, *MT_Contam_Stderr*. Instead we added the following columns:
  - *Contamination*
  - *Contamination_Err*
  - *Contamination_Meas*
  - *Contamination_Note*
- Changed the column order to increase human readability

### 2.3.1 -> 2.4.0 [not breaking]

- Made the *snpSet* field introduced in 2.3.0 non-mandatory

### 2.3.0 -> 2.3.1 [breaking]

- Renamed *1240k* to *1240K* in all fields and column names

### 2.2.0 -> 2.3.0 [breaking]

- Defined the new, optional columns *Genetic_Source_Accession_IDs* and *Data_Preparation_Pipeline_URL* for the .janno file
- Added a mandatory field *snpSet* to the POSEIDON.yml file. It was later made optional in 2.4.0

### 2.1.0 -> 2.2.0 [not breaking]

- Relaxed the .janno file definition significantly: Instead of requiring a long list of variables, the standard now allows to omit any column except the mandatory *Individual_ID*, *Group_Name* and *Genetic_Sex*. The column order becomes irrelevant and arbitrary, additional variables can be added, as long as their column names do not clash with the set of pre-defined ones.
- The NULL value in .janno files can now be not just `n/a`, but alternatively also an empty string "".

### 2.0.1 -> 2.1.0 [not breaking]

- Added multiple optional fields to the POSEIDON.yml file. These include checksum fields for the genotype data as well as the .janno and .bib file. Also fields for paths to a README and a CHANGELOG file.
- Simplified and improved the standard definition document

### 2.0.0 -> 2.0.1 [breaking]

- UTF-8 encoding became mandatory for all files in a Poseidon package
- Made many implicit details about the fields in the POSEIDON.yml and the .janno file more explicit


# Poseidon v.2: DAG Genotype Data Organisation

Poseidon v.2 is a solution for genotype data organisation established within the Department of Archaeogenetics at the Max Planck Institute for the Science of Human History (MPI-SHH) in Jena. 

- [The Poseidon package](#the-poseidon-package)
    - [Structure](#structure)
    - [The `POSEIDON.yml` file](#the-poseidonyml-file-mandatory)
    - [The genotype data files](#the-genotype-data-files-mandatory)
    - [The `X.janno` file](#the-xjanno-file-mandatory)
    - [The `X.bib` file](#the-xbib-file-optional)
    - [The `README.txt` file](#the-readmetxt-file-optional)
    - [The `CHANGELOG.txt` file](#the-changelogtxt-file-optional)
- [Naming Poseidon packages](#naming-poseidon-packages)
    
***

## The Poseidon package

All ancient and modern data are distributed into so-called packages, which are directories containing a dedicated set of files. Packages correspond to published sets of genomes, or in case of unpublished projects, ongoing (and growing) sets of samples currently analysed. All text files in the package are UTF-8 encoded.

### Structure

Every package should have the following content: 

- A `POSEIDON.yml` file to formally define the package
- Genotype data in eigenstrat or plink format
- A `X.janno` file to store context information 
- A `X.bib` file for literature references

It can also contain the following files:

- A `README.txt` file for arbitrary context information
- A `CHANGELOG.txt` file to document changes to the package

Example:

```
Switzerland_LNBA_Roswita/POSEIDON.yml
Switzerland_LNBA_Roswita/Switzerland_LNBA.janno
Switzerland_LNBA_Roswita/Switzerland_LNBA.plink.bed
Switzerland_LNBA_Roswita/Switzerland_LNBA.plink.bim
Switzerland_LNBA_Roswita/Switzerland_LNBA.plink.fam
Switzerland_LNBA_Roswita/Switzerland_LNBA.bib
Switzerland_LNBA_Roswita/README.txt
Switzerland_LNBA_Roswita/CHANGELOG.txt
```

### The `POSEIDON.yml` file [mandatory]

The `POSEIDON.yml` file lists metainformation in a standardized, machine-readable format.

- It must be a valid [YAML file](https://yaml.org/).
- Its fields are documented in the [POSEIDON_yml_fields.tsv file](https://github.com/poseidon-framework/poseidon2-schema/blob/master/POSEIDON_yml_fields.tsv) in this repository.

Example:

```
poseidonVersion: 2.0.1
title: Schiffels_2016
description: Genetic data published in Schiffels et al. 2016
contributor:
  - name: Stephan Schiffels
    email: stephan.schiffels@institute.org
  - name: Paul Panther
    email: gemuese@test.com
packageVersion: 1.12
lastModified: 2020-02-28
bibFile: Schiffels_2016.bib
genotypeData:
  format: PLINK	
  genoFile: Schiffels_2016.bed	
  snpFile: Schiffels_2016.bim	
  indFile: Schiffels_2016.fam	
jannoFile : Schiffels_2016.janno
```

When a package is modified in any way (e.g. updates of the context information in the `.janno` file), then the `packageVersion` field should be incremented and the `lastModified` field updated to the current date.

### The genotype data files [mandatory]

The genotype data can be stored in the following formats, given that it is indicated correctly in the `POSEIDON.yml` file.

|          | EIGENSTRAT | PLINK |
|----------|------------|-------|
| genoFile | [`.geno` (genotype file)](https://github.com/argriffing/eigensoft/blob/890ef8f24b6cf0b68e9dd11608f9a058a95ff2cd/CONVERTF/README#L70)| [`.bed` (binary biallelic genotype table)](https://www.cog-genomics.org/plink/1.9/formats#bed)  |
| snpFile  | [`.snp` (snp file)](https://github.com/argriffing/eigensoft/blob/890ef8f24b6cf0b68e9dd11608f9a058a95ff2cd/CONVERTF/README#L70) | [`.bim` (extended MAP file)](https://www.cog-genomics.org/plink/1.9/formats#bim)  |
| indFile  | [`.ind` (indiv file)](https://github.com/argriffing/eigensoft/blob/890ef8f24b6cf0b68e9dd11608f9a058a95ff2cd/CONVERTF/README#L70) | [`.fam` (sample information)](https://www.cog-genomics.org/plink/1.9/formats#fam)  |

###  The `X.janno` file [mandatory]

The `.janno` file is a tab-separated text file with a header line. It holds a clearly defined set of context information (columns) for each sample (rows) in a package.

- The variables (columns), variable types and possible content of the janno file are documented in the [janno_columns.tsv file](https://github.com/poseidon-framework/poseidon2-schema/blob/master/janno_columns.tsv) in this repository.
- A `.janno` file must have all of these columns in exactly this order with exactly these column names. 
- If information is unknown or a variable does not apply for a certain sample, then the respective cell(s) can be filled with the NULL value `n/a`. Ideally, a `.janno` file should have the least number of n/a-values possible.
- The order of the samples (rows) in the `.janno` file must be equal to the order in the files that hold the genetic data.
- The values in the columns **Individual_ID** and **Group_Name** must be equal to the terms used in the first and second column of the `.fam` file.
- Multiple columns of the `.janno` file are list columns that hold multiple values (either strings or numerics) separated by `;`.
- The decimal separator for all floating point numbers is `.`.

### The `X.bib` file [optional]

[BibTeX](http://www.bibtex.org/) file with all references listed in `X.janno`.

### The `README.txt` file [optional]

Informal information accompanying the package.

### The `CHANGELOG.txt` file [optional]

Informal documentation of important changes in the history of a package.

***

## Naming Poseidon packages

The naming of packages should follow a simple scheme:

Ancient published: YEAR_NAME_IDENTIFIER

```
2018_Lamnidis_Fennoscandia  
2019_Wang_Caucasus  
2019_Flegontov_PaleoEskimo  
```

Ancient unpublished: IDENTIFIER_NAME

```
Switzerland_LNBA_Roswita  
Italy_Mesolithic_Paul  
SouthEastAsia_Simon  
```

Modern published: YEAR_(NAME)_IDENTIFIER

```
2015_1000_Genomes-1240K_haploid_pulldown
2016_Mallick_SGDP1240K_diploid_pulldown
2014_Lazaridis_HOmodern
2016_Lazaridis_HOmodern
2019_Flegontov_HO_NewSiberian
2018_Lipson_SEA
```

Modern unpublished: IDENTIFIER_NAME

```
Eurasia_newHO_Paul
Afrika_newHO_Andrea
```

Identifiers can be somewhat informal as long as the project is ongoing, they just need to be unique. As soon as a project gets published, we create a final version of the respective package with the YEAR_NAME_IDENTIFIER label.

External projects can be integrated similarly by using their publication name, or by temporary internal identifiers such as `Iron_Age_Boston_Share`.


# Poseidon v.2: DAG Genotype Data Organisation

Poseidon v.2 is a solution for genotype data organisation established within the Department of Archaeogenetics at the Max Planck Institute for the Science of Human History (MPI-SHH) in Jena. 

***

## The Poseidon v.2 `package`

All ancient and modern data are distributed into so-called packages, which are directories containing a dedicated set of files. Packages correspond to published sets of genomes, or in case of unpublished projects, ongoing (and growing) sets of samples currently analysed. All text files in the package are UTF-8 encoded.


### Structure

Every package should have the following files: 

- The `POSEIDON.yml` file
- The `X.janno` file
- The `X.bed`, `X.bim`, `X.fam` files

It also can contain the following files:

- The `README.txt` file
- The `CHANGELOG.txt` file
- The `LITERATURE.bib` file

Example:

```
Switzerland_LNBA_Roswita/POSEIDON.yml
Switzerland_LNBA_Roswita/Switzerland_LNBA.janno
Switzerland_LNBA_Roswita/Switzerland_LNBA.plink.bed
Switzerland_LNBA_Roswita/Switzerland_LNBA.plink.bim
Switzerland_LNBA_Roswita/Switzerland_LNBA.plink.fam
Switzerland_LNBA_Roswita/README.txt
Switzerland_LNBA_Roswita/CHANGELOG.txt
Switzerland_LNBA_Roswita/LITERATURE.bib
```

###  The `POSEIDON.yml` file [mandatory]

The `POSEIDON.yml` file lists metainformation in a standardized, machine-readable format.

- The `POSEIDON.yml` file must be a valid [YAML file](https://yaml.org/).
- The fields of the `POSEIDON.yml` file are documented in the [POSEIDON_yml_fields.tsv file](https://github.com/poseidon-framework/poseidon2-schema/blob/master/POSEIDON_yml_fields.tsv) in this repository.

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
lastModified: 2020-02-28
bibFile: LITERATURE.bib
genotypeData:	
  format: PLINK	
  genoFile: Schiffels_2016.bed	
  snpFile: Schiffels_2016.bim	
  indFile: Schiffels_2016.fam	
jannoFile : Schiffels_2016.janno
```

###  The `X.janno` file [mandatory]

The `.janno` file is a UTF-8 encoded, tab-separated text file with a header line. It holds a clearly defined set of context information (columns) for each sample (rows) in a package.

- The variables (columns), variable types and possible content of the janno file are documented in the [janno_columns.tsv file](https://github.com/poseidon-framework/poseidon2-schema/blob/master/janno_columns.tsv) in this repository.
- A `.janno` file must have all of these columns in exactly this order with exactly these column names. 
- If information is unknown or a variable does not apply for a certain sample, then the respective cell(s) can be filled with the NULL value `n/a`. Ideally, a `.janno` file should have the least number of n/a-values possible.
- The order of the samples (rows) in the `.janno` file must be equal to the order in the files that hold the genetic data.
- The values in the columns **Individual_ID** and **Group_Name** must be equal to the terms used in the first and second column of the `.fam` file.
- Multiple columns of the `.janno` file are list columns that hold multiple values (either strings or numerics) separated by `;`

### The `X.bed`, `X.bim`, `X.fam` files [mandatory]

Binary plink genotype files consisting of [`.bed` (PLINK binary biallelic genotype table)](https://www.cog-genomics.org/plink/1.9/formats#bed), [`.bim` (PLINK extended MAP file)](https://www.cog-genomics.org/plink/1.9/formats#bim) and [`.fam` (PLINK sample information)](https://www.cog-genomics.org/plink/1.9/formats#fam).

### The `README.txt` file [optional]

The README.txt file contains arbitrary, human-readable information.

Example:

```
This package contains a rather interesting set of samples. 
@Uebertruplf_2021 even claimed that they are the most important for this particular area and time period.
```

### The `CHANGELOG.txt` file [optional]

Documentation of important changes in the history of a package.

Example:

```
- 2021_10_01: Fixed a spelling mistake in the site name "Hosenacker"->"Rosenacker". 
- 2021_05_05: The authors of @Gassenhauer_2021 made some previously restricted samples for their publication available later and we added them.
- 2021_03_08: Creation of the package.
```

### The `LITERATURE.bib` file [optional]

Bibtex file with all references mentioned in `POSEIDON.yml`, `README.txt` and `CHANGELOG.txt`

***

## Naming Poseidon v.2 `package`s

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

***

## DAG internal procedures

Individual contributors would create packages in dedicated poseidon folders in their user project directories, e.g. `/project1/user/xyz/poseidon/2018_Lamnidis_Fennoscandia`. That way, subfolders belong to individual maintainers and be writable only by them. 

The poseidon admins would then link these packages into the official `/projects1/poseidon` repo, located on the HPC storage unit of the MPI-SHH, where we distinguish ancient and modern genotype data:

```
/projects1/poseidon/ancient/…  
/projects1/poseidon/modern/…
```

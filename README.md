# Poseidon v.2: DAG Genotype Data Organisation

Poseidon v.2 is a solution for genotype data organisation established within the Department of Archaeogenetics at the Max Planck Institute for the Science of Human History (MPI-SHH) in Jena. 

## The Poseidon v.2 `package`

All ancient and modern data are distributed into so-called packages, which are directories containing a dedicated set of files. Packages correspond to published sets of genomes, or in case of unpublished projects, ongoing (and growing) sets of samples currently analysed.

### Structure

Every package should have the following files: 

- The `POSEIDON.yml` file
- one or multiple data-subfolders with date name: YYYY_MM_DD, each with
  - The `X.janno` file
  - The `X.bed`, `X.bim`, `X.fam` files

It also can contain the following files:

- The `README.txt` file
- The `CHANGELOG.txt` file
- The `LITERATURE.bib` file

Example:

```
Switzerland_LNBA_Roswita/POSEIDON.yml
Switzerland_LNBA_Roswita/README.txt
Switzerland_LNBA_Roswita/CHANGELOG.txt
Switzerland_LNBA_Roswita/LITERATURE.bib
Switzerland_LNBA_Roswita/2019_03_20/
Switzerland_LNBA_Roswita/2019_05_15/  
...
Switzerland_LNBA_Roswita/2019_05_15/Switzerland_LNBA.janno
Switzerland_LNBA_Roswita/2019_05_15/Switzerland_LNBA.plink.bed
Switzerland_LNBA_Roswita/2019_05_15/Switzerland_LNBA.plink.bim
Switzerland_LNBA_Roswita/2019_05_15/Switzerland_LNBA.plink.fam
```

###  The `POSEIDON.yml` file [mandatory]

The POSEIDON.yml file lists metainformation in a standardized, machine-readable format.

Example:

```
poseidonVersion": v2.0.1
title: Schiffels_2016
description: Genetic data published in Schiffels et al. 2016
contributor:
  name: Stephan Schiffels
  email: stephan.schiffels@institute.org
lastModified: 2020-02-28
bibFile: sources.bib
```

### The `README.txt` file [optional]

The README.txt file contains arbitrary, human-readable information.

Example:

```
This package contains a rather interesting set of samples. 
@Gassenhauer_2011 even claimed that they are the most important for this particular area and time period.
```

### The `CHANGELOG.txt` file [optional]

Documentation of important differences between the data-subfolders.

Example:

```
2019_05_15
- The authors of @Gassenhauer_2019 made some previously restricted samples for their publication available now and we added them.
- The 2019_03_20 version also had a spelling mistake in the site name "Hosenacker"->"Rosenacker"

2019_03_20
- Initial, published version of this data as reported by @Gassenhauer_2019.
```

### The `LITERATURE.bib` file [optional]

Bibtex file with all references mentioned in `POSEIDON.yml`, `README.txt` and `CHANGELOG.txt`

###  The `X.janno` file [mandatory]

The .janno file is a tab-separated text file with a header line that holds a clearly defined set of metainformation (columns) for each sample (rows) in a package. 

The variables (columns), variable types and possible content of the janno file are documented in a google doc (ask the admins).

A .janno file must have all of these columns in exactly this order with exactly these column names. If information is unknown or a variable does not apply for a certain sample, then the respective cell(s) can be filled with the NULL value n/a. Ideally, a .janno file should have the least number of n/a-values possible.

The order of the samples (rows) in the .janno file must be equal to the order in the files that hold the core genetic data.

### The `X.bed`, `X.bim`, `X.fam` files [mandatory]

...

### Naming

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

### DAG internal procedures

Individual contributors would create packages in dedicated poseidon folders in their user project directories, e.g. `/project1/user/xyz/poseidon/2018_Lamnidis_Fennoscandia`. That way, subfolders belong to individual maintainers and be writable only by them. 

The poseidon admins would then link these packages into the official `/projects1/poseidon` repo, located on the HPC storage unit of the MPI-SHH, where we distinguish ancient and modern genotype data:

```
/projects1/poseidon/ancient/…  
/projects1/poseidon/modern/…
```

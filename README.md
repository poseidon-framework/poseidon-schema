# The Poseidon Standard

Poseidon is a solution for genotype data organisation established within the Department of Archaeogenetics at the Max Planck Institute for the Science of Human History (MPI-SHH) in Jena.

Detailed documentation for Poseidon can be found at [https://poseidon-framework.github.io](https://poseidon-framework.github.io)

A changelog is available [here](https://poseidon-framework.github.io/#/changelog).

## The Poseidon package structure

All ancient and modern data in Poseidon are distributed into so-called packages, which are directories containing a dedicated set of files. Packages correspond to published sets of genomes, or in case of unpublished projects, ongoing (and growing) sets of samples currently analysed. All text files in the package are UTF-8 encoded.

Every package should have the following files: 

- A `POSEIDON.yml` file to formally define the package
- Genotype data in eigenstrat or plink format
- A `.janno` file to store context information
- A `.bib` file for literature references

It can also contain the following files:

- A `README.txt` file for arbitrary context information
- A `CHANGELOG.txt` file to document changes to the package

Example:

```
Switzerland_LNBA_Roswita/POSEIDON.yml
Switzerland_LNBA_Roswita/Switzerland_LNBA.plink.bed
Switzerland_LNBA_Roswita/Switzerland_LNBA.plink.bim
Switzerland_LNBA_Roswita/Switzerland_LNBA.plink.fam
Switzerland_LNBA_Roswita/Switzerland_LNBA.janno
Switzerland_LNBA_Roswita/Switzerland_LNBA.bib
Switzerland_LNBA_Roswita/README.txt
Switzerland_LNBA_Roswita/CHANGELOG.txt
```

## The `POSEIDON.yml` file

The `POSEIDON.yml` file lists relative file paths and metainformation in a standardized, machine-readable format.

- It must be a valid [YAML file](https://yaml.org/).
- Its fields of the `POSEIDON.yml` file are documented in the [POSEIDON_yml_fields.tsv file](https://github.com/poseidon-framework/poseidon2-schema/blob/master/POSEIDON_yml_fields.tsv) in this repository.

Example:

```
poseidonVersion: 2.5.0
title: Switzerland_LNBA_Roswita
description: LNBA Switzerland genetic data not yet published # optional
contributor:
  - name: Roswita Malone
    email: roswita.malone@example.org
  - name: Paul Panther
    email: paul.panther@example.edu
packageVersion: 1.1.2
lastModified: 2021-01-28
genotypeData:	
  format: PLINK	
  genoFile: Switzerland_LNBA_Roswita.bed
  genoFileChkSum: 95b093eefacc1d6499afcfe89b15d56c # optional
  snpFile: Switzerland_LNBA_Roswita.bim
  snpFileChkSum: 6771d7c873219039ba3d5bdd96031ce3 # optional
  indFile: Switzerland_LNBA_Roswita.fam
  indFileChkSum: f77dc756666dbfef3bb35191ae15a167 # optional
  snpSet: 1240K
jannoFile : Switzerland_LNBA_Roswita.janno
jannoFileChkSum: 555d7733135ebcabd032d581381c5d6f # optional
bibFile: sources.bib
bibFileChkSum: 70cd3d5801cee8a93fc2eb40a99c63fa # optional
readmeFile: README.txt # optional
changelogFile: CHANGELOG.txt # optional
```

When a package is modified in any way (e.g. updates of the context information in the `.janno` file), then the `packageVersion` field should be incremented and the `lastModified` field updated to the current date.

## Genotype data

Genotype data in Poseidon packages is stored either in PLINK (binary) or EIGENSTRAT format.

|   | PLINK (binary) | EIGENSTRAT |
|---|---|---|
| genotype file | [`.bed` (binary biallelic genotype table)](https://www.cog-genomics.org/plink/1.9/formats#bed) | [`.geno` (genotype file)](https://github.com/DReichLab/EIG/blob/fb4fb59065055d3622e0f97f0149588eae630a3e/CONVERTF/README#L67)
| SNP file  | [`.bim` (extended MAP file)](https://www.cog-genomics.org/plink/1.9/formats#bim) | [`.snp` (snp file)](https://github.com/DReichLab/EIG/blob/fb4fb59065055d3622e0f97f0149588eae630a3e/CONVERTF/README#L67) |
| individual file  | [`.fam` (sample information)](https://www.cog-genomics.org/plink/1.9/formats#fam) | [`.ind` (indiv file)](https://github.com/DReichLab/EIG/blob/fb4fb59065055d3622e0f97f0149588eae630a3e/CONVERTF/README#L67) |

In addition to these files and their checksums, you also should provide a `snpSet` entry which determines the shape of the genotype file. Currently, only `1240K`, `HumanOrigins` or `Other` are allowed. While technically not a mandatory field, for backwards compatibility, we encourage users to set this field, and in fact our software also encourages this through required user input.

##  The `.janno` file

The `.janno` file is a tab-separated text file with a header line. It holds context information (variables/columns) for each sample (objects/rows) in a package.

- A set of strictly defined core variables (defined by column name) and their possible content are documented here: [janno_columns.tsv](https://github.com/poseidon-framework/poseidon2-schema/blob/master/janno_columns.tsv)
- A `.janno` file can have all of these core variables, or only a subset of them. 
- Only three columns are mandatory to make the file valid: **Poseidon_ID**, **Group_Name** and **Genetic_Sex**
- Arbitrary columns not defined here can be added as long as their column names do not clash with the defined ones.
- The column order is irrelevant.
- If information is unknown or a variable does not apply for a certain sample, then the respective cell(s) can be filled with the NULL value `n/a` or simply an empty string.
- The order of the samples (rows) in the `.janno` file must be equal to the order in the genetic data files (`.ind`, `.fam`).
- The values in the columns **Poseidon_ID**, **Group_Name** and **Genetic_Sex** must be equal to the terms used in the genetic data files (`.ind`, `.fam`).
- Multiple pre-defined columns of the `.janno` file are list columns that hold multiple values (either strings or numerics) separated by `;`.
- The decimal separator for all floating point numbers is `.`.

For a more extensive documenation of the columns and their interaction see [https://poseidon-framework.github.io/#/janno_details](https://poseidon-framework.github.io/#/janno_details).

## The `.bib` file

[BibTeX](http://www.bibtex.org/) file with all references listed in the `.janno` file. The bibtex keys must fit to ones used in the `.janno` file.

Example:

```
@article{CassidyPNAS2015,
    doi = {10.1073/pnas.1518445113},
    url = {https://doi.org/10.1073%2Fpnas.1518445113},
    year = 2015,
    month = {dec},
    publisher = {Proceedings of the National Academy of Sciences},
    volume = {113},
    number = {2},
    pages = {368--373},
    author = {Lara M. Cassidy and Rui Martiniano and Eileen M. Murphy and Matthew D. Teasdale and James Mallory and Barrie Hartwell and Daniel G. Bradley},
    title = {Neolithic and Bronze Age migration to Ireland and establishment of the insular Atlantic genome},
    journal = {Proceedings of the National Academy of Sciences}
}
```

## The `README.txt` file

Informal information accompanying the package.

Example:

```
This package contains a rather interesting set of samples relevant for the peopling of the Territory of Christmas Island in the Indian Ocean. We consider this especially relevant, because ...
```

## The `CHANGELOG.txt` file

Documentation of important changes in the history of a package.

Example:

```
V 1.2.0: Fixed a spelling mistake in the site name "Hosenacker"->"Rosenacker"
V 1.1.1: Added mtDNA contamination estimation to .janno file
V 1.1.0: The authors of @Gassenhauer_2021 made some previously restricted samples for their publication available later and we added them
V 1.0.0: Creation of the package
```

## The Sequencing Source file

Poseidon 2.7.0 added an option to specify sequencing source data. This is a tab-separated table, much like the Janno file, but following a different schema, specified in the file `sequencingSourceFile_columns.tsv`. Note that the primary entities in this table are Sequencing entities (typically corresponding to DNA libraries or even multiple runs/lanes of the same library). The link to the Individuals listed in the Janno-file are made through a foreign-key relationship into `Poseidon_ID`.

For the [ENA](https://www.ebi.ac.uk/ena/browser/home), we have a [convenience script](https://github.com/poseidon-framework/scripts/blob/main/get_ena_table.py) which helps downloading the table, except for the Poseidon_ID column which needs to be manually added.

Note that due to the heterogenous way users submit data to these archives, many columns in this table are less formalised than they could be. We generally advice simply using the above script and copy whatever data is in the archives into the respective columns.
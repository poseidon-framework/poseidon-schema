# The `.janno` file 

This documentation includes some more background about some of the columns in the `.janno` file beyond the general remarks [here](https://github.com/poseidon-framework/poseidon2-schema#the-xjanno-file-mandatory) and the overview table [here](https://github.com/poseidon-framework/poseidon2-schema/blob/master/janno_columns.tsv). This should make it more easy to compile the necessary information for both published and unpublished data.

# Spatial position

The `.janno` file contains five columns to describe the spatial origin of an individual sample:  `Country`, `Location`, `Site` and finally `Latitude` and `Longitude`. 

The `Country` column should contain a present-day political country name following the `English short name` in [ISO 3166](https://www.iso.org/iso-3166-country-codes.html). 

The `Location` column allows for free form text entry and can contain further, unspecified location information. This might be the name of an administrative or geographic region, or an arbitrary unit of reference like a mountain, lake or city close to the point of discory of the respective sample.

The `Site` column should contain a site name, ideally in the latin alphabet and ideally the name that is commonly used in publications.

The `Latitude` and `Longitude` column should contain geographic coordinates (WGS84) in decimal degrees (DD) with a precision of not more than five places after the decimal point. This yields a precision of about [1.1132m at the equator](https://en.wikipedia.org/wiki/Decimal_degrees) which is sufficient to describe the position of an archaeological site. Coordinates in other formats like for example Degrees Minutes Seconds (DMS) or in completely different coordinate reference systems should be transformed. There exist many Open Source software solutions to do that, most based on the [PROJ library](https://proj.org/index.html) e.g. the [The World Coordinate Converter](https://twcc.fr/en/#).

# Temporal position

The temporal position of a sample is encoded with seven different columns in the `.janno` file: 
`Date_C14_Labnr`, `Date_C14_Uncal_BP`, `Date_C14_Uncal_BP_Err`, `Date_BC_AD_Median`, `Date_BC_AD_Start`, `Date_BC_AD_Stop`, `Date_Type`

The `Date_Type` column handles the general distinction between the most common forms of dating: `C14`, `contextual` and `modern`. The entry `modern` is reserved for present day reference samples, so not ancient DNA. If the sample is directly (or very reliably indirectly) radiocarbon dated and the columns `Date_C14_Labnr`, `Date_C14_Uncal_BP` and `Date_C14_Uncal_BP_Err` can be filled, then `C14` applies. `contextual` covers everything else, including age attribution based on the archaeologically determined stratigraphy or typological information. The `contextual` value should also be chosen if the sample is only dated very indirectly (e.g. radiocarbon dates from other, unrelated features of the respective site) or dated with other physical or chemical dating methods (e.g. dendrochronology or optically stimulated luminescence).

If a sample is radiocarbon dated (`Date_Type = C14`), then the three columns `Date_C14_Labnr`, `Date_C14_Uncal_BP` and `Date_C14_Uncal_BP_Err` can be filled. Each of these can hold multiple values separated by `;` to allow for multiple radiocarbon dates for each aDNA sample. With multiple values the number and order of values in the columns should of course be equal.

Each radiocarbon date has a unique identifier: the Lab number. It consists of a [Lab Code](http://www.radiocarbon.org/Info/labcodes.html) issued by the journal [Radiocarbon](https://www.cambridge.org/core/journals/radiocarbon) for each laboratory and a serial number. This lab code makes the date well identifiable and should be reported in `Date_C14_Labnr` with the Lab code separated from the number with a minus symbol.



# Genetic summary data

# Context information


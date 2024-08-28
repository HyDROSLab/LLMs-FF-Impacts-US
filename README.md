[![DOI](https://zenodo.org/badge/848545347.svg)](https://zenodo.org/doi/10.5281/zenodo.13386241)

# Large Language Model-Based Classification of Flash Flood Impacts Across the United States  
by Jorge A. Duarte {1}, Jonathan J. Gourley {2,4}, Humberto J. Vergara {3}, Pierre E. Kirstetter {4,5}, Charles D. Nicholson {6}, Maciej Adamiak {7,8}
```
{1} Cooperative Institute for Severe and High-Impact Weather Research and Operations, Norman, OK, USA
{2} NOAA National Severe Storms Laboratory, Norman, OK, USA
{3} Department of Civil and Environmental Engineering, The University of Iowa, Iowa City, IA, USA
{4} School of Meteorology, The University of Oklahoma, Norman, OK, USA
{5} School of Civil Engineering \& Environmental Science, The University of Oklahoma, Norman, OK, USA
{6} School of Industrial \& Systems Engineering, The University of Oklahoma, Norman, OK, USA
{7} Institute of Urban Geography, Tourism Studies and Geoinformation, Faculty of Geographical Sciences, University of Lodz, Łódź, Poland
{8} HeiGIT gGmbH, an Affiliated Institute at Heidelberg Institute for Geoinformation Technology, Heidelberg University, Heidelberg, Germany
```

This repository contains the data sets used for the publication of the journal article titled _Large Language Model-Based Classification of Flash Flood Impacts Across the United States_.

Two distinct data sets are provided in `CSV` format, and are located within the `/data/` folder: 
- [expertly-classified_IBW_LSRs_GPT-FFSI_FLASH_Moments_663.csv](./data/expertly-classified_IBW_LSRs_GPT-FFSI_FLASH_Moments_663.csv)
  - This data set contains 663 expertly-classified flash flood Local Storm Reports, spanning a time period between May of 2018 to June of 2020
  - **Experts manually classified these reports** into Impact-Based Warning (IBW) categories (`base`, `considerable`, and `catastrophic`)
  - These reports were then matched to FLASH MaxUnitQ and MaxARI products. spatiotemporal values for these product were extracted, as well as for their intersections (MaxUnitQ values delimited by its corersponding MaxARI field, and MaxARI values delimited by its corresponding MaxUnitQ field)
  - The following statistical moments and values were calculated from these _matched_ spatiotemporal values:
    - Moments: `mean`, `variance`, `skewness`, `curtosis`
    - Values: `90th quantile`, `95th quantile`, `99th quantile`, `maximum`
  - A large language model (LLM, _GPT-3.5-turbo_) was used to probabilistically classify each report into Flash Flood Severity Index (FFSI) categories (`minor`, `moderate`, `serious`, `severe`, and `catastrophic`)
    - Additionally, an _FFSI score_ was calculated as a summary metric based on each report's FFSI class probabilities
  
- [historical_LSRs_GPT-FFSI_FLASH_Moments_22k.csv](./data/historical_LSRs_GPT-FFSI_FLASH_Moments_22k.csv)
  - This data set contains 22,341 historical flash flood Local Storm Reports, spanning a time period between April 2018 and June 2022
  - These reports **originally did NOT have any impact classification** associated with them
  - These reports were then matched to FLASH MaxUnitQ and MaxARI products. spatiotemporal values for these product were extracted, as well as for their intersections (MaxUnitQ values delimited by its corersponding MaxARI field, and MaxARI values delimited by its corresponding MaxUnitQ field)
  - The following statistical moments and values were calculated from these _matched_ spatiotemporal values:
    - Moments: `mean`, `variance`, `skewness`, `curtosis`
    - Values: `90th quantile`, `95th quantile`, `99th quantile`, `maximum`
  - A large language model (LLM, _GPT-3.5-turbo_) was used to probabilistically classify each report into Flash Flood Severity Index (FFSI) categories (`minor`, `moderate`, `serious`, `severe`, and `catastrophic`)
    - Additionally, an _FFSI score_ was calculated as a summary metric based on each report's FFSI class probabilities

## Expertly-Classified Local Storm Reports

The following table describes the column names and contents for the file [expertly-classified_IBW_LSRs_GPT-FFSI_FLASH_Moments_663.csv](./data/expertly-classified_IBW_LSRs_GPT-FFSI_FLASH_Moments_663.csv), which contains 663 expertly-classified Local Storm Reports.

| COLUMN_NAME                      | DESCRIPTION                                                                                                                       | DATA_TYPE |
|:---------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|:----------|
| time                             | UTC time for the event's report (format: "yyyy-mm-dd HH:MM:00")                                                                   | String    |
| office                           | Weather forecast office filing the event's report (e.g. "LIX") (format: "XYZ")                                                    | String    |
| local_time                       | Local time for the event's report (format: "yyyy-mm-dd HH:MM:00")                                                                 | String    |
| county                           | County name for the location of the event's report (e.g. "EAST BATON ROUGE")                                                      | String    |
| location                         | Name of the location for the event's report (e.g. city name, physical address, intersection)                                      | String    |
| state                            | State in which the event is being reported (e.g. "TX") (format: "XY")                                                             | String    |
| event_type                       | Type of event being reported (e.g. "FLASH FLOOD")                                                                                 | String    |
| magnitude                        | Impact-Based Warning (IBW) class manually assigned by experts to the reported event (e.g. "base", "considerable", "catastrophic") | String    |
| source                           | Source for the reported event (e.g. "TRAINED SPOTTER", "EMERGENCY MGR", etc.)                                                     | String    |
| lat                              | Latitude where the event is being reported                                                                                        | Float     |
| lon                              | Longitude where the event is being reported                                                                                       | Float     |
| remark                           | Natural language (plain text) remark attached to the event's report upon issuance                                                 | String    |
| category                         | Category of hazard being reported (BLANK FOR ALL INSTANCES)                                                                       | String    |
| MINOR                            | Event's probability for FFSI class minor provided by the LLM                                                                      | Float     |
| MODERATE                         | Event's probability for FFSI class moderate provided by the LLM                                                                   | Float     |
| SERIOUS                          | Event's probability for FFSI class serious provided by the LLM                                                                    | Float     |
| SEVERE                           | Event's probability for FFSI class severe provided by the LLM                                                                     | Float     |
| CATASTROPHIC                     | Event's probability for FFSI class catastrophic provided by the LLM                                                               | Float     |
| FFSI                             | Event's FFSI score calculated from its combined class probabilities                                                               | Float     |
| EXTRA                            | Additional output (if any) produced by the LLM                                                                                    | String    |
| CREST_MaxUnitQ_MEAN              | Mean for the event's CREST MaxUnitQ distribution extracted over time and space                                                    | Float     |
| CREST_MaxUnitQ_VAR               | Variance for the event's CREST MaxUnitQ distribution extracted over time and space                                                | Float     |
| CREST_MaxUnitQ_SKEW              | Skewness for the event's CREST MaxUnitQ distribution extracted over time and space                                                | Float     |
| CREST_MaxUnitQ_KURT              | Kurtosis for the event's CREST MaxUnitQ distribution extracted over time and space                                                | Float     |
| CREST_MaxUnitQ_Q90               | 90th quantile for the event's CREST MaxUnitQ distribution extracted over time and space                                           | Float     |
| CREST_MaxUnitQ_Q95               | 95th quantile for the event's CREST MaxUnitQ distribution extracted over time and space                                           | Float     |
| CREST_MaxUnitQ_Q99               | 99th quantile for the event's CREST MaxUnitQ distribution extracted over time and space                                           | Float     |
| CREST_MaxUnitQ_MAX               | Maximum for the event's CREST MaxUnitQ distribution extracted over time and space                                                 | Float     |
| CREST_MaxUnitQ_intersection_MEAN | Mean for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space                                         | Float     |
| CREST_MaxUnitQ_intersection_VAR  | Variance for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space                                     | Float     |
| CREST_MaxUnitQ_intersection_SKEW | Skewness for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space                                     | Float     |
| CREST_MaxUnitQ_intersection_KURT | Kurtosis for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space                                     | Float     |
| CREST_MaxUnitQ_intersection_Q90  | 9th quantile for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space                                 | Float     |
| CREST_MaxUnitQ_intersection_Q95  | 95th quantile for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space                                | Float     |
| CREST_MaxUnitQ_intersection_Q99  | 99th quantile for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space                                | Float     |
| CREST_MaxUnitQ_intersection_MAX  | Maximum for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space                                      | Float     |
| QPE_ARI_Max_MEAN                 | Mean for the event's CREST MaxARI distribution extracted over time and space                                                      | Float     |
| QPE_ARI_Max_VAR                  | Variance for the event's CREST MaxARI distribution extracted over time and space                                                  | Float     |
| QPE_ARI_Max_SKEW                 | Skewness for the event's CREST MaxARI distribution extracted over time and space                                                  | Float     |
| QPE_ARI_Max_KURT                 | Kurtosis for the event's CREST MaxARI distribution extracted over time and space                                                  | Float     |
| QPE_ARI_Max_Q90                  | 90th quantile for the event's CREST MaxARI distribution extracted over time and space                                             | Float     |
| QPE_ARI_Max_Q95                  | 95th quantile for the event's CREST MaxARI distribution extracted over time and space                                             | Float     |
| QPE_ARI_Max_Q99                  | 99th quantile for the event's CREST MaxARI distribution extracted over time and space                                             | Float     |
| QPE_ARI_Max_MAX                  | Maximum for the event's CREST MaxARI distribution extracted over time and space                                                   | Float     |
| QPE_ARI_Max_intersection_MEAN    | Mean for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space                                         | Float     |
| QPE_ARI_Max_intersection_VAR     | Variance for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space                                     | Float     |
| QPE_ARI_Max_intersection_SKEW    | Skewness for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space                                     | Float     |
| QPE_ARI_Max_intersection_KURT    | Kurtosis for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space                                     | Float     |
| QPE_ARI_Max_intersection_Q90     | 9th for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space                                          | Float     |
| QPE_ARI_Max_intersection_Q95     | 95th for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space                                         | Float     |
| QPE_ARI_Max_intersection_Q99     | 99th for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space                                         | Float     |
| QPE_ARI_Max_intersection_MAX     | Maximum for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space                                      | Float     |


## Historical Local Storm Reports

The following table describes the column names and contents for the file [historical_LSRs_GPT-FFSI_FLASH_Moments_22k.csv](./data/historical_LSRs_GPT-FFSI_FLASH_Moments_22k.csv), which contains 22,341 historical Local Storm Reports.

| COLUMN_NAME                      | DESCRIPTION                                                                                        | DATA_TYPE |
|:---------------------------------|:---------------------------------------------------------------------------------------------------|:----------|
| valid                            | UTC time for the event's report (format: "yyyymmddHHMM")                                           | String    |
| valid2                           | UTC time for the event's report (format: "yyyy/mm/dd HH:MM")                                       | String    |
| lat                              | Latitude where the event is being reported                                                         | Float     |
| lon                              | Longitude where the event is being reported                                                        | Float     |
| mag                              | Magnitude of hazard being reported ("None" FOR ALL INSTANCES)                                      | String    |
| wfo                              | Weather forecast office filing the event's report (e.g. "LIX") (format: "XYZ")                     | String    |
| typecode                         | Iowa Environmental Mesonet event type categorization code (e.g. "F")                               | String    |
| typetext                         | Iowa Environmental Mesonet event type categorization text (e.g. "FLASH FLOOD")                     | String    |
| city                             | Name of the location for the event's report (e.g. city name, physical address, intersection)       | String    |
| county                           | County name for the location of the event's report (e.g. "EAST BATON ROUGE")                       | String    |
| state                            | State in which the event is being reported (e.g. "TX") (format: "XY")                              | String    |
| source                           | Source for the reported event (e.g. "TRAINED SPOTTER", "EMERGENCY MGR", etc.)                      | String    |
| remark                           | Natural language (plain text) remark attached to the event's report upon issuance                  | String    |
| ugc                              | Iowa Environmental Mesonet computed NWS UGC code (6 character), sometimes null                     | String    |
| ugcname                          | Iowa Environmental Mesonet computed NWS UGC name (up to 128 character), sometimes null             | String    |
| category                         | Category of hazard being reported (BLANK FOR ALL INSTANCES)                                        | String    |
| MINOR                            | Event's probability for FFSI class minor provided by the LLM                                       | Float     |
| MODERATE                         | Event's probability for FFSI class moderate provided by the LLM                                    | Float     |
| SERIOUS                          | Event's probability for FFSI class serious provided by the LLM                                     | Float     |
| SEVERE                           | Event's probability for FFSI class severe provided by the LLM                                      | Float     |
| CATASTROPHIC                     | Event's probability for FFSI class catastrophic provided by the LLM                                | Float     |
| FFSI                             | Event's FFSI score calculated from its combined class probabilities                                | Float     |
| EXTRA                            | Additional output (if any) produced by the LLM                                                     | String    |
| CREST_MaxUnitQ_MEAN              | Mean for the event's CREST MaxUnitQ distribution extracted over time and space                     | Float     |
| CREST_MaxUnitQ_VAR               | Variance for the event's CREST MaxUnitQ distribution extracted over time and space                 | Float     |
| CREST_MaxUnitQ_SKEW              | Skewness for the event's CREST MaxUnitQ distribution extracted over time and space                 | Float     |
| CREST_MaxUnitQ_KURT              | Kurtosis for the event's CREST MaxUnitQ distribution extracted over time and space                 | Float     |
| CREST_MaxUnitQ_Q90               | 90th quantile for the event's CREST MaxUnitQ distribution extracted over time and space            | Float     |
| CREST_MaxUnitQ_Q95               | 95th quantile for the event's CREST MaxUnitQ distribution extracted over time and space            | Float     |
| CREST_MaxUnitQ_Q99               | 99th quantile for the event's CREST MaxUnitQ distribution extracted over time and space            | Float     |
| CREST_MaxUnitQ_MAX               | Maximum for the event's CREST MaxUnitQ distribution extracted over time and space                  | Float     |
| CREST_MaxUnitQ_intersection_MEAN | Mean for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space          | Float     |
| CREST_MaxUnitQ_intersection_VAR  | Variance for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space      | Float     |
| CREST_MaxUnitQ_intersection_SKEW | Skewness for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space      | Float     |
| CREST_MaxUnitQ_intersection_KURT | Kurtosis for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space      | Float     |
| CREST_MaxUnitQ_intersection_Q90  | 9th quantile for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space  | Float     |
| CREST_MaxUnitQ_intersection_Q95  | 95th quantile for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space | Float     |
| CREST_MaxUnitQ_intersection_Q99  | 99th quantile for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space | Float     |
| CREST_MaxUnitQ_intersection_MAX  | Maximum for the event's CREST (MaxUnitQ ∩ MaxARI) distribution extracted over time and space       | Float     |
| QPE_ARI_Max_MEAN                 | Mean for the event's CREST MaxARI distribution extracted over time and space                       | Float     |
| QPE_ARI_Max_VAR                  | Variance for the event's CREST MaxARI distribution extracted over time and space                   | Float     |
| QPE_ARI_Max_SKEW                 | Skewness for the event's CREST MaxARI distribution extracted over time and space                   | Float     |
| QPE_ARI_Max_KURT                 | Kurtosis for the event's CREST MaxARI distribution extracted over time and space                   | Float     |
| QPE_ARI_Max_Q90                  | 90th quantile for the event's CREST MaxARI distribution extracted over time and space              | Float     |
| QPE_ARI_Max_Q95                  | 95th quantile for the event's CREST MaxARI distribution extracted over time and space              | Float     |
| QPE_ARI_Max_Q99                  | 99th quantile for the event's CREST MaxARI distribution extracted over time and space              | Float     |
| QPE_ARI_Max_MAX                  | Maximum for the event's CREST MaxARI distribution extracted over time and space                    | Float     |
| QPE_ARI_Max_intersection_MEAN    | Mean for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space          | Float     |
| QPE_ARI_Max_intersection_VAR     | Variance for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space      | Float     |
| QPE_ARI_Max_intersection_SKEW    | Skewness for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space      | Float     |
| QPE_ARI_Max_intersection_KURT    | Kurtosis for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space      | Float     |
| QPE_ARI_Max_intersection_Q90     | 9th for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space           | Float     |
| QPE_ARI_Max_intersection_Q95     | 95th for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space          | Float     |
| QPE_ARI_Max_intersection_Q99     | 99th for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space          | Float     |
| QPE_ARI_Max_intersection_MAX     | Maximum for the event's CREST (MaxARI ∩ MaxUnitQ) distribution extracted over time and space       | Float     |

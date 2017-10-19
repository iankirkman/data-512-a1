# data-512-a1
Assignment 1 for DATA 512 (Human-Centered Data Science). See: https://wiki.communitydata.cc/HCDS_(Fall_2017)/Assignments#A1:_Data_curation

Released by: Ian Kirkman ikirkman@uw.edu 10/19/2017

## Project Goal
The goal of this assignment is to analyze traffic on English Wikipedia over time, and then document the process and the resulting dataset and visualization according to best practices for open research that were outlined in class.

## License Info
 - The raw data was accessed from the Wikimedia Foundation API, with [terms of use](https://wikimediafoundation.org/wiki/Terms_of_Use/en).
 - The content of this project directory is released under the [MIT license](LICENSE.md).

## Data Sources
All source data was pulled from the Wikimedia foundation API. 

The [legacy API](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts) was used for page views between January 2008 and July 2016. The legacy API includes webcrawlers, and began separating mobile and desktop traffic in October 2014.

The [current API](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews) was used for page views between July 2016 and September 2017. It allows for an exclusion of webcrawlers (which we utilize in our call), as well as mobile-app and mobile-web data (which are combined for our purposes).

Raw data is saved from each API call in the [DATA](DATA/) folder, with the naming convention: `apiname_accesstype_firstmonth-lastmonth.json`.

## Processing Steps
See the project [jupyter notebook](hcds-a1-data-curation.ipynb) for detailed processing steps.

## Output
The raw data is processed into a single [csv table](OUTPUT/en-wikipedia_traffic_200801-201709.csv) with the following fields:

| Column | Value |
| :--- | :--- |
| year | YYYY |
| month | MM |
| pagecount_all_views | num_views |
| pagecount_desktop_views | num_views |
| pagecount_mobile_views | num_views |
| pageview_all_views | num_views |
| pageview_desktop_views | num_views |
| pageview_mobile_views | num_views |

A [visualization](OUTPUT/output_image.png) is also created from the processed data, showing the page views for each of the API/access type combinations in every month between 1/08-9/17 in which data was reported for that API/access type combination. 


## Known Issues
There are a few differences between the legacy and current APIs, which we handled in the following manners:
 - The legacy API includes webcrawlers, whereas the current API allows them to be filtered out. Since it is ideal to filter them out, we did so with the Pageviews API. However, the Pagecounts API data will include crawlers.
 - The Pageviews API separates mobile-app and mobile-web access types. We combined them into a total mobile access type, which is comparable to the legacy API.
 - The date ranges covered for each API vary. Pagecounts provides data between 1/08-7/16, with mobile data separated from desktop starting in 10/14. Pageviews provides data between 7/16-9/17, with mobile data separated from desktop for the duration. We accommodated the different date ranges by using zero placeholders in the CSV for months that the source did not report data, and only plotted the non-zero ranges in our visualization.
 - Slight differences in schema and naming conventions are highlighted in the detailed steps of the jupyter notebook.

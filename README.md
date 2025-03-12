# Urban Heat Island
 Capstone Project for General Assembly DAB03
## Content:
- Background
- Problem Statement
- Data Extraction and Cleaning
- Feature Engineering
- Exploratory Data Analysis
- Data Modelling
- Key Insights and Recommendations
- References

## Background
The Urban Heat Island (UHI) effect is a phenomenon where built-up areas in highly urbanized regions tend to exhibit higher temperatures than the rural areas. This could be due to various factors such as reduced vegetation, high building density, and high population. The increased prevalence of UHI contributes to elevated energy consumption to escape the urban heat and adverse health effects such as higher risk of heat injury. UHI poses a challenge to sustainable urban development, and is an important aspect of global warming that should be studied.

In Singapore, UHI is prevalent in areas with high building density such as the Central Business District (comprising of the area between Raffles Place, Tanjong Pagar and Marina Bay) and surprisingly, despite its lower building density, Tai Seng.

## Problem Statement
Given that Singapore has rapidly urbanized since independence in 1965, we are more susceptible to the UHI effect. What are the factors that affect UHI intensity in Singapore, and what can be done to mitigate them?

## Data Extraction and Cleaning

![image](https://github.com/user-attachments/assets/758a83f5-3a28-4dce-9d8b-6b0e145a5cc7)

Meteorological data was collected from the [Meteorological Service Singapore](https://www.weather.gov.sg/climate-historical-daily/), which maintains a network of 62 weather stations throughout Singapore since 1980. Data collected at each station contains information such as the daily temperature (maximum, minimum, mean), rainfall (total, 30min-max, 60min-max, 120min-max), and wind speed (maximum, mean).

However, out of the 62 stations, not all of them have collected all the meteorological data, with some stations only collecting rainfall data. Most of the weather stations were only set up in 2009, thus there is only data from 2009 onwards or only collecting temperature data. With this in mind, we have selected 20 stations that contain the most data to use for the analysis.

![image](https://github.com/user-attachments/assets/fd713b5a-d1db-4ee9-bf6f-34f83989e1ba)

As the data collected from MSS does not have humidity data, the humidity data is pulled from NEA's API, found on [data.gov](https://api.data.gov.sg/v1/environment/relative-humidity). This API provides humidity readings from the 20 stations at every minute from 2016 to 2025. As we are not analysing data at that level of granularity for this project, we will be resampling the data to obtain the mean humidity for each day. 

Other data such as percentage of [forested area](https://tablebuilder.singstat.gov.sg/table/TS/M891231), [electrical consumption](https://tablebuilder.singstat.gov.sg/table/TS/M890841 ), [number of vehicles](https://tablebuilder.singstat.gov.sg/table/TS/M650271), [number of residential units](https://tablebuilder.singstat.gov.sg/table/TS/M400751), [total population](https://tablebuilder.singstat.gov.sg/table/TS/M810001), and [town population](https://www.singstat.gov.sg/find-data/search-by-theme/population/geographic-distribution/latest-data) were all pulled from Singapore Department of Statistics. 

## Feature Engineering

As we do not have a direct data on UHI intensity, the Pulau Ubin station is designated as the rural station, and temperatures from the other 19 weather stations will be compared against the tempearture readings from the Pulau Ubin Station. The difference between the two temperatures will be taken as the UHI intensity. 

Another factor that might affect UHI that is of interest will be the building density of an area. As there is no readily available data regarding building density, we extract the data from [URA Master Plan](https://www.ura.gov.sg/maps/index.html). The URA Master Plan shows the Gross Plot Ratio (GPR) of each building. GPR is the ratio of the gross floor area to total land area. Higher GPR indicates that the building is taller, and thus we use this data as a proxy for building density.

## Exploratory Data Analysis
![image](https://github.com/user-attachments/assets/64f6185c-fc37-4331-a338-72b08d4da00b)

As the CBD is located within the Central Region, one would expect that the UHI intensity within the Central Region would be the highest. However, the average UHI intensity in the East region was actually higher than that in the Central Region, especially past 2016.



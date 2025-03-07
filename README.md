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

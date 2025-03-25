# Urban Heat Island
 Capstone Project for General Assembly DAB03
## Content:
- [Background](https://github.com/delwyn-goh/Urban-Heat-Island?tab=readme-ov-file#background)
- [Problem Statement](https://github.com/delwyn-goh/Urban-Heat-Island/tree/main?tab=readme-ov-file#problem-statement)
- [Data Extraction and Cleaning](https://github.com/delwyn-goh/Urban-Heat-Island/tree/main?tab=readme-ov-file#data-extraction-and-cleaning)
- [Feature Engineering](https://github.com/delwyn-goh/Urban-Heat-Island/tree/main?tab=readme-ov-file#feature-engineering)
- [Exploratory Data Analysis](https://github.com/delwyn-goh/Urban-Heat-Island/tree/main?tab=readme-ov-file#exploratory-data-analysis)
- [Data Modelling](https://github.com/delwyn-goh/Urban-Heat-Island/tree/main?tab=readme-ov-file#exploratory-data-modelling)
- [Key Insights and Recommendations](https://github.com/delwyn-goh/Urban-Heat-Island/tree/main?tab=readme-ov-file#key-insights-and-recomendations)

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

The data were combined together into one csv file for the data modelling. As there were missing values for some dates in the meteorological data, they were imputed using KNN Imputer from the Scikit-learn package.


## Data Modelling

For this project, we are using three different type of Decision Tree models: Random Forest, XGBoost and LightGBM.


<img src="https://github.com/user-attachments/assets/d374c19b-e1d9-46e2-9982-2fdd84be72a8" width="640">


<ins>Decision Tree (Source: viso.ai)</ins>

In laymen terms, Decision Tree models follow a flowchart, with a question being asked at each step that is split into branches.


<img src = "https://github.com/user-attachments/assets/861e0aec-796b-4b09-b1cd-c5df1a91772a" width = "640">

<ins>Random Forest (Source: Spotfire)</ins>

Random Forest models build an ensemble of decision trees (hence the forest name), and they each decision tree is trained on a random subset of features and data. By averaging the output of all the trees, we are able to get  better performance when compared to decision tree models.

<img src = "https://github.com/user-attachments/assets/c27e8f43-762a-4d85-8994-28f1f7e8f992" width = "640">

<ins>XGBoost (Source: Medium)</ins>

XGBoost is a type of decision tree boosting model, where decision trees are built sequentially, and each new tree that is built corrects the error made by the previous trees. XGBoost performs level-wise tree growth, and we can end up with a large amount of leaves depending on the tree depth.

<img src = "https://github.com/user-attachments/assets/4cf35352-c5e0-4c07-8ea5-4bfc098c20f0" width = "640">

<ins> LightGBM (Source: Medium) </ins>

LightGBM is another form of of decision tree bossting similar to XGBoost, and tends to perform better and more efficiently for large datasets. The key difference from XGBoost is that LightGBM performs leaf-wise growth, where it expands upon the leaf with the highest performance improvement from the previous iteration.

### <ins>Modelling Results</ins>
![image](https://github.com/user-attachments/assets/c7d7c7ae-802e-4cf3-8c21-8c2977fbd442)

Out of all the models, the Random Forest model performed the best, with the highest R<sup>2</sup> values, lowest RMSE values and a fast runtime at approximately 12s. Comparatively, the XGBoost and LightGBM models have much lower R<sup>2</sup> values and higher RMSE values.

### <ins> Feature Importance </ins>
![image](https://github.com/user-attachments/assets/ad3f57b6-0421-45f8-baec-3569e6628e35)


## Key Insights and Recomendations

From the Random Forest model, we can see that humidity, town population, GPR (building density), wind speed and amount of forested area have a larger impact on UHI intensity. Of these features, humidity, town population and GPR have a positive impact (increase in feature results in increase in UHI) upon the UHI intensity, while wind speed and forested area have a negative impact on UHI intensity. Other features such as day and month also play a part on the UHI intensity, but that is out of our control. 

So how can we target these features to reduce UHI intensity? One possible way would be the introduction of wind corridors. By aligning the buildings along the prevailing wind direction, we can ensure that the wind is allowed to flow properly without any obstruction. This results in better airflow, which will increase the wind speed in that area.

We should also try to increase the amount of forested area in Singapore, as tree canopies help to provide shade that reduces surface temperatures and limits the evaporation. Plants in general also tend to absorb less heat when compared to concrete man-made structures.

However, given the limited land area available in Singapore, it may not be feasible for us to pursue increased forested area with the population and economic growth of Singapore. The next best alternative would be to introduce urban greenery. Some forms of urban greenery are roof gardens, green roofs and vertical gardens.

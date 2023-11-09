# DATA 512 - Project Part 1: Common Analysis
## Wildfires Analysis for Twin Falls, Idaho

### Goal

More and more frequently, summers in the western US have been characterized by wildfires with smoke billowing across multiple western states. There are many proposed causes for this: climate change, US Forestry policy, growing awareness, just to name a few. Regardless of the cause, the impact of wildland fires is widespread. There is a growing body of work pointing to the negative impacts of smoke on health, tourism, property, and other aspects of society.

The aim of this analysis is to study the wildland fires within 1250 miles of the city of Twin Falls, Idaho for the last 60 years (1963-2020). A smoke estimate is then created to estimate the wildfire smoke impact which is later modeled to make predictions for the next 30 years (until 2049). The end goal is to be able to inform policy makers, city managers, city councils, or other civic institutions, to make an informed plan for how they could or whether they should make plans to mitigate future impacts from wildfires.

### Datasets

The source dataset for this analysis is the [Combined Wildland Fire Datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81) dataset which was used to retrieve the historical data of wildfires. This dataset was collected and aggregated by the US Geological Survey, and is relatively well documented. Fire polygons in this dataset are available in ArcGIS and GeoJSON formats.

### API and Documentation:

Air Quality Data was needed to evaluate the performance of the smoke estimate created. This data was requested from the US Environmental Protection Agency (EPA) Air Quality Service (AQS) API. This is a historical API and does not provide real-time air quality data. The [documentation](https://aqs.epa.gov/aqsweb/documents/data_api.html) for the API provides definitions of the different call parameter and examples of the various calls that can be made to the API.

The US EPA was created in the early 1970's. The EPA reports that they only started broad based monitoring with standardized quality assurance procedures in the 1980's. Many counties will have data starting somewhere between 1983 and 1988. However, some counties still do not have any air quality monitoring stations. The API helps resolve this by providing calls to search for monitoring stations and data using either station ids, or a county designation or a geographic bounding box. Some [additional information on the Air Quality System can be found in the EPA FAQ](https://www.epa.gov/outdoor-air-quality-data/frequent-questions-about-airdata) on the system.

### Intermediate Data Files: 

In this study, three intermediate data files were generated. Two data files were generated in the first step - Data Retrieval. These are:
1. 'final_wildfire_data.json': This is the JSON file that has the data of 84319 wildfire instances that are within 1250 miles of Twin Falls, Idaho between the years 1963 and 2020.
2. 'Yearly_AQI_Data.csv': This CSV file contains the maximum AQI data for every fire season (May 1st to October 31st) on an yearly basis for Twin Falls, Idaho.

The third intermediate file was generated during the second step of the analysis - Data Preprocessing. This file is:
1. 'Wildlife_Data_Processed.csv': This CSV file contains the cleaned wildfires dataset. This dataset was created by removing irrelevant columns, filtering out overlapping wildfires, and ignoring circular fires of size greater than 1 acre from the 'final_wildfire_data.json' file. The final dataset had 72608 rows and 9 columns.

All these three intermediate data files have been stored in the [Results](https://github.com/TanushreeYandra/data-512-projectpart1/tree/main/Results) directory.

### Known Issues or Special Considerations with the Data:

It is important to note that both the datasets - Wildfires and AQI data have been created using multiple valid assumptions. The AQI data for instance was calculated for the ‘fire season’ every year which lasts from May 1st to October 31st. For every fire season, the maximum AQI was chosen as the AQI estimate for that year. Since this analysis was concerned about the potential extreme impacts of wildfires on air quality and how high pollution events correlate with smoke estimates, considering the maximum AQI for each year felt suitable.

### Results

Three visualizations were generated which have been stored in the [Results](https://github.com/TanushreeYandra/data-512-projectpart1/tree/main/Results) directory:
1. Histogram of the distribution of wildfires by their distance from Twin Falls, Idaho
2. Line graph of the total acres burned by wildfires every year
3. Time series graph containing the cumulative smoke estimate and the maximum AQI estimate for every year

### Research Implications:

This assignment was an eye-opener on the number of wildfires that have taken place in the US in the last 60 years. It also taught me to deal with a new type of data files - GeoJSON. Secondly, having a keen interest in sustainability, this project was really fun and insightful. It felt like detective work where one probes further and further into the data to understand why a certain phenomenon is taking place. The whole aspect of creating a smoke estimate from scratch, trying out different combinations of features, finding the best combination, evaluating it, and then finally modeling was tedious yet very exciting to work on. The modeling process especially was very difficult as I tried several models before arriving at the moving average model. This assignment thus taught me about the various models that can be used to model a data with a lot of peaks and dips when one has little to no predictors.

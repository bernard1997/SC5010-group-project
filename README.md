# A comprehensive study on the indicative factors of Diabetes Mellitus using machine learning
## Team 4

## About

This is a mini project for SC5010 (Introduction to Data Analysis) which focuses on how diabetes in different countries can be grouped together using machine learning and how their macroindicators can be used to classify the different diabetes trends observed across the countries. The notebook can be viewed in the following order: 
1) Timeseries analysis and clustering
2) Data cleaning for the macroindicators
3) Random forest modelling 

## Contributers
@ Lim Yi Yang - involved in the neural network (self organizing maps (SOM) for time series clustering and analysis of the different diabetes trend. 

@ Leong Say Hao - involved in data cleaning of the macroindicators and primary EDA analysis.

@ Koh Tiang Guan Bernard - involved in Random Tree modeling and insights derivation. 

## Problem definition
1) Is there any common pattern of the diabetes trend observed across the different countries? 
2) Could the macroindicators (which describes the state of a country's economy) be used to classify the diabetes trend? 

## Models used 
1) Self Organizing Maps (SOM). https://github.com/JustGlowing/minisom
2) Random forest modelling. 

## Description of the various notebooks
### Timeseries analysis and clustering
* From the time series dataframe, we used diabetes prevalence rate in 2010,2011,2015,2017,2019,2021 as an input into the Minisom algorithm. The diabetes prevalence rate was obtained from IDF (International Diabetes foundation) and World Bank. 
* MiniSom reduces the dimensionality of the input data into a 2D graph. Next, the algorithm clusters the trend of the diabetes prevalence rate.  
* From each cluster, the mean distance between the inputs was output as a 'red' line trend in the 2D graphs. 
* The countries' diabetes prevalence trend was clustered based on the shortest Euclidean distance from its closest nodes 
* For the hyper-parameters, we used a learning rate = 0.1, sigma = 0.3 and number of clusters = 6 as hyperparameters in the algorithm, followed by random weight initialisation and 50 000 training iterations

### Data cleaning for the macroindicators
* The average value from the list seen in the original macroindicator files were calculated from 2010 - 2021.

### Random Forest Modelling
* The macroindicators files that were cleaned in the previous notebook "Data cleaning for the macroindicators" were merged with the cluster file obtained after SOM was used to cluster the different diabetes trend among the countries 
* As some of the macroindicators were expressed in different formats (eg. expressed as percentage of GDP/ expressed as current currency), we choose one format to represent that particular macroindicator. The list of macroindicators used were the following: 
    1) Current account balance (Percent of GDP)
    2) General government net lending/borrowing (Percent of GDP)
    3) General government revenue (Percent of GDP)
    4) General government total expenditure (Percent of GDP)
    5) Gross domestic product per capita, current prices (U.S. dollars)
    6) Inflation, average consumer prices (Percent change)
    7) Population (Persons)
    8) Total investment (Percent of GDP)
    9) Gross national savings (Percent of GDP)
    10) Education Index
* After extracting the macroindicators, we did an EDA analysis. We found that some of the macroindicators such as GDP per capita and education index could be important features to predict the diabetes trend in a country due to dissimilar boxplots observed among the different diabetes clusters. Hence, we narrowed down our hypothesis and hypothesized that these indicators are crucial to predict the diabetes trend in a country. 
* Subsequently, using GridSearchCV package from skLearn, we found the best hyperparameters for our Random Forest model from our training dataset (depth = 9, no. of estimators = 500) and determined the feature importance of the chosen macroindicators. 

## Conclusions
* There were varying levels of diabetes around the world and we were able to cluster the different trends into 6 unique clusters. Countries in Africa had the lowest diabetes prevelance and experienced the lowest increase in diabetes prevelance. 
* Although HDI was a important macroindicator to classify the diabetes trends, we realised that it was a composite index made up of education index, GDP per capita, and life expectancy. 
* Better classfication accuracy obtained when we HDI index was broken down to its components. However, life expectancy was not included in our model nor in our test dataset as we realised that life expectancy was negatively affected by diabetes rather than the other way around. 
* At the end, GDP per capita, education index, and current account balance were the top 3 macroindicators that can be used to determine which diabetes trend countries belong to. 
* Our model also proved to be quite accurate in determining the different diabetes clusters (classification accuracy = 0.652), albeit some misclassification between cluster 3 and 5. 

## What was learn during the project? 
* Handling imbalanced datasets using SMOTE to upsample the minority classes
* Neural networks such as SOM
* Data extraction and data cleaning 
* GitHub posting 
* Interpreting results from Random Forest model and relating it to their univariate plots. 

## References
1) https://github.com/JustGlowing/minisom
2) https://diabetesatlas.org/data/en/
3) https://www.sciencedirect.com/science/article/pii/S0168822717303753
4) https://datahub.io/world-bank/sh.sta.diab.zs
5) https://ourworldindata.org/grapher/diabetes-prevalence
6) https://hdr.undp.org/en/data

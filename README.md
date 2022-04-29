# Chicago-Crime-Analysis
This project was completed as part of CIS 545- Big Data Analytics at University of Pennsylvania

## Introduction
Using the voluminous open source data available, we want to provide our readers insights on crime trends in the city of Chicago and identify hotspots where crimes are commonly witnessed, and make them aware of dangerous times of the day, dangerous days of the year etc. With this data, one can be made aware of the patterns certain crimes present beforehand and keep themselves safe. This can also be helpful in reinforcing security in vulnerable areas to protect residents or visitors and possibly stopping crime before it has occurred. 

Through this project we aim to analyze the trends of crimes in Chicago and visualize them to find out where and when they took place and what kind of a crime it was. We perform extensive exploratory data analysis and predictive analysis on the information about various crimes reported on a daily basis in the city and present a detailed study on crime trends in the city of Chicago.
We use PySpark to load and analyse the large amount of data for Exploratory Data Analysis, scikit learn for making predictive analysis and seaborne, Plotly, Folium and matplotlib for visualizations.

## Data Acquisition
The data was obtained from [Chicago Data Portal](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2).

The dataset reflects reported incidents of crime that occurred in the City of Chicago from 2001 to present, excluding the most recent seven days. (As of March 21 2022). The Data is extracted from the Chicago Police Department’s CLEAR (Citizen Law Enforcement Analysis and Reporting) system. The dataset has around 7.5M rows and 22 columns where each row represents a reported crime. Some significant columns of interest to us in the dataset are as follows :
- ID (Unique identifier for the record)
- Case Number (The Chicago Police Department Records Division Number which is unique to the incident).
- Date (when did the incident occurred)
- Block (where did the incident occurred)
- IUCR (The Illinois Uniform Crime Reporting code)
- Description (Primary description of the incident)
- Year
- Location
- Arrest (Whether or not an arrest related to the incident was made)

## Project Pipeline

### Data Wrangling and Pre-Processing
As part of Data Cleaning we drop irrelevant columns and handle missing values. All the features that have missing values are mostly the features that relate to geographical location (for example, X-coordinate, Y-coordinate, Latitude, Longitude, etc.) This is probably because the Chicago Crime dataset is mainly based on crimes reported by people involved in or around the crime scene. These reports don’t always contain the exact accurate location of the crime. The missing values in the whole dataset are present in the columns ‘Location Description’, ‘Ward’, ‘Community Area’, ‘X Coordinate’, ‘Y Coordinate’, ‘Updated On’, ‘Latitude’, ‘Longitude’ and ‘Location’. Since these features are not direct numeric values, we can’t use summary statistical functions to fill in the missing values. So after deciding which columns to keep we removed these values from the dataset. We also added a couple of columns like ‘Month’, ‘Day of the Week’, ‘Hour’, ‘Minute’ and ‘Second’ to the dataset to perform Exploratory Data Analysis.

### Exploratory Data Analysis and Visualization
The primary goal of performing EDA and visualization is to maximize the end-user’s insight into a data set and into the underlying structure of a dataset. We perform the following visualizations- 
1. The most prevalent crimes in Chicago over the last decade
2. Which year did Chicago witness a surge in the number of crimes?
3. What was the average percentage of arrests that were successful in the last 10 years? 
4. What are the successful arrest percentage statistics per year?
5. What are some locations around the city that can be identified as crime hotspots?
6. What are some common places where most of the crimes are committed?
7. Analysing the trends of Crime Occurrences by Hour of the Day, Week and Month

### Predictive Data Analysis
The Chicago Crime Dataset gives us information about the location (Latitude, Longitude, Block, Ward, etc) where the crime took place as well as information about time (Hour, Day, Month, Year) when the time took place. In our Exploratory Data Analysis, we found that certain crimes were more likely to occur at certain times and at certain places so in this section we try to analyse if this geographical and time data can be used to predict the type of crime that would occur. Due to lack of computational resources and time, we restricted our dataset to include data for crimes occurring after 2018.

We use 3 Machine Learning models — Random Forest, K-Nearest Neighbours and Decision Tree as well as a Voting Ensemble model for our analysis. We evaluated all our models on the basis of Accuracy Precision, Recall and F1 score. The results were as follows- 

Model | Accuracy | Precision | Recall | F1 Score | 
:---: | :---: | :---: | :---: |:---: |
Random Forest | 0.411 | 0.411 | 0.383 | 0.411 | 
K-Nearest Neighbors | 0.255 | 0.255 | 0.237 | 0.255 | 
Decision Tree | 0.295 | 0.295 | 0.298 | 0.295 | 
Voting Ensemble | 0.355 | 0.355 | 0.357 | 0.355 | 

All the models perform very badly on our dataset, the best model is Random Forest with achieves an F1 score of 0.411. This is probably because Location and time data alone is not enough for predicting the Primary Type of the crime. For the prediction task, the quality of predictions depends on the quality of data. Crime occurs because of social/economic factors as well and doesn’t depend only on the location and time of the incident. These aren’t captured in the dataset given and so the prediction is not very accurate as there is not enough correlation between crimes and data given. 


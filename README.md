# Predict Bike Sharing Demand with AutoGluon

# Bike-Sharing-Demand-Prediction
This project aims to enhance the mobility and convenience of the public through bike-sharing programs in metropolitan areas. One of the main challenges is maintaining a consistent supply of bikes for rental.

## Table of Content
  * [Problem Statement](#problem-statement)
  * [Dataset](#dataset)
  * [Dependencies](#dependencies)
  * [Installation](#installation)
  * [Data Pipeline](#data-pipeline)
  * [Project Structure](#project-structure)
  * [Report and Findings](#report-and-findings)
  * [Conclusion](#conclusion)


## Problem Statement
Many metropolitan areas now offer bike rentals to improve mobility and convenience. Ensuring timely access to rental bikes is critical to reducing wait times for the public, making a consistent supply of rental bikes a major concern. The expected hourly bicycle count is particularly crucial in this regard. We have to build a Regression model to predict the number of bikes required at any point of time.


## Dataset
The dataset is from Seoul's Bike Sharing Program. The data set includes over 8000 records and 14 attributes based on historical usage patterns, including temperature, time, and other data. For more information on the dataset, please visit the Kaggle website at [Kaggle Bike Sharing Demand Dataset](https://www.kaggle.com/competitions/bike-sharing-demand/data)


## Dependencies
```
Python 3.7
MXNet 1.8
Pandas >= 1.2.4
AutoGluon 0.2.0 
```

## Installation
For this project,I have used Sagemaker Studio provided by AWS workspace. This will simplify much of the installation needed to get started.

For local development, you will need to setup a jupyter lab instance.
* Follow the [jupyter install](https://jupyter.org/install.html) link for best practices to install and start a jupyter lab instance.
* If you have a python virtual environment already installed you can just `pip` install it.
```
pip install jupyterlab
```
* There are also docker containers containing jupyter lab from [Jupyter Docker Stacks](https://jupyter-docker-stacks.readthedocs.io/en/latest/index.html).

## Data Pipeline
  1. Analyze Data: 
      In this initial step, we attempted to comprehend the data and searched for various available features. We looked for things like the shape of the data, the 
      data types of each feature, a statistical summary, etc. at this stage.
  2. EDA: 
      EDA stands for Exploratory Data Analysis. It is a process of analyzing and understanding the data. The goal of EDA is to gain insights into the data, identify 
      patterns, and discover relationships and trends. It helps to identify outliers, missing values, and any other issues that may affect the analysis and modeling 
      of the data.
  3. Data Cleaning: 
      Data cleaning is the process of identifying and correcting or removing inaccuracies, inconsistencies, and missing values in a dataset. We inspected the dataset 
      for duplicate values. The null value and outlier detection and treatment followed. For  the outliers, we used the Clipping method to handle the outlier without 
      any loss to the data.
  4. Feature Engineering: 
      At this step, we did the encoding of categorical features. We used the correlation coefficient and VIF analysis to remove multi-colinearity and to 
      select the most relevant features. we used a square root transformation for the target variable as it transformed the variable into a well-distributed form.
  5. Model Training and Implementation:  
      We scaled the features to bring down all of the values to a similar range. We pass the features to 11 different regression models. We also did 
      hyperparameter tuning using GridSearchCV.
  6. Performance Evaluation: 
      After passing it to various regression models and calculating the metrics, we choose a final model that can make better predictions. We evaluated different 
      performance metrics but choose our final model using the r2 score and adj r2 score.
      
      
## Project Structure
```
├── README.md
├── Dataset 
│   ├── [SeoulBikeData.csv](https://github.com/Navneet2409/bike-sharing-demand-prediction/files/10743655/SeoulBikeData.csv)
├── Problem Statement
│
├── Know Yoour Data
│
├── Understanding Your Variables
│
├── EDA
│   ├── Numeric & Categorical features
│   ├── Univariate Analysis
│   ├── Bivariate and Multivariate Analysis
│
├── Data Cleaning
│   ├── Duplicated values
│   ├── Missing values
│   ├── Skewness
│   ├── Treating Outliers
│
├── Feature Engineering
│   ├── Regression Plot
|   ├── Correlation Coefficient and Heatmap
|   ├── VIF
│   ├── Encoding
|   ├── Normalization of Target Variable
│
├── Model Building
│   ├── Train Test Split
|   ├── Scaling Data
|   ├── Model Training
│
├── Model Implementation
|   ├── AutoGluon
│       ├── Linear Regression
|       ├── Lasso
|       ├── Ridge
│       ├── Elastic Net
|       ├── KNN
|       ├── SVM
|       ├── Decision Tree
|       ├── Random Forest
|       ├── AdaBoost
│       ├── XGBoost
|       ├── LightGBM
|       ├── Model Result
|
├── Report
├── Presentation
├── Result
└── Reference
```

## Report and Findings
* [Project Report](project_report.md)


## Conclusion
In this project, we tackled a regression problem in which we had to predict the bike sharing count  to match increasing popularity of bike rentals in metropolitan areas to enhance mobility and convenience for the public. It emphasizes the importance of providing timely access to rental bikes to reduce wait times for users, making a steady supply of rental bikes a key factor.

We began our analysis by performing EDA on all of our datasets. First, we looked at our dependent variable, "Rental Bike Count." After that, we looked at categorical variables and numerical variables and discovered their correlation, distribution, and connection to the dependent variable. Additionally, we hot-encoded the categorical variables and removed some numerical features which are used only for EDA purposes and have multi-collinearity.
Following that, we examine several well-known individual models, ranging from straightforward Linear Regression and Regularization Models (Ridge, Lasso, and Elastic Net) to more complex and ensemble models like Random Forest, Gradient Boost, and Light GBM. To enhance the performance of our model, we performed hyperparameter tuning.

1. The majority of rentals are for daily commutes to workplaces and colleges. While planning for extra bikes to stations the peak rental hours must be considered, i.e. 7–9 am and 5–6 pm.
2. We see 2 rental patterns across the day in bike rental count - first for a Working Day where the rental count is high at peak office hours (8 am and 5 pm) and the second for a Non-working day where the rental count is more or less uniform across the day with a peak at around noon.
3. Hour of the day: Bike rental count is mostly correlated with the time of the day. As indicated above, the count reaches a high point during peak hours on a working day and is mostly uniform during the day on a non-working day.
4. Temperature: People generally prefer to bike at moderate to high temperatures. We see the highest rental counts between 32 to 36 degrees Celcius
5. Season: We see the highest number of bike rentals in the Spring (July to September) and Summer (April to June) Seasons and the lowest in the Winter (January to March) season.
6. Weather: As one would expect, we see the highest number of bike rentals on a clear day and the lowest on a snowy or rainy day
7. Humidity: With increasing humidity, we see a decrease in the bike rental count.
8. I have chosen the Light GBM model which is above all else I want better expectations for the rented_bike_count and time isn't compelling here. As a result, various linear models, decision trees, Random Forests, and Gradient Boost techniques were used to improve accuracy. I compared R2 metrics to choose a model.
9. Due to less no. of data in the dataset, the training R2 score is around 99% and the test R2 score is 92.5%. Once we get more data we can retrain our algorithm for better performance.    

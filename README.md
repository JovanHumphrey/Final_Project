# Oregon Fire Analysis and Prediction (1992-2015)
## Backround
As data analysts we want to use our skills to help our local and global communities, so for this project we wanted to explore an issue regarding climate-change. As Oregonians the issue of wildfires is of recurring relevance to our lives. After decades of ever-more frequent wildfires Oregon saw its worst fire season in 2021. With average temperatures continuing to rise locally and around the globe, the situation shows no signs of slowing. We discovered a great dataset with which to explore this topic. This data is from Kaggle and includes an SQLite file and various CSV files containing data about 1.88 million US wildfires over 23 years.

Questions we hope to answer in the coming weeks:

• Have wildfires in Oregon increased in frequency?

• Have Oregon wildfires increased in size over time?

• Has Oregon wildfire season changed over time?

• Using machine-learning can we predict how wildfires may change in the next 5 years?

• Can we determine which areas of the State are of higher-risk?

## Plan
We will communicate primarily through Slack over the next few weeks, with check-ins on Saturdays and Sundays, as well as during class time. For the first segment Nina explored the raw data and cleaned it up for use. Alex explored possible machine learning options. Jovan created the repository and documented the process.

## Data Cleaning
After importing libraries and the SQLite file into Jupyter Notebook, and creating an engine to talk to the database we performed the following steps:

1. Inspected the names of the tables and printed the columns to see what data we have to work with.

2. Filtered the data to show only fire data from Oregon. This left us with 61,088 rows of data.

3. Determined what the data types in the columns are.

4. Created a dataframe of Oregon fires with only the columns relevant to our inquiry.

5. Checked the counts of the columns to see if any have missing data, then dropped those rows. This left us with 60,751 rows of data.

6. Explored the value counts of the column containing causes of fires in Oregon.

7. Explored the value counts of the column containing counties where fires are reported.

8. Converted Julian version of discover dates and containment dates into a readable format, and dropped the Julian versions from the dataframe.

9. Calculated the number of days each fire burned for.

## Machine Learning

Once the data has been cleaned, machine learning models can be run on some of the numerical data. 

Fires dataframe was merged with precipitation and temperature dataframes grouped by year and county. Final dataframe for ML included county code, year, average fire size, average discovery month, average containment month, average fire duration, average precipitation, and average temperature (832 rows × 6 columns).

Simple multiple linear regression and various tuned random forest regression models were tested. Also attempted was a time series VAR model, but it did not pass the Granger’s Causality Test. 

![final-db-ml](https://user-images.githubusercontent.com/10467547/171321862-92e6a640-5aff-478d-8819-8059a471898e.png)

![param-ml](https://user-images.githubusercontent.com/10467547/171323115-06e06a2d-89b7-4dec-a914-ddd0873e6c96.png)

### Multilinear Regression

Method:
1. Split into train and test sets. 
2. Run .LinearRegression()
3. Fit and test the model. 

Accuracy:
r2 =  -0.235

Conclusion: Not a good model. R2 score is negative, which is not good. 

### Random Forest Regression

Method: 
1. Split into train and test sets.
2. Scale the data (because we have very large values)
3. Run .RandomForestRegressor()
4. Fit and test the model.
5. Tune with GridSearchCV. {'criterion': 'mse',  'max_depth': 7,  'max_features': 'sqrt', 'n_estimators': 500}
6. Tune multiple times with RandomizedSearchCV. Final parameters: {'n_estimators': 415,  'min_samples_split': 2, 'min_samples_leaf': 2, 'max_features': 'sqrt', 'max_depth': None}

Accuracy:
No tuning: 21.86%, r2 = 0.193
GridSearchCV: 38.6%, r2 = 0.215
RandomSearchCV:  47.41 %, r2 = 0.258

![plots-compare-ml](https://user-images.githubusercontent.com/10467547/171323141-57c1032a-6d89-4d44-88fc-673d36fe3e95.png)


Conclusion: Not a good model. Accuracy and r2 scores are too low. 

### VAR Time Series

Method: 
1. Test causation using Granger’s causality test
2. Perform cointegration test
3. Split the series into training and testing data
4. Check for stationarity and make the time series stationary
5. Select the order (p) of VAR model
6. Train the VAR model of selected order (p)
7. Check for serial correlation of residuals (errors) using Durbin Watson statistic
8. Train the VAR model of selected order (p)
9. Invert the transformation to get the real forecast
10. Plot of forecast vs actuals
11. Evaluate the forecast

Accuracy:
Did not pass the Granger’s causality test.

Conclusion: Could not use this model because it did not pass the Granger's causality test. 

### Lessons and Future Improvements

To improve the random forest regression analysis, we should have encoded (dummy or simple) for the year and the county code to improve accuracy. Even so, these were not the best models and data to use.
What we were really after was a forecasting model that would help us predict fire outcomes into the future using a form of time series analysis, and the best data to use is geographic data (MODIS) paired with weather and vegetation data, using Google Earth Engine. MODIS data includes a product, Global Daily Fire Location Product, that would be best for this analysis. We thought VAR would be the best model to use in this instance, but actually the Autoregressive Integrated Moving Average model (ARIMA) would be best, which finds the best autoregression (AR) model and the moving average (MA) of weighted linear combination to obtain the prediction method. Global Fire Season Severity Analysis and Forecasting by  Ferreira et al. (2019) outlined their methods for accomplishing a fire prediction model, and future model building for Oregon could also use similar methods, including ARIMA. 

A future project could include a categorical analysis using neural networks that could predict final fire class size (A,B,C,D,E,F,or G) based on current parameters you entered, including current temperature, humidity, county, month of the year, acres burned already, and duration so far. MODIS data could also be incorporated. Unfortunately, we did not have the time to complete this model. 





## Database
We will be using postgresql running in AWS RDS.

Here is the ERD containing the graphical representation of table relationships:

![ERD](/Resources/ERD.png)


## Presentation
Our presentation will likely contain the following:

• Plot of fire frequency

• Plot of fire size

• Plot of fire season

• Plots of 2027 predictions

• Plot of high-risk areas

• The results of our machine learning tests

Link to presentation url: [Google Slides](https://docs.google.com/presentation/d/1HnTpr4Q7CoKs2C2mUdPNOzatUi6lzNOUqUnBa2203Vg/edit#slide=id.g11cc23ada21_0_0)

Link to Heroku app: [https://oregonfires.herokuapp.com/](https://oregonfires.herokuapp.com/)

Team: Alex Dallman, Jovan Humphrey, Nina Q

Sources: https://www.kaggle.com/datasets/rtatman/188-million-us-wildfires
         https://www.ncdc.noaa.gov/cag/county/mapping/35/pcp/200506/1/value.  
         https://data.oregon.gov/Natural-Resources/Oregon-counties-map/djry-8qn8

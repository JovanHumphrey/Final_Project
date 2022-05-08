# Oregon Fire Analysis and Prediction (1993-2017)
## Backround
As data analysts we want to use our skills to help our local and global communities, so for this project we wanted to explore an issue regarding climate-change. As Oregonians the issue of wildfires is of recurring relevance to our lives. After decades of ever-more frequent wildfires Oregon saw its worst fire season in 2021. With average temperatures continuing to rise locally and around the globe, the situation shows no signs of slowing. We discovered a great dataset with which to explore this topic. This data is from Kaggle and includes an SQLite file and various CSV files containing data about 1.88 million US wildfires over 25 years.

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



## Mockup Database
Our database will likely contain the following:

• Plot of fire frequency

• Plot of fire size

• Plot of fire season

• Plots of 2027 predictions

• Plot of high-risk areas

• The results of our machine learning tests

Team: Alex Dallman, Jovan Humphrey, Nina Q

Source: https://www.kaggle.com/datasets/rtatman/188-million-us-wildfires
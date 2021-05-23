# PyBer_Analysis

## Overview of Project 

### Purpose
The purpose of this analysis is to create a summary DataFrame of ride-sharing data by city type.\
City types are classified as Rural, Suburban, or Urban.\
A multiple-line graph was also created that shows the total weekly fares for each city type.

### Resources used
- Data Source : city_data.csv, ride_data.csv
- Software : Python 3.7.9, Jupyter Notebook 6.1.4, Pandas 1.1.3, Numpy 1.17.0, Anaconda 1.7.2

## Results
### Summary DataFrame of ride-sharing data:
The city_data and the ride_data files were read into jupyter notebook as DataFrames, using pandas.\
The city_data file contains information about the names of the cities, and the number of drivers each city has. Each city was further categorized as a type, either rural, suburban, or urban.\
The ride_data file contains information of the rides in each of the cities. It includes the ride_id, the date and the time that the ride was undertaken, and the fare charged for that particular ride.\
The two data frames were merged over the names of the cities. This allows the information of each ride, as well as the type category of the city, and the number of drivers they have to be available in one DataFrame. The figure below shows the first five entries from the merged DataFrame.

![merged_dataframe_rideshare](https://user-images.githubusercontent.com/71800628/119249670-10520f80-bb60-11eb-8dcd-574c783385ed.png)

Further analysis was done using this merged DataFrame.\
The total rides, total drivers, and the total amount of fares were extracted from the DataFrame. The average fare per ride, and per driver was calculated for each city type.\
The information was then assembled into a summary dataframe.\
(Image of the dataframe is in the Analysis section below.)

To create the map, first the fares were summed up for each date, and for each city type, as shown in the code snippet below.
```
# 2. Using groupby() to create a new DataFrame showing the sum of the fares 
#  for each date where the indices are the city type and date.
total_fare_per_date_df = pyber_data_df.groupby(["type", "date"]).sum()[["fare"]]
total_fare_per_date_df
```
\
The DataFrame was then re-arranged to get a better visualization, by setting the date as the index, and the columns as each city types, and the fares as values populating the DataFrame, as shown in the code snippet below.
```
# 4. Create a pivot table with the 'date' as the index, the columns ='type', and values='fare' 
# to get the total fares for each type of city by the date. 
fare_per_date_pivot_df = total_fare_per_date_df.pivot(index="date", columns="type", values="fare")
fare_per_date_pivot_df.head(10)
```
\
The re-arranged DataFrame was then filtered to contain data between the dates 1st January 2019 through 30th April 2019.

![rearranged_dataframe](https://user-images.githubusercontent.com/71800628/119249700-47282580-bb60-11eb-82f0-d3119e40770c.png)

Some of the values here were null because there were no ride-sharing in some dates (seen mostly for the rural cities). Therefore a new DataFrame was created from this one showing the fares for each week, instead of each date.

![pivot_weekly_dataframe](https://user-images.githubusercontent.com/71800628/119249708-54451480-bb60-11eb-9b5d-07e46e49684c.png)

The data from this DataFrame was then used to create the map, using matplotlib.pyplot, that showed the weekly fares for each city type. (Figure of plot in the Analysis section.)

## Analysis
The figure below shows the weekly fares for each city type from Jan.1st through Apr.30th 2019.

![chart](https://user-images.githubusercontent.com/71800628/119249718-63c45d80-bb60-11eb-96f5-305ba77d5d2b.png)

From the figure the following conclusions may be drawn,\
For the given timeline,
1. Urban cities earned the maximum number of fares (averaging close to a little over $2000), followed by suburban cities (averaging close to $1000). Rural cities earned the least (averaging close to $250).\
Therefore urban cities on average earned about twice more than suburban, and 8 times more than rural. Suburban cities earned about 4 times more than rural.
2. Towards the end of February, earnings peaked in all three city types. April too saw a rise in total fares in urban and rural cities. Urban cities furthurmore saw peaks in total fares in March where that the most earnings appeared to happen happened from mid-Feb. through mid-Apr.


From the ride-sharing summary DataFrame, the following conclusions may be drawn. 

![rideshare_summary](https://user-images.githubusercontent.com/71800628/119249731-82c2ef80-bb60-11eb-9f57-890318bdbf47.png)

1. Overall the total fares of the urban cities is almost twice that of the suburban cities, and almost 9 times more than the rural cities.
2. The total number of rides in the urban cities is 2.6 times more than the suburban cities, and 13 times more than the rural cities.
3. The total number of drivers in the urban cities is almost 5 times more than the suburban cities, and almost 31 times more than the rural cities.
4. The fares per driver, and per ride is the highest for rural, followed by suburban, and then urban cities. 
5. Drivers in rural cities are payed almost 1.4 times more than suburban, and 3.3 times more than urban city drivers.
6. Suburban drivers are payed 2.5 times more than urban city drivers.

We therefore note a trend that as the numbers of drivers in a city type increase, the average pay per driver decreases, the average fare per ride decreases, but the total fares increase.\
Urban cities earn almost 8 times more than rural cities by having 31 times more numbers of drivers, even though their drivers get payed 3.3 times less on average. 

## Summary
The following is recommended to address disparities among city types.
1. Rural and suburban cities are underserved compared to the urban cities.\
Incentivize the urban drivers to encourage them to serve the suburban and rural cities.

2. The total number of rides are markedly less in rural and suburban compared to urban cities.\
Adjust the fare per ride so that people living in the rural and suburban are encouraged to use pyber rideshare.

3. The chart shows fluctuations in urban areas over time.\
In order to flatten the curve, to meet demands while keeping revenue high, design a dynamic fare per ride depending upon the volume of service requests.

# PyBer Analysis Report

### Purpose
- PyBer is a virtual python-based ride-sharing app company valued at $2.3 billion and this analysis project is to 
perform an explanatory analysis on all the rideshare data from January to early May of 2019 with compelling visualizations. 
- The aims of this analysis is to get a snapshot of ride-sharing performance for different city type (Urban, Suburban and Rural), 
and to get idea about how to improve access of ride-sharing services and determine affordability for undeserved neighborhood.

### Techniques used
- Python with pandas, numpy and scipy.stats for ETL
- matplotlib.pyplot and FiveThirtyEight for visualization 
- jupyter notebook 

### Exploratory Analysis on ride share data 
#### 1) Ride sharing performance by city type
![Bubble Chart of ride sharing data](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/Fig1.png)
- The bubble chart showcases the average fare versus the total number of rides with bubble size based on the total number of drivers for each city type, including urban, suburban, and rural
- For the urban city type area there's more drivers and lower total fares which means ride-sharing is more available for the customers in urban city type than rural and suburban city type area.  

#### 2) Descriptive boxplots by city type
![Number of rides by city type](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/Fig2.png)
![Ride fare data by city type](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/Fig3.png)
![Drivers count data by city type](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/Fig4.png)
- Total number of rides and drivers are significantly higher in urban city type than other and the average ride fare is slightly higher in rural area. 

#### 3) Pie Charts of key indicators
![Percentage of total fares by city type](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/Fig5.png)
![Percentage of total rides by city type](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/Fig6.png)
![Percentage of total drivers by city type](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/Fig7.png)
- From the pie charts, 62% of the revenue generated from urban city type area with 68% of ride sharing traffics and 86% of drivers of the company.

### Technical Analysis

#### 1) Summary of Ride Sharing Performance by each City Type 
![SummaryDF](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/SummaryDF.PNG)
- The total rides of Urban area has almost 3 times more rides than Suburban and 10 times more rides than Rural area.
- The total fare of Urban city type is bigger than combined total fare of Suburban and Rural city type. 
- But the average fare per ride and aerage fare per driver is significantly higher in Rural city.
 
#### 2) Total Fare by each City Type
![Total_Fare_by_CityType](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/Total_Fare_by_CityType.png)
- The Urban city type and Suburban city type shows seasonal tendency in total fare data. 
- At the brginning of the January, it has lower total fares and gradually increse until March. At March total fares has a little spike and shows declining trend after. 

### Summary of Analysis
- From the revenue generating point of view Urban City type has most strategic importance and for the driver's policy it has more impact cause of number of total drivers. 
- For the customer in rural area with lower avg.fare per ride and higher number of drivers they have easier access to ride-sharing service than other areas. Also life style of urban city type leads to bigger number of total rides than other city type. 
- Since the avg.fare per ride and the avg.fare per driver is higher in rural area, for new drivers in rural city type has more potential growth if the company can promote more numbe of rides in rural city type.

### Techinques and challenges for analysis [Pyber_analysis_pyhon](https://github.com/Juuune/PyBer_Analysis/blob/master/PyBer.ipynb)
#### 1) Tranform data for analysis


#### 2) Create and merge dataframe 
There was some challenges with programming and it can be resolved with google search and slack flow search and etc.  
 - to drop index of summary dataframe 
 - to get weekly resample 
 - get dataframe pivot table 
 
 - To drop index of summary dataframe (*solution : summary_df.rename_axis(None, inplace=True) , from pandas document* )
 - To get weekly resample (*solution : sum_week_df = sum_new_df.resample('W').sum(), from pandas document* )
 - Get dataframe pivot table (*solution : sum_fares_df=sum_fares_df.pivot_table(), from slack flow search*)
 
#### 3) Key indicator calculation
 There was some challenges with caculating total driver since each row of resource data has total number of drivers for each city and single ride info at the smae time. so we can't use groupby() sum or mean directly. 
 - Columns of resource data : city,	date,	fare,	ride_id,	driver_count(total driver of that city),	type(city type)
 
 To Calculate the total drivers, firtst create another dataframe that contains number of drivers count and groupby city and city type. 
 - *city_drivers = pyber_data_df.groupby(["type","city"]).mean()["driver_count"]*
 - *city_drivers_df = pd.DataFrame(city_drivers)*
 
 Then you can get the total drivers count fot each city type with groupby function.
 - *total_drivers = city_drivers_df.groupby(["type"]).sum()["driver_count"]*
 
#### 4) Graphing, etc
Fisrt import the matplotlib.dates as mdates for easy use and for setting of x tick I used tick helpers - MonthLocator and DateFormatter.
- To change datetime format into montly data (*solution : ax.xaxis.set_major_formatter(mdates.DateFormatter("%b")), google search*)
- To set the range of xaxis with Monthlocator (*solution : months = mdates.MonthLocator(range(1, 5), interval=1), google search*)
- Setting x-axis (*solution : ax.xaxis.set_major_locator(months)*) 


## Recommendations and Next Steps

### Recommendations for Future Analysis

- From the PyBer ride sharing data analysis, Urban type city has most strategic focus and generates bigger revenue. but ride sharing performance in Urban city type shows low performance in January and Feburary. It seemd they need some marketing support on January and Feburary for better performance. 

- Even though the driver in Urban city type has benefit of large amount of rides the avg. fare per driver in Urban city type is significantly lower than other city types that means there's more short distance rides. If company can provide easy access or efficient way for next ride that will increase total rides for Urban drivers. 

- For further analysis we can look into datetime data and see if the time of the day has certain impact on riding performance and to see those difference among city type is statiscally significant. 

### Additional Analysis 1 - Ride sharing performance by Time 

- Analyze total rides and total fares by each time interval to see whether there's a difference in ride performance by time.

- Technical Steps 
 First Set the time interval from 00:00 to 24:00 by every 2 hour and give each interval a index number.
 Then create another column for time-interval and assign timeindex from datetime column data. (ignore the date info and only read time info from the columns).
 create a line plot with x- axis for time interval and y-axis for total rides and another plot with y-axis for total fares.

### Additional Analysis 2 - Statistical significance of difference

- Analyze how manay cities of each city type has PyBer ride sharing service and determine whether the differences we analyze before is significant. 

- Technical Steps
First calculate number of cities for each city types to get the smaple size.
perform t-test to get p-value for determin the those differences among city type are statistically significant.

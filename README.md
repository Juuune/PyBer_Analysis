# PyBer Analysis Report

## Background and Results

### Purpose

- PyBer is a virtual python-based ride-sharing app company valued at $2.3 billion and this analysis project is to 
perform an explanatory analysis on all the rideshare data from January to early May of 2019 with compelling visualizations. 
- The aims of this analysis is to get a snapshot of ride-sharing performance for different city type (Urban, Suburban and Rural), 
and to get idea about how to improve access of ride-sharing services and determine affordability for undeserved neighborhood

### Technical Analysis

#### 1) Summary of Ride Sharing Performance by each City Type 
![SummaryDF](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/SummaryDF.PNG)

- The total rides of Urban area has almost 3 times more rides than Suburban and 10 times more rides than Rural area and 
- the total total fare of Urban city type is bigger than combined total fare of Suburban and Rural city type. 
- But the average fare per ride and aerage fare per driver is significantly higher in Rural city.
 
#### 2) Total Fare by each City Type
![Total_Fare_by_CityType](https://github.com/Juuune/PyBer_Analysis/blob/master/analysis/Total_Fare_by_CityType.png)

- The Urban city type and Suburban city type shows seasonal tendency in total fare data. 
- At the brginning of the January, it has lower total fares and gradually increse until March. At March total fares has a little spike and shows declining trend after. 

### Summary
- From the revenue generating point of view Urban City type has most ddstrategic importance and for the driver's policy it has more impact cause of number of total drivers. 
- Since the avg.fare per ride and the avg.fare per driver is higher in Rural area it seemed new drivers in Rural city type has more potential growth than other city type.


## Challenges Encountered and Overcome

### Challenges and Difficulties Encountered and Technical Analyses Used

#### 1) Programming
There was some challenges with programming and it can be resolved with google search and slack flow search and etc.  
 - to drop index of summary dataframe 
 - to get weekly resample 
 - get dataframe pivot table 
 
#### 2) Data analysis
There was some challenges with caculating total driver since each row of resource data has total number of drivers for each city and single ride info at the smae time. so we can't use groupby() sum or mean directly. 
 - Columns of resource data : city,	date,	fare,	ride_id,	driver_count(total driver of that city),	type(city type)

#### 3) Graphing, etc
PyBer data has datetime format of yyyy-mm-dd tt:mm:ss (ex, 2019-01-01 09:45:36). To get the monthly x-axis we need to adjust the datetime data and x-axis format. 
 
### Technical Analyses Used

#### 1) Programming
 - To drop index of summary dataframe (*solution : summary_df.rename_axis(None, inplace=True) , from pandas document* )
 - To get weekly resample (*solution : sum_week_df = sum_new_df.resample('W').sum(), from pandas document* )
 - Get dataframe pivot table (*solution : sum_fares_df=sum_fares_df.pivot_table(), from slack flow search*)
 
#### 2) Data analysis
 To Calculate the total drivers, firtst create another dataframe that contains number of drivers count and groupby city and city type. 
 - *city_drivers = pyber_data_df.groupby(["type","city"]).mean()["driver_count"]*
 - *city_drivers_df = pd.DataFrame(city_drivers)*
 
 Then you can get the total drivers count fot each city type with groupby function 
 - *total_drivers = city_drivers_df.groupby(["type"]).sum()["driver_count"]*
 
#### 3) Graphing, etc
Fisrt import the matplotlib.dates as mdates for easy use and for setting of x tick I used tick helpers - MonthLocator and DateFormatter.
- To change datetime format into montly data (*solution : ax.xaxis.set_major_formatter(mdates.DateFormatter("%b")), google search*)
- To set the range of xaxis with Monthlocator (*solution : months = mdates.MonthLocator(range(1, 5), interval=1), google search*)
- Setting x-axis (*solution : ax.xaxis.set_major_locator(months)*) 
 
 
## Recommendations and Next Steps

### Recommendations for Future Analysis

- From the PyBer ride sharing data analysis, Urban type city has most strategic focus and generates bigger revenue. but ride sharing performance in Urban city type shows low performance in January and Feburary. It seemd they need some marketing support on January and Feburary for better performance. 

- Even though the driver in Urban city type has benefit of large amount of rides the avg. fare per driver in Urban city type is significantly lower than other city types that means there's more competition. 

- For further analysis we can look into datetime data and see if the time of the day has certain impact on riding performance and to see whether geographical location has impact on ride performance.  

### Additional Analysis 1 - Ride sharing performance by Time 

* Description of Approach

* Technical Steps

### Additional Analysis 2 - Ride sharing performance by Geographic area

* Description of Approach

* Technical Steps

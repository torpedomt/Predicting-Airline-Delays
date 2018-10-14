# Predicting-Airline-Delays(still working)
## Introduction

Flights can be delayed due to multiple factors such as weather, air control and so on. Even
though many of these factors have random occurrence patterns, being able to evaluate and
predict how these factors affect the delay rate is meaningful not only for passengers but also for
airline companies. With the increased volume of time series fight data, we begin by using
Python3 to understand, clean and transform the data. We will then explore and build models to
generalize and predict the delay patterns for future flight datasets.

## Data collection

Currently, the primary method for acquiring data for flights and weather is by API. Typically, to
access data via API, the ‘requests’ function is being utilized in Python 3. Python package
‘requests’ provides the ability for obtaining data from REST API and inputting data into Python
by JSON format for analyzing. In this project, the source of flight status and weather data is
acquired by ‘FlightAware API’ which provides comprehensive data attributes to analyze
relationship between delay rate and other factors.

During API data collection process, we inputted a local csv file that contains top 30 airports’
name into Python and passed the names of them as parameters; then we used ‘departed’ query
method to get departed information of those 30 airports. At this point, flight identity, the required
parameter in ‘Flightinfo’ query method, had already been included in collected dataset. By using
‘Flightinfo’ query method, we can generate the raw flight status dataset directly via ‘FlightAware
API’.
Moreover, the weather conditions of the top 30 airports are obtained by ‘Metar_Ex’ query
method. At first, we transformed the normal date format that we need into UNIX timestamp.

Then, by adjusting the ‘HowMany’ and ‘offset’ attributes in API request, we can require 24
different weather information for the specific airport per hour. The weather dataset contains
several aspects of weather such as cloud issues, air temperature, atmospheric pressure, visibility,
etc.

## Data Cleaning
Firstly, all the time data we obtained from ‘Flightaware API’ are in UNIX epoch time form,
which are seconds since 1970. Thus, we need to transform UNIX epoch time back into real time
form for future work. To perform this task, we use ‘ctime’ function in ‘time’ package in Python.

During cleaning time data, we also observe that two of our crucial parameters, actual arrival time
and actual departure time have some missing values. Thus, we choose to delete the rows that have missing actual
arrival or departure time.

Redundant data is another issue in the datasets we collected. And we tried to fix this problem by combining several attributes with similar information together.

## Files
Python Files :
    
    Collection Part:
        
        collect_departed.py
            This file helps collect the flights information based on the
	          top 30 airports in the U.S. from local csv file called 
            'airports.csv'.
	
         collect_flightinfo.py	
	          This file helps collect the flights information.

          weather.py
              This file helps collect the weather information.
    
    
    Cleaning Part (Python\Cleaning):
          clean.py
              This file has many functions that clean the results that we get from
              the python files in collection part.
Input Files: 
    
    airline_ICAO.csv
        This file contains the criteria that helps clean the flight series data 
        into correct formats
     
    airports.csv
        This file contains the top 30 airports in the U.S. and is used to passed
        as parameters in collect_departed.py to generate the raw outputs



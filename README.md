# Visualising Flight Delays Data

## Summary
In this project I visualised the data acquired from [Bureau of Transportation Statistics](http://www.transtats.bts.gov/OT_Delay/OT_DelayCause1.asp) under US department of Transportation. The final visualization focus on comparing the trend of arrival delays by year and month to provide viewer a clear understanding of the causes of flight delays.    

## Design

#### 1. Data Acquisition
The downloaded the original data file containing the information of flights delay and performance data from [Bureau of Transportation Statistics](http://www.transtats.bts.gov/OT_Delay/OT_DelayCause1.asp) website. The file size is 35.2 MB. And it includes the data during the period of Jan 2004 to Dec 2015. 

#### 2. Data Wrangling
The original data is quite clean. After exploring the original data and doing visualization I reorganized the data a few times to fit my need. The final data size is 37KB.

#### 3. Data Exploration
I used R studio to explore the data. There are 199135 entries and 22 fields including year, month, carrier, airport, arrival flight, delay flights, and delays by five different causes.  

There five delay causes are defined as ([source](http://www.rita.dot.gov/bts/help/aviation/html/understanding.html#q4)): 
- Air Carrier: The cause of the cancellation or delay was due to circumstances within the airline's control (e.g. maintenance or crew problems, aircraft cleaning, baggage loading, fueling, etc.).
- Extreme Weather: Significant meteorological conditions (actual or forecasted) that, in the judgment of the carrier, delays or prevents the operation of a flight such as tornado, blizzard or hurricane.
- National Aviation System (NAS): Delays and cancellations attributable to the national aviation system that refer to a broad set of conditions, such as non-extreme weather conditions, airport operations, heavy traffic volume, and air traffic control.
- Late-arriving aircraft: A previous flight with same aircraft arrived late, causing the present flight to depart late.
- Security: Delays or cancellations caused by evacuation of a terminal or concourse, re-boarding of aircraft because of security breach, inoperative screening equipment and/or long lines in excess of 29 minutes at screening areas.

After exploring, I decided to focus on the year to year and month to month trend of the flight delays and it causes. 

I fisrt reorganized the data with the number of delays grouped by year and month. And I output the data is in tsv format with the 9 fields: year, month, arrival flights, total delays, carrier delay, weather delay, nas delay, late aircraft delay, and security delay. Later I found out in order for the interaction to work, I need to have all the causes as levels in one field, therefore, I reshape and output the data again, this time only with 4 fields, year, month, cause, number.  

**Problem encountered:** 
The default tsv output in R include a quoted index column without field name, however, when d3 read in the data, it will treat it as the value for the first field. It took me a long time to figure out this is the reason for the strange charts I saw in the browser.  

In the end, I also added the total operations and total delay information into the data frame.

#### 4. Data Visualization

- What information to communicate?

I want to provide a comprehensive overview of flight on-time/ delay performance from 2004 to 2015. Users can freely explore the data including the data on total on-time flight, total delays, and delays divided by different causes. After exploring the data, the users can have a general understanding of the trend and the composition of the causes for delay.

I found out during the exploration phase that the overal numbers are more interesting patterns than the pencentage data (e.g. Total Flight Delay/Total Operations) over time.       

- How many charts?

Three charts that focus on two different aspects. The first chart describe the general trend of the  flight on-time/ delay performance over time. The other two charts focus on the the comparison of different delay causes.

- Which chart to use?

Line chart are good at showing the trend over time. Therefore I chose to use the line chart in two of the charts.
I also layered a scatter plot on one of the chart to prompt users to check the detailed information. 
In addition, I also want to show the proposition information as well as compare the total using stack bar chart.    


- Charts layout?

The charts are designed to have uniform width and placed in one row. Because it is intuitive for the people to scroll up and down and visually pleasing. 


- Interaction or Animation? 
I would like to give the viewers the chance to explore the data for themselves. Therefore, I chose to make my chart interactive. 
I also designed to use the same legend to control two related charts at the same time.  


## Interations and Feedbacks

> Version 1 (Static Charts)
Set the two charts position and selected the chart type. Successfully displayed one set of data. 
Issue: Cannot display multiple causes in one chart.  

> Version 2 (Static Charts)
- Solved the issue of displaying multiple delay cuases in one chart.
- Added legend and repositioned the charts. 

Issue: Need to change the legend name

> Version 3 (Interactive Charts)
- Added interaction to the charts. 

And I showed the charts to my friends and family.

> Version 4 (After feedback)
**Feedback:** People like playing with the charts. But in general they think it need more explanations. More specifically, my friend Sungwon want to see the year/month trend of the delay data. Mirosha thinks that without reading the small texts on the right it is hard to tell that you can interact with the graph. My dad thinks it is good to include the total arrival data.   

- Added a third line chart to show the year/month trend as suggested by my friend. 

- Reorganized the data to include the total operations as well as the total delays. 
*In the process of reorganizing data and I discovered that I was using the delay minutes counts instead of the operations. Fixed that issue as well.* 
*And after adding the data, I found the stacked chart no longer make sense. I considering different solution, I decided to filter the added information out for two charts that focus on the cause of the delay.* 

- Added definition of the delay causese and the instruction for interaction at the start of the page. 


> Version 5 (Final Version)

- Added short notes at the bottom of the charts. 

* During the final checking, I found the month data is not properly ordered, which have a big impact on the pattern.* 
- Fixed the month order problem.

## Resources

- http://www.r-statistics.com/tag/transpose/
- http://dimplejs.org/advanced_examples_viewer.html?id=advanced_interactive_legends
- https://github.com/PMSI-AlignAlytics/dimple/wiki/dimple.legend
- https://github.com/PMSI-AlignAlytics/dimple/wiki/dimple.series

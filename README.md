# bikesharing

## Project Overview
The client is preparing a pitch to promote the idea of a bike-sharing program in Des Moines, Iowa. In support of this, the client requests a presentation of an analysis of Citi Bike in New York City; the analysis of the Citi Bike data for a surveyed period of time is visualized with various charts and illustrations organized by Tableau into a dashboard and a story.

## Resources

### Data Sources

- `https://ride.citibikenyc.com/system-data` (The Citi Bike System Data page)
    - The Citi Bike Trip Histories section has a link to a bucket with all the trip data grouped by month. The `.zip` file for the surveyed period - August 2019 - has been included in this repository.

### Software

- Python 3.9.13
- Jupyter Notebook 6.4.12
- Pandas 1.4.4
- Tableau Public 2022.3

## Data Analysis and Visualization in Tableau
The data for August 2019 was selected because the year is believed to be recent enough and the month is believed to be peak traffic. One of the columns in the unzipped `.csv` file is the duration of the trip, and it is established as an integer containing the duration in seconds. A Jupyter Notebook file (also included in this repository) with Pandas loads this `.csv` file into a DataFrame, uses the Pandas Datetime conversion method to re-frame the trip duration column into the HH:MM:SS format, and then exports the results into a separate `.csv` file for use in Tableau. One quirk of this conversion is that the trip duration column now has "1970-01-01" in the timestamp; apparently, when converting to datetime, the time stamp is based on Epoch time - trip duration becomes hours, minutes, and seconds after the first day of 1970.

The "adjusted" `.csv` file is imported into Tableau to generate the necessary visuals for storytelling.

1. The first "worksheet" simply takes the count of data entries in the `.csv` file. The only product is a simple display of the total number of trips taken in the month of August 2019.

2. The second worksheet is a pie chart grouping the total number of trips by the user types: The single-ride and day pass customers and the annual membership subscribers.

3. The third worksheet is a horizontal bar chart grouping the total number of trips according to the hour of the starting timestamp.

4. The fourth worksheet is a map plotting out the coordinates of the starting points of all the trips in August 2019. Each point is sized and shaded according to how many trips started there.

5. The fifth worksheet is the same as the fourth except the coordinates reflect the ending points of the trips.

6. The sixth worksheet is a pie chart illustrating the distribution of riders by gender. To make the legend properly reflect the gender, a Calculated Field is created to convert the gender entry (0, 1, and 2) to their respective value ("UNKNOWN", "MALE", "FEMALE").

7. The seventh worksheet plots the average bike trip duration against the age of the rider by their birth year. After converting the trip duration column to the datetime type, the duration values used in this chart are derived from a Calculated Field that subtracts the start time from the stop time and converts the difference from days to seconds.

8. The eighth worksheet maps out how many trips each bike has taken in order to determine which ones are due for maintenance and repairs. This is done by plotting the number of trips against the bike ID number. After much planning and deliberation, the decision is to filter the bike ID numbers to show only the top fifty based on number of trips and to sort the results in descending order for better readability.

9. The ninth worksheet tracks bike utilization with a circle plot. Each circle represents a bike ID number and is sized based on the accumulated trip time. The trip time values are the ones taken from the Calculated Field used in the seventh worksheet. Colors to reflect the different trip time sums help to better illustrate which bikes have been ridden the longest.

10. The tenth worksheet is a line graph displaying the number of bikes checked out by duration for all users. The trip duration column is used twice, hours with minutes within. The hours are set to a filter which can be made available, and the first three values (0 hours, 1 hour, and 2 hours) are selected so only those three hour groups are shown.

11. The eleventh worksheet takes the tenth worksheet and adds gender with a filter included with all gender options selected. This line graph has three colored lines with each color corresponding to a gender option.

12. The twelfth worksheet is a heatmap with start time hours on the rows and stop time weekdays on the columns (the criteria are formatted for better readability). The count of records is set to `Colors` to provide the colors for the heatmap.

13. The thirteenth worksheet takes the twelfth worksheet and adds gender with a filter included with all gender options selected. There are now three heatmaps, one for each gender option.

14. The fourteenth worksheet is a heatmap with user type and start time weekday at the rows and gender at the columns. This heatmap shows the distribution of bike trips by gender and weekday in two different categories - the short-term customers and the long-term subscribers.

15. The fifteenth worksheet is a line graph displaying the number of bike users that month by age and gender for the customers and the subscribers. This is an extra visualization that further explores the distribution of age, gender, and user type.

16. The sixteenth worksheet is a bar chart showing the top fifty end stations according to how many bikes stop there. The bars also have the station ID numbers as a label in addition to the station name at the axis. This is an extra visualization that provides another perspective to the information shown in the fifth worksheet.

## Results
The resulting story is published on Tableau Public. The link to this Visualization is: https://public.tableau.com/app/profile/owen.wang/viz/NYCCitiBikeAnalysis_16714261301580/TheStoryofCitiBikeNYC

The story describes the state of Citi Bike in New York City within six story points, included in screenshots. The story is told in context of how Citi Bike is priced:

- https://citibikenyc.com/pricing
- https://citibikenyc.com/pricing/single-ride
- https://citibikenyc.com/pricing/day
- https://citibikenyc.com/pricing/annual

### Citi Bike is Popular in NYC
![Citi Bike is used nearly all over NYC](https://github.com/Owen-Wang1234/bikesharing/blob/main/Storypoint1.png)
The first story point shows that Citi Bike is used extensively in New York City. The month of August 2019 accumulated a total of 2,344,224 bike trips, with maps showing all the bike stations in the city and their popularity based on how many bike trips started or ended there. The chart at the bottom shows that people of (literally) all ages use the Citi Bike service.

### The Best Times for Citi Bike
![Citi Bike is great for commuters and weekenders](https://github.com/Owen-Wang1234/bikesharing/blob/main/Storypoint2.png)
The second story point shows that Citi Bike is great for people communiting between work and home as well as people just looking for a leisure trip. The peak hour ranges are between start of 8:00 AM and end of 9:00 AM and especially between start of 4:00 PM and end of 7:00 PM, where people are usually starting and/or ending their work shift. There is still a fair amount of bike usage in the middle of the day, though the heat map shows that this usually comes from weekend trips. The lull in the early mornings before sunrise and the late nights after sunset may prove useful when circulating bikes between active use and reserve for maintenance or repairs.

### The Demographics of Citi Bike
![Citi Bike has many subscribers](https://github.com/Owen-Wang1234/bikesharing/blob/main/Storypoint3.png)
The third story point breaks down the Citi Bike demographics by type and gender. The pie charts show that nearly 5/6 of all the bike trips in August 2019 were by annual subscribers, most likely local residents, and a quarter of the bike trips were by females with 2/3 by males (the remaining segment appears to not have gender information available). The heat maps reinforce this point, and implies that the "unknowns" are very likely weekenders who just took a single ride or a day pass from a kiosk (where demographics is likely not a required input).

### Drilling Deeper into Demographics
![Looking deeper into the demographics](https://github.com/Owen-Wang1234/bikesharing/blob/main/Storypoint4.png)
The fourth story point drills deeper into the demographics illustrated in the previous story point. The subscribers skew towards younger ages with the peak at birth year 1990 (age 29 at time of sampling). This visualization demonstrates a potential fault when asking users for demographic information; although some minimum age is implied (the maximum birth year is 2003 to correspond to the minimum age of 16), the user appears to be free to enter any birth year at will resulting in entries that date as far back as 1885.

One point of interest is the spike in the birth year 1969 (age 50). It is unknown if this is unique to August 2019 or if this is widespread in the entire Citi Bike database, but this implies that this value might be a stock filler value if the user does not supply a valid birth year (if at all). Interestingly, this only happens to the "unknown" category and is particularly prominent with non-subscribers, so customers may simply decline to provide any demographics when purchasing a single ride or day pass from a kiosk.

### How Long are Bikes Used?
![The bike trips are usually less than one hour](https://github.com/Owen-Wang1234/bikesharing/blob/main/Storypoint5.png)
The fifth story point looks at how long the bikes are used, in general and by gender. The peak is between five and six minutes, and a majority of bike trips do not exceed thirty minutes. However, some trips do go past an hour or two or even more, so that should be factored in when checking which bikes should be due for maintenance or repairs.

### Possible Logistics of Citi Bike
![How often, how long, and where](https://github.com/Owen-Wang1234/bikesharing/blob/main/Storypoint6.png)
The last story point examines the logistical side of Citi Bike. Since all bikes will need maintenance and repairs at some point in their lifetime, it is important to track how many trips a bike has taken, and how long that bike has been running. The data provided does not necessarily provide the complete picture (the bikes with the longest run time are not necessarily the bikes with the most trips), but some criteria can be put together to best estimate the threshold for pulling a bike for maintenance, repair, or even replacement. The bottom bar chart shows the top end stations identifying the name and ID and how many bike trips ended there; this helps determine which stations are popular and where extra attention may be placed.

## Summary
Based on the story, the conclusion is that Citi Bike can be a very popular service if Des Moines has enough parallels with New York City in demographics and city infrastructure. Citi Bike can be especially popular for tourists and locals living and staying in downtown, city centers, and universities where and vehicle ownership is difficult. Citi Bike can be most effective for quick commutes to destinations that are within biking distance, but this requires appropriate city infrastructure that can allow safe bike traffic with minimal risk when dealing with motor vehicles. Above all else, Citi Bike works only if the culture supports the venture.

However, viability of Citi Bike in Des Moines requires a deeper study and insight into the city culture, infrastructure, and demographics. One immediate imperative prior to further analysis is to clean up the data; there are presences of null values in station IDs, and decisions will need to be made as to what to do with birth year and gender entries that do not appear valid.

One future visualization that should be investigated is to chart out a map with start station IDs as the primary criterion (place in the `Pages` shelf) and end station coordinates on the axes. The count of trips will size and color the points on map to show which trips are the most popular. Adding the end station names and IDs to the `Tooltip` cards allows the user to identify the destinations by hovering the cursor over the points. This can help to form a general idea of the routes. Advanced geographical analysis can determine any trends on what is in each destination and what might bring people there (Tourism? Business? Residence? Etc.). An example screenshot is included as a concept.

![Concept map - destinations for starting points](https://github.com/Owen-Wang1234/bikesharing/blob/main/Concept1.png)

Another future visualization is a variation of the previous visualization; the chart replaces the start station IDs on the `Pages` shelf with the start time hours and exchanges the end station parameters for the start station parameters. The result allows the user to track the level of activity at the stations hour-by-hour to see how many trips start where at what time of the day. An example screenshot is included as a concept.

![Concept map - destinations for starting points](https://github.com/Owen-Wang1234/bikesharing/blob/main/Concept2.png)

This can be adjusted by changing the start time parameter between hour, day, or weekday to see how start station activity changes by the day of the month or day of the week. This comes in handy when the user wishes to try this with different months and years available on the Citi Bike data page.
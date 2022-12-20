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

15. The fifteenth worksheet is a line graph displaying the number of bike users that month by gender for the customers and the subscribers.

16. The sixteenth worksheet is a bar chart showing the top fifty end stations according to how many bikes stop there. The bars also have the station ID numbers as a label in addition to the station name at the axis.

## Results
The resulting story is published on Tableau Public. The link to this Visualization is: https://public.tableau.com/app/profile/owen.wang/viz/NYCCitiBikeAnalysis_16714261301580/TheStoryofCitiBikeNYC

The story describes the state of Citi Bike in New York City within six story points.

## Summary
Based on the story, the conclusion is:
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

## Results
The resulting story is published on Tableau Public. The link to this Visualization is:

## Summary
Based on the story, the conclusion is:
# Module 11: Data Collection
# data-collection-challenge

## Overview
----
In this challenge, the main objective was to use the Python libraries Splinter and Beautiful Soup, examine the provided websites' HTML code with Chrome DevTools, and parse and extract data from web pages. Part 1 was designed to scrape titles and article blurbs from a news site about Mars, while Part 2 scraped the Mars weather data website and used Pandas to analyze the data. Part 2 also includes data represented in charts.


## Part 1: Scrape Titles and Preview Text from Mars News
----
Variables Created:
| Variable Name | Description |
|---------|------|
| mars_soup | BeautifulSoup object |
| all_text | stores text found by using mars_soup |
| articles | list storing each dictionary with its Title and Preview pair |

The first steps toward scraping the website involved importing Splinter and BeautifulSoup from Python. Splinter enables the code to visit the website in a browser and gather/inspect the HTML code. BeautifulSoup allows the coder to dig through the HTML for tags and classes of elements, and extract the information needed.

After using Splinter and BeautifulSoup to visit and parse the website I created an empty list named "articles" to store dictionaries of the requested information (article titles and previews). I explored the webpage on my own using Chrome DevTools to search for the tags that would allow me to search for the article titles and previews. I found the class for all text on the website as "list_text", as well as the classes "content_title" and "article_teaser_body" to use in my code. 

Next I created a variable to hold all the plain text elements on the page, named "text_elements". I then created a for-loop to search through "text_elements", and defined variables to pull the titles and previews: "title" and "preview". The title and preview variables each use the .find().text function to search for their classes ("content_title" and "article_teaser_body", respectively). I created a dictionary ("article_dict") to store each "title" and "preview" pair, and used the .append() function to store each dictionary in the "articles" list.

Once I implemented the for-loop and ran it without errors, I printed the list to confirm that each article's dictionary had the correct information, then closed the browser.

## Part 2: Scrape and Analyze Mars Weather Data
----
| Variable Name | Description |
|---------|------|
| soup | BeautifulSoup object |
| weather_df | dataframe for Mars weather data taken from HTML |
| mars_weather | list to contain row information from weather_df |
| columns | list of columns from keys in the mars_weather list |
| mars_weather_df | dataframe created from the mars_weather list |
| avg_temp | average temps grouped by Martian Month |
| avg_temp_df | df created from avg_temp, used to create bar chart |
| coldest_month | stores min avg temp by Martian month |
| hottest_month | stores max avg temp by Martian month |
| coldest | finds the corresponding Martian month with min avg temp |
| hottest | finds the corresponding Martian month with max avg temp |
| avg_pressure | avg pressure grouped by Martian month |
| avg_pressure_df | df created from avg_pressure, used to create bar chart |

# Data Preparation
In this portion of the assignment I used Splinter and BeautifulSoup again to visit and read the HTML from the website, as well as explore the website with Chrome DevTools.

Once parsing was completed, the tags and classes for table elements were extracted:
    * header row: th
    * data row: tr, td, class = "data-row"
    
The instructions pointed to using BeautifulSoup to scrape the table information, but I could not get the code to work (original code is shown below and is still in the notebook for grading purposes, but it is commented out).

![Failed Beautiful Soup Code](Mars_Weather_Results/part_2_soup_fail.png?raw=true)

Instead I used Pandas to scrape the table information and arrange it into a dataframe (named weather_df) by coding pd.read_html(url)[0] where the [0] makes sure that the table is read as a table and not a list. This step allowed me to use weather_df in order to loop through its rows using .iterrows(), and storing each key and value pair in a JSON dictionary format. The keys were also remaned in this step to make the column names easier to understand. The dictionaries are stored in a list named mars_weather, which was then converted into the main dataframe mars_weather_df.

In the next step I prepared mars_weather_df for analysis. First I checked each column's data type with the .info() function and also confirmed that each cell was a non-null value. The only column that needed a different data type was the Terrestrial Date, which was converted to datetime by using pd.to_datetime().

# Data Analysis
1. The first question was how many months are on Mars, and I used mars_weather_df["Martian Month"].nunique() to find that there are 12 months on Mars in a Martian year.

2. Next was finding how many Martian days' worth of data were available, and mars_weather_df["Sol (Martian Days)"].nunique() found that there are 1867 Martian days' worth of data.

3. The next question involved average low temperatures by month. To accomplish this I first found the average temp for each month by using a .groupby() function combined with a .mean() function to calculate average low temp by month: avg_temp = mars_weather_df.groupby("Martian Month")["Min Temp Cel"].mean(). Then I converted avg_temp into its own df (avg_temp_df), renaming the Min Temp Cel column as Min Temp Avg, and used this df to create a bar chart for the average min temp for each Martian month. See figure below. This figure can also be found in the Mars_Weather_Results folder.

![Min Avg Temp by Martian Month](Mars_Weather_Results/min_avg_temp_by_month.png?raw=true)

As shown by the chart and verified by finding the min and max average temps, Martian Month 3 is the coldest month and Martian Month 8 is the hottest month.

4. The fourth question wanted us to find the average atmospheric pressure by Martian Month. First I found avg_pressure by mars_weather_df.groupby('Martian Month')['Pressure'].mean(), which stores the average pressure per month. Lastly I converted avg_pressure into a dataframe (avg_pressure_df) and used the df to create a bar chart showing the average pressure per month, shown below and also saved in the Mars_Weather_Results folder.

![Avg Pressure by Martian Month](Mars_Weather_Results/avg_pressure_by_month.png?raw=true)

Martian Month 9 had the highest average pressure.

5. 
* The data was analyzed to answer the following questions, and a data visualization was created to support each answer: (30 points)
    
    * Which month, on average, has the lowest atmospheric pressure? The highest? (10 points)
    * How many terrestrial days exist in a Martian year? A visual estimate within 25% was made. (10 points)
    
Using the Xpert Learning Assistant and the prompt "module 11 challenge "how many terrestrial (earth) days are there in a martian year?" hints", 
    
The DataFrame was exported into a CSV file. (5 points)


## Summary
----



## References
In this challenge, I referenced:
* Xpert Learning Assistant
* Module 11 activities
* Office hours
* Classmate questions/suggestions on Slack
* Stack Overflow, inserting images into Github markdown: https://stackoverflow.com/questions/13051428/how-to-display-images-in-markdown-files-on-github

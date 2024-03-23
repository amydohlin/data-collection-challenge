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

In this portion of the assignment I used Splinter and BeautifulSoup again to visit and read the HTML from the website, as well as explore the website with Chrome DevTools.

Once parsing was completed, the tags and classes for table elements were extracted:
    * header row: th
    * data row: tr, td, class = "data-row"
    
The instructions pointed to using BeautifulSoup to scrape the table information, but I could not get the code to work (original code is shown below and is still in the notebook for grading purposes, but it is commented out). Instead I used Pandas to scrape the table information and arrange it into a dataframe.
![](Mars_Weather_Results/part_2_soup_fail.png?raw=true)

issue with the min temp not showing up in table; took out the (C) in the column name and that fixed the problem, not sure why
    

* The HTML table was extracted into a Pandas DataFrame. Either Pandas or Splinter and Beautiful Soup were used to scrape the data. The columns have the correct headings and data types. (15 points)

* The data was analyzed to answer the following questions: (10 points)
    * How many months exist on Mars? (5 points)
    * How many Martian days' worth of data are there? (5 points)

* The data was analyzed to answer the following questions, and a data visualization was created to support each answer: (30 points)
    * Which month, on average, has the lowest temperature? The highest? (10 points)
    * Which month, on average, has the lowest atmospheric pressure? The highest? (10 points)
    * How many terrestrial days exist in a Martian year? A visual estimate within 25% was made. (10 points)
    
Using the Xpert Learning Assistant and the prompt "module 11 challenge "how many terrestrial (earth) days are there in a martian year?" hints", 
    
The DataFrame was exported into a CSV file. (5 points)


## Summary
----



## References
In this challenge, I referenced:
Xpert Learning Assistant
Module 11 activities
Office hours
Classmate questions and suggestions on Slack

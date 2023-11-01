# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The dataset primarily involved generating unique IDs based on the city and country of the visitor. These IDs are then associated with the products viewed by these visitors. The goal of this analysis was to extract meaningful insights and answer specific questions pertaining to this dataset.

## Process
Step 1: Data Exploration and Preparation: The initial phase of the project involved accessing and preparing the dataset. I imported data from five excel sheets and initiated data cleaning procedures. The importing process was challenging as the numerous columns had specific data-types that needed to be matched.
For the cleaning process, I identified and removed columns such as productRefundAmount, productQuantity, productRevenue, itemQuantity, itemRevenue, transactionRevenue, searchKeyword, and userId that contained null values, streamlining the dataset for analysis.

Step 2: Data Analysis and Transformation: The second phase of the project involved on eyeballing the data through the process of SELECT * FROM my_table. This query helped a lot on analyzing the values went missing and values I should be looking at to start answering questions and also making up the questions.

## Results
During this analysis, I have used queries to answer the following questions to gain valuable insight:

Which cities and countries have the highest level of transaction revenues on the site?

I identified the cities and countries with the highest transaction revenues on the website. This shows the most economically active regions and can guide strategic decisions.

What is the average number of products ordered from visitors in each city and country?

Our analysis provided the average number of products ordered by visitors from different cities and countries. This information is essential in understanding user behavior and preferences in various regions.

Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?

I explored the data to identify patterns in the types of products ordered by visitors from different cities and countries. This analysis revealed whether specific product categories were more popular in certain regions.

## Challenges 
While conducting this analysis, I encountered some notable challenges. One of the key hurdles was dealing with columns containing null values, which required careful consideration and management. At first, I tried deleting the columns that contained the Null values, however, that would result in deleting the whole row as well which contained valuable data.
Additionally, when creating the tables, it was hard to match the data-type for which the original excel tables contained. 

## Future Goals
If I had more time and resources, I would consider doing a more meaningful analysis on the correlation of pagepathlevels depending on which city and country access on which product page.



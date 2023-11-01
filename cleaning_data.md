What issues will you address by cleaning the data?


Dropped columns that have no data.
Number standardization by dividing certain columns with 10,000 to make decise values.
Replacement of NULL values into 0 in certain columns. 
Make new column for date to change data-type and date format.

More detailed analysis on tables and columns in the following link:
https://docs.google.com/document/d/1h-_69UhmaawlN82t0feKq0sk1SgZx02NAvGZdfzOCg4/edit?usp=sharing

Queries:
Below, provide the SQL queries you used to clean your data.


For all_sessions table:

fullvisitorid column

        SELECT fullvisitorid
        FROM all_sessions1
        WHERE fullvisitorid IS NULL

        no null values

        SELECT DISTINCT(fullvisitorid)
        FROM all_sessions1

        14223/15134 = 93.98 % of data with unique values 


ChannelGrouping column

        SELECT channelgrouping
        FROM all_sessions1
        WHERE channelgrouping IS NULL

        no null values

        SELECT DISTINCT(channelgrouping)
        FROM all_sessions1


        7 data are unique values: 
        "Organic Search"
        "Display"
        "Referral"
        "Affiliates"
        "Paid Search"
        "Direct"
        "(Other)"

TIME column

        SELECT time
        FROM all_sessions1
        WHERE time IS NULL

        No null values 

COUNTRY column 

        SELECT country
        FROM all_sessions1
        WHERE country IS NULL

        no null values 

        SELECT DISTINCT(country)
        FROM all_sessions1

        136 different countries

        SELECT country
        FROM all_sessions1
        WHERE country IN ('(not set)')

CITY column

        SELECT city
        FROM all_sessions1
        WHERE city IN ('(not set)', 'not available in demo dataset')

        SELECT *
        FROM all_sessions
        WHERE city IS NULL 
        -> no null values

        SELECT DISTINCT(city)
        FROM all_sessions1

        266 distinct values 

        SELECT *
        FROM all_sessions
        WHERE city LIKE 'not available in demo dataset'
        DELETE FROM all_sessions
        WHERE city = 'not available in demo dataset';

        SELECT *
        FROM all_sessions
        WHERE city LIKE '(not set)'
        DELETE FROM all_sessions
        WHERE city = '(not set)';

        -> deletion of irelevant data

totalTransactionRevenue Column

        SELECT totalTransactionRevenue
        FROM all_sessions
        WHERE totalTransactionRevenue IS NOT NULL

        transactions

        SELECT transactions
        FROM all_sessions
        WHERE transactions IS NOT NULL

        If we were to use the existing 81 rows of totalTransactionRevenue and transactions for calculating the transactions 
        among city or country, we will get a biased outcome because of such small number of datasets

timeOnSite column

        SELECT timeOnSite
        FROM all_sessions
        WHERE timeOnSite IS NOT NULL

        11834/15134 * 100% = 78.19%

pageViews column

        SELECT pageViews
        FROM all_sessions
        WHERE pageViews IS NULL

        no null values

        SELECT pageViews
        FROM all_sessions
        WHERE pageViews >= 20

sessionQualityDim column

        SELECT sessionQualityDim
        FROM all_sessions
        WHERE sessionQualityDim IS NOT NULL

        SELECT sessionQualityDim 
        FROM all_sessions
        WHERE sessionQualityDim > 0 AND sessionQualityDim < 10


Date Column

        SELECT date 
        FROM all_sessions1
        WHERE date IS NULL

        ALTER TABLE all_sessions
        ADD COLUMN new_date DATE;

        UPDATE all_sessions
        SET new_date = TO_DATE(CAST(date AS VARCHAR), 'YYYYMMDD');
        -> change date format using TO_DATE


visitId column

        SELECT visitId 
        FROM all_sessions1
        WHERE visitId IS NULL

        SELECT DISTINCT(visitId)
        FROM all_sessions1

Type column

        SELECT type
        FROM all_sessions1
        WHERE type IS NULL


productRefundAmount column 

        SELECT productRefundAmount
        FROM all_sessions1
        WHERE productRefundAmount IS NOT NULL


productQuantity column 

        SELECT productQuantity
        FROM all_sessions1
        WHERE productQuantity IS NOT NULL

        SELECT productQuantity
        FROM all_sessions1
        WHERE productQuantity < 10

productPrice column

        SELECT productPrice 
        FROM all_sessions1
        WHERE productPrice IS NOT NULL


        SELECT productPrice /10000
        FROM all_sessions1

productRevenue column 

        SELECT productRevenue
        FROM all_sessions1
        WHERE productRevenue IS NOT NULL

productSKU     

        SELECT productSKU
        FROM all_sessions1
        WHERE productSKU IS NOT NULL

        SELECT DISTINCT(productSKU)
        FROM all_sessions1
        

v2ProductName column 

        SELECT v2ProductName
        FROM all_sessions1
        WHERE v2ProductName IS NULL


        SELECT DISTINCT(v2ProductName)
        FROM all_sessions1


V2ProductCategory column 


        SELECT V2ProductCategory
        FROM all_sessions1
        WHERE V2ProductCategory IS NULL

        SELECT DISTINCT(V2ProductCategory)
        FROM all_sessions1

productVariant column

        SELECT productVariant
        FROM all_sessions1
        WHERE productVariant IS NULL

        SELECT DISTINCT(productVariant)
        FROM all_sessions1
" LG"
" BLUE"
" YELLOW"
"(not set)"
" 2XL"
" RED"
" GREEN"
" MD"
" SM"
"Single Option Only"
" XL"

currencyCode column

        SELECT currencyCode
        FROM all_sessions1
        WHERE currencyCode IS NOT NULL

        SELECT DISTINCT(currencyCode)
        FROM all_sessions1


itemQuantity column

        SELECT itemQuantity
        FROM all_sessions1
        WHERE itemQuantity IS NOT NULL

itemRevenue column

        SELECT itemRevenue
        FROM all_sessions1
        WHERE itemRevenue IS NOT NULL

transactionRevenue column 

        SELECT transactionRevenue
        FROM all_sessions1
        WHERE transactionRevenue IS NOT NULL

transactionId column 

        SELECT transactionId
        FROM all_sessions1
        WHERE transactionId IS NOT NULL

pageTitle column 

        SELECT  pageTitle
        FROM all_sessions1
        WHERE pageTitle IS NOT NULL

pagePathLevel1 column 

        SELECT  pagePathLevel1
        FROM all_sessions1
        WHERE pagePathLevel1 IS NOT NULL

ecommerceAction_type column 

        SELECT ecommerceAction_type
        FROM all_sessions1
        WHERE ecommerceAction_type IS NOT NULL

        SELECT DISTINCT(ecommerceAction_type)
        FROM all_sessions1


ecommerceaction_step column 
        SELECT ecommerceaction_step
        FROM all_sessions1
        WHERE ecommerceaction_step IS NOT NULL


        SELECT DISTINCT(ecommerceaction_step)
        FROM all_sessions1



ecommerceaction_option column

        SELECT ecommerceaction_option
        FROM all_sessions1
        WHERE ecommerceaction_option IS NOT NULL


        SELECT DISTINCT(ecommerceaction_option)
        FROM all_sessions1


For all_sessions table Cleaning Query:


DELETE FROM all_sessions
WHERE city = '(not set)';

DELETE FROM all_sessions
WHERE city = 'not available in demo dataset';

ALTER TABLE all_sessions
DROP COLUMN totalTransactionRevenue;

ALTER TABLE all_sessions
DROP COLUMN transactions;


ALTER TABLE all_sessions
ADD COLUMN new_date DATE;

UPDATE all_sessions
SET new_date = TO_DATE(CAST(date AS VARCHAR), 'YYYYMMDD');


ALTER TABLE all_sessions
DROP COLUMN productRefundAmount;

ALTER TABLE all_sessions
DROP COLUMN productQuantity;

UPDATE all_sessions
SET productPrice = productPrice / 10000;
     
ALTER TABLE all_sessions
DROP COLUMN productRevenue;

DELETE FROM all_sessions
WHERE currencyCode IS NULL;

ALTER TABLE all_sessions
DROP COLUMN itemQuantity;

ALTER TABLE all_sessions
DROP COLUMN itemRevenue;

ALTER TABLE all_sessions
DROP COLUMN transactionRevenue;

DELETE FROM all_sessions
WHERE pageTitle IS NULL;

ALTER TABLE all_sessions
DROP COLUMN searchKeyword;

UPDATE all_sessions
SET  timeOnSite = 0
WHERE timeOnSite is NULL;

For sales_report table:

        SELECT *
        FROM sales_report

        SELECT *
        FROM sales_report
        WHERE total_ordered IS NULL
        DELETE FROM sales_report
        WHERE total_ordered IS NULL;


For analytics table:


        SELECT visitNumber
        FROM analytics 
        WHERE visitNumber IS NULL

        SELECT DISTINCT(visitNumber)
        FROM analytics 

        SELECT VisitId
        FROM analytics 
        WHERE VisitId IS NULL

        SELECT DISTINCT(VisitId)
        FROM analytics 

        SELECT visitStartTime
        FROM analytics 
        WHERE visitStartTime IS NULL

        SELECT date
        FROM analytics 
        WHERE date IS NULL

        SELECT fullvisitorId
        FROM analytics 
        WHERE fullvisitorId IS NULL

        SELECT DISTINCT(fullvisitorId)
        FROM analytics 

        SELECT userId
        FROM analytics 
        WHERE userId IS NOT NULL

        ALTER TABLE analytics
        DROP COLUMN userId;

        SELECT channelGrouping
        FROM analytics 
        WHERE channelGrouping IS NULL

        SELECT DISTINCT(channelGrouping)
        FROM analytics 

        "Organic Search"
        "Display"
        "Referral"
        "Affiliates"
        "Paid Search"
        "Direct"
        "Social"

        SELECT socialEngagementType
        FROM analytics 
        WHERE socialEngagementType IS NULL

        SELECT DISTINCT(socialEngagementType)
        FROM analytics 


        SELECT units_sold
        FROM analytics 
        WHERE units_sold IS NULL

        SELECT units_sold
        FROM analytics 
        WHERE units_sold < 10

        SELECT pageviews
        FROM analytics 
        WHERE pageviews IS NULL

        SELECT pageviews
        FROM analytics 
        WHERE pageviews > 50

        SELECT timeonsite
        FROM analytics 
        WHERE timeonsite IS NULL


        SELECT bounces
        FROM analytics 
        WHERE bounces IS NOT NULL

        ALTER TABLE analytics
        DROP COLUMN bounces;

        SELECT revenue
        FROM analytics 
        WHERE revenue IS  NULL

        UPDATE analytics
        SET revenue = revenue / 10000;

        SELECT unit_price
        FROM analytics 
        WHERE unit_price IS  NULL

        UPDATE analytics
        SET unit_price = unit_price / 10000;

For products table:

        SELECT SKU
        FROM products 
        WHERE SKU IS  NULL

        SELECT DISTINCT("SKU")
        FROM products 

        SELECT name
        FROM products 
        WHERE name IS  NULL

        SELECT DISTINCT(name)
        FROM products 

        SELECT orderedQuantity
        FROM products 
        WHERE orderedQuantity IS  NULL

        SELECT stockLevel 
        FROM products 
        WHERE stockLevel IS  NULL

        SELECT restockingLeadTime 
        FROM products 
        WHERE restockingLeadTime IS  NULL

        SELECT sentimentScore 
        FROM products 
        WHERE sentimentScore IS  NULL

        DELETE FROM products
        WHERE sentimentScore  IS NULL;


        SELECT sentimentMagnitude
        FROM products 
        WHERE sentimentMagnitude IS NULL

For sales_by_SKU table:

        SELECT productSKU
        FROM sales_by_SKU 
        WHERE productSKU IS NULL

        SELECT total_ordered
        FROM sales_by_SKU 
        WHERE total_ordered IS NULL

For sales_report table: 

        SELECT total_ordered
        FROM sales_report 
        WHERE total_ordered IS NULL


        SELECT name
        FROM sales_report 
        WHERE name IS NULL

        SELECT stockLevel
        FROM sales_report 
        WHERE stockLevel IS NULL

        SELECT restockingLeadTime
        FROM sales_report 
        WHERE restockingLeadTime IS NULL

        SELECT "sentimentScore"
        FROM sales_report 
        WHERE "sentimentScore" IS NULL

        SELECT "sentimentMagnitude"
        FROM sales_report 
        WHERE "sentimentMagnitude" IS NULL


        SELECT "ratio"
        FROM sales_report 
        WHERE "ratio" IS NOT NULL

        DELETE FROM sales_report
        WHERE ratio  IS NULL;

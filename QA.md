What are your risk areas? Identify and describe them.

Duplicate values: Duplicate values can result in redundant storage and increase the overall data volume, which may impact database performance and storage costs.


QA Process:
Describe your QA process and include the SQL queries used to execute it.

Checking for unique fields

Query 1: Find the rows with duplicate visitId 


SELECT COUNT(distinct visitid) FROM (
SELECT al.visitid AS visitid , an.units_sold AS units_sold
FROM all_sessions al
INNER JOIN analytics an
ON al.visitid::BIGINT = an."visitId"
    ) tmp

1284 rows 
Query 2: Find the number of total visitId

SELECT COUNT("visitId") FROM analytics

1048575 rows 

Our joined result set tells us that there are more visitId than there are distinct visitId.

Does this make sense? 
After eyeballing the analytics table maunally, we can see that for one specific visitId, there are multiple visitNumbers, date, fullVisitorId, and different unitprice for a product. I think we can say that for this analysis it is safe to say that it is tolerable to have more visitId than there are distinct visitId. However, in terms of data storage, the massive amount of rows can increase the overall data volumn, which may impact the storage costs to increase. 

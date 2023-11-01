Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT 
    City, Country, SUM(transactionRevenue) AS TotalRevenue
FROM 
    all_sessions AS al
WHERE 
    transactionRevenue is NOT NULL
GROUP BY 
    City, Country
ORDER BY 
    TotalRevenue DESC;


Answer:
City: not available in demo dataset Country: United States Totalrevenue: 21909500000
City: Sunnyvale Country: United States Totalrevenue: 200000000




**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries: 

SELECT 
    al.city, al.country, AVG(sr.total_ordered) AS average_products_ordered
FROM 
    all_sessions AS al
JOIN 
    sales_report sr
ON 
    al.productSKU = sr.productSKU
GROUP BY 
    al.city, al.country
ORDER BY 
    average_products_ordered DESC;

Answer:
total rows: 240 TOP 10

"Brno"	            "Czechia"	        319
"Riyadh"	        "Saudi Arabia"	    319
"Rexburg"	        "United States"	    250.5
"Sacramento"        "United States"	    189
"Lisbon"	        "Portugal"	        189
"Kalamazoo"	        "United States"	    105
"Saint Petersburg"	"Russia"	        101.25
"Avon"	            "United States"	    100
"Rome"	            "Italy"	            97.75
"Sherbrooke"	    "Canada"	        97




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

SELECT
    a.country,
    a.city,
    v2ProductCategory,
    COUNT(v2productcategory) AS product_count
FROM
    all_sessions a
LEFT JOIN
    sales_report sr
ON
    a.productSKU = sr.productSKU
GROUP BY
    a.country,
    a.city,
    v2ProductCategory
ORDER BY
    a.country,
    a.city,
    product_count DESC;



Answer:
By analyzing the tables, we can identify in which city and country the visitors want more of a product. 

"Canada"	"Toronto"	"Home/Apparel/Men's/Men's-T-Shirts/"	18
"Canada"	"Toronto"	"Home/Shop by Brand/YouTube/"	        16
"Canada"	"Toronto"	"Home/Office/"	                        9
"Canada"	"Toronto"	"Home/Drinkware/"                   	9
"Canada"	"Toronto"	"Home/Electronics/"	                    8
"Canada"	"Toronto"	"Home/Bags/More Bags/"	                1
"Canada"	"Toronto"	"Home/Lifestyle/"	                    1
"Canada"	"Waterloo"	"Home/Apparel/"	                        1





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

WITH ranked_products AS (
    SELECT
        a.country,
        a.city,
        v2ProductName AS product_name,
        SUM(sr.total_ordered) AS total_quantity,
        ROW_NUMBER() OVER (PARTITION BY a.country, a.city ORDER BY SUM(sr.total_ordered) DESC) AS rank
    FROM
        all_sessions a
    LEFT JOIN
        sales_report sr
    ON
        a.productSKU = sr.productSKU
    GROUP BY
        a.country,
        a.city,
        v2ProductName
)
SELECT
    country,
    city,
    product_name AS top_selling_product
FROM
    ranked_products
WHERE 
    rank = 1
ORDER BY 
    country, city;


Answer:

"Canada"	"Burnaby"	    "Android Men's  Zip Hoodie"
"Canada"	"Calgary"	    "YouTube Leatherette Notebook Combo"
"Canada"	"Charlottetown"	"Google Ballpoint Pen Black"
"Canada"	"Edmonton"	    "YouTube Notebook and Pen Set"
"Canada"	"Kitchener"	    "Digital Lightshow Smart Speaker and Notification Center"
"Canada"	"Mississauga"	"Google Toddler Hoodie Royal Blue"
"Canada"	"Montreal"	    "Google French Terry Cap"
"Canada"	"New York"	    "Google Men's  Zip Hoodie"

compare the top-selling products across different locations to identify patterns or trends.

**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SELECT
    al.country,
    al.city,
    SUM(an.revenue) AS total_revenue
FROM
    all_sessions AS al
LEFT JOIN
    analytics AS an
ON
    al.visitId = an.visitId
WHERE
    an.revenue IS NOT NULL
GROUP BY
    al.country,
    al.city
ORDER BY
    al.country,
    al.city;



Answer:

"Israel"	"Tel Aviv-Yafo"	                    32990000
"United States"	"Chicago"	                    306000000
"United States"	"Mountain View"	                62810000
"United States"	"New York"	                    57990000
"United States"	"not available in demo dataset"	396000000
"United States"	"San Francisco"	                74159998
"United States"	"San Jose"	                    153000000
"United States"	"Sunnyvale"	                    649239992

You can identify cities or countries that contribute significantly to revenue, as well as those with lower contributions.







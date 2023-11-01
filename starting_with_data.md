Question 1: Find all duplicate records

SQL Queries:

SELECT *
FROM all_sessions
WHERE (fullvisitorId, visitId) IN (
    SELECT fullvisitorId, visitId
    FROM all_sessions
    GROUP BY fullvisitorId, visitId
    HAVING COUNT(*) > 1
);

Answer: 1122 rows with duplicate records 



Question 2: Find the total number of unique visitors (fullVisitorID)

SQL Queries:

SELECT COUNT(DISTINCT fullVisitorID)
FROM all_sessions;


Answer: 14223 rows



Question 3: Find each unique product viewed by each visitor:

SQL Queries:

SELECT al.fullVisitorID, al.pagetitle ,COUNT(DISTINCT an.pageviews) AS unique_products_viewed
FROM all_sessions AS al
LEFT JOIN
    analytics AS an
ON
    al.visitId = an.visitId
WHERE an.pageviews <> 0 
GROUP BY fullVisitorID, al.pagetitle;

Answer:

fullVisitorId           pagetitle                                                   pageviews
"00122544416887869"	"   Nest-USA"	                                                    1
"0014219973461482301"	"Clearance Sale"	                                            1
"0014262055593378383"	"Women's T-Shirts | Apparel | Google Merchandise Store"	        1
"0032840389344625281"	"Kids' Apparel | Google Merchandise Store"	                    1
"0045033268620668448"	"Men's Performance Wear | Apparel | Google Merchandise Store"	1
"007429458190280592"	"YouTube | Shop by Brand | Google Merchandise Store"	        1
"010375512815293876"	"YouTube | Shop by Brand | Google Merchandise Store"	        1
"0121805766582605968"	"Bags | Google Merchandise Store"	                            1



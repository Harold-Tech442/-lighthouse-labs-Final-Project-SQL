## Answer the following questions and provide the SQL queries used to find the answer.

    
## **Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

### SQL Queries:
```SQL
-- cities with the highest revenues

SELECT 
	alls.city,
	SUM(alls.productprice*sr.total_ordered) AS total_revenue
	
FROM all_sessions AS alls
JOIN sales_report AS sr ON alls.productsku = sr.productsku
GROUP BY alls.city
ORDER BY total_revenue DESC
LIMIT 5;
```
```SQL
-- countries with the highest revenues

SELECT 
	alls.country,
	SUM(alls.productprice*sr.total_ordered) AS total_revenue
	
FROM all_sessions AS alls
JOIN sales_report AS sr ON alls.productsku = sr.productsku
GROUP BY alls.country
ORDER BY total_revenue DESC
LIMIT 5;
```

### Answer:
Cities with the highest level of transaction revenues include: Mountain View, San Francisco, Sunnyvale, and Palo Alto. 
### NOTE: I noticed that some values in “city” in the all_sessions table were missing during the data cleaning process. Unfortunately, I ran out of time, and had to move on to the questions section.

## **Question 2: What is the average number of products ordered from visitors in each city and country?**

### SQL Queries:
```SQL
-- average number of products ordered from visitors in each city

SELECT 
	alls.city,
	AVG(sr.total_ordered)AS average
	
FROM all_sessions AS alls
JOIN sales_report AS sr ON alls.productsku = sr.productsku
GROUP BY alls.city;
```
```SQL
-- average number of products ordered from visitors in each country

SELECT 
	alls.country,
	AVG(sr.total_ordered)AS average
	
FROM all_sessions AS alls
JOIN sales_report AS sr ON alls.productsku = sr.productsku
GROUP BY alls.country
;
```

### Answer:
I got 227 results for cities and 127 for countries. I didn't know if I had to list every single one.

## **Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**

### SQL Queries:
```SQL
-- to calculate patterns in the types (product categories) of products ordered from visitors in each city

select 'total',
    city,
    v2productcategory,
	SUM(itemquantity)
from all_sessions
GROUP BY city, v2productcategory
union
select 'average',
    city,
    v2productcategory,
	AVG(itemquantity)
from all_sessions
GROUP BY city, v2productcategory
union
select 'min',
    city,
    v2productcategory,
	MIN(itemquantity)
from all_sessions
GROUP BY city, v2productcategory
union
select 'max',
    city,
    v2productcategory,
	MAX(itemquantity)
from all_sessions
GROUP BY city, v2productcategory
```

### Answer:

## **Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**

### SQL Queries:
```SQL
-- calculating the top-selling product from each city

SELECT
    alls.city,
	sr.name,
    MAX(sr.total_ordered) AS max_product
FROM all_sessions AS alls
JOIN sales_report AS sr ON alls.productsku = sr.productsku
GROUP BY alls.city, sr.name
```
```SQL
-- calculating the top-selling product from each city

SELECT
    alls.country,
	sr.name,
    MAX(sr.total_ordered) AS max_product
FROM all_sessions AS alls
JOIN sales_report AS sr ON alls.productsku = sr.productsku
GROUP BY alls.country, sr.name
```

### Answer:


## **Question 5: Can we summarize the impact of revenue generated from each city/country?**

### SQL Queries:
```SQL	
-- revenues from cities

SELECT 
	alls.city,
	SUM(alls.productprice*sr.total_ordered) AS total_revenue
	
FROM all_sessions AS alls
JOIN sales_report AS sr ON alls.productsku = sr.productsku
GROUP BY alls.city;
```
```SQL
-- revenues from countries

SELECT 
	alls.country,
	SUM(alls.productprice*sr.total_ordered) AS total_revenue
	
FROM all_sessions AS alls
JOIN sales_report AS sr ON alls.productsku = sr.productsku
GROUP BY alls.country;
```
### Answer:



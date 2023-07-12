### Question 1: Find all duplicate records

SQL Queries:
```SQL
### Find all duplicate records
-- find all duplicate records
SELECT visitid, count(*)
FROM analytics
GROUP BY visitid
HAVING count(*) > 1
```

Answer: 

### Question 2: Find the total number of unique visitors (`fullVisitorID`)

SQL Queries:
```sql
-- Find the total number of unique visitors (`fullVisitorID`)
SELECT DISTINCT COUNT(fullvisitorid)
FROM analytics
```

Answer:

### Question 3: Find the total number of unique visitors by referring sites

SQL Queries:
```sql
-- Find the total number of unique visitors by referring sites
SELECT DISTINCT 
	COUNT(fullvisitorid) AS unique_visitors,
	channelgrouping

FROM analytics
GROUP BY channelgrouping
HAVING channelgrouping = 'Referral'
```

Answer:

### Question 4: Find each unique product viewed by each visitor

SQL Queries: 
```sql
-- Find each unique product viewed by each visitor
SELECT DISTINCT 
	alls.fullvisitorid,
	p.name
FROM all_sessions alls
JOIN products p ON alls.productsku = p.sku
```

Answer:

### Question 5: compute the percentage of visitors to the site that actually makes a purchase

SQL Queries:
```sql
-- compute the percentage of visitors to the site that actually makes a purchase
```
Answer:

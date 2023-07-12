## What issues will you address by cleaning the data?
By cleaning the data, I will be ensuring the integrity of the data. This involves rectifying any anomaly that will affect the validity of future analytic exercises. The process will involve:
### Removing unwanted, irrelevant, or duplicate values:
For all tables that it applies to. E.g., I will remove irrelevant tables like totaltransactionrevenue, sessionqualitydim, etc. from all_sessions. Also, for the  date column in all_sessions, I will convert the column to the appropriate data type.
### Ensure accurate data types.
I was having problems uploading csv files for a few of the tables, so I had to upload some columns with different data types with the hopes of changing them after importing the csv files. So, after finally importing the csv files into postgres, I converted time, date, etc. to their correct datatype.
### Address any missing values
To update missing values in the city column of the all_sessions table. (Unfortunately, I didn't get around to doing this).

## Queries:
Below, provide the SQL queries you used to clean your data.
```SQL
-- to remove unwanted columns
all_sessions 
ALTER TABLE all_sessions
	DROP COLUMN totaltransactionrevenue,
	DROP COLUMN transactions,
	DROP COLUMN sessionqualitydim,
	DROP COLUMN productrevenue
;
```
```SQL
-- to divide unit_price by 1,000,000 for all_sessions and analytics tables
UPDATE all_sessions 
SET productprice = ROUND(productprice/1000000, 2);
```
```SQL
UPDATE analytics 
SET unit_price = ROUND(unit_price/1000000, 2);
```
```SQL
-- to ensure unique product count by comapring number of rows in general query and sku query
SELECT DISTINCT
	*
FROM products;

SELECT DISTINCT
	sku
FROM products;
```
```SQL
to change data type to TIME
SELECT date, TO_TIMESTAMP(date) :: DATE
FROM all_sessions
```
```SQL
-- To update missing values in the city column of the all_sessions table. 
--Unfortunately, I didn't get around to doing this.

# What are your risk areas? Identify and describe them.

My risk areas would include the validity of the data. Specifically, if the system was setup to capture the right and relevant data. Other risks include having the right data type, and duplicate entries.

# QA Process:
## Describe your QA process and include the SQL queries used to execute it.

### Step 1: 
Data Profiling: I will determine the data types, null values, and unique values in each table.
```sql
-- Get column data types and nullability for the products table 
SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'products';
```
```sql
-- Count unique values for the fullvisitorid column in the all_sessions table
SELECT COUNT(DISTINCT fullvisitorid)
FROM all_sessions;
```

# Step 2: 
Data Validation: I will perform some queries to determine certain validations.
```sql
-- Check for missing data in the all_sessions table
SELECT *
FROM all_sessions
WHERE productsku IS NULL;
```
```sql
-- Check for duplicate data in the sales_report table
SELECT productsku, COUNT(*)
FROM sales_report
GROUP BY productsku
HAVING COUNT(*) > 1;
```


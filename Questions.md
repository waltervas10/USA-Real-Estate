# Answering Business Questions:

## 1)	Average price and total listings by bedroom count:

```sql
SELECT bed, 
       AVG(CAST(price AS BIGINT)) AS avg_price, 
       COUNT(*) AS total_listings
FROM real_estate
GROUP BY bed
ORDER BY bed;
```
### Breakdown:

**AVG(CAST(price AS BIGINT)) AS avg_price:** This calculates the average price for each bedroom category, casting the price to BIGINT.

**COUNT(*) AS total_listings:** This counts all listings for each bedroom count.

**GROUP BY bed:** This groups the results based on the number of bedrooms.

#### Results:

| Bed              | Avg Price | Total Listings |
|------------------|-----------|----------------|
| 1 Bedroom House  | $383,875   | 30,562         |
| 2 Bedroom House  | $392,296   | 127,039        |
| 3 Bedroom House  | $416,828   | 301,579        |
| 4 Bedroom House  | $613,303   | 177,553        |
| 5 Bedroom House  | $891,762   | 51,745         |
| 6 Bedroom House  | $970,654   | 13,456         |

#### Analysis: 

 This query provides insight into how the number of bedrooms affects house prices.
 
 It also shows the distribution of listings across different bedroom counts.
 
 The results help determine whether more bedrooms generally correlate with higher prices, offering valuable information for potential buyers or investors targeting specific property sizes.

## 2) Average price by house size ranges:

```sql
CREATE VIEW house_size_ranges AS
SELECT *,
  CASE
    WHEN house_size BETWEEN 500 AND 1000 THEN '500-1000'
    WHEN house_size BETWEEN 1001 AND 1500 THEN '1000-1500'
    WHEN house_size BETWEEN 1501 AND 2000 THEN '1500-2000'
    ELSE '2000+' 
  END AS size_range
```

#### Breakdown:
**CREATE VIEW house_size_ranges AS:** This command creates a view called ***house_size_ranges***.

The **CASE** statement assigns a **size_range** category to each row based on the value in the **house_size** column.

This results in a new column, ***size_range,*** in the view, showing the house size category for each row.


#### Analysis: 

The size ranges were chosen to group houses into meaningful categories for easier analysis

These ranges (500-1000 sq ft, 1000-1500 sq ft, etc.) reflect typical housing size brackets, allowing us to investigate price differences across categories. 

Grouping by size range also helps identify market patterns, such as whether larger homes command higher average prices or if specific size ranges are more common in certain states.

## 3) Average Prices Per State

```sql
SELECT  
    state, 
    AVG(CAST(price AS NUMERIC(18, 2))) AS avg_price
FROM 
    real_estate
WHERE 
    price IS NOT NULL
GROUP BY 
    state
ORDER BY 
    avg_price DESC;
```
#### Breakdown:


**state:** Selects the state column to group results by state.

**AVG(CAST(price AS NUMERIC(18, 2))) AS avg_price:** Calculates the average price per state, casting price as NUMERIC(18, 2) for precision with up to 18 total digits and 2 decimal places.

**price IS NOT NULL:** Excludes rows where price is NULL, ensuring only valid prices are included in the calculation.

**state:** Groups the results by state so each row represents a unique state.

**avg_price DESC:** Sorts the results in descending order by avg_price, showing states with the highest average prices first.

#### Analysis:

This query explores how house prices vary within each state. 


Analyzing these patterns helps uncover which states on average are the most expensive to move to.

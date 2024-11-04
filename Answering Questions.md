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

## 2)	Most and least expensive places to buy a house:

```sql
SELECT city, state, AVG(CAST(price AS DECIMAL(18, 2))) AS avg_price
FROM real_estate
GROUP BY city, state
ORDER BY avg_price DESC;
```

#### Breakdown:

**SELECT city, state:** This selects the city and state columns from the real_estate table.

**AVG(CAST(price AS DECIMAL(18, 2))) AS avg_price:** This calculates the average price for each group (city and state) and casts the price to DECIMAL(18, 2) for precise decimal handling. This ensures that the average price will have two decimal places.

**FROM real_estate:** Specifies the table from which to retrieve the data.

**GROUP BY city, state:** Groups the results by both city and state, allowing to compute the average price for each unique combination.

**ORDER BY avg_price DESC:** Orders the results in descending order based on the average price, so the highest average prices appear first.

#### Least 10:                                                              

| City       | State       | Average Price |
|------------|-------------|---------------|
| Gilead     | Nebraska    | $1,000.00     |
| Caraway    | Arkansas    | $8,500.00     |
| Wheatland  | Indiana     | $8,900.00     |
| Iron Gate  | Virginia    | $10,000.00    |
| Lanesboro  | Pennsylvania| $10,000.00    |
| Melbeta    | Nebraska    | $12,000.00    |
| Millfield  | Ohio        | $12,334.00    |
| Lamont     | Iowa        | $12,500.00    |
| McCracken  | Kansas      | $14,000.00    |
| Midland    | Maryland    | $14,500.00    |   

#### Top 10:

| City            | State          | Average Price         |
|-----------------|----------------|-----------------------|
| International   | California     | $2,147,483,600.00     |
| Avon            | Montana        | $24,750,000.00        |
| Big Sandy       | Montana        | $17,450,000.00        |
| Golden Beach    | Florida        | $15,108,333.33        |
| Sagaponack      | New York       | $11,814,500.00        |
| Olney           | Montana        | $11,500,000.00        |
| Wise River      | Montana        | $11,300,000.00        |
| Bellevue        | Texas          | $10,034,750.00        |
| Kattskill Bay   | New York       | $10,000,000.00        |
| Parmelee        | South Dakota   | $9,154,500.00         |


### **To view and download the results, please click here:** [Question 2 Analysis Results](https://github.com/waltervas10/USA-Real-Estate/raw/refs/heads/main/Q2-Most%20and%20least%20expensive%20places%20to%20buy%20a%20house.csv)

#### Analysis: 

This query ranks cities and states based on their average house prices. 

By identifying the most and least expensive locations, the results provide insights into regional housing market trends. 

This information can guide buyers or investors toward affordable markets or highlight areas with premium property prices.

The top 10 most expensive and least expensive places will be especially useful in comparative analysis.


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






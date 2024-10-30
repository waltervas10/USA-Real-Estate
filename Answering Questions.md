# Answering Business Questions:

## 1)	Average price and count of houses by bedroom count:

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

#### Explanation: 

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








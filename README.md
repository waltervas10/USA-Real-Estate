# USA Real Estate Data Analysis Project by Walter A. Vasquez

## About

I chose a real estate dataset from Kaggle for this project because it presents a diverse array of information, perfect for resolving complex questions. The initial step involved cleaning the data in Excel to ensure its accuracy and consistency. I then used MySQL for in-depth analysis to resolve the questions. Finally, I created visualizations from my findings using Tableau, making the results not only accessible but also engaging. 

#### Dataset:
https://www.kaggle.com/datasets/ahmedshahriarsakib/usa-real-estate-dataset/data

## Purpose of The Project:

This project aims to uncover market trends, identify investment opportunities, and evaluate property performance across different US cities and states. Insights gained from this analysis will support data-driven decision-making for real estate stakeholders, including agents, investors, and developers, ultimately enhancing their understanding of the housing market dynamics.


### Business Questions To Answer:

#### 1.	Average price and total listings by bedroom count?
-	What is the average price for 1-bedroom, 2-bedroom, etc.?
- How many listings exist for each?

#### 2.	Average price by house size ranges?
- Ranges such as: 500-1000, 1000-1500, 1500-2000, 2000+ sq ft.

  
#### 3. Average price per state?

<br><br>

## Approaches Used

### 1) Clean Data in Excel

**Loading the Dataset:**

Initially, the cleaning of the data was going to be performed using SQL, but the dataset had some values that didn't match. MySQL was not able to upload smoothly, so I then decided to check out the data in Excel.

***To view the raw data, please click here:*** [rawdata](https://github.com/waltervas10/USA-Real-Estate/blob/5e2bacaa732396c38917e69837fd3be909972cb1/rawdata.png)

- **Upon reviewing the dataset, I noticed:**                          
  - Several entries appeared unusual or incorrect
  - Listings with 99 or 473 bedrooms and bathrooms
  - Records contained missing values
  - NULL values
  - Incorrect formats

- **I then performed data cleaning.**
  - I limited the dataset to houses with a maximum of 6 bedrooms and 6 bathrooms
  - Removed any blank fields within these columns
  - Corrected the formats
  - Corrected the missing values

 ### 2) Prepare Data for Analysis
 > The clean data was then succesfully imported into MySql and was ready to begin preparation

**Creating a new column:** price_per_sqft

```sql
ALTER TABLE real_estate 
ADD price_per_sqft FLOAT;
UPDATE real_estate 
SET price_per_sqft = price / house_size;
```



 - The **price_per_sqft** metric enriches the dataset by providing a standardized way to compare the price of houses based on their living space.
 - This allows for better analysis across properties of varying sizes, helping to identify trends such as whether smaller houses tend to have a higher price per square foot.
 - This metric is particularly useful when evaluating the value-for-space ratio within different cities or states.


<br><br>

## Answering Business Questions:

The data is now ready to begin analysis and answer business questions.

### 1)	Average price and count of houses by bedroom count:

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

#### Analysis:

This query provides insight into how the number of bedrooms affects house prices.

It also shows the distribution of listings across different bedroom counts.

The results help determine whether more bedrooms generally correlate with higher prices, offering valuable information for potential buyers or investors targeting specific property sizes.

#### Results:

| Bed              | Avg Price | Total Listings |
|------------------|-----------|----------------|
| 1 Bedroom House  | $383,875   | 30,562         |
| 2 Bedroom House  | $392,296   | 127,039        |
| 3 Bedroom House  | $416,828   | 301,579        |
| 4 Bedroom House  | $613,303   | 177,553        |
| 5 Bedroom House  | $891,762   | 51,745         |
| 6 Bedroom House  | $970,654   | 13,456         |


## ***To view the rest of questions, please click here:*** [Answering Questions](https://github.com/waltervas10/USA-Real-Estate/blob/48c8190415c5795986fa731f0796d356cc891682/Answering%20Questions.md)

<br><br>

## Create a Dashboard in Tableau:

> Once data is analyzed, I then imported all files into Tableau and started working on the visualizations.

### **Question 1 Visualization:** Average price and total listings by bedroom count

![Q2Visualization](https://github.com/waltervas10/USA-Real-Estate/blob/a9a228d085cdf1ce57e928aadea9ee780aaa548c/Question%201%20Visualization.png)
-----------

<br><br>


### **Question 2 Visualization:** Average price by house size ranges

![Q2 Visualization](https://github.com/waltervas10/USA-Real-Estate/blob/974183fb2398c99f42d752ef7d2d30bd3fe0588d/Q2%20Visualization.png)


<br><br>


### **Question 3 Visualization:** Average price per state



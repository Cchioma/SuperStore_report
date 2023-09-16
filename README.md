![background image](https://github.com/Cchioma/SuperStore_report/blob/main/store_1.jpg)

# Super Store Data Analysis
## Introduction
The goal of this project is to analyze and derive valuable insights from a comprehensive superstore dataset that encompasses various aspects of the business. The dataset includes information such as order details, customer demographics, product categories, shipping methods, and financial metrics. The aim is to provide actionable recommendations to enhance operational efficiency, customer satisfaction, and overall profitability for the superstore chain.

## Business Questions
1.   Profit distribution
2.   Sales distribution
3.   Most ordered category of product
4.   Mostly ordered subcategory
5.   How the product is ordered over the year
6.   Relationship between sales, profit, and quantity
7.   Category and shipped class used, show the distribution.
8.   Most ordered category of product in each region
9.   Segment of buyers in each Region
10.  Sub-category and which category they belong to
11.  Sales made in each region
12.  Profit made in each region
13.  Sales made from each category
14.  Profit made from each category
15.  States with loss (negative profit)

## Data Preparation

I cleaned and analyzed the data using Python on Jupiter Notebook. Firstly, I imported the necessary libraries:
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```
Then, I Loaded the dataset:
```
store_data = pd.read_csv('superstore_cleaned.csv')
```
I reviewed the first 3 rows of the dataset:
```
store_data.head(3)
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/head3.PNG)

I checked for data types:
```
store_data.dtypes
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/distribution.PNG)

## Data Cleaning
The dataset contained 22 columns and 9994 rows. The dataset can be found [here](https://github.com/Cchioma/SuperStore_report/blob/main/superstore_cleaned.csv) I cleaned them as follows:

1.  Checked for missing values and there were none.
   ```
  store_data.isnull().sum()
   ```
2.  Converted order_date column to date type
   ```
  store_data['order_date'] = pd.to_datetime(store_data['order_date'])
   ```
3.  Extracted month name from order_date column
   ```
  store_data['month'] = store_data['order_date'].dt.month_name()
   ```
4.  Sorted  month name according to calendar
   ```
  month_order = ['January', 'February', 'March','April', 'May','June', 'July', 
 'August', 'September', 'October', 'November', 'December']
  store_data['month'] = pd.Categorical(store_data['month'], ordered=True, 
  categories=month_order)
  ```

## Analysis and Insights
1.   Sales distribution:  I created a new column month_sales by grouping sales by month and plotted a line chart using Matplotlib.
   
```
month_sales = store_data.groupby('month')['sales'].sum()
month_sales.plot(marker='o', markersize=8, linestyle='-')
plt.title('Distribution of Sales')
plt.xticks(rotation=45)
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/sales_by_month.png)

#### Insight: The company recorded its highest sales in November followed by September and March. It recorded the least sales in February.

2.    Profit distribution: I created a new column month_profit by grouping profit by month and plotted a line chart using Matplotlib.

```
month_profit = store_data.groupby('month')['profit'].sum()
month_profit.plot(marker='o', markersize=8, linestyle='-')
plt.title('Distribution of Profit')
plt.xticks(rotation=45)
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/profit_by_month.png)

#### Insight: The company recorded its highest profit in December followed by September and March. It recorded its lowest profit in January.

3.   Most ordered category of product: I created a new column prod_category by grouping  quantity by category and plotting a bar chart using Matplotlib.

```
prod_category = store_data.groupby('category')['quantity'].sum()
prod_category.plot(kind = 'bar')
plt.xticks(rotation=45)
plt.xlabel(' ')
plt.ylabel('Quantity')
plt.title(' Product Category by Quantity')
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/most_ordered_cat.png)

#### Insight: The most ordered Product Category is Office Supplies

4.   Most ordered subcategory: I created a new column prod_category by grouping subcategories by quantity and plotting a bar chart using Matplotlib.

```
prod_category = store_data.groupby('sub_category')['quantity'].sum().sort_values(ascending = False)
prod_category.plot(kind = 'bar')
plt.xticks(rotation=45)
plt.xlabel(' ')
plt.ylabel('Quantity')
plt.title(' Product Sub_category by Quantity')
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/most_ordered_subcat.png)

#### Insight: The most ordered product Sub-Category is Binders, followed by paper and furnishings

5.  How the product is ordered over the year:  I Plotted a line chart using Seaborn to show the quantity of products ordered over time.

```
sns.set_style("whitegrid")
sns.lineplot(x='month', y='quantity', data=store_data, marker='o', markersize=8, color='g')
plt.xlabel(' ')
plt.ylabel('Quantity ordered')
plt.title('Quantity of products ordered  over time')
plt.xticks(rotation=45)
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/product_over_time.png)

#### Insight: The company recorded the highest orders in January, August, and November. It recorded its lowest orders in February.

6.  Relationship between sales, profit, and quantity:  I created a scatter plot to show the relationship between sales, profit, and quantity.

```
fig = plt.figure(figsize=(8,6))
sns.scatterplot(x='sales', y='profit', size='quantity',  hue = 'quantity', data=store_data)
plt.title('Relationship between Sales, Profit, and Quantity')
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/sales_profit_quant2.png)

#### Insight: The profit increased as sales increased for a few products ordered. The quantity of products ordered did not have a significant effect on the sales and profit made in the company. The highest profit and sales occurred when just 2 orders were made. The company also recorded negative profit when a large order was made.

7.   Category and shipped class used: I created a bar chart showing the distribution of ship mode by category.

 ```
sns.countplot(data=store_data, x='category',hue='ship_mode')
plt.title('Ship mode distribution by Category')
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/shipmode_category.png)

#### Insight: Most products were shipped using standard class followed by second class. Most number of products shipped were in the office supplies category followed by the furniture category.

8.   Most ordered category of product in each region: I created a new column region_product by grouping category by region. I created a bar chart showing the total quantity of ordered goods in each category per region.

```​
sns.countplot(data=store_data, x='region',hue='category')
plt.title('Category distribution by Region')
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/cat_region.png)
#### Insight: The most ordered category is office supplies. West region recorded the highest number of orders followed by the East region.

9.   Segment of buyers in each Region: I created a bar chart using Seaborn to show the distribution of buyer segments by region.

```
sns.countplot(data=store_data, x='region',hue='segment')
plt.title('Buyers segment by Region')
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/region_by_segment.png)
#### Insight: Consumer products were the most ordered followed by corporate products. The west region recorded the highest numbers of buyers followed by the East region. 

10.   Sub-category and which category they belong to: I created a bar chart using seaborn to show the distribution of Sub-category by category.

```
plt.figure(figsize=(15, 10))
sns.countplot(data=store_data, x='sub_category',hue='category')
plt.title('Distribution of Sub-category by Category')
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/cat_by_subcat.png)
#### Insight: The most ordered sub-category is Binders followed by paper. Both sub-categories belong to the office supplies category. 

11.   Sales made in each region: I created a new column region_sales by grouping sales by region and plotting a bar chart using Matplotlib.

```
region_sales = store_data.groupby('region')['sales'].sum()
region_sales.plot(kind = 'bar')
plt.title('Distribution of Sales across Regions')
plt.xlabel(' ')
plt.xticks(rotation=45)
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/region_by_sales.png)
#### Insights: West region recorded the highest sales followed closely by the East region. The region with the least sales is the South region.

12.   Profit made in each region: I created a new column region_profit by grouping profit by region and plotting a bar chart using Matplotlib.

```
region_profit = store_data.groupby('region')['profit'].sum()
region_profit.plot(kind = 'bar')
plt.title('Distribution of Profit across Regions')
plt.xlabel(' ')
plt.xticks(rotation=45)
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/profit%20by%20region.png)
#### Insight: West region recorded the highest profit followed closely by the East region. The region with the least profit is the Central region.

13.   Sales made from each category: I created a new column cat_sales by grouping sales by category and plotting a bar chart using Matplotlib.

```
cat_sales = store_data.groupby('category')['sales'].sum()
cat_sales.plot(kind = 'bar')
plt.title('Distribution of Sales across Product Category')
plt.xlabel(' ')
plt.xticks(rotation=45)
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/sales%20by%20category.png)

#### Insights: The Technology category recorded the highest sales followed closely by the Furniture category.

14.   Profit made from each category: I created a new column cat_profit by grouping profit by category and plotting a bar chart using Matplotlib.

```
cat_profit = store_data.groupby('category')['profit'].sum()
cat_profit.plot(kind = 'bar')
plt.title('Distribution of Profit across Product Category')
plt.xlabel(' ')
plt.xticks(rotation=45)
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/profit_by_cat.png)
#### Insight: The Technology category generated the most profit followed closely by the office supplies category.

15.   States with loss (negative profit): I created a new column store_data_neg_profit with negative profit and plotted a column chart showing the states with negative profit.

```
store_data_neg_profit = store_data[store_data['profit'] < 0]
​fig = plt.figure(figsize=(15,10))
#create a bar chart using Matplotlib
plt.bar(store_data_neg_profit['state'], store_data_neg_profit['profit'], color='red')
plt.xlabel(' ')
plt.ylabel('Profit')
plt.title('States with Negative Profit')
plt.xticks(rotation=45)
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/states_loss.png)
#### Insight: The state of Ohio recorded the least profit followed closely by North Carolina and Texas

## Recommendations

1.	Given that the company's highest sales and profits are typically recorded in November and December, They could consider launching marketing campaigns and promotions during these months to maximize revenue.
2.	To improve January's performance, It can explore strategies to sustain the holiday season's momentum into the new year.
3.	Since "Office Supplies" is the most ordered category, and "Binders" and "Paper" are the most ordered subcategories consider expanding the product range or introducing new, related items to capitalize on this popularity.
4.	The company should investigate the products and circumstances that lead to negative profits with large orders. They can introduce cost-saving measures or pricing adjustments to avoid such losses.
5.	The company should explore opportunities to optimize shipping costs and delivery times to improve customer satisfaction and potentially increase sales.
6.	Given that the West region consistently records the highest sales and profit, The company can consider allocating additional resources and marketing efforts to it to further capitalize on this market.
7.	The company can analyze the consumer and corporate segments' buying behavior to tailor marketing and product offerings to their specific needs and preferences.





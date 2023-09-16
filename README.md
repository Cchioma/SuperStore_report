![background image](https://github.com/Cchioma/SuperStore_report/blob/main/store3.jpg)

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

#### Insight: The company recorded it's highest sales in November followed by September and March. It recorded the least sales in February.

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

### Insight:
The company recorded the highest orders in January, August and November. It recorded its lowest orders in February.

6.  Relationship between sales, profit, and quantity:  I created a scatter plot to show the relationship between sales, profit, and quantity.

```
fig = plt.figure(figsize=(8,6))
sns.scatterplot(x='sales', y='profit', size='quantity',  hue = 'quantity', data=store_data)
plt.title('Relationship between Sales, Profit, and Quantity')
plt.show()
```
![](https://github.com/Cchioma/SuperStore_report/blob/main/sales_profit_quant2.png)

#### Insight: The profit increased as sales increased for a few products ordered. The quantity of products ordered did not have a significant effect on the sales and profit made in the company. The highest profit and sales occurred when just 2 orders were made. The company also recorded negative profit when a large order was made.

7.   




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

## Data Preparation/Cleaning

I cleaned and analyzed the data using Python on [Jupiter Notebook](). Firstly, I imported the necessary libraries:
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
1[](https://github.com/Cchioma/SuperStore_report/blob/main/head3.PNG)

The dataset contained 13 columns and 41,757 rows. The dataset can be found here I cleaned them as follows:

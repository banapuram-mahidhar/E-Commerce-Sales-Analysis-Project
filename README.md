# E-Commerce Sales Analysis Project

## Project Overview

This project focuses on analyzing E-Commerce sales data to gain meaningful business insights related to sales, profit, customer segments, and product performance.
The analysis is performed using Python, Pandas, and Plotly/Matplotlib for data visualization.

The goal of this project is to help stakeholders understand sales trends, profitability, and customer behavior to support better decision-making.

## Objectives

### The project answers the following business questions:

1.Calculate monthly sales and identify the highest and lowest sales months

2.Analyze sales by product category (highest & lowest)

3.Perform sales analysis by sub-category

4.Analyze monthly profit and find the most profitable month

5.Analyze profit by category and sub-category

6.Analyze sales and profit by customer segment

7.Calculate and analyze the sales-to-profit ratio

```graphql
E-Commerce-Sales-Analysis/
│
├── E_Commerce.ipynb        # Jupyter Notebook with full analysis
├── README.md               # Project documentation
├── images/
│   └── project_overview.png   # Project visualization (optional)
└── dataset/
    └── ecommerce_data.csv     # Dataset used (if allowed to share)

```

## Importing Libraries and installing if requared

---python
import pandas as pd
import numpy as np
import matplotlib .pyplot as plt
import seaborn as sns

pip install plotly
pip install nbformat

import plotly.express as px
import plotly .graph_objects as go
import plotly .io as pio
import plotly.colors as cloors
pio.templates.default = "plotly_white"

---

## loading the data
```python
df = pd.read_csv(
    r"C:\Users\massm\OneDrive\New folder\python_in_VS\Sample - Superstore.csv",
    encoding="latin1"
)
df.head()
```

## data understanding
```python
df.info()
df.isnull().sum()
df.duplicated().sum()
```

## data cleaning
### 1.changing the data type and creating new columns
```python
df.head()

df["Order Date"] = pd.to_datetime(df["Order Date"],format="%d-%m-%Y")
df["Ship Date"] = pd.to_datetime(df["Ship Date"],format="%d-%m-%Y")
df["Order Month"] = df["Order Date"].dt.month
df["Order Year"] = df["Order Date"].dt.year
df["order day of week"] = df["Order Date"].dt.dayofweek

df.dtypes

df.head()
```

## data analysis
### 1.You need to calculate the monthly sales of the store and identify which month had the highest sales and which month had the lowest sales.
```python
sales_by_Month = df.groupby("Order Month")["Sales"].sum().reset_index()
sales_by_Month
fig = px.line(sales_by_Month,
              x="Order Month",
              y="Sales",
              title="Monthly_Sales_Analysis")
fig.show()

```

### 2. You need to analyze sales based on product categories and determine which category has the lowest sales and which category has the highest sales.
```python
sales_by_category = df.groupby("Category")["Sales"].sum().reset_index()

sales_by_category
fig = px.pie(sales_by_category,values="Sales",names="Category",
             hole = 0.5,color_discrete_sequence = px.colors.qualitative.Pastel)
fig.update_traces(textposition = "inside",textinfo ="percent+label")
fig.update_layout(title_text = "sales analysis by category",title_font=dict(size=24))
fig.show()

```

### 3.The sales analysis needs to be done based on sub-categories
```python
Sales_by_Subcategory = df.groupby("Sub-Category")["Sales"].sum().reset_index()

Sales_by_Subcategory

fig = px.bar(Sales_by_Subcategory,x="Sub-Category",
             y="Sales",title="Sales analysis by Sub-Category")
fig.show()

```

### 4.You need to analyze the monthly profit from sales and determine which month had the highest profit.
```python
profit_by_Month = df.groupby("Order Month")["Profit"].sum().reset_index()

profit_by_Month

fig = px.line(profit_by_Month ,x="Order Month",y="Profit",title="Profit_by_Monthly")
fig.show()

```

### 5.Analyze the profit by category and sub-category.
***profit by category***
```python
Profit_by_Category = df.groupby("Category")["Profit"].sum().reset_index()

Profit_by_Category

fig = px.bar(
    Profit_by_Category,
    x="Category",
    y="Profit",
    title="Total Profit by Category",
    text_auto=True
)
fig.show()

```

***Profit_by_sub-category***
```python
Profit_by_sub_Category = df.groupby("Sub-Category")["Profit"].sum().reset_index()

Profit_by_sub_Category

fig = px.bar(
    Profit_by_sub_Category,
    x="Sub-Category",
    y="Profit",
    title="Total Profit by Sub-Category",
    text_auto=True
)
fig.show()
```

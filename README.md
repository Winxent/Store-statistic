<img width="284" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/d1fd18e6-9332-40a2-91be-3bf4fa479f0c"># Store-statistic
Goal: Data Analysis on store sales and profits dataset using Python and data visualisation using Tableau.

![rainbow](https://github.com/Winxent/portfolio/assets/146320825/5dc438d2-e138-4db0-97a0-e5ae8c3473e8)

# Introduction
Analyzing store profit and sales is crucial for a business's success because it provides actionable insights into its financial health and performance. This analysis helps in identifying trends, assessing the impact of various factors on profitability, and making informed decisions to optimize sales strategies and operations. It enables businesses to allocate resources effectively, respond to market changes, and ultimately maximize their profitability and sustainability.

Below is the raw dataset file:

https://docs.google.com/spreadsheets/d/1Scs5u9jgiYKOVWj_CVlRHaSSn-RuTEpQ/edit?usp=sharing&ouid=107402225492318840480&rtpof=true&sd=true

![rainbow](https://github.com/Winxent/portfolio/assets/146320825/5dc438d2-e138-4db0-97a0-e5ae8c3473e8)

# Data Cleaning (Python)
Check the chosen dataset if it needs any data cleaning. Go through all the fields, check for any null values or incorrect data types

Import Pandas library and load the dataset into Google Collaboratory 

https://colab.research.google.com/drive/1SLPRove3m7KUGXSEDrB1DWQCFbnysIyd?usp=sharing

```
import pandas as pd
df=pd.read_csv("/content/drive/MyDrive/Colab Notebooks/Expert+-+Superstore+-+Master.xlsx - Master.csv")
df.head()
```
<img width="1157" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/0b0b8926-dea4-4a78-9493-d2ac5c535319">

## A – Remove duplicate rows
First we have to find the duplicate:
```
df.duplicated().sum()
```
Using these 2 functions we can find the total number of duplicates.
2

View the duplicated rows:
```
df[df.duplicated(keep=False)]
```
<img width="629" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/749fa115-6512-4e6d-b702-7f7786607034">

##  B – Handle missing values
```
df.isna().sum()
```

<img width="148" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/733a62c2-e07d-4f55-abc1-7f620f207da6">

No missing value found.

## C – Correct data formats
Check data type
```
df.dtypes
```

<img width="126" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/1a515048-a9f6-4480-a660-79fce72c387c">

Due to too many columns, .info function could not show all the columns.
The below function is made to display all the columns:
```
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
print(df.head())
```
<img width="748" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/0822b7ce-4b5b-4f86-9620-c1f5b7a5191b">
<img width="768" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/a6731a14-30b8-428e-958e-0874dda800cb">
<img width="678" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/f8ee320d-9c52-4965-815e-1615725481bb">

Datatypes error:
1.	Profit per Customer, should be in float type 
2.	Profit per Order, should be in float type
3.	Sales Forecast, should be in float type
4.	Sales per Customer, should be in float type.
5.	Order Date, should be in date format
6.	Profit, should be in float type
7.	Sales, should be in int type
8.	Ship Date, should be in date type

After investigation, it seems that the data type can’t convert to float is because there is a comma

<img width="58" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/9eca00ff-a36b-4aea-afed-08288fbf9565">

### 1. String to float datatype
We need to remove the comma first
```
df['Profit per Customer']=df['Profit per Customer'].str.replace(',','')
```
Then we change then to float type:
```
df[‘Profit per Customer’] = df[‘Profit per Customer’].astype(float)
```
Repeat all for float type error.

### 2. String to date datatype
Change to date function
```
df['Order Date'] = pd.to_datetime(df['Order Date'])
```
Repeat for Ship Date

### 3. String to int datatype
Change string to int for sales column
```
df['Sales']=df['Sales'].str.replace(',','')
df['Sales'] = df['Sales'].astype(int)
```

<img width="292" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/f518d50a-526e-444b-9910-f2811a3d24c1">

Now all the datatypes are correct

## D – Drop irrelevant columns
Number of record has no meaning as it is always one, checked by unique and nunique function:
```
df["Number of Records"].nunique()
```
ans: 1

It has no comparison value, hence it is dropped 
```
df.drop('Number of Records', axis=1,inplace = True)
```
Since there is always only 1 customer, sales per customer, profit per order and sales per profit can be drop as it is repeat in profit and sales column.
```
df.drop(['Sales per Customer','Profit per Customer','Profit per Order'], axis=1,inplace = True)
```

Sales forecast and unit estimated can also be drop as they show no significant analysis
```
df.drop(['Sales Forecast','Unit Estimated'], axis=1,inplace = True)
```

## E – Fix inconsistent data entry
Check inconsistent data entry using unique function
```
df["City"].unique()
list(df['City'].unique())
```
After checking the columns one by one, there is no inconsistent data entry

## F – Trim whitespaces
No columns have any extra whitespaces errors

## G – Correct spelling errors
There are no spelling errors

## H – Correct numerical errors
There are no numerical errors

![rainbow](https://github.com/Winxent/portfolio/assets/146320825/5dc438d2-e138-4db0-97a0-e5ae8c3473e8)

# Data Analysis (Python)
There are 10000 rows, 22 columns. There are Column types of both categorical and numerical and they provide us the information about the Store details. Day to ship actual vs schedule, shipping status and shipping mode for the product. Segment, category and sub category of the product. Product name, customer name, manufacturer for identification. City, Country, Region and Sate for the location information. Order Id and order date to keep track of the order. Profit, Profit Ratio, Sales and Quantity for analysis.

Key performance indicators: Sales, profit, profit ratio, of the products can be used to analyse the performance of the store. The analysis can even be segregated based on product category, location, shipping mode and so on. We can even investigate base on manufacturer as well.

New information, indicators can be drawn through this dataset is Cost which can be generated from the profit ratio and sales.
```
df['Cost']=df['Sales']*(1-(df['Profit Ratio'].str.rstrip('%').astype('float') / 100.0))
```
## Data Exploration
### Describing the datasets
```
df.describe()
```
<img width="468" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/3d83f3da-6323-4cfb-b934-4f27dcbec53c">

### Shape and Size of your dataset
In order to have a better data description we usually check the Shape and Size of our dataset along with the general description of datasets such as count, unique values etc.
```
df.shape
```
10000 rows and 24 columns after adding 2 new indicators

```
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
print(df.head(16))
```
<img width="574" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/6f5b2ed6-8a44-4674-b2dd-6b80e999abed">
<img width="636" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/8bcab946-bc20-4d22-b92f-9e0f0fb36466">
<img width="468" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/0d0cc665-ebf0-47e3-9212-a25e6c13e42c">

By investigating the shape and size of our data set:
1.	Aware of the size of your datasets
2.	Aware that your columns have numerical or categorical 
3.	Major information/ description of the datasets, provided some insight of the data stored in the datasets. Example:
  a.	Sub-Category
  b.	Manufacturer
  c.	Ship Mode
  d.	Location
  e.	Segment
  f.	Ship Status

## Data Aggregation:
It helps us understand the data trends and values based on the compact display of values. Helps describe the data, and generate insight from the characteristic of the data. A store business owner might want to look into the sales and decide which products have better performance so that he or she can focus more than these products. A store owner can also look into which products give negative profit. 

### 1. Check the types of columns we have
```
df.dtypes
```
<img width="183" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/6c00d2a6-c134-46db-a881-54de116b163f">


### 2. For Categorical Columns we check the count of unique entries and their values
```
df['Ship Status'].unique()
```
array(['Shipped Early', 'Shipped Late', 'Shipped On Time'], dtype=object)

```
df['Category'].unique()
```
array(['Office Supplies', 'Technology', 'Furniture'], dtype=object)

```
df['Country'].unique()
```
array(['United Kingdom', 'France', 'Germany', 'Italy', 'Spain', 'Netherlands', 'Sweden', 'Belgium', 'Austria', 'Ireland', 'Portugal', 'Finland', 'Denmark', 'Norway', 'Switzerland'], dtype=object)

```
df['Discount'].unique()
```
array(['0%', '10%', '15%', '40%', '50%', '60%', '35%', '20%', '30%', '45%', '70%', '65%', '80%', '85%'], dtype=object)

```
df['Region'].unique()
```
array(['North', 'Central', 'South'], dtype=object)

```
df['Segment'].unique()
```
array(['Corporate', 'Consumer', 'Home Office'], dtype=object)

```
df['Ship Mode'].unique()
```
array(['Standard Class', 'Second Class', 'Same Day', 'First Class'], dtype=object)

```
df['Sub-Category'].unique()
```
array(['Storage', 'Accessories', 'Labels', 'Phones', 'Copiers',
       'Appliances', 'Fasteners', 'Art', 'Envelopes', 'Binders',
       'Bookcases', 'Machines', 'Paper', 'Supplies', 'Tables', 'Chairs',
       'Furnishings'], dtype=object)

Some categorical columns have too many unique values to be displayed.

### For the Numerical Columns lets find the minimum and maximum values
```
df.describe()
```

<img width="468" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/50c9b5af-176e-4dfe-b62d-283e6bc62b23">

<img width="662" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/acdb329c-ab9e-4c9a-ae4f-a677f2e2768c">

## Summary Statistic:
Summarized the large datasets into insightful numbers and gist of information about the data. Business owner can understand the general situation, make decisions and monitor the changes. Summaries of data help us understand the detailed trends followed in datasets based on concise information using measures of location and spread 

There are 3 types of summary statistics:
### 1.	Measures of location:
Mean (Average of a data set), Median (middle value of the data set), Mode (most repeated number),

<img width="660" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/2cf0ff9c-479f-4cab-a089-77b470c09c67">

```
df.mode()
```

<img width="468" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/6d14eda6-6135-4988-965a-1d29c0df8d7b">
<img width="431" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/21640563-c5a8-44ff-a5a4-40882fa5696a">

To count the number of mode:
```
df[df["Product Name"] == 'Eldon File Cart, Single Width'].count()
```
count: 30

```
df[df["Profit"] == 0].count()
```
Count: 293

```
df.var()
```

<img width="284" alt="image" src="https://github.com/Winxent/Store-statistic/assets/146320825/2f4741fa-79bd-4aab-81c1-02d08330da6b">

#### Group by 
Creating table with grouped information


### 2.	measures of spread:
To understand the spread and distribution of data. and to find outliers.
```
df.groupby('Ship Status').mean()
```


#### 3.	Graphics and charts:
Dash board.







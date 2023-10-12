# Store-statistic
Goal: Data Analysis on store sales and profits dataset using Python and data visualisation using Tableau.

![rainbow](https://github.com/Winxent/portfolio/assets/146320825/5dc438d2-e138-4db0-97a0-e5ae8c3473e8)

# Introduction
Analyzing store profit and sales is crucial for a business's success because it provides actionable insights into its financial health and performance. This analysis helps in identifying trends, assessing the impact of various factors on profitability, and making informed decisions to optimize sales strategies and operations. It enables businesses to allocate resources effectively, respond to market changes, and ultimately maximize their profitability and sustainability.

Below is the raw dataset file:

https://docs.google.com/spreadsheets/d/1Scs5u9jgiYKOVWj_CVlRHaSSn-RuTEpQ/edit?usp=sharing&ouid=107402225492318840480&rtpof=true&sd=true

![rainbow](https://github.com/Winxent/portfolio/assets/146320825/5dc438d2-e138-4db0-97a0-e5ae8c3473e8)

# Data Cleaning
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

## D – Drop irrelevant columns
## E – Fix inconsistent data entry
## F – Trim whitespaces
## G – Correct spelling errors
## H – Correct numerical errors



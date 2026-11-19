# Experiment No. 1: Data Cleaning and Preprocessing

## Aim

To perform data cleaning and preprocessing on a business dataset using Python libraries for better data quality and analysis readiness.

## Dataset

The dataset used for this experiment is `heartdisease.csv`. It contains
medical and demographic information related to heart disease patients.

The dataset is opened and analyzed using Jupyter Notebook to study its
data structure, identify data types, and perform basic statistical
analysis for data-cleaning and preprocessing purposes.

## Algorithm

1.  Import essential Python libraries.
2.  Load the dataset using Pandas.
3.  View the dataset structure, data types, and memory usage.
4.  Check for missing values and duplicates.
5.  Perform data summary statistics using `describe()`.
6.  View initial and final records using `head()` and `tail()`.
7.  Sort and group the data based on key attributes.
8.  Rename columns or modify data where necessary.
9.  Save the cleaned dataset for further analysis.

## Functions and Methods Used in the Experiment

### 1. Data Loading and Basic Exploration

  Function / Method      Description  
  ---------------------- ------------------------------------------------------\
  `pd.read_csv()`        Reads a CSV file into a Pandas DataFrame.\
  `df.info()`            Displays column names, data types, and memory usage.\
  `df.dtypes`            Returns the data types of all columns.\
  `df['column'].dtype`   Returns the data type of a specific column.\
  `df.describe()`        Provides summary statistics for numerical columns.\
  `df.head()`            Displays the first 5 rows of the DataFrame.\
  `df.tail()`            Displays the last 5 rows of the DataFrame.\

### 2. Sorting and Grouping

  Function / Method    Description  
  -------------------- ---------------------------------------------  
  `df.sort_values()`   Sorts the DataFrame by one or more columns.  
  `df.groupby()`       Groups data based on one or more columns.  
  `groupby.sum()`      Returns the sum for each group.  
  `groupby.mean()`     Returns the mean for each group.  
  `groupby.median()`   Returns the median for each group.  
  `groupby.max()`      Returns the maximum value in each group.  
  `groupby.min()`      Returns the minimum value in each group.  

### 3. Data Summary and Manipulation  

  Function / Method   Description  
  ------------------- ----------------------------------------------  
  `df.mean()`         Calculates the mean for all numeric columns.  
  `df.rename()`       Renames columns in the DataFrame.  

### 4. Optional Additions  

  Function / Method         Description  
  ------------------------- ----------------------------------------------  
  `df.isnull().sum()`       Checks for missing values in each column.  
  `df.duplicated().sum()`   Counts duplicate rows.  
  `df.dropna()`             Removes rows containing missing values.  
  `df.fillna()`             Fills missing values with a specified value.  
  `df.drop_duplicates()`    Removes duplicate rows.  
  `df.shape`                Returns the number of rows and columns.  
  `df.columns`              Lists column names in the DataFrame.  

## Program & Output
<< Enter your code and the corresponding screenshot of the output in this section>>
# 1. Import libraries  
import pandas as pd  
import numpy as np  
from IPython.display import display  

# 2. Load dataset  
df = pd.read_csv("heartdisease.csv")  
print("Original Dataset:")  
display(df)  

# 3. Explore dataset structure  
print("Dataset Information:")  
df.info()  

print("\nData Types:")  
print(df.dtypes)  

print("\nIndividual Column Data Types:")  
for column in df.columns:  
    print(f"{column}: {df[column].dtype}")  

print("\nDataset Shape:", df.shape)  
print("\nColumn Names:", df.columns.tolist())  

# 4. Check missing values and duplicates  
print("Missing Values per Column:")  
print(df.isnull().sum())  
  
print("\nNumber of Duplicate Rows:")  
print(df.duplicated().sum())  

# 5. Summary statistics  
print("Summary Statistics:")  
display(df.describe(include="all"))  

# 6. First and last five records  
print("First Five Records:")  
display(df.head())  

print("Last Five Records:")  
display(df.tail())  

# 7. Sort data by age, if available  
age_col = next((c for c in df.columns if c.lower() == "age"), None)  
if age_col:   
    sorted_df = df.sort_values(by=age_col)  
    print("Dataset Sorted by Age:")  
    display(sorted_df.head())  
else:
    print("Age column not found; sorting skipped.")  

    # 8. Group data by sex, if available   
sex_col = next((c for c in df.columns if c.lower() == "sex"), None)  
if sex_col:  
    grouped = df.groupby(sex_col)  
    print("Group Mean:")  
    display(grouped.mean(numeric_only=True))  
    print("Group Sum:")  
    display(grouped.sum(numeric_only=True))  
    print("Group Median:")  
    display(grouped.median(numeric_only=True))  
    print("Group Maximum:")  
    display(grouped.max(numeric_only=True))  
    print("Group Minimum:")  
    display(grouped.min(numeric_only=True))  
else:  
    print("Sex column not found; grouping skipped.")   

    # 9. Mean of numeric columns    
print("Mean Values:")    
print(df.mean(numeric_only=True))    

# 10. Rename selected columns if present    
rename_map = {  
    c: new for c, new in {  
        "age": "Age",  
        "sex": "Sex",  
        "chol": "Cholesterol",  
        "trestbps": "Blood_Pressure"  
    }.items() if c in df.columns  
}
df.rename(columns=rename_map, inplace=True)  
print("Renamed Columns:")  
print(df.columns.tolist())  

for column in df.select_dtypes(include="number").columns:  
    if df[column].isna().any():  
        df[column] = df[column].fillna(df[column].mean())  

# Fill missing categorical values with mode  
for column in df.select_dtypes(exclude="number").columns:  
    if df[column].isna().any():  
        modes = df[column].mode(dropna=True)  
        if not modes.empty:  
            df[column] = df[column].fillna(modes.iloc[0])  

print("Missing Values After Cleaning:")  
print(df.isnull().sum())  

# 12. Remove duplicates and display cleaned dataset  
df.drop_duplicates(inplace=True)  
print("Cleaned Dataset:")  
display(df)
print("Dataset Shape After Cleaning:", df.shape)  
print("Duplicate Rows After Cleaning:", df.duplicated().sum())  

# 13. Save cleaned dataset
df.to_csv("cleaned_heartdisease.csv", index=False)  
print("Cleaned dataset saved successfully as cleaned_heartdisease.csv")  



## Result
output 
Original Dataset:
   age  sex  ... 
0   ...  ...  ...
1   ...  ...  ...

Dataset Information:
<class 'pandas.core.frame.DataFrame'>
RangeIndex: ... entries
Data columns (total ... columns):
...

Data Types:
age        int64
sex        int64
...

Dataset Shape:
(rows, columns)

Missing Values:
age       ...
sex       ...
chol      ...

Duplicate Rows:
...

Summary Statistics:
              age       sex       chol
count         ...
mean          ...
std           ...
min           ...
max           ...

First Five Records:
...

Last Five Records:
...

Sorted Dataset:
...

Mean Values Grouped by Sex:
...

Maximum Values Grouped by Sex:
...

Minimum Values Grouped by Sex:
...

Median Values Grouped by Sex:
...

Missing Values After Cleaning:
age       0
sex       0
...

Dataset Shape After Cleaning:
(rows, columns)

Cleaned dataset saved successfully!





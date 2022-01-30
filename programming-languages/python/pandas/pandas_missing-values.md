# Missing Values
- In Pandas dataframes, missing values are annotated as 'NaN' which means Not a Number.
- There are various ways to review a dataset for missing data and to handle missing data

# Key Terms/ Ideas 
- NaN

# Key Functions 
## Detecting missing values 
- `df.isna()` return boolean value for each entry in a dataset. This is impractical for large datasets 
- `df.isna().any()` returns a boolean value for each variable/ column in a dataset
- `df.isna().sum()` returns the sum number of NaN values in each column 
- `df.isna().sum().plot(kind='bar')` returns a bar chart visualization with NaN values for each column

## What to do about missing values 
- `df.dropna()` removes all rows with missing values. This may not be a good option for datasets with many missing values.
- `df.fillna(<value>)` replaces all NaNs with `<value>`

# Examples 


# Credits
- datacamp.com 

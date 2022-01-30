# Key terms
* Slicing 
* Subsetting
* `.loc[]`
* `.iloc[]`
* index

# Two methods of slicing dataframes
1. Index values
2. Row, column numbers

## Slicing by index (row) value
* **Dataframes must be sorted by index before sorting (_unlike Python lists_)**
   *  Set single index and sort: `df_srtd = df.set_index(["indx1"]).sort_index()` 
   *  Set double index and sort: `df_srtd = df.set_index(["indx1", "indx2"]).sort_index()`

### Outer index slicing
* Outer index applies if there is more than one index in the dataframe. 
* Using the `.loc[]` function, choose the starting row (index) and last index desired. 
* `.loc[]` slices `inclusive : inclusive`
* `df_srtd.loc["Chow Chow" : "Poodle"]` will return the dataset indexed from the Chow Chow row to the Poodle row

### Inner index slicing 
* Must pass a tuple to properly slice by inner index
* Pandas will not throw an error if you attempt to slice the inner index as the outer index. It will return an empty dataset, which can be confusing.
* `df_srtd.loc[("start index 1", "start index 2") : ("end index 1", "end index 2")]`

### Slicing columns
* Pass two arguments to the `.loc[]` method (i.e. `subset = df_srtd.loc[ : , "col 1":"col2"]` will return all rows (` : ` denotes all) and only column 1 and column 2)

### Slicing rows and columns
* Example (single index): `subset = df_srtd.loc["indx1", "col 1":"col2"]`
* Example (double index): `subset = df_srtd.loc[ ("indx1","indx2):("end indx1","end indx2"), "col1"]`

### Slicing by dates
#### Using `.loc[]`
* Keep dates in ISO 8601 format, that is, `yyyy-mm-dd`
* Sort index based off of column containing dates (i.e. `df_srtd = df.set_index(["date"]).sort_index()`
* Slice by full date: `df_srtd = df.loc["YYYY-MM-DD":"YYYY-MM-DD"]`
* Slice by partial date: `df_srtd = df.loc["2018":"2020"]`
   * Sorting by partial dates is `inclusive:inclusive`. The example above would include all 2018, 2019, 2020

#### Using boolean conditions 
```python
# Use Boolean conditions to subset temperatures for rows in 2010 and 2011
temperatures_bool = temperatures[(temperatures["date"] >= "2010-01-01") & (temperatures["date"] <= "2011-12-31")]
print(temperatures_bool)

# Set date as an index and sort the index
temperatures_ind = temperatures.set_index("date").sort_index()

# Use .loc[] to subset temperatures_ind for rows in 2010 and 2011
print(temperatures_ind.loc["2010":"2011"])

# Use .loc[] to subset temperatures_ind for rows from Aug 2010 to Feb 2011
print(temperatures_ind.loc["2010-08":"2011-02"])
```

## Subsetting by row, column number
* Use `iloc[]` 
* `subset = df.iloc[2:5, 1:3]` 

# Credits
- datacamp.com 

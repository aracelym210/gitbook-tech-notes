# Key terms
* Slicing 
* Subsetting
* `.loc[]`
* `.iloc[]`
* index

# Two methods of slicing dataframes
1. Index values
2. Row, column numbers

## Slicing by index value
* **Dataframes must be sorted by index before sorting (_unlike Python lists_)**
   *  Set single column index and sort: `df_srtd = df.set_index(["col1"]).sort_index()` 
   *  Set double column index and sort: `df_srtd = df.set_index(["col1", "col2"]).sort_index()`

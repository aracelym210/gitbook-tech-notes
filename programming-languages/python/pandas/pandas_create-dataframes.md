# Creating dataframes
- This cheatsheet shows the various methods to read data into a pandas dataframe

# Key Terms/ Ideas 
- Manually create a dataframe with a list of dictionaries
- Manually create a dataframe with a dictionary of lists
- Reading and writing CSVs with Pandas

# Key Functions 
- `pd.Dataframe(<list or dictionary with data>)` create a dataframe from scratch 
- `df = pd.read_csv("dataset.csv")` reads a CSV file into a dataframe 
- `df.to_csv("new_dataset.csv")` converts a dataframe to CSV


# Examples 
## List of dictionaries
- Creating a dataframe with this method handles data row by row 
```python
dogs = [
  {"name": "Leia", "breed": "Lab", "mixed": True},
  {"name": "Hilo", "breed": "German Shorthaired Pointer", "mixed": True},
  {"name": "Luna", "breed": "Corgi", "mixed": False}
]

dogs_df = pd.Dataframe(dogs)
```

## Dictionary of lists 
- Creating a dataframe wit hthis method handles data column by column 
```python
dogs = {
  "name": ["Leia", "Hilo", "Luna"],
  "breed": ["Lab", "German Shorthaired Pointer", "Corgi"],
  "mixed": [True, True, False]
}

dogs_df = pd.Dataframe(dogs)
```


# Credits
- datacamp.com 

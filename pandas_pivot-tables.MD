# Pivot Tables
* Perform subsetting and calculations on pivot tables

# Key Terms
* index
* columns
* axis argument 

# Key functions
* Create pivot table with `.pivot_table("column name", index="<index>", columns="<column>")`
   * `column name` should be the column by which we want to aggregate 
   * The `index` argument lists the columns to group by and display in rows (recall, index == rows)
     * Create multiple indicies by assigning a list to index. `index = ['index 1', 'index 2', ..., 'index n']` 
   * The `column` argument lists the columns to group by and display in columns 
   
      ```python 
      dogs_height_by_breed_vs_color = pack.pivot_table(
                                        "height_cm", index = "breed", columns = "color")
       ```
* Default aggregation function: `.mean(axis=index)`
   * The `axis` argument is found in some methods for calculating summary statistics on a DataFrame
   * The default value is index, which will calculate statistics across rows

* Use `dt.<compontent>` for accessing various "components" of a datetime type value (i.e. month, year, day, etc.)

# Examples 
## Create pivot table with two incidies using `.dt<component>` functionality
```python
# Add a year column to temperatures
temperatures["year"] = temperatures["date"].dt.year

# Pivot avg_temp_c by country and city vs year
temp_by_country_city_vs_year = temperatures.pivot_table("avg_temp_c", index = ["country","city"], columns = "year")

# See the result
print(temp_by_country_city_vs_year)
```
### Results 
```
year                              2000    2001    2002    2003    2004  ...    2009    2010    2011    2012    2013
country       city                                                      ...                                        
Afghanistan   Kabul             15.823  15.848  15.715  15.133  16.128  ...  15.093  15.676  15.812  14.510  16.206
Angola        Luanda            24.410  24.427  24.791  24.867  24.216  ...  24.325  24.440  24.151  24.240  24.554
Australia     Melbourne         14.320  14.180  14.076  13.986  13.742  ...  14.647  14.232  14.191  14.269  14.742
              Sydney            17.567  17.855  17.734  17.592  17.870  ...  18.176  17.999  17.713  17.474  18.090
Bangladesh    Dhaka             25.905  25.931  26.095  25.927  26.136  ...  26.536  26.648  25.803  26.284  26.587
...                                ...     ...     ...     ...     ...  ...     ...     ...     ...     ...     ...
United States Chicago           11.090  11.703  11.532  10.482  10.943  ...  10.298  11.816  11.214  12.821  11.587
              Los Angeles       16.643  16.466  16.430  16.945  16.553  ...  16.677  15.887  15.875  17.090  18.121
              New York           9.969  10.931  11.252   9.836  10.389  ...  10.142  11.358  11.272  11.972  12.164
Vietnam       Ho Chi Minh City  27.589  27.832  28.065  27.828  27.687  ...  27.853  28.282  27.675  28.249  28.455
Zimbabwe      Harare            20.284  20.861  21.079  20.889  20.308  ...  20.524  21.166  20.782  20.523  19.756

[100 rows x 14 columns]
```


# Credits
* Datacamp.com

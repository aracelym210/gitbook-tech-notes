# Creating basic visualizations with matplotlib library 

# Key Terms / Ideas 
- Common alias for plotting with matplotlib - `import matplotlib.pyplot as plt`
- Histogram
- Bar plot
- Line plot
- Scatter plot
- Layering plots 
- Transparency/ transulent 

# Key functions 
## Histogram
- Good for showing distribution of a numeric variable. This type of graph/ plot will show us typical numerical ranges for a variable by grouping.
- Distribution is grouped into "bins," which can be modified by passing the optional argument `.hist(bins=<int>)`

    ```python
    # Format 
    df["num_variable"].hist()
    plt.show()
    
    # Example
    dog_pack["height_cm"].hist(bins=5)
    plt.show()
    ```
- If you want to show two types of distributions in the same chart, you can __layer__ your histogram plots 

    ```python
    # Filtering using boolean logic to select the height of female and male dogs
    # Change the opaqeness of the histograms with the optional argument .hist(alpha=<float>)
    # 1 = filled; 0 = invisible 
    
    dog_pack[dog_pack["sex"] == "F"]["height_cm"].hist(alpha=0.7)
    dog_pack[dog_pack["sex"] == "M"]["height_cm"].hist(alpha=0.7)

    
    # Add legend to differentiate which plot is which 
    # (matplotlib will automatically assign different colors)  
    plt.legend(["F","M"])
    
    
    plt.show()
    
    ```
    
    

## Bar plot
- Can reveal relationships between a categorical variable (i.e. application, operating system, port number) and numeric variable (i.e. byte size).

    ```python
    # Format
    vals_to_plot = df.groupby("category")["numeric var to perform math operation"].mean()
    
    # Example
    avg_weight_by_breed = dog_pack.groupby("breed")["weight_kg"].mean()
    
    avg_weight_by_breed.plot(kind="bar")
    plt.show()
    
    # Add title to plot
    df.plot(kind="bar",
            title="Title")
    plt.show()
    ```

## Line plot
- Good for visualizing changes in numeric value over time (i.e. weight change over time)

    ```python
    # Format
    df.plot(x="<column with date>", y="numeric value", kind="line")
    plt.show()
    
    # Example
    leia.plot(x="date", y="weight_lb", kind="line")
    plt.show()
    
    # Rotating axis labels using optional rot argument, where the number is degrees to rotate by
    leia.plot(x="date", y="weight_lb", kind="line", rot=45)
    plt.show()
    ```

## Scatter plot
- Good for visualizing relationships between two numeric variables (i.e. height vs weight) 

    ```python
    # Format 
    df.plot(x="num var 1", y="num var 2", kind="scatter")
    plt.show()
    
    # Example
    leia.plot(x="height_in", y="weight_lb", kind="scatter")
    plt.show()
    ```

# Examples
```python 
# Import matplotlib.pyplot with alias plt
import matplotlib.pyplot as plt

# Look at the first few rows of data
print(avocados.head())
print()

# Get the total number of avocados sold of each size
nb_sold_by_size = avocados.groupby("size")["nb_sold"].sum()
print(nb_sold_by_size)

# Create a bar plot of the number of avocados sold by size
nb_sold_by_size.plot(kind="bar")

# Show the plot
plt.show()
```
### Results (chart not pictured)
```
         date          type  year  avg_price   size    nb_sold
0  2015-12-27  conventional  2015       0.95  small  9.627e+06
1  2015-12-20  conventional  2015       0.98  small  8.710e+06
2  2015-12-13  conventional  2015       0.93  small  9.855e+06
3  2015-12-06  conventional  2015       0.89  small  9.405e+06
4  2015-11-29  conventional  2015       0.99  small  8.095e+06

size
extra_large    1.562e+08
large          2.015e+09
small          2.055e+09
Name: nb_sold, dtype: float64
```

# Credits
- datacamp.com

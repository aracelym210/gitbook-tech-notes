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


# Credits
- datacamp.com

---
title: Edx_Dat208x Intro to Python Data Science
image: images/dat208x.png  
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Fri Nov 16 2018 11:12:00 GMT+0000 (GMT)
tags:
  - new
  - programming  
  - edx  
  - courses  
  - python  
  - data science
---

# Introduction to Python for Data Science  

 1. https://courses.edx.org/courses/course-v1:Microsoft+DAT208x+1T2018/course/  
 2. https://www.datacamp.com/courses/introduction-to-python-for-data-science-microsoft  

available at the above urls.  

## Part 4: Numpy

First thing you can perform element calculations straight up with numpy:  

    import numpy as np  
    np_height = np.array([1.73, 1.68, 1.71, 1.89, 1.79])
    np_weight = np.array([65.4, 59.2, 63.6, 88.4, 68.7])

    bmi = np_weight/np_height **2

The above will run the bmi code for each item in the list, without the need for crazy looping.  
**Numpy knows how to work arrays as if they were single values**  

 * presumes array is of single types  
 * if multiple different types it will try to convert them  
 * numpy arrays are different to lists and will perform differently to them

#### subsetting  

    In:     bmi  
    Out:    array([21.852, 20.975, 21.75, 24.747, 21.441])  
    In:     bmi > 23  
    Out:    array([False, False, False, True, False], dtype=bool)  
    In:     bmi[bmi > 23]  
    Out:    array([24.747])  

#### 2d Numpy Arrays  
`ndarray` = N-dimensional array.  

    np_2d = np.array([1.73, 1.68, 1.71, 1.89, 1.79], [65.4, 59.2, 63.6, 88.4, 68.7])  
    np_2d.shape     # (2, 5)    - 2 rows, 5 columns  
    np_2d[0][2]     # 1.71      - select the row first and then the column  
    np_2d[0, 2]     # Same as above np_2d[row, column]  
    np_2d[:, 1:3]   # Values from Columns 1 and 2 in both rows. returns a 2d array with 2 rows and 2 columns  
    np_2d[1, :]     # selects the 2nd row and gets all the columns  


#### Basic Stats  

City data with height and weight of its inhabitants. ( shape = (5000, 2) )  
    
    np.mean(np_city[:, 0])      # return the mean of the height all 5000's citizens  
    np.median(np.city[:, 0])    # return the height of the person in the middle  
    np.corrcoef(np_city[:, 0], np_city[:, 1])   # check if height and weight are correlated  
    np.std(np_city[:, 0])       # standard deviation
    np.sum()  
    np.sort()  

generate random data: 
    
    np.random.normal(distribution mean, distribution standard deviation, number of samples)                         
    height = np.round(np.random.normal(1.75, 0.20, 5000), 2)  
    weight = np.round(np.random.normal(60.32, 15, 5000), 2)  
    np_city = np.column_stack((height, weight))  

useful tricks with indices:  
    
    positions = ['GK', 'M', 'A', 'D', ...]  
    heights = [191, 184, 185, 180, ...]  
    np_positions = np.array(positions)  
    np_heights = np.array(heights)  
    gk_heights = np_heights[np_positions == "GK"]  
    other_heights = np_heights[np_positions != "GK"]


## Matplotlib

#### Basic Plots

    import matplotlib.pyplot as plt  
    year = [1950, 1970, 1990, 2010]  
    pop = [2.519, 3.692, 5.263, 6.972]
    plt.plot(year, pop)  
    plt.show()  
    plt.scatter(year, pop)
    plt.show()

you can change the type of the scale using the by setting the `xscale` or `yscale`  
    
    # Change the line plot below to a scatter plot
    plt.scatter(gdp_cap, life_exp)
    # Put the x-axis on a logarithmic scale
    plt.xscale('log')
    # Show plot
    plt.show()

##### Why use log scales in graphs?  
https://www.forbes.com/sites/naomirobbins/2012/01/19/when-should-i-use-logarithmic-scales-in-my-charts-and-graphs/#794c61365e67  

logs are just another way of writing exponential equations, one that allows you to separate the exponent on one side of the equation. The equation 24 = 16 can be rewritten as log 2 16 = 4 and pronounced "log to the base 2 of 16 is 4."  It is helpful to remember that the log is the exponent (An exponent refers to the number of times a number is multiplied by itself), in this case, "4".  The equation y = log b (x) means that y is the power or exponent that b is raised to in order to get x. The common base for logarithmic scales is the base 10. However, other bases are also useful. While a base of ten is useful when the data range over several orders of magnitude, a base of two is useful when the data have a smaller range.

#### Histograms  

    import matplotlib.pyplot as plt  
    # help(plt.hist)        
    plt.hist(list_of_values, no_of_bins=no)    # call with list of values and how many bins you want to divide the data into   

#### Customisation  

Label axis (do before show method):
    
    plt.xlabel('label for x-axis')  
    plt.ylabel('label for y-axis')  
    plt.title('Graph Title Here....')  
    plt.yticks([ list of ticks for the y axis ]) # ex [0, 2, 4, 6, 8, 10]  
    # You can add a second list to the yticks function which is a list with the display names of the ticks  
    plt.yticks([0, 2, 4, 6, 8, 10],
                ['0', '2B', '4B', '6B', '8B', '10B'])  
    # Add further data to plot to show population explosion  
    population = [1.0, 1.262, 1.650] + population  
    year = [1800, 1850, 1900] + year  
    # Switch from a line graph to a filled graph using `fill_between()`  
    plt.fill_between(year, population, 0, color='green')

`fill_between(x_list, y_list, 0, color)`  
The 0 in the above is to fill untill zero.  

    plt.scatter(x = gdp_cap, y = life_exp, s = np.array(pop) * 2, c=col, alpha=0.8)
    s = size?
    c = color?
    alpha = opacity

    plt.text    # adds text to graph
    plt.grid    # adds gridlines to graph  

### Pandas

Pandas is a data science package that performs operations on a dataframe. 

##### Column 

    # To tell the dataframe that you want the first column as the column name  
    import pandas as pd
    brics = pd.read_csv("path/to/file.csv", index_col=0)
    # Get Column
    brics["column_name"]  
    brics.country  
    # Create Column  
    brics["density"] = brics["population"]/brics["area"] * 10000000

##### Row

For row access use `loc`:

    brics.loc["row_index"]      # returns row information displayed as a column  

to get one element row/column:

    brics.loc["row_label", "column_label"]  
    brics["column_label"].loc["row_label"]
    brics.loc["row_label"]["column_label"]
    brics.column_label.loc["row_label"]

Selecting a single column will return a Pandas Series, wrapping it in brackets will return a DataFrame

    brics["column_label"]   # Series
    brics[["column label"]] # Dataframe
    brics[["row1", "row2"], ["column1", "column2"]]  
    

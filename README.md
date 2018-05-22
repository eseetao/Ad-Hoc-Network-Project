# ECE 143 - Individual Project

The goal of this project is to generate rectangular subsections of ad-hoc networks. Each rectangle is independent randomly generated on a grid. One single network cannot span the entire grid and following networks must be trimmed to maximum coverage if it intersects an existing, previous network. This project can support a 10x10 grid as well as any other dimension specified by the user by changing parameters in the code.

A detailed explaination and answers to questions will be documented below. 

## Getting Started

The project contains one Jupyter notebook.

### Prerequisites

This project uses the libraries random, matplotlib.pyplot, and matplotlib.patches.

```
import random
import matplotlib.pyplot as plt
import matplotlib.patches as patches
```

## Discussion

Explain what these tests test and why

```
Give an example
```

## Trade-Offs and Limitations

In order to determine when the plot is filled and stop generating rectangles, we create a set of rectangle plots. We trim the rectangle plots and trim them to check if the entire plot is filled. The basic idea is that if the entire plot is filled, any next generated rectangle should be trimmed to have a height or width of 0. If this is the case, we should break the loop to stop generating rectangles.

This check method is more efficient than another approach of using a sliding 1 x 1 window to check if there is an empty plot. The sliding window would need 3 nested loops, 2 of which would sweep both x and y coordinates while the last loop would sweep the rectangle master list. Depending on unlucky generation of low widths and heights, this will be a very slow approach.

## Analysis

It is interesting to note that when plotting the total area vs the average number of rectangles, it is somewhat linear. This is probably due to the probability distribution being uniform that corresponds to the linearity of the area vs average number of rectangles. The figure below shows the plot of the relationship. 

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/AreaVsRectangles.png)

Questions:

1. Given an overall desired coverage footprint and a sequence of n communications
towers, what is the resulting resolved coverage?

- blah

2. What is the total area of coverage relative to the desired total coverage area of the
original footprint? That is, are there any gaps in coverage?

- blah

3. On average, how many communications towers are required before full coverage is
obtained?

- For a 10 x 10 plot, it takes an average of 31 rectangles to fill the entire plot. 
- For a 2 x 5 plot, it takes an average of 6 rectangles to fill the entire plot. 
- For a 15 x 10 plot, it takes an average of 39 rectangles to fill the entire plot. 
- For a 8 x 7 plot, it takes an average of 21 rectangles to fill the entire plot. 
- For a 30 x 10 plot, it takes an average of 55 rectangles to fill the entire plot. 
- For a 20 x 20 plot, it takes an average of 72 rectangles to fill the entire plot. 


## Authors

* **Erik Seetao** 



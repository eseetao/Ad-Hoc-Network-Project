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

The main technical challenge of this project is getting the currently generated rectangle to trim based on overlap with other previous rectangles. The approach that this project will take is to create two main functions, generate_rectangle and trim_rectangle. Using a master list that contains all the parameters of the generated rectangles in the form of starting coordinates, width, and height, we generate a rectangle and compare it with previous rectangles, trimming any overlaps based on maximum resulting area. We generate a rectangle on the plot with limits specified by user. Because the number of rectangles generated is so variable, we assign random colors to each. Width and height are of uniform distribution from 1 until the ceiling limit. If through trimming we get a rectangle that has width or height trimmed to 0, we generate another rectangle. This ensures that we do not place down a network rectangle that has no area.

The logic behind this is simple: comparing two rectangles, a previous and currently generated one, it will either overlap or not. If the two rectangles do not overlap, we leave the current one alone. If it does, the rectangle will fit in one of eight cases:
- Overlap on any 4 vertices, with each of the vertices being 1 case
- Vertical protrusions
- Horizontal protrusions
- Is contained within a previous rectangle
- Envelops previous rectangle

After idenfitying which case it is and trimming it, both rectangles no longer overlap. Simply sweep through the master list of rectangles, with most being non overlapping rectangles, the currently generated rectangle will be trimmed based on neighboring overlapping rectangles. Finally when sweeping through all the previous rectangles, the current rectangle will have the according valid rectangle coverage and be added to the master list of rectangles. On the chance that the rectangle does fall within at least one previous rectangle, the trimming function will trim its width or height to 0. This means that the ad-hoc network area has already been covered and the current one should not be generated on top of the area. In such cases, we will generate another rectangle to try and fill a valid nonzero area instead of placing down an ad-hoc network with 0 area.

This is an extremely effective method of filling gaps using the criteria of randomly generated starting points, widths, and heights. 


### The plots of varying dimensions are shown in the figures below:

10 x 10

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/10x10%20plot.png)

1 x 1

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/1x1%20plot.png)

2 x 5

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/2x5%20plot.png)

8 x 7

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/8x7%20plot.png)

15 x 10

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/15x10%20plot.png)

30 x 10

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/30x10%20plot.png)

20 x 20

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/20x20%20plot.png)


## Trade-Offs and Limitations

The method of trimming a current rectangle based on previous rectangles is far more efficient than trimming the rectangle based on a conglomerate polygon of all previous rectangles' area summed. This alternative approach would combine all the areas of the previous rectangles into a polygon and use that to determine the trim boundaries of the current rectangle. However, this approach can get confusing and difficult, especially when the randomly generated rectangles create a polygon with multiple protrusions and concavities. 

In order to determine when the plot is filled and stop generating rectangles, we create a set of rectangle plots. We trim the rectangle plots and trim them to check if the entire plot is filled. The basic idea is that if the entire plot is filled, any next generated rectangle should be trimmed to have a height or width of 0. If this is the case, we should break the loop to stop generating rectangles.

This check method is more efficient than another approach of using a sliding 1 x 1 window to check if there is an empty plot. The sliding window would need 3 nested loops, 2 of which would sweep both x and y coordinates while the last loop would sweep the rectangle master list. Depending on unlucky generation of low widths and heights, this will be a very slow approach.

## Analysis

It is interesting to note that when plotting the total area vs the average number of rectangles, it is somewhat linear. This is probably due to the probability distribution being uniform that corresponds to the linearity of the area vs average number of rectangles. The figure below shows the plot of the relationship. 

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/AreaVsRectangles.png)

Questions:

1. Given an overall desired coverage footprint and a sequence of n communications
towers, what is the resulting resolved coverage?

- For a 10x10 desired coverage footprint, we sample n = 2, 4, 6, 8, and 10 towers. The resulting plot is shown below for 10x10. We can observe a linear relationship between the different number of towers. An interesting point is that for lower numbers of towers such as 2 or 4, there is slightly more coverage probably due to the fact that with a low number of randomly generated towers, there is less probability of overlap which does not take away from the intial generated area. 

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/10x10%20towers.png)

Also, a plot for a 15x5 coverage area is also shown below. As we expected, it is also a linear graph.

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/15x5%20towers.png)


2. What is the total area of coverage relative to the desired total coverage area of the
original footprint? That is, are there any gaps in coverage?

- Initially with lower numbers of generated rectangles, there are definitely gaps in coverage. An example of a resulting plotted coverage for n = 8 towers on a 10x10 area is show below. Relative to the number of towers, the total area of coverage is linear, as explained above. 

![alt text](https://github.com/eseetao/Individual-Project/blob/master/Images/n%3D8%20towers%20sample.png)

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



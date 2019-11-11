# Assignment

Here is the assignment for the Info'Vis: Color and Geo .

You can learn more from the [lecture slides](https://docs.google.com/presentation/d/1cKYRVT2eHdbc0HXdVBpt8FZa5ZJ47xnk8bcYWDQWQ6I/edit?usp=sharing) and [In Class Coding Practice](https://github.com/nyuvis/infovis_practice_color_geo/tree/master/in-class practice).

In this assignment, we need to implement a choropleth map of Unemployment Rate in US ([data source](https://blog.datawrapper.de/how-to-choose-a-color-palette-for-choropleth-maps/)).  In the end of this assignment, you will be able to visualize the distribution of unimplement rate in a county-level US map together with a legend of how the color is used in this map.

#### Important Variables

`color_domain`: the array of values that maps to the array of stop colors. (What is a stop? Check [this article](https://blog.datawrapper.de/how-to-choose-a-color-palette-for-choropleth-maps/) and more content in **Practice 2-3**)

`color_range`: the array of stop colors. Now we defined 5 colors as suggested in the [color brewer](http://colorbrewer2.org/#type=sequential&scheme=YlGn&n=5).

`opacityScale`: the scaling function for opacity.

`linearGradient`: the linear gradient color patterns.

#### Instructions

Please follow the instructions below:

* Step 1: Redefine the stop values. The present values in `color_domain`  are randomly chosen. Now please use the strategy of *quartiles*. You can define the quartiles as described in [this post](https://www.geeksforgeeks.org/d3-js-d3-quantile-function/). 

* Step 2: Create your opcity scale follow the instructions in **Practice 2-1**.

* Step 3: Replace the fixed number `0.5` by opcities that are assigned according to the unemployment rate. Check the instructions in **Practice 2-1**.

* Step 4: Replace the fixed color `#66c2a4` by color hues that are assigned according to the unemployment rate. Check the instructions in **Practice 2-2**.

* Step 5: Set the colors of the rectangles used in the legend. Because we are using a linear scale to assign color hues, we want to show the linear gradient in the legend. To implement this, please read the tutorial [here](https://www.visualcinnamon.com/2016/05/smooth-color-legend-d3-svg-gradient.html). More specifically,

  * we have to implement the color patterns of linear gradient first (this part has been implemented in the part of *define svg gradient*).
  * then we need to create an SVG element, say, a rectangle and fill with gradient. 

  What you need to do here is to assign the predefined linear gradient color to this rectangle at the place where we mark `step 5`.
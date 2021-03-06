# Assignment

Here is the assignment for the Info'Vis: Color and Geo .

You can learn more from the [lecture slides](https://docs.google.com/presentation/d/1cKYRVT2eHdbc0HXdVBpt8FZa5ZJ47xnk8bcYWDQWQ6I/edit?usp=sharing) and [In Class Coding Practice](https://github.com/nyuvis/infovis_practice_color_geo/tree/master/in-class%20practice).

In this assignment, we need to implement a choropleth map of Unemployment Rate in US ([data source](https://blog.datawrapper.de/how-to-choose-a-color-palette-for-choropleth-maps/)).  In the end of this assignment, you will be able to visualize the distribution of unemployment rate in a county-level US map together with a legend of how the color is used in this map. 

* The **final** result should be like this:
  ![image](https://user-images.githubusercontent.com/9759891/68878604-01221400-06d6-11ea-9365-f537c3ea4051.png)



* If we **only** apply the color scale, **without** using the opacity scale, the map looks the one below.
  ![image](https://user-images.githubusercontent.com/9759891/68553889-d47aad80-03f2-11ea-9380-e933933644e4.png)

### Files
`assignment.html`: the front-end code. You only need to change the content here.

`data-VDNaC.csv`: the data file of unemployment rates.

`us.json`: the geo data file for drawing county-level US map.

### Important Variables
`pairRateWithId`: the mapping from id to rate.

`pairNameWithId`: the mapping from id to county name.

`rates`: a sorted array of unemployment rates.

`color_domain`: the array of values that maps to the array of stop colors. (What is a stop? Check [this article](https://blog.datawrapper.de/how-to-choose-a-color-palette-for-choropleth-maps/) and more content in **Practice 2-3**)

`color_range`: the array of stop colors. Now we defined 5 colors as suggested in the [color brewer](http://colorbrewer2.org/#type=sequential&scheme=YlGnBu&n=5).

`opacityScale`: the scaling function for opacity.

`linearGradient`: the linear gradient color patterns.

### Instructions

Please follow the instructions below:

* Step 1: Redefine the stop values. The present values in `color_domain`  are randomly chosen. Now please use the strategy of *quartiles*. You can define the quartiles as described in [this post](https://www.geeksforgeeks.org/d3-js-d3-quantile-function/). Please keep in mind, to use the function `d3.quantile`, the array should be already sorted. In the code, you can use `rates` directly.
* Step 2: Create your opacity scale follow the instructions in **Practice 2-1**. Here we can just map the minimal value to 0.2, and map the maximum to 1. 
* Step 3: Replace the fixed number `0.5` by opacities that are assigned according to the unemployment rate. Check the instructions in **Practice 2-1**. You can access the unemployment rate by using `pairRateWithId[d.id]`.

* Step 4: Replace the fixed color `#66c2a4` by color hues that are assigned according to the unemployment rate. Check the instructions in **Practice 2-2**.

* Step 5: Set the colors of the rectangles used in the legend. Because we are using a linear scale to assign color hues, we want to show the linear gradient in the legend. To implement this, please read the tutorial [here](https://www.visualcinnamon.com/2016/05/smooth-color-legend-d3-svg-gradient.html). More specifically,

  * we have to implement the color patterns of linear gradient first (this part has been implemented in the part of *define svg gradient*).
  * then we need to create an SVG element, say, a rectangle and fill with gradient. 

  What you need to do here is to assign the predefined linear gradient color to this rectangle at the place where we mark `step 5`.
  
  
  
  **Hint:** 
  
  - In **step 5**, `url(#linear-gradient)` in the tutorial means the color that the element with the **id** of `linear-gradient` represents.
  - In **step 2**, there are two ways of creating opacity scale. As described above, you can use code as
  
  ```javascript
  .domain([minVal, maxVal])
  .range([0.2, 1])
  ```
  
  Another opacity scale is also fine, which maps `color_domain` to another pre-defined 5-element array. For example, you can use the code as below:
  
  ```javascript
  .domain(color_domain)
  .range(d3.range(0.2, 1, (1-0.2)/5)) 
  // the line above gives you an uniformly distributed 5 element from 0.2 to 1/
  ```
  
  Please keep in mind,the domain array and the range array should have the same size. 
  
  If the domain has 5 elements and the  range array has only 2 elements, then the scale maps the first 2 elements in the domain array to the 2 elements in the range one.
  
  After applying both hue scale and opacity scale (5 stops), the result will look like below:
  
  ![image](https://user-images.githubusercontent.com/9759891/69161705-90a23b00-0ab9-11ea-802d-45d647d21f59.png)

This one shown above is also acceptable as a final result for your submission. 
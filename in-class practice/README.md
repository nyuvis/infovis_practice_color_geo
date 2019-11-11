# In-Class Coding Practice 

Here is the coding practice for Info'Vis: Color and Geo. 

You can learn more from the [lecture slides](https://docs.google.com/presentation/d/1cKYRVT2eHdbc0HXdVBpt8FZa5ZJ47xnk8bcYWDQWQ6I/edit?usp=sharing) and [after-class assignment](https://github.com/nyuvis/infovis_practice_color_geo/tree/master/assignment).

## Practice 1: Categorical Color Scale, Line Chart

Practice 1 is to help you get familiar with the online color tools that provide color scheme suggestions and create color scales using d3.

**Important variables**:

`nline`  the number of randomly generated lines shown in the chart.

`labels`  the categories that the lines represent.

`color`  the color scale used to assign colors to lines.

#### Practice 1-1: Choose Appropriate Color Scheme

[practice_1.html](https://github.com/nyuvis/infovis_practice_color_geo/blob/master/in-class%20practice/practice_1.html) presents a line chart of 5 randamly generated lines. Each line represents a category. Please change the colors we used for lines. 

In the lecture, we provide a list of on-line tools that give coloring suggestions. Explore them, and choose a color scheme you feel appropriate for the categories. When you choose the colors, don't forget the desired properties of a categorical color scale.

**Hint:**  change the color array used for defining the **range** of  `color` . Here, **d3.scaleOrdinal()** can be used to create a color scale for categoris.

If the number of labels/categories is more than the number of colors, the chart will reuse the colors.

#### Practice 1-2: Design A Bad Color Scale

Redefine the variable `color` and create a **bad** color scale.

Please watch the video and think of what is good for categorical color scales.

**Hint:** Try to answer the following questions:

* Is there any color that stands out (e.g. brighter or darker than others)?
* Is there any lines hard to be perceived with this background color?

#### Practice 1-2: Design Scalable Line Chart

Change the variable `nline` to `10` and `20`, how does your chart look like?

Try to answer the follwoing questions:

* How many lines do you think your line chart can best support?
* If you have quite a few lines, say, 100 lines, that you want to explore, what should you do to visualize those lines?

## Practice 2: Quantitative Color Scale, Chropleth Map

Practice 2 is to help you be familiar with the usage of quatitative color scales (diverging , sequential). In this practice, you will be asked to color a chropleth map which visualizes the unemployment rate(%) in the US in September, 2019 ([data source](https://www.bls.gov/web/laus/laumstrk.htm)).

#### Practice 2-1: Change Color Intensity

We can change the **opacity** of the filling color of states according to their unemployment rate. In default, we think the darker the higher rate. Open [practice2_1.html](https://github.com/nyuvis/infovis_practice_color_geo/blob/master/in-class%20practice/practice2_1.html) to finish the practice.

First, we defined a `fillColor` at line 40. Here we use the function `d3.color() ` to change the color to rgb form.

Then, we need to define a numeric scaling function for opacity. Find the `step 1` in the code. We can define the scale as below:

```javascript
scale = d3.scaleLinear()
	// keep in mind, the parameters for domain() and range() should be arrays
	.domain([minVal, maxVal])
	// you can map minVal to 0 here. 
	.range([0.2, 1]);
```

And then, we need to change the opacity according to the unemployment rate value. Find the `step 2` in the code. We can change the color opacity as below:

``````javascript
color.opacity = scale(d.properties.value);
// here you can set opacity directly because we set fillColor = d3.color("#....") above
``````

Another way of setting the color is to set attribute of `opacity` directly when appending the `path`. The code is like below:

```javascript
svg.selectAll("path")
	.data(json.features)
	.enter()
  .append("path")
  .attr("d", path)
  .attr("stroke", "#fff")
  .attr("stroke-width", "1")
  .attr("fill", fillColor)
  .attr("opacity", d => scale(d.properties.value));
// the above line is equal to the code below
// .attr("opacity", function(d) {
// 		return scale(d.properties.value);
//	});
```

#### Practice 2-2: Change Color Hue

We can change the **hue** of the filling color of states according to their unemployment rate. In default, we think the darker the higher rate. Open [practice2_2.html](https://github.com/nyuvis/infovis_practice_color_geo/blob/master/in-class%20practice/practice2_2.html) to finish the practice.

First we defined `lowColor` and `highColor` at line 40, 41.

Then we need to define a scale function to map values to different **color**s. Find the `step 1` in the code. We can define the scaling function as below:

```javascript
colorScale = d3.scaleLinear()
	.domain([minVal, maxVal])
	.range([lowColor, highColor]);
```

Now we can apply the color scale when coloring the states. Find the `step 2` in the code. Instead of  *return highColor*  directly, we need to return `colorScale(d.properties.value)`  so that we can get the assigned color hue according to the value.

#### Practice 2-3: Apply Multiple Color Hues

Check [this article](https://blog.datawrapper.de/how-to-choose-a-color-palette-for-choropleth-maps/) to know more about **How to choose a color palette for choropleth maps**. In this article, it shows the choropleth map after applying color plettes with multiple stop colors. And it covers different strategies of assigning **stop colors** (min/max, min/median/max, quartiles, etc.).

In the practice 2-2, we have set stop colors to *min* and *max*. How about setting 3 stop colors for *min*, *median*, and *max*?

Now, let's start from the `stop 0` and `step 1` in the code. In `step 0`, you should choose a sequential color scheme. Check how we do it in **practice 1-1**.

In step 1, you can implement the color scale as below:

```javascript
var median = d3.median(dataArray);
var colors = [an array of colors you choose];
colorScale = d3.scaleLinear()
	.domain([minVal, median, maxVal])
	.range(colors);
```

And then you can reuse the code for the `step 2` as we have done in the previous practice.

#### Practice 2-4: Change Color Hue And Intensity

If you want to make the difference between colors/vaules more obvious, you can change both color hue and color intensity. To implement this, you can use the strategies we cover in the **practice 2-1** and **practice 2-2**.

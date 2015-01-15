#D3 Tutorial
##Data Visualization
One of the hotest technology keywords used today across all industries is Data Visualization.  The primary goal of DV has always been to communicate information clearly\efficiently and, for the longest time, was limited to using expensive\complex tools that produced standard excel-like graphs(line,bar,ect...).  However the current demand in today's marketplace is that of innovation and flexibiliy, specifically in HOW the data is displaed and the open source community has stepped up to the challenge by creating some amazing tools and javascript librarys to make fill this need.  The only limitation...your imagination.  

##Intro To D3
D3 stands for Data Driven Documentation and is a JavaScript library created by Mike Bostock.  d3.js6 is “a JavaScript library for manipulating documents based on data”.  D3 is all about helping you to take information and make it more accessible to others via a web browser.  

The give you a better idea of it's capabilites let's look at the following examples:

  * NYTimes article: ["A Chicago divided By Killings" ](http://www.nytimes.com/interactive/2013/01/02/us/chicago-killings.html) 
  * Mike Bostock's: [Congressional Network Analysis](http://christopherroach.com/pydata2013/)
  * Paul MacGregors: [Home Page]( http://p--m.co/ )

##Demo
D3 is very frequently used in conjunction with the <svg> (scalable vector graphics) HTML tag, and it will also be used for the purpose of this tutorial. There is a “height" and "width" attibute for the svg tag that define the dimensions of the element. Within the <svg> tags, we will be placing <circle> tags, which creates a circle svg. <circle> tags have “cx” and “cy” attributes, that determine the coordinates for the center of the circle graphics in relation to the top left of the svg element. There is also a “r” attribute for radius, and “fill” will determine the color within the borders of the graphic.

```javascript
<svg width="720" height="720">
  <circle cx="40" cy="60" r="10"></circle>
  <circle cx="80" cy="60" r="10"></circle>
  <circle cx="120" cy="60" r="10"></circle>
</svg>
```  
at the bottom of the body tag and inside a script tag, place a source tag:

```javascript
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"> </script>
```
To begin implementing d3 within the html, we need to use d3 select methods to assign elements of the DOM to javascript variables. d3.select(“svg”) will return the first element with the DOM that is a <svg>, svg.selectAll(“circle”) will return all <circle> elements from the document inside an array. 

```javascript
var svg = d3.select("svg");
var circle = svg.selectAll("circle");
```
Now that all the circles are assigned to the circles array, we can begin to use D3’s .style and .attr methods to change their appearance and location.

```javascript
circle.style("fill", "steelblue");
circle.attr("r", 30);
```
The above code will change the value of “fill” to the color ”steelblue" for every circle on the page. Any value that can be set on the circles( or any element) through css , can be changed by the style method. Had we used standard javascript, we would have to explicitly iterate through the “circle” array, this is not the case with D3. The .attr works in a manner similar to the .style method. The attribute to be changed is specified first, in the above case the “r” attribute, followed by the value of 30. An anonymous function may be used in place of a specific value, this is what allows data to be applied to the html in ways that are visually dramatic.

```javascript
circle.attr("cx", function() { return Math.random() * 720; });
```
The .data method is a crucial part of what makes D3 so powerful. It is what binds the data to the selected elements, which can then in turn be assigned to different values or passed into functions as mentioned previously. Each piece of data in the array below, will be bound to the circle with a corresponding index in the "circle" array.

```javascript
circle.data([32, 57, 112]);
```
Bound data can be passed as the first argument of a function used in an attr or style method, and conventionally it will be represented with a “d”. The index of the element within its array is also available as a second argument. This can be useful when positioning elements relative to one another in a deliberate manner.

```javascript
circle.attr("cx", function(d, i) { return i * 100 + 30; });
```
in this next example, there is a data array with a 4th element inside, “293.” Because 293 does not have a corresponding DOM element to append to, we must use the .enter().append() methods to create an additional circle in which we can provide it with a radius of 293.
```javascript
var circle = svg.selectAll("circle").data([32, 57, 112, 293]);
var circleEnter = circle.enter().append("circle");
```
It is necessary when using these methods that elements are appended and selected from their correct parent element. In this case: 293 is attached to its parent data, which is the child of circle, which is selected from its parent element of svg. 

 

The next step takes circles off of the page. similar to previous steps, we have to select an element by following its parent elements. however when removing elements it is as though we are swapping new arrays out with old ones. the .data adds a new array of circle radiuses. the .exit method applies it to the circle variable, and the .remove() method removes the previous array of [32, 57, 112, 293]. 
```javascript
var circle = svg.selectAll("circle")
.data([32, 57]
circle.exit().remove();
``` 
you cannot take away an array without both the .exit and the .remove methods. 

##Bonus
Win fabulous prizes by making your own changes to the alphabet animation. You must edit at least two of the four attributes we demonstrated in [link to file](url) and [link to file](url) (x axis, y axis, color, and opacity), but you are welcome to experiment further.

*Download the [starter file](url) 
*Make your desired edits
*Save file as your_name.html
*Upload the file to our [repo](https://github.com/D3-J2GWK/D3)
* Briefly describe what you did to the class
##Glossary 

*Selecting Elements
—selection: the array of elements pulled from the current document. 	

—d3.selectAll: a method that selects all elements that match the specified selector. The elements will be selected in the document from top-to-bottom. 

—selection.style: sets the CSS style property with the specified name to the specified value on all selected elements. 
selection.style(name:value)
—selection.property: sets the property with the specified name to the specified value on all selected elements. This can be used for the HTML elements have special properties that are not addressable using standard attributes or styles.
selection.property(name:value)

—scales: are an optional feature in D3. They are functions that map from an input domain (like a a set of numbers or names) to an output range. They can be used to simplify the code needed to map a dimension of data to a visual representation.
 

—shapes: SVG has a number of built-in simple shapes, such as axis-aligned rectangles and circles. For greater flexibility, you can draw shapes using D3's path data generators. 

	
*Binding Data

—selection.data: Joins the specified array of data with the current selection. The specified values is an array of data values (like numbers or objects) or a function that returns an array of values. 


*Entering Elements

—enter: Returns placeholder nodes for each data element in the current selection that doesn’t have a corresponding existing DOM element.
 selection.enter()

—append: Appends a new element with the specified name as the last child of each element in the current selection, returning a new selection containing the appended elements.
selection.append(name)
—Method Chaining: syntax that allows several method calls to be chained together in a single statement.


*Exiting Elements	

—exit: returns  the existing DOM elements in the current selection for which no new data element was found.
selection.exit()
—remove: Removes the elements in the current selection from the current document. 
selection.remove()

*All Together
n/a

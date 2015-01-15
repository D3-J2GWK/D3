#D3 Tutorial
##Data Visualization
One of the hotest technology keywords used today across all industries is Data Visualization.  The primary goal of DV has always been to communicate information clearly\efficiently and, for the longest time, was limited to using expensive\complex tools that produced standard excel-like graphs(line,bar,ect...).  However the current demand in today's marketplace is that of innovation and flexibiliy, specifically in HOW the data is displaed and taliored to a specific audience. Once again the open source community has stepped up to the challenge by creating some amazing tools and javascript librarys to fill this need.  The only limitation...your imagination....WOOOAAAA...

##Intro To D3
D3 stands for Data Driven Documentation and is a JavaScript library created by Mike Bostock.  d3.js6 is “a JavaScript library for manipulating documents based on data”.  D3 is all about helping you to take information and make it more accessible to others via a web browser.  

The give you a better idea of it's capabilites let's look at the following examples:

  * NYTimes article: ["A Chicago divided By Killings" ](http://www.nytimes.com/interactive/2013/01/02/us/chicago-killings.html) 
  * Mike Bostock's: [Congressional Network Analysis](http://christopherroach.com/pydata2013/)
  * Paul MacGregors: [Home Page]( http://p--m.co/ )
  * [Koalas to the Max](http://www.koalastothemax.com/)

Check out the following [site](http://techslides.com/over-2000-d3-js-examples-and-demos) to see over 2000 additional samples
##Demo
The following demo has been created to walk through the basics of D3 by creating circles.  A [circletempale.html](https://github.com/D3-J2GWK/D3/blob/master/circletemplate.html) file has been provided to help faciliate the excercise and only requires that the code blocks be uncommented in order to execute the code blocks.  Please take a moment to download and run in your browser.

D3 is very frequently used in conjunction with the <svg> tag and is used to create scalable vector graph images which contain many of the same properties used by the <canvas> tag.  There is a “height" and "width" attibute that define the dimensions of the element and within the <svg> tags we will be adding one or more <circle> tags, to generalte...well...circles.  Circles require the “cx”,“cy” and "r" attributes, which determine the coordinates for placement and size of the circle.

So even without even using D3 one is still able to generate circles using the following lines which has also been included in the template.

```javascript
<svg width="720" height="720">
  <circle cx="40" cy="60" r="10"></circle>
  <circle cx="80" cy="60" r="10"></circle>
  <circle cx="120" cy="60" r="10"></circle>
</svg>
```  
In order to actually start using D3 we will need to make sure it is referenced somewhere in our file.  At the bottom of the body tag and inside a script tag you should see a refernce to the following:

```javascript
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"> </script>
```
To begin implementing D3 we need to use it's select() and selectAll() methods to begin assigning the existing svg and circle elements of the DOM to javascript variables. D3.select(“svg”) will return the first element in the document with the specified selector, in this case the <svg> tag.  The svg.selectAll(“circle”) will then return ALL <circle> elements that are children of the svg.  Take moment to uncomment this line of code in the Step 1 section of the template and refresh your browswer.

```javascript
var svg = d3.select("svg");
var circle = svg.selectAll("circle");
```
Now that all the circles are assigned to the circles array, we can begin to use D3’s .style and .attr methods to change their appearance and location.

```javascript
circle.style("fill", "steelblue");
circle.attr("r", 30);
```
The above code will change the value of “fill” to the color ”steelblue" for every circle on the page. Any value that can be set on the circles through css, can be changed using the style method. Had we used standard javascript, we would have to explicitly iterate through the “circle” array however D3 does a great job of doing this for us. Go D3...GO...The .attr works in a manner similar to the .style method. The attribute to be changed is specified first, in the above case the “r” attribute, followed by the value of 30. 

```javascript
circle.attr("cx", function() { return Math.random() * 720; });
```
The .data method is a crucial part of what makes D3 so powerful. It is what binds the data to the selected elements, which then in turn can be assigned to different values or passed into functions as mentioned previously. Each piece of data in the array below, will be imported and bound toa corresponding index and key in the "circle" array.

```javascript
circle.data([32, 57, 112]);
```
Bound data can be passed as the first argument of a function used in an attr or style method, and D3 accesses this key using the built-in “d” variable. The index of the element within its array is also available as a second predefined variable. This can be useful when positioning elements relative to one another in a deliberate manner.

```javascript
circle.attr("cx", function(d, i) { return i * 100 + 30; });
```
in this next example, there is a data array with a 4th element inside, “293.” Because 293 does not have a corresponding DOM element to append to, we must use the .enter().append() methods to create an additional circle in which we can provide it with additoinal attributes. 
```javascript
var circle = svg.selectAll("circle").data([32, 57, 112, 293]);
var circleEnter = circle.enter().append("circle");
```
The next step takes circles off of the page. similar to previous steps, we have to select an element by following its parent elements. however when removing elements it is as though we are swapping new arrays out with old ones. The .data() method adds a new array of circle attributes and the .exit() method applies passes these existing elements to the .remove() method never to be seen again. 
```javascript
var circle = svg.selectAll("circle")
.data([32, 57]
circle.exit().remove();
``` 

##Final Review
Now that you have a better understanding of several key D3 methods, specifically .attr() and .style(), we'd like to review one additional visualization followed by a challenge..should you choose to accept...and if we feel up to it, perhaps award some fabulous prizes to "Most Original Data Viz".  

The following viz titled ["General Update Pattern"]( http://bl.ocks.org/mbostock/3808234) is another Mike Bostock creation pulled from the list of over 2800 demo's, and is an excelent example of several previously reviewed key D3 methods and newly introducted ones, such as transition(). It also includes several well written update and randomization functions. Take moment to [download]() it from the github repository and open in a browser. 

The most prominent feature of this viz is transition and what appers to be pre and post states of data, in this case the alphabet.  Let's quickly review how this is done and then ask that you add some artistic flare in makeing some customizations based on your preferences.  

We first use D3 to enter the Data Join phase, where existing data is merged with incoming data and a distinction is made between existing, overlapping and the data that should be removed.  

```javascript
    // DATA JOIN
    // Join new data with old elements, if any.
    var text = svg.selectAll("text")
    .data(data, function(d) { return d; });
```

Now the Update phase to edit properties of any previous existing data. Here we see same .attr() and .style() methods as before, representing the x axis point and font-family.  We can see that the index (i) value is being multiplied by 32 for each data element in the pipeline forcing the existing data to reposition. 

```javascript
    // UPDATE
    // Update old elements as needed.
    text.attr("class", "update")
      .transition()
      	.duration(750)
      	.attr("x", function(d, i) { return i * 32; })
      	.style("fill","black");
```   
Now we enter the Enter() phase. Once again the transision() method is being used to visually change the data as well as reposition all data. Pay particular attention the the pre .attr("y", -60) and post .attr("y", 0) attribute values and style().  

```javascript
     // ENTER
    // Create new elements as needed.
      text.enter().append("text")
      .attr("class", "enter")
      .attr("dy", ".35em")
      .attr("y", -60)
      .attr("x", function(d, i) { return i * 32; })
      .style("fill-opacity", 1e-6)
      .text(function(d) { return d; })
    .transition()
      .duration(750)
      .attr("y", 0)
      .style("fill-opacity", 1);
      
```
Finally the Exit() phase where data is tranistioned out of the vis. Yet again pay attention to the .attr("y", 60) and .style("fill-opacity", 1e-6) attribute values along with the remove() method. 

```javascript
  // EXIT
  // Remove old elements as needed.
    text.exit()
      .attr("class", "exit")
    .transition()
      .duration(750)
      .attr("y", 60)
      .style("fill-opacity", 1e-6)
      .remove();
```
   
##Bonus
So onto the bonus.  We will now show you an update of the previous viz, describe some of the changes and ask that you give it a try.  

DEMO....

We now ask that you edit at least two of the four attributes we demonstrated but by no means will rule out any additional changes that you "intuitively" figure out. Instructions are below...Happy Coding...

  * Download the [bonus.html file](https://github.com/D3-J2GWK/D3/blob/master/bonus.html) 	
  * Save it as your_name.html
  * Upload the file to our [repo](https://github.com/D3-J2GWK/D3) once changes are made
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

#D3 Tutorial
##Data Visualization
One of the hotest technology keywords used today across all industries is Data Visualization.  The primary goal of DV has always been to communicate information clearly\efficiently and, for the longest time, was limited to using expensive\complex tools that produced standard excel-like graphs(line,bar,ect...).  However the current demand in today's marketplace is that of innovation and flexibiliy, specifically in HOW the data is displaed and the open source community has stepped up to the challenge by creating some amazing tools and javascript librarys to make fill this need.  The only limitation...your imagination.  

##Intro To D3
D3 stands for Data Driven Documentation and is a JavaScript library created by Mike Bostock.  d3.js6 is “a JavaScript library for manipulating documents based on data”.  D3 is all about helping you to take information and make it more accessible to others via a web browser.  

The give you a better idea of it's capabilites let's look at the following examples:

  * NYTimes article: ["A Chicago divided By Killings" ](http://www.nytimes.com/interactive/2013/01/02/us/chicago-killings.html) 
  * Mike Bostock's: [Congressional Network Analysis](http://christopherroach.com/pydata2013/)
  * Paul MacGregors: [Home Page]( http://p--m.co/ )


```javascript
<body>
<svg width="720" height="720">
  <circle cx="40" cy="60" r="10"></circle>
  <circle cx="80" cy="60" r="10"></circle>
  <circle cx="120" cy="60" r="10"></circle>
</svg>
```  
at the bottom of the body tag and inside a script tage, place a source tag:

```javascript
<script
src="http://d3js.org/d3.v3.min.js" charset="utf-8">
</script>
```


```javascript
var svg = d3.select("svg");
var circle = svg.selectAll("circle");
```


```javascript
circle.style("fill", "steelblue");
circle.attr("r", 30);
```

```javascript
circle.attr("cx", function() { return Math.random() * 720; });
```

```javascript
circle.data([32, 57, 112]);
```
```javascript
circle.attr("cx", function(d, i) { return i * 100 + 30; });
```
```javascript
var circle = svg.selectAll("circle").data([32, 57, 112, 293]);
var circleEnter = circle.enter().append("circle");
```
```javascript
var circle = svg.selectAll("circle")
.data([32, 57]
circle.exit().remove();
``` 

glossaryglossaryglossaryglossaryglossaryglossaryglossaryglossaryglossaryglossaryglossaryglossary


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

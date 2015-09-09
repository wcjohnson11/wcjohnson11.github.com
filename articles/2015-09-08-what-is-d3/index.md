# D3, ever heard of it?

### What is it?
D3 is a JavaScript Library that combines powerful visualization components with a data-driven approach to DOM manipulation. As a library it is extremely flexible, working directly with HTML, CSS and SVG to display data in any way you can imagine. It is also fun to write thanks to it's functional style that allows for method chaining, and code reusability.

When I was first learning JavaScript, D3 was one of the most compelling prospects of being a skilled coder. Looking at examples like these made me so excited that I had to keep coding. The sheer variety of data visualizations out there and their expressiveness had me geeking out. The ability to convey an idea and an accompanying mass of data was extraordinarily appealing to me.

### Getting started with D3
D3 can seem daunting but it's really very simple to use.
You select the document, or a section of the document like so 

```js
d3.select('body');
d3.select('#container');
```

You can change any attribute of this element like so 
```js
d3.select('body').style('background-color', 'black'); 
```

If you're familiar with jQuery or Prototype, this must feel pretty similar
How about some funky dynamic styling? 

```js
d3.selectAll("p").style("color", function() { 
return "hsl(" + Math.random() * 360 + ",100%,50%)"; });
```

 The above will randomly color all paragraphs on a page, pretty sweet right?
 
 <script type="text/javascript">
// Creating radio buttons

var shapeData = ["Triangle", "Circle", "Square", "Rectangle"], 
    j = 3;  // Choose the rectangle as default

// Create the shape selectors
var form = d3.select("body").append("form");

labels = form.selectAll("label")
    .data(shapeData)
    .enter()
    .append("label")
    .text(function(d) {return d;})
    .insert("input")
    .attr({
        type: "radio",
        class: "shape",
        name: "mode",
        value: function(d, i) {return i;}
    })
    .property("checked", function(d, i) {return i===j;});

 </script>

 <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.6/d3.min.js"></script>
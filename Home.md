# Rough.js API

This page describes all you can do with RoughJS. 
Note, this documentations is for v2.0. 

[If you're looking for examples, click here.](https://github.com/pshihn/rough/wiki/Examples).

# RoughCanvas

This is the main interface when drawing on Canvas using RoughJS. 

<a name="constructor" href="#constructor">#</a> rough.<b>canvas</b>(<i>canvasElement</i>, [<i>config</i>])

Instantiate RoughCanvas by passing in the canvas node to <b>rough.canvas()</b> method. 

<a href="#config"><i>config</i> is optional. 

```js
var rc = rough.canvas(document.getElementById('myCanvas'));
```

## Methods

For each method, <a href="#options"><i>options</i></a> are optional - they configure how the shape is drawn/filled. Default options can be configured in the <b>rough.canvas</b> instantiator described above. 

### line
```js
<i>roughCanvas</i>.<b>line</b>(x1, y1, x2, y2, [options])
```


<a name="lineMethod" href="#lineMethod">#</a> roughCanvas.<b>line</b>(<i>x1</i>, <i>y1</i>, <i>x2</i>, <i>y2</i>, [<i>options</>])

Draws a line from coordinates (x1, y1) to (x2, y2). 
<a href="#options"><i>options</i> are optional and describe how to draw this shape. 

<a name="linearPathMethod" href="#linearPathMethod">#</a> rough.<b>linearPath</b>(<i>points</i>)

Draws lines connecting the points passed in. <i>points</i> is an array of (x, y) coordinates. Each coordinate is an array of two elements: [x, y]

<i>Returns</i> a <a href="#linearpath">LinearPath</a>.

```js
rough.linearPath([[10, 0], [20, 20], [120, 320]]);
```

<a name="rectangleMethod" href="#rectangleMethod">#</a> rough.<b>rectangle</b>(<i>x1</i>, <i>y1</i>, <i>width</i>, <i>height</i>)

Draws a rectangle with x, y as the top-left coordinates, with the specified width and height

<i>Returns</i> a <a href="#rectangle">Rectangle</a>.

<a name="polygonMethod" href="#polygonMethod">#</a> rough.<b>polygon</b>(<i>points</i>)

Draws a polygon with the points passed in as vertices. <i>points</i> is an array of (x, y) coordinates. Each coordinate is an array of two elements: [x, y]

<i>Returns</i> a <a href="#polygon">Polygon</a>.

<a name="ellipseMethod" href="#ellipseMethod">#</a> rough.<b>ellipse</b>(<i>x</i>, <i>y</i>, <i>width</i>, <i>height</i>)

Draws an ellipse with the center at x, y; and with the specified width and height.
Note that width = rx * 2, and height = ry * 2. (rx, ry are horizontal and vertical radii).

<i>Returns</i> an <a href="#ellipse">Ellipse</a>.

<a name="circleMethod" href="#circleMethod">#</a> rough.<b>circle</b>(<i>x</i>, <i>y</i>, <i>radius</i>)

Draws a circle with the center at x, y; and with the specified radius. 

<i>Returns</i> an <a href="#circle">Circle</a>.


<a name="arcMethod" href="#arcMethod">#</a> rough.<b>arc</b>(<i>x</i>, <i>y</i>, <i>width</i>, <i>height</i>, <i>start</i>, <i>stop</i>, <i>closed</i>)

Draws an arc. An arc is described as a section of en ellipse. <i>x</i>, <i>y</i> represent the center of that ellipse. <i>width</i>, <i>height</i> are the dimensions of that ellipse. 

<i>start</i>, <i>stop</i> are the start and stop angles for the arc. 

<closed> is a boolean argument. If true, lines are drawn to connect the two end points of the arc to the center. 

<i>Returns</i> an <a href="#arc">Arc</a>.

![Rough.js arc](https://roughjs.com/images/cap_arc.png)

``` javascript
var arc1 = rough.arc(200, 100, 200, 180, -Math.PI + (Math.PI / 3), -Math.PI / 2, true);
arc1.fill = "red";
rough.arc(200, 100, 200, 180, -Math.PI, -0.75 * Math.PI, true);
var openArc = rough.arc(200, 100, 150, 130, -0.2 * Math.PI, 0.6 * Math.PI, false);
openArc.strokeWidth = 10;
```

<a name="curveMethod" href="#curveMethod">#</a> rough.<b>curve</b>(<i>points</i>)

Draws a curve passing through the points passed in. <i>points</i> is an array of (x, y) coordinates. Each coordinate is an array of two elements: [x, y]

<i>Returns</i> a <a href="#curve">Curve</a>.

<a name="pathMethod" href="#pathMethod">#</a> rough.<b>path</b>(<i>d</i>)

Draws a path described using a [SVG path](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths) data string. 

<i>Returns</i> a <a href="#path">Path</a>.

![Rough.js svg](https://roughjs.com/images/cap_svg.png)

``` javascript
var path = rough.path("M213.1,6.7c-32.4-14.4-73.7,0-88.1,30.6C110.6,4.9,67.5-9.5,36.9,6.7C2.8,22.9-13.4,62.4,13.5,110.9 C33.3,145.1,67.5,170.3,125,217c59.3-46.7,93.5-71.9,111.5-106.1C263.4,64.2,247.2,22.9,213.1,6.7z");
path.fill = "#424242";
path.hachureAngle = 90;
```

# Drawable

Drawable is the base class that represents any object that may appear on the canvas - lines, curves, shapes, paths. 

Drawable has properties to configure its style (stroke, fill, roughness). These properties override the properties of the same name defined in the <a href="#roughcanvas">RoughCanvas</a>.

Updating any property on a Drawable object updates the UI automatically in an efficient way. No redraw method needs to be called. 

<b>drawable</b>.<a href="#roughness">roughness</a><br/>
<b>drawable</b>.<a href="#bowing">bowing</a><br/>
<b>drawable</b>.<a href="#stroke">stroke</a><br/>
<b>drawable</b>.<a href="#strokewidth">strokeWidth</a><br/>
<b>drawable</b>.<a href="#fillstyle">fillStyle</a><br/>
<b>drawable</b>.<a href="#fill">fill</a><br/>
<b>drawable</b>.<a href="#fillweight">fillWeight</a><br/>
<b>drawable</b>.<a href="#hachureangle">hachureAngle</a><br/>
<b>drawable</b>.<a href="#hachuregap">hachureGap</a><br/>

# Line

Line inherits all properties from <a href="#drawable">drawable</a>. Other properties:

### Properties

- line.<b>x1</b><br/><i>(number)</i> x-coordinate for the start of the line.
- line.<b>y1</b><br/><i>(number)</i> y-coordinate for the start of the line.
- line.<b>x2</b><br/><i>(number)</i> x-coordinate for the end of the line.
- line.<b>y2</b><br/><i>(number)</i> y-coordinate for the end of the line.

# LinearPath

Object representing a set of connected lines. Inherits all properties from <a href="#drawable">drawable</a>.

### Methods

- linearPath.<b>getPoint</b>(<i>index</i>)<br/>
Get the point at the specified <i>index</i>.<br/>
<i>Returns</i> an array representing coordinates [x, y].

- linearPath.<b>setPoint</b>(<i>index</i>, <i>x</i>, <i>y</i>)<br/>
Updates the coordinates of the point and the specified index.

# Rectangle

In addition to the properties below, Rectangle inherits all properties from <a href="#drawable">drawable</a>. 

### Properties

- rectangle.<b>x</b><br/><i>(number)</i> x-coordinate for the top-left corner of the rectangle.
- rectangle.<b>y</b><br/><i>(number)</i> y-coordinate for the top-left corner of the rectangle.
- rectangle.<b>width</b><br/><i>(number)</i> width of the rectangle.
- rectangle.<b>height</b><br/><i>(number)</i> height of the rectangle.

# Polygon

Polygon inherits all properties from <a href="#drawable">drawable</a>.

### Methods

- polygon.<b>getPoint</b>(<i>index</i>)<br/>
Get the coordinates of the vertex at the specified <i>index</i>.<br/>
<i>Returns</i> an array representing coordinates [x, y].

- polygon.<b>setPoint</b>(<i>index</i>, <i>x</i>, <i>y</i>)<br/>
Updates the coordinates of the vertex and the specified index.

# Ellipse

In addition to the properties below, Ellipse inherits all properties from <a href="#drawable">drawable</a>. 

### Properties

- ellipse.<b>x</b><br/><i>(number)</i> x-coordinate for center of the ellipse.
- ellipse.<b>y</b><br/><i>(number)</i> y-coordinate for center of the ellipse.
- ellipse.<b>width</b><br/><i>(number)</i> width of the ellipse (2 * rx).
- ellipse.<b>height</b><br/><i>(number)</i> height of the ellipse (2 * ry).
- ellipse.<b>numSteps</b><br/><i>(number)</i> number of segments Rough.js approximates when drawing the ellipse. Default value is 9. 

# Circle

In addition to the properties below, Circle inherits all properties from <a href="#drawable">drawable</a>. 

### Properties

- circle.<b>x</b><br/><i>(number)</i> x-coordinate for center of the circle.
- circle.<b>y</b><br/><i>(number)</i> y-coordinate for center of the circle.
- circle.<b>width</b><br/><i>(number)</i> radius of the circle.
- circle.<b>numSteps</b><br/><i>(number)</i> number of segments Rough.js approximates when drawing the circle. Default value is 9. 

# Arc

Arc is described as a section of an ellipse. A <b>closed</b> arc has lines drawn from the center of the ellipse to the ends of the arc. 

In addition to the properties below, Arc inherits all properties from <a href="#drawable">drawable</a>. 

### Properties

- arc.<b>x</b><br/><i>(number)</i> x-coordinate for center of the ellipse used for the arc.
- arc.<b>y</b><br/><i>(number)</i> y-coordinate for center of the ellipse used for the arc.
- arc.<b>width</b><br/><i>(number)</i> width of the ellipse (2 * rx) used for the arc.
- arc.<b>height</b><br/><i>(number)</i> height of the ellipse (2 * ry) used for the arc.
- arc.<b>closed</b><br/><i>(boolean)</i> Flag indicating if the arc should be connected to the center. Default value is <b>false</b>.
- arc.<b>numSteps</b><br/><i>(number)</i> number of segments Rough.js approximates when drawing the arc. Default value is 9.

# Curve

Curve drawn by passing through a set of points. It inherits all properties from <a href="#drawable">drawable</a>.

### Methods

- curve.<b>getPoint</b>(<i>index</i>)<br/>
Get the coordinates of the point at the specified <i>index</i>.<br/>
<i>Returns</i> an array representing coordinates [x, y].

- curve.<b>setPoint</b>(<i>index</i>, <i>x</i>, <i>y</i>)<br/>
Updates the coordinates of the point and the specified index.

# Path

A Path is described using a [SVG path](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths) data string. It inherits all properties from <a href="#drawable">drawable</a>. 

### Properties

- path.<b>path</b><br/><i>(string)</i> instructions to draw the [SVG path](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths).
- path.<b>numSteps</b><br/><i>(number)</i> number of segments Rough.js approximates when drawing the curves in the path. Default value is 9.
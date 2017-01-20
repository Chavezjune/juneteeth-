Fist step - instantiate the RoughCanvas object. This canvas object can  be used to create different shapes, lines, curves and paths. 

RoughCanvas has properties that can be used to configure the overall style (default style) of all the objects drawn on it. For example, changing the fill-color or the stroke-width will change the fill-color and stroke-width of all the objects. Individual objects can override these properties. 

# RoughCanvas

<a name="constructor" href="#constructor">#</a> <b>RoughCanvas</b>(<i>canvasElement</i>, <i>width</i>, <i>height</i>)

Instantiate RoughCanvas by passing in the canvas node and the dimensions of the canvas. The constructor will resize the canvas element. 

```js
var rough = new RoughCanvas(document.getElementById('myCanvas'), 500, 500);
```

## Properties

<a name="roughness" href="#roughness">#</a> rough.<b>roughness</b>

Numerical value indicating how rough the drawing is. A rectangle with the roughness of 0 would be a perfect rectangle. Default value is 1.

This property can be overridden by setting the same property on any sketch object. 

<a name="bowing" href="#bowing">#</a> rough.<b>bowing</b>

Numerical value indicating how curvy the lines are when drawing a sketch. A value of 0 will cause straight lines. 
Default value is 1. 

This property can be overridden by setting the same property on any sketch object. 

<a name="stroke" href="#stroke">#</a> rough.<b>stroke</b>

String value representing the color of the drawn objects. Default value is black (#000000).

<a name="strokewidth" href="#strokewidth">#</a> rough.<b>strokeWidth</b>

Numerical value to set the width of the strokes (in pixels). Default value is 1. 

![Rough.js stroke sample](https://pshihn.github.io/rough/images/cap_rough.png)

```js
rough.stroke = "#66AA88";
rough.strokeWidth = 6;
rough.rectangle(20, 20, 120, 120);
var r2 = rough.rectangle(160, 20, 120, 120)
r2.stroke = "red";
r2.strokeWidth = 2;
```

<a name="fillstyle" href="#fillstyle">#</a> rough.<b>fillStyle</b>

Rough.js supports two styles of filling a shape: <b>hachure</b> and <b>solid</b>.
Default value is hachure.

<i>hachure</i> draws parallel lines with the same roughness as defined by the <a href="#roughness">roughness</a> and the <a href="#bowing">bowing</a> properties of the shape or the canvas. It can be configured using the <a href="#fillweight">fillWeight</a>, <a href="#hachureangle">hachureAngle</a>, and <a href="#hachuregap">hachureGap</a> properties.

<i>solid</i> is more like a conventional fill.

<a name="fill" href="#fill">#</a> rough.<b>fill</b>

String value representing the color used to fill a shape. In hachure style fills, this represents the color of the hachure lines. 

<a name="fillweight" href="#fillweight">#</a> rough.<b>fillWeight</b>

Numeric value representing the width of the hachure lines. Default value of the fillWeight is set to half the <a href="#strokewidth">strokeWidth</a> of that shape.

<a name="hachureangle" href="#hachureangle">#</a> rough.<b>hachureAngle</b>

Numerical value that defines the angle of the hachure lines. Default value is -41 degrees. 

<a name="hachuregap" href="#hachuregap">#</a> rough.<b>hachureGap</b>

Numerical value that defines the average gap, in pixels, between two hachure lines.  Default value of the hachureGap is set to four times the <a href="#strokewidth">strokeWidth</a> of that shape. 

![Rough.js fill sample](https://pshihn.github.io/rough/images/cap_fill2.png)

```js
var rough = new RoughCanvas(myCanvas, 400, 400);
rough.fill = "#FF6688";
rough.rectangle(20, 20, 120, 120);
var r2 = rough.rectangle(160, 20, 120, 120)
r2.fillWeight = 2;
r2.hachureAngle = 60;
r3 = rough.rectangle(20, 160, 120, 120);
r3.hachureGap = 10;
r4 = rough.rectangle(160, 160, 120, 120);
r4.fillStyle = "solid";
```

## Methods

<a name="addMethod" href="#addMethod">#</a> rough.<b>add</b>(<i>drawable</i>)

Add a <a href="#drawable">drawable</a> to the canvas. A drawable is anything that appears on the canvas - a line, a circle, an SVG path, etc.

<a name="removeMethod" href="#removeMethod">#</a> rough.<b>remove</b>(<i>drawable</i>)

Remove a <a href="#drawable">drawable</a> from the canvas. 

<a name="clearMethod" href="#clearMethod">#</a> rough.<b>clear</b>()

Clears the canvas. Removes all shapes, paths, lines, and curves. 

<a name="lineMethod" href="#lineMethod">#</a> rough.<b>line</b>(<i>x1</i>, <i>y1</i>, <i>x2</i>, <i>y2</i>)

Draws a line from coordinates (x1, y1) to (x2, y2). 

<i>Returns</i> a <a href="#line">Line</a>.

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

![Rough.js arc](https://pshihn.github.io/rough/images/cap_arc.png)

``` javascript
var arc1 = rough.arc(200, 100, 200, 180, -Math.PI + (Math.PI / 3), -Math.PI / 2, true);
arc1.fill = "red";
rough.arc(200, 100, 200, 180, -Math.PI, -0.75 * Math.PI, true);
var openArc = rough.arc(200, 100, 150, 130, -0.2 * Math.PI, 0.6 * Math.PI, false);
openArc.strokeWidth = 10;
```

<a name="curveMethod" href="#curveMethod">#</a> rough.<b>curve</b>(<i>points</i>)

Draws a curve passing through the points passed in. <i>points</i> is an array of (x, y) coordinates. Each coordinate is an array of two elements: [x, y]

<i>Returns</i> a <a href="#polygon">Curve</a>.

<a name="pathMethod" href="#pathMethod">#</a> rough.<b>path</b>(<i>d</i>)

Draws a path described using a [SVG path](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths) data string. 

<i>Returns</i> a <a href="#path">Path</a>.

![Rough.js svg](https://pshihn.github.io/rough/images/cap_svg.png)

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

Polygon inherits all properties from <a href="#drawable">drawable</a>

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


## API

this.roughness = 1;
    this.bowing = 1;

    this.stroke = "#000";
    this.strokeWidth = 1;

    this.fill = null;
    this.fillStyle = "hachure";
    this.fillWeight = -1;
    this.hachureAngle = -41;
    this.hachureGap = -1;

    this.maxRandomnessOffset = 2;

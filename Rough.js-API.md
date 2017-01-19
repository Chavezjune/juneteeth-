Fist step - instantiate the RoughCanvas object. This canvas object can  be used to create different shapes, lines, curves and paths. 

RoughCanvas has properties that can be used to configure the overall style (default style) of all the objects drawn on it. For example, changing the fill-color or the stroke-width will change the fill-color and stroke-width of all the objects. Individual objects can override these properties. 

## RoughCanvas

<a name="constructor" href="#constructor">#</a> <b>RoughCanvas</b>(<i>canvasElement</i>, <i>width</i>, <i>height</i>)

Instantiate RoughCanvas by passing in the canvas node and the dimensions of the canvas. The constructor will resize the canvas element. 

```js
var rough = new RoughCanvas(document.getElementById('myCanvas'), 500, 500);
```

### Properties

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



<a name="fill" href="#fill">#</a> rough.<b>fill</b>

String value representing the color to fill a shape. 



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

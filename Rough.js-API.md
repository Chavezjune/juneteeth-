The main object to work with is RoughCanvas. This canvas object can  be used to create different shapes, lines, curves and paths. 

The canvas object has properties that can be used to configure the overall style (default style) of all the objects drawn on it. For example, changing the fill-color or the stroke-width will change the fill-color and stroke-width of all the objects. Individual objects can override these properties. 

## RoughCanvas

<a name="constructor" href="#constructor">#</a> <b>RoughCanvas</b>(<i>canvasElement</i>, <i>width</i>, <i>height</i>)

Instantiate RoughCanvas by passing in the canvas node and the dimensions of the canvas. The constructor will resize the canvas element. 

```js
var rc = new RoughCanvas(document.getElementById('myCanvas'), 500, 500);
```

### Properties

<a name="max" href="#max">#</a> d3.<b>max</b>(<i>array</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/max.js "Source")

Returns the maximum value in the given *array* using natural order. If the array is empty, returns undefined. An optional *accessor* function may be specified, which is equivalent to calling *array.map(accessor)* before computing the maximum value.

## API


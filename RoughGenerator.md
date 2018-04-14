When a shape is drawn using RoughJS, a lot of randomization is used to create the sketchy look and feel. There are times when you want to maintain the initially rendered shape, i.e. not randomize again on subsequent redraws. (See this [issue](https://github.com/pshihn/rough/issues/27)).

This is where generators come in. **RoughGenerator** has the same api as [RoughCanvas](https://github.com/pshihn/rough/wiki#roughcanvas) but it does not actually draw the shape - it returns the set of instructions to draw that sketchy shape at a later stage. This object (with instructions) is what we're calling a *drawable*.

Generators are also useful when creating shapes without an actual drawing context; for example, on the server or in a web worker.

## Instantiating RoughGenerator
You can get the generator from your RoughCanvas, RoughSVG object, or from the root rough object.
If your code is running in an environment without HTML Canvas (background worker or on the server), you can use the last option to generate sketchy shapes without actually drawing them on a canvas

```javascript
let roughCanvas = rough.canvas(document.getElementById('myCanvas'), config);
let generator = roughCanvas.generator;
```
```javascript
let generator = rough.generator(config, size);
```

The [config](https://github.com/pshihn/rough/wiki#config) is the same object used when creating RoughCanvas.
The *size* object suggests a size of the canvas when drawing without an actual canvas.

```javascript
let generator = rough.generator(config, { width: 600, height: 600 });
```

## Using generators and drawables

Get the *drawable* from the generator and then later pass the drawable to RoughCanvas' **draw** method

```javascript
let rect1 = generator.rectangle(10, 10, 100, 100);
let rect2 = generator.rectangle(10, 120, 100, 100, {fill: 'red'});
roughCanvas.draw(rect1);
roughCanvas.draw(rect2);
```

## Remembering shapes without generators

RoughCanvas also returns the *drawable* object when drawing a shape. This can be used later using the **draw** method

```javascript
let shape = roughCanvas.rectangle(10, 10, 100, 100);
// After some time, clear canvas and draw the same shape again
roughCanvas.draw(shape);
```

## Persisting Shapes

The *drawable* object is serializable. You can store these generated shapes as JSON in a file/database.
```javascript
let rect = generator.rectangle(10, 10, 100, 100);
store(JSON.stringify(rect));
```

## SVG Path info
Generator has a **toPaths(drawable)** method that turns a drawable into PathInfo objects
```javascript
let rect = generator.rectangle(10, 10, 100, 100, {fill: 'red'});
let paths = generator.toPaths(rect);
```
*paths* here is an array of PathInfo objects.

**Note:** The paths must be rendered in the same order as they are returned. 

### PathInfo
Path info object represents all the information you may need to render a shape to a SVG Path.

It has following members:

**d:** A string containing a series of path descriptions.

**stroke:** Stroke color of the path.

**strokeWidth:**  Stroke width to use for the path.

**fill:** Color used to fill the path.

**pattern:** Object describing the pattern to fill the path with (PatternInfo).

Note: Only _fill_ or _pattern_ is specified in a PathInfo instance. Never both. 

### PatternInfo
This object describes the [pattern](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/pattern) to use to fill a path.

Members:
**height:** Height attribute.

**width:** Width attribute.

**x:** x attribute.

**y:** y attribute.

**viewBox:** viewBox attribute to use for this pattern.

**path:** PathInfo object to use as the pattern.



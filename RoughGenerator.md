When a shape is drawn using RoughJS, a lot of randomization is used to create the sketchy look and feel. There are times when you want to maintain the initially rendered shape, i.e. not randomize again on subsequent redraws. (See this [issue](https://github.com/pshihn/rough/issues/27)).

This is where generators come in. **RoughGenerator** has the same api as [RoughCanvas](https://github.com/pshihn/rough/wiki#roughcanvas) but it does not actually draw the shape - it returns the set of instructions to draw that sketchy shape at a later stage. This object (with instructions) is what we're calling a *drawable*.

## Instantiating RoughGenerator
You can get the generator from the canvas object or from the root rough object.
If your code is running in an environment without HTML Canvas (background worker or on the server), you can use the second option to generate sketchy shapes without actually drawing them on a canvas

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

The *drawable* object is serializable. So, you can store these generated shapes as JSON in a file/database.
```javascript
```


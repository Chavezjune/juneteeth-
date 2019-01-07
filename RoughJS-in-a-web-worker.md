If you want to delegate most of RoughJS computation to a [web worker](https://developer.mozilla.org/en-US/docs/Web/API/Worker) thread, it is really simple. 

Use the *rough-async* distributable, and pass the URL to *worker.js* distributed with RoughJS.

```html
<script src="https://rawgit.com/pshihn/rough/master/dist/rough-async.js"></script>
```
```javascript
let canvas = rough.canvas(canvasNode, { workerURL: './worker.js' });
```

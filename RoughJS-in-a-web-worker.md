If you want to delegate most of RoughJS computation to a [web worker](https://developer.mozilla.org/en-US/docs/Web/API/Worker) thread, it is really simple. 

Simply include [Workly](https://github.com/pshihn/workly) (only ~1kb in size) in your page, and RoughJS will automatically move most of the processing to a worker. 

```html
<script src="https://cdn.jsdelivr.net/gh/pshihn/workly/dist/workly.min.js"></script>
```

If you want to use workly, but not use the default CDN to load it in the web worker, pass the URL to RoughCanvas at instantiation.

```html
<script src="{Custom URL for Workly}"></script>
```
```javascript
let canvas = rough.canvas(canvasNode, { worklyURL: customURL });
```

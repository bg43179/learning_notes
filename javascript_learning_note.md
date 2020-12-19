## Events:
- capturing (trickling): from top(outermost) to button(innermost)
- bubbling: from button(innermost) to top(outermost)

```javascript
addEventListner(type, listener, useCapture)
```

> Bubbling by default, set `true` for useCapture to enable capturing

It's used to determine the exection order of events
```html
<div id="outer">
  <div id="middle">
    <a href="" id="inner" >click</a>
  </div>
</div>
```

```javascript
var outer = document.getElementById('outer');
var middle = document.getElementById('middle');
var inner = document.getElementById('inner');

outer.addEventListener('click',
  () => console.log('trigger outer div'), true);
middle.addEventListener('click',
  () => console.log('trigger middle div'), true);
inner.addEventListener('click',
  () => console.log('trigger inner button'), true);
```

Since the `useCapture` is `true`, it will trigger events from outermost to innermost on click the anchor tag.

```javascript
// output
trigger outer div
trigger middle div
```

### e.preventDefault
> Why was innermost not trigged here?

Becasue empty anchor tag will redirect to the current page by default,so it stopped the event chain. We can use `e.stopPreventDefault` here to get rid of the default behavior.

```javascript
inner.addEventListener('click',
  (e) => {
    e.preventDefault();
    console.log('trigger inner button');
  }, true));

//  and the output will be
trigger outer div
trigger middle div
trigger middle button
```

### e.stopPropgagtion:
> What if we want to click outer div but prevent midde div, inner button be triggered?

By using `stopPropgagtion`, we can stop the event chain.
```javascript
outer.addEventListener('click',
  (e) => {
    e.stopPropgagtion();
    console.log('trigger outer div');
  }, true));

//  and the output will be
trigger outer div
```

[Reference](https://segmentfault.com/a/1190000008227026)
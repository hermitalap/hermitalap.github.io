# 

#### html2canvas
根据元素将网页上的内容转换为canvas对象
[html2canvas](http://html2canvas.hertzen.com/)
```html
<div id="capture" style="padding: 10px; background: #f5da55">
    <h4 style="color: #000; ">Hello world!</h4>
</div>
```

```javascript
html2canvas(document.querySelector("#capture")).then(canvas => {
    document.body.appendChild(canvas)
});
```


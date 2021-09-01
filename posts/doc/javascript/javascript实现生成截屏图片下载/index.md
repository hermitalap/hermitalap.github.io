# 

### 实现方法
[[html2canvas]]
[[Canvas2Image]]
### 实例
```html
<body>
<div class="demo-container">
    <div id="capture" id="demo">
        <div class="red"></div>
        <p>如果原来使用百分比设置元素宽高，请更改为px为单位的宽高，避免样式二次计算导致的模糊</p>
        <p>如果原来使用百分比设置元素宽高，请更改为px为单位的宽高，避免样式二次计算导致的模糊</p>
        <p>如果原来使用百分比设置元素宽高，请更改为px为单位的宽高，避免样式二次计算导致的模糊</p>
        <p>如果原来使用百分比设置元素宽高，请更改为px为单位的宽高，避免样式二次计算导致的模糊</p>
        <p>如果原来使用百分比设置元素宽高，请更改为px为单位的宽高，避免样式二次计算导致的模糊</p>
    </div>		
</div>
<button id="saveImg">截图并下载</button>
</body>
<!-- <script src="./canvas2image.js"></script> -->
<script src="https://superal.github.io/canvas2image/canvas2image.js"></script>
<script src="./html2canvas.min.js"></script>

<script>
    var btn = document.getElementById("saveImg");  
    btn.onclick =function(){
    html2canvas(document.querySelector("#capture")).then(canvas => {
        
        var context = canvas.getContext('2d')
        // 【重要】关闭抗锯齿
        context.mozImageSmoothingEnabled = false
        context.webkitImageSmoothingEnabled = false
        context.msImageSmoothingEnabled = false
        context.imageSmoothingEnabled = true

        var img = Canvas2Image.convertToJPEG(canvas, canvas.width/2, canvas.height/2)
        let dataURL = img.getAttribute('src')
        document.body.appendChild(img)
        // 下载图片
        let a = document.createElement('a')
        a.context = "下载"
        document.body.appendChild(a)
        a.href = img.src
        // 设置下载标题
        a.download = "pic.jpg"
        a.click()

    });
    }
</script>

```

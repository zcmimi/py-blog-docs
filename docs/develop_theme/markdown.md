提供了过滤器`markdown`与`markdown_math`

在模板中可以使用:

`text|markdown`将`text`从`markdown`源码转换为`HTML`

`text|markdown_math`在`markdown`的基础上添加了`LaTeX`支持:

行内公式: `$...$` -> `<code><latex>...</latex>`

行间公式: `$$...$$` -> `<code><latex_display>...</latex_display>`

## 使用`katex`渲染公式

### 在`head`中引入`katex.js`

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex/dist/katex.min.css">
<script src="https://cdn.jsdelivr.net/npm/katex/dist/katex.min.js"></script>
```

### 渲染函数

```javascript
function katex_(){
    if(typeof(katex)=='undefined')return;
    document.querySelectorAll('code latex').forEach((x)=>{
        var y=document.createElement('span');
        katex.render(x.innerText,y,{throwOnError: false});
        x.parentElement.replaceWith(y.children[0]);
    });
    document.querySelectorAll('code latex_display').forEach((x)=>{
        var y=document.createElement('span');
        katex.render(x.innerText,y,{displayMode:true,throwOnError: false});
        x.parentElement.replaceWith(y.children[0]);
    });
}
```
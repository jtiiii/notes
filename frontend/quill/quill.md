# Quill 入门笔记

官网地址：https://quilljs.com

## Quill 是什么？

quill是一款轻量强大的html-text编辑器。



## 安装

### CDN

```html
<!-- Main Quill library -->
<script src="//cdn.quilljs.com/1.3.6/quill.js"></script>
<script src="//cdn.quilljs.com/1.3.6/quill.min.js"></script>

<!-- Theme included stylesheets -->
<link href="//cdn.quilljs.com/1.3.6/quill.snow.css" rel="stylesheet">
<link href="//cdn.quilljs.com/1.3.6/quill.bubble.css" rel="stylesheet">

<!-- Core build with no theme, formatting, non-essential modules -->
<link href="//cdn.quilljs.com/1.3.6/quill.core.css" rel="stylesheet">
<script src="//cdn.quilljs.com/1.3.6/quill.core.js"></script>
```



### NPM

```shell
$npm install quill
```



### Source

```shell
$git clone git@github.com:quilljs/quill.git
```



## 快速使用

```js
var quill = new Quill('#editor', {
    theme: 'snow'
});

/* ------------ */
var container = document.getElementById('editor');
var quill = new Quill(container,{ theme: 'snow'});
```

## 配置项

```javascript
new Quill(container, options);
```

+ container : 容器
+ options: 参数

### Options

| 参数名               | 默认值          | 说明                                                  |
| -------------------- | --------------- | ----------------------------------------------------- |
| `bounds`             | `document.body` | dom选择器                                             |
| `debug`              | `warn`          | 调试信息，默认输出warn和erro信息                      |
| `formats`            | All formats     | 格式，默认附带所有格式化策略,详细阅读[此处](#formats) |
| `modules`            | None            |                                                       |
| `placeholder`        | None            | 当无任何文字输入的时候展示                            |
| `scrollingContainer` | `null`          |                                                       |
| `themes`             | None            | 外观主题，官方原生支持两种主题：`snow`和`bubble`      |



#### formats

Quill具备多种格式化策略

暂略



### Api

Quill 提供了
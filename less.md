less工具介绍
==========

* 安装.less文件编译环境

LESSCSS官方有一款基于Node.js的库，用于编译.less文件。

使用时，首先全局安装less（部分系统下可能需要在前面加上sudo切换为超级管理员权限）

node安装：
```javascript
npm install -g less
```

编译.less文件命令
```javascript
lessc test.less test.css
```

* less相关语法

- 变量

变量允许我们单独定义一系列通用的样式，然后在需要的时候去调用。所以在做全局样式调整的时候我们可能只需要修改几行代码就可以了。

LESS源码：
```css
@color: #4D926F;

#header {
    color: @color;
}
h2 {
    color: @color;
}
```
编译后的CSS：
```css
#header {
    color: #4D926F;
}
h2 {
    color: #4D926F;
}
```

- 混合(Mixins)

混合可以将一个定义好的class A轻松的引入到另一个class B中，从而简单实现class B继承class A中的所有属性。我们还可以带参数地调用，就像使用函数一样。

LESS源码：
```css
.rounded-corners (@radius: 5px) {
    -webkit-border-radius: @radius;
    -moz-border-radius: @radius;
    -ms-border-radius: @radius;
    -o-border-radius: @radius;
    border-radius: @radius;
}

#header {
    .rounded-corners;
}
#footer {
    .rounded-corners(10px);
}
```

编译后的CSS：
```css
#header {
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    -ms-border-radius: 5px;
    -o-border-radius: 5px;
    border-radius: 5px;
}
#footer {
    -webkit-border-radius: 10px;
    -moz-border-radius: 10px;
    -ms-border-radius: 10px;
    -o-border-radius: 10px;
    border-radius: 10px;
}
```

- 嵌套

我们可以在一个选择器中嵌套另一个选择器来实现继承，这样很大程度减少了代码量，并且代码看起来更加的清晰。

LESS源码：
```css
#header {
    h1 {
        font-size: 26px;
        font-weight: bold;
    }
    p {
        font-size: 12px;
        a {
            text-decoration: none;
            &:hover {
                border-width: 1px
            }
        }
    }
}
```
编译后的CSS：
```css
#header h1 {
    font-size: 26px;
    font-weight: bold;
}
#header p {
    font-size: 12px;
}
#header p a {
    text-decoration: none;
}
#header p a:hover {
    border-width: 1px;
}
```

- 函数和运算

运算提供了加，减，乘，除操作；我们可以做属性值和颜色的运算，这样就可以实现属性值之间的复杂关系。LESS中的函数一一映射了JavaScript代码，如果你愿意的话可以操作属性值。

LESS源码：
```css
@the-border: 1px;
@base-color: #111;
@red:        #842210;

#header {
    color: (@base-color * 3);
    border-left: @the-border;
    border-right: (@the-border * 2);
}
#footer {
    color: (@base-color + #003300);
    border-color: desaturate(@red, 10%);
}
```
编译后的CSS：
```css
#header {
    color: #333;
    border-left: 1px;
    border-right: 2px;
}
#footer {
    color: #114411;
    border-color: #7d2717;
}
```

更多语法说明可以参阅 <a href="http://lesscss.net/article/document.html" target="_blank">LESSCSS语法中文说明文档</a>

# less 火狐浏览器下调试
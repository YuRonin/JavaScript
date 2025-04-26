# 声明变量时优先使用 `const`

在声明变量时，优先使用 `const`。如果发现变量需要被修改，再改为 `let`。

## 为什么 `const` 声明的对象可以修改其属性？

这是因为对象是引用类型，存储的是地址。只要地址不变，就不会报错。因此，建议使用 `const` 来声明数组和对象。

### 示例

#### 数组

```javascript
const arr = [1, 2, 3];
arr.push(4); // 不会报错
arr = [1, 2, 3, 4]; // 会报错（因为这是重新定义了一个数组）
```

#### 对象

```javascript
const obj = {
    name: '123',
    age: 14,
};
obj.school = "星星小学"; // 不会报错
obj = {
    name: '123',
    age: 14,
    school: '星星小学',
}; // 会报错
```

# `DOM树`和`DOM对象`

## 作用和分类

作用：就是使用JS去操作html和浏览器
分类：`DOM`（文档对象模型），`BOM`（浏览器对象模型）

### `DOM`

用来操作HTML或者XML文档交互的API
DOM是浏览器提供一套专门用来操作网页内容的功能

#### `DOM作用`
开发网页内容特效和用户交互

#### `DOM`树
1. 将HTML文档以树的结构表现出来，我们称作为DOM树
2. 描述网页内容关系的名词
3. 作用：文档树直观的体现了标签与标签之间的关系

#### `DOM`对象
1. 将浏览器根据HTML标签生成JS对象
2. 所有的标签属性都可以在这对象上找到
3. 修改这个对象的属性会自动映射到这个标签上

#### `document`是什么
1. DOM提供的一个对象
2. 网页所有内容都在document里面

# 获取`DOM元素`

## 获取一个DOM元素
使用`document.querySelector('')`
可以直接对`DOM元素`修改

## 获取多个DOM元素
使用`document.querySelectorAll('')`
不可以直接对`DOM元素`修改，因为获取的是数组
伪数组没法使用`pop()` `push()`等方法

### 对里面`DOM元素`进行修改
需要对里面进行遍历，获取到里面的对象，才能进行修改

## 其他获取DOM元素方法（早期）

```javascript
document.getElementById('') //通过id获取第一个元素
document.getElementsByTagName('') //根据标签获取一类元素
document.getElementsByClassName('') //根据类名获取所有元素
```

# 修改`DOM元素`内容

## .innerHTML

`.innerHTML` 是一个属性，用于获取或设置元素的 HTML 内容。  
它可以直接插入 HTML 代码，适合需要动态生成复杂结构的场景。

### 示例

```javascript
const element = document.querySelector('#example');

element.innerHTML = '<p>这是一个段落</p>';

console.log(element.innerHTML); // 输出：<p>这是一个段落</p>
```

### 注意事项
1. 使用 `.innerHTML` 会覆盖元素内部的所有内容。
2. 如果插入的 HTML 包含用户输入，可能会导致 XSS（跨站脚本攻击）风险。

## .innerText

`.innerText` 是一个属性，用于获取或设置元素的文本内容。  
它会忽略 HTML 标签，仅操作纯文本，适合需要显示或修改文本的场景。

### 示例

```javascript
const element = document.querySelector('#example');

element.innerText = '这是纯文本内容';

console.log(element.innerText); // 输出：这是纯文本内容
```

### 注意事项
1. `.innerText` 会自动忽略 HTML 标签，仅保留文本。
2. 它会受到 CSS 样式（如 `display: none`）的影响，隐藏的内容不会被获取。

# H5自定义属性
data-自定义属性
在标签上一律以data-开头
在DOM对象上一律以dataset对象方式获取

# 事件监听

## 语法
元素对象.addEventListener('事件类型',要执行的函数);

## 事件监听版本

### on
事件源.on事件 = function() {}

### addEventListener
事件源.addEventListener(事件，事件处理函数)

### 区别：
on方式会被覆盖，addEventListener方式可以绑定多次，拥有事件更多特性，推荐使用

## 事件类型
1. 鼠标触发
click 鼠标点击
mouseenter 鼠标经过
mouseleave 鼠标离开

2. 表单获得光标
focus 获得焦点
blur 失去焦点

3. 键盘触发
keydown 键盘按下触发
keyup 键盘抬起触发

4. 表单输入触发
input 用户输入事件

# 事件对象

## 获取事件对象

### 事件对象
也是对象，对象里面有事件触发时的相关信息
例如鼠标点击事件中，事件对象就存了鼠标点在哪个位置等信息

### 使用场景
可以判断用户按下哪个键，比如按下回车键可以发布新闻
可以判断鼠标点击了哪个元素，从而做相应的操作

# 环境对象
环境对象：值得是函数内部特殊的变量this，它代表这当前函数运行时处在的环境
每个函数里面都有this 环境对象
普通函数里面this指向的是window

## 作用
函数的调用方式不同，this指向的对象也不同

# 回调函数
函数A作为传递给函数B，我们称函数A为回调函数
通俗易懂：当一个函数当作参数来传递给另外一个函数的时候，这个函数就是回调函数

# 事件流、事件捕获、事件冒泡

## 事件流和两个阶段说明

### 事件流
指的是事件完整执行过程中的流动路径

#### 说明
1. 假设页面有个div，当触发事件时候，会经历两个阶段，分别是捕获阶段、冒泡阶段
2. 简单来说：捕获阶段是从父到子，冒泡阶段是从子到父
3. 实际工作都是使用事件冒泡为主

## 事件捕获

### 概念
从DOM的根元素开始去执行对应的事件（从外到里）
事件捕获需要写对应代码才能看到效果

### 代码
DOM.addEventListener(事件类型, 事件处理函数, 是否使用捕获机制)

### 说明
1. 第三个参数传入true，代表是捕获阶段触发
2. 若传入false代表冒泡阶段触发，默认就是false
3. 若使用L0事件监听，则只有冒泡阶段，没有捕获

## 事件冒泡

### 概念
当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发，这一过程被称为事件冒泡
简单理解：当一个元素触发事件后，会依次向上调用所有父级元素的同名事件

## 阻止冒泡

事件对象.stopPropagation()

### 注意
从此方法可以阻断事件流动传播，不光在冒泡阶段有效，捕获阶段也有效果

## 解绑事件
on事件，直接使用null覆盖就可以实现事件的解绑
addEventListener方式，必须使用removeEventListener（事件类型，事件处理函数，[获取捕获或者冒泡阶段]） 需要注意匿名函数无法解绑

## 鼠标经过事件的区别

### 鼠标经过事件
mouseover和mouseout会有冒泡效果
mouseenter和mouseleave没有冒泡效果（推荐）

# 事件委托
事件委托是利用事件流的特征解决一些开发需求的知识技巧

## 优点：
减少注册次数，可以提高程序性能

## 原理：
事件委托其实是利用事件冒泡的特定
给父元素注册事件，当我们触发子元素的时候，会冒泡到父元素身上，从而触发父元素的事件

## 如何找到真正触发元素
事件对象.target.tagName

# 阻止默认行为
我们某些情况下需要组织默认行为的发生，比如组织连接的跳转，表单域跳转

## 语法
事件对象.preventDefault()

# 页面加载事件
加载外部资源（如图片、外联CSS和Js等）加载完毕时触发的事件

## 为什么要学？
有些时候需要等页面资源全部处理完了做一些事件
老代码喜欢把script写在head中，这时候找DOM元素找不到

## 事件名`Load`

## 监听页面所有资源加载完毕
等待页面所有资源加载完毕后，就回去执行回调函数
window.addEventListener('load',function() {

})

## DOMContentLoaded事件
事件被触发，而无需等待样式表、图像等完全加载
document.addEventListener('DOMContentLoaded',function() {

})

# 页面滚动事件
滚动条在滚动的时候持续触发的事件

## 事件名`scroll`

## 监听整个页面滚动
document.addEventListener('scroll', function() {

})

## 被卷去头部或者左侧是哪个属性
scrollTop / scrollLeft
可以读取，也可以修改

## 检测页面滚动的头部距离（被卷去的头部）用那个属性
document.documentElement.scrollTop

# 页面尺寸事件

## 窗口尺寸改变时候触发的事件
window.addEventListener('resize', function() {

})

## 获取元素宽高
获取元素的可见不分宽高（不包含边框，margin，滚动条等）
clientWidth和clientHeight

## 元素尺寸与位置

### 获取宽高
获取元素的自身宽高、包含元素自身位置的宽高、padding、border
offestWidth和offsetHeight
获取出来的是数值，方便计算
注意：获取的是可视宽高，如果盒子是隐藏的，获取的结果是0

### 获取位置
获取元素距离自己定位父级元素的左、上距离
offsetLeft和offsetTop 注意是只读属性

# 日期对象的使用

## 日期对象
用来表示时间的对象

## 作用
可以得到当前系统的时间

## 实例化
在代码用new关键字的，都称作为实例化

## 获取当前时间
const data = new Date();

## 日期对象方法
因为日期对象返回的数据我们不能直接使用，所以需要转换为实际开发中常用的格式
`getFullYear()` 获取年份 获取四位年份
`getMonth()` 获取月份 取值为0~11
`getDate()` 获取月份中的每一天 不同月份取值也不相同
`getDay()` 获取星期 取值为0~6
`getHours()` 获取小时 取值为0~23
`getMinutes()` 获取分钟 取值为0~59
`getSeconds()` 获取秒 取值为0~59

`toLocaleString()` 获取年月日 时分秒以字符串的形式输出

# 时间戳
三种方式获得时间戳
1. 使用getTime()方法
`````javascript
const date = new Date()
console.log(date.getTime())
`````

2. 简写 +new Date()
`````javascript
console.log(+new Date())
`````

3. 使用Date.now()
无需实例化
智能得到当前的时间戳，前面两种可以返回指定时间的时间戳

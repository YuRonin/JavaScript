# JavaScript 变量声明

## 使用 `const` 优先声明变量

- 优先使用 `const` 声明变量。
- 如果变量需要被修改，再改为 `let`。

### 为什么 `const` 声明的对象可以修改其属性？

- 对象是引用类型，存储的是地址。
- 只要地址不变，就不会报错。
- 建议使用 `const` 声明数组和对象。

#### 示例

##### 数组

```javascript
const arr = [1, 2, 3];
arr.push(4); // 不会报错
arr = [1, 2, 3, 4]; // 会报错（重新定义了一个数组）
```

##### 对象

```javascript
const obj = { name: '123', age: 14 };
obj.school = "星星小学"; // 不会报错
obj = { name: '123', age: 14, school: '星星小学' }; // 会报错
```

---

# DOM 和 BOM

## DOM 树与 DOM 对象

### DOM 树

- 将 HTML 文档以树的结构表现出来。
- 描述网页内容关系的名词。
- 作用：直观体现标签之间的关系。

### DOM 对象

- 浏览器根据 HTML 标签生成的 JS 对象。
- 修改对象属性会自动映射到标签上。

### `document` 对象

- DOM 提供的一个对象。
- 网页所有内容都在 `document` 中。

---

# 获取 DOM 元素

## 单个 DOM 元素

- 使用 `document.querySelector('')`。

## 多个 DOM 元素

- 使用 `document.querySelectorAll('')`。
- 返回伪数组，需遍历后修改。

### 早期方法

```javascript
document.getElementById(''); // 通过 id 获取
document.getElementsByTagName(''); // 根据标签获取
document.getElementsByClassName(''); // 根据类名获取
```

---

# 修改 DOM 元素内容

## `.innerHTML`

- 获取或设置元素的 HTML 内容。
- 可插入 HTML 代码。

### 示例

```javascript
const element = document.querySelector('#example');
element.innerHTML = '<p>这是一个段落</p>';
```

### 注意事项

1. 会覆盖元素内部所有内容。
2. 插入用户输入的 HTML 可能导致 XSS 风险。

## `.innerText`

- 获取或设置元素的纯文本内容。
- 忽略 HTML 标签。

### 示例

```javascript
const element = document.querySelector('#example');
element.innerText = '这是纯文本内容';
```

### 注意事项

1. 忽略 HTML 标签，仅保留文本。
2. 受 CSS 样式影响，隐藏内容不会被获取。

---

# H5 自定义属性

- 以 `data-` 开头。
- 在 DOM 对象中通过 `dataset` 获取。

---

# 事件监听

## 语法

```javascript
元素对象.addEventListener('事件类型', 要执行的函数);
```

## 事件监听方式

### `on` 方式

- `事件源.on事件 = function() {}`

### `addEventListener` 方式

- `事件源.addEventListener(事件, 事件处理函数)`

### 区别

- `on` 方式会被覆盖。
- `addEventListener` 可绑定多次，推荐使用。

---

# 事件对象

## 获取事件对象

- 事件对象存储事件触发时的相关信息。

### 使用场景

- 判断用户按下的键。
- 判断鼠标点击的元素。

---

# 环境对象

- 函数内部特殊变量 `this`。
- 指向当前函数运行的环境。

---

# 回调函数

- 函数 A 作为参数传递给函数 B，称函数 A 为回调函数。

---

# 事件流

## 阶段说明

1. 捕获阶段：从父到子。
2. 冒泡阶段：从子到父（实际工作中以冒泡为主）。

## 事件捕获

- 从 DOM 根元素开始执行事件（从外到里）。

### 示例

```javascript
DOM.addEventListener(事件类型, 事件处理函数, true);
```

## 事件冒泡

- 事件从子元素向父元素传播。

### 阻止冒泡

```javascript
事件对象.stopPropagation();
```

---

# 事件委托

- 利用事件冒泡特性，将事件绑定到父元素。

### 优点

- 减少注册次数，提高性能。

### 获取触发元素

```javascript
事件对象.target.tagName;
```

---

# 阻止默认行为

- 使用 `事件对象.preventDefault()`。

---

# 页面加载事件

## `load` 事件

- 等待页面所有资源加载完毕后触发。

### 示例

```javascript
window.addEventListener('load', function() {});
```

## `DOMContentLoaded` 事件

- 不等待样式表、图像等加载完毕。

### 示例

```javascript
document.addEventListener('DOMContentLoaded', function() {});
```

---

# 页面滚动事件

## `scroll` 事件

- 滚动条滚动时触发。

### 示例

```javascript
document.addEventListener('scroll', function() {});
```

### 获取滚动距离

- `document.documentElement.scrollTop`

---

# 页面尺寸事件

## `resize` 事件

- 窗口尺寸改变时触发。

### 示例

```javascript
window.addEventListener('resize', function() {});
```

## 获取元素宽高

- `clientWidth` 和 `clientHeight`：可见部分宽高。
- `offsetWidth` 和 `offsetHeight`：包含边框和 padding 的宽高。

---

# 日期对象

## 获取当前时间

```javascript
const date = new Date();
```

## 常用方法

- `getFullYear()`：获取年份。
- `getMonth()`：获取月份（0~11）。
- `getDate()`：获取日期。
- `getDay()`：获取星期（0~6）。
- `getHours()`：获取小时。
- `getMinutes()`：获取分钟。
- `getSeconds()`：获取秒。

---

# 时间戳

## 获取时间戳的三种方式

1. 使用 `getTime()` 方法：

```javascript
const date = new Date();
console.log(date.getTime());
```

2. 简写 `+new Date()`：

```javascript
console.log(+new Date());
```

3. 使用 `Date.now()`：

```javascript
console.log(Date.now());
```

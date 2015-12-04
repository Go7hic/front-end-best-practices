# front-end-best-practices
一些前端的最佳实践，包括 html,css,javascript


## HTML

### 语义

HTML5为我们提供大量的语义元素的目的就是为了准确地描述内容，确保你受益于其丰富的词汇。

```html
<!-- bad -->
<div id="main">
  <div class="article">
    <div class="header">
      <h1>Blog post</h1>
      <p>Published: <span>21st Feb, 2015</span></p>
    </div>
    <p>…</p>
  </div>
</div>

<!-- good -->
<main>
  <article>
    <header>
      <h1>Blog post</h1>
      <p>Published: <time datetime="2015-02-21">21st Feb, 2015</time></p>
    </header>
    <p>…</p>
  </article>
</main>
```

确保你了解你使用的语义元素。错误的方式使用语义元素是很糟糕的。

```html
<!-- bad -->
<h1>
  <figure>
    <img alt=Company src=logo.png>
  </figure>
</h1>

<!-- good -->
<h1>
  <img alt=Company src=logo.png>
</h1>
```

### 简洁

保持代码简洁。忘记你的旧 XHTM L的习惯。

```html
<!-- bad -->
<!doctype html>
<html lang=en>
  <head>
    <meta http-equiv=Content-Type content="text/html; charset=utf-8" />
    <title>Contact</title>
    <link rel=stylesheet href=style.css type=text/css />
  </head>
  <body>
    <h1>Contact me</h1>
    <label>
      Email address:
      <input type=email placeholder=you@email.com required=required />
    </label>
    <script src=main.js type=text/javascript></script>
  </body>
</html>

<!-- good -->
<!doctype html>
<html lang=en>
  <meta charset=utf-8>
  <title>Contact</title>
  <link rel=stylesheet href=style.css>

  <h1>Contact me</h1>
  <label>
    Email address:
    <input type=email placeholder=you@email.com required>
  </label>
  <script src=main.js></script>
</html>
```

### 可访问性

可访问性不应该是后面来做的事。你也不必是一个WCAG专家来提高你的
网站,你可以立即修复小事情,就会有巨大的差别,如:
- 学习正确使用“alt”属性
- 确保你的链接和按钮等标记(没有“< div class = button”暴行)
- 不是完全依赖颜色信息交流
- 明确标签表单控件

```html
<!-- bad -->
<h1><img alt="Logo" src="logo.png"></h1>

<!-- good -->
<h1><img alt="My Company, Inc." src="logo.png"></h1>
```

### 语言编码


虽然语言和字符编码的定义是可选的,它总是推荐声明在文档级别,即使他们HTTP头中指定。在其它任何支持utf - 8
字符编码。

```html
<!-- bad -->
<!doctype html>
<title>Hello, world.</title>

<!-- good -->
<!doctype html>
<html lang=en>
  <meta charset=utf-8>
  <title>Hello, world.</title>
</html>
```

### 性能

除非在有一个有效的理由加载脚本内容之前,不要阻止呈现的页面。如果您的样式文件很大,绝对孤立的样式最初和推迟装运所需的二次声明在一个单独的样式表。
两个HTTP请求要慢得多,但速度是最的感知
重要的因素。

```html
<!-- bad -->
<!doctype html>
<meta charset=utf-8>
<script src=analytics.js></script>
<title>Hello, world.</title>
<p>...</p>

<!-- good -->
<!doctype html>
<meta charset=utf-8>
<title>Hello, world.</title>
<p>...</p>
<script src=analytics.js></script>
```

## CSS

### 分号

分号在技术上是一个分离器,总是把它当作终结者。

```css
/* bad */
div {
  color: red
}

/* good */
div {
  color: red;
}
```

### 盒模型

盒子模型应该为整个文档是一样的。一个全局
“* { box-sizing:border-box;}”是可以的,但不要改变默认的盒模型
如果你能避免它在特定的元素。

```css
/* bad */
div {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
}

/* good */
div {
  padding: 10px;
}
```

### 流

如果你能避免最好不要改变一个元素的默认行为。尽可能的保持元素
自然文档流。例如,删除图像下的 white-space 不应该让你改变其默认显示:

```css
/* bad */
img {
  display: block;
}

/* good */
img {
  vertical-align: middle;
}
```

同样的,如果你能避免最好不要把一个元素脱离文档流。

```css
/* bad */
div {
  width: 100px;
  position: absolute;
  right: 0;
}

/* good */
div {
  width: 100px;
  margin-left: auto;
}
```

### 定位

css有很多方法来定位元素，但是最好使用下面的属性/值，按照优先顺序:

```
display: block;
display: flex;
position: relative;
position: sticky;
position: absolute;
position: fixed;
```

### 选择器

减少选择器紧密耦合的DOM。考虑添加一个类的元素你想当你超过3结构伪类选择器匹配,或后代
兄弟姐妹组合子。

```css
/* bad */
div:first-of-type :last-child > p ~ *

/* good */
div:first-of-type .info
```

避免重载你的选择器在你不需要的时候。

```css
/* bad */
img[src$=svg], ul > li:first-child {
  opacity: 0;
}

/* good */
[src$=svg], ul > :first-child {
  opacity: 0;
}
```

### 特殊点

不要让值和选择器难以覆盖。减少使用id和
避免“!important”。
```css
/* bad */
.bar {
  color: green !important;
}
.foo {
  color: red;
}

/* good */
.foo.bar {
  color: green;
}
.foo {
  color: red;
}
```

### Overriding

Overriding的样式让选择器和调试困难。尽可能的避免它。
```css
/* bad */
li {
  visibility: hidden;
}
li:first-child {
  visibility: visible;
}

/* good */
li + li {
  visibility: hidden;
}
```

### 继承

不要重复声明样式,可以继承的。

```css
/* bad */
div h1, div p {
  text-shadow: 0 1px 0 #fff;
}

/* good */
div {
  text-shadow: 0 1px 0 #fff;
}
```

### 简洁

保持代码简洁。尽可能的使用简写属性,避免使用多个属性。


```css
/* bad */
div {
  transition: all 1s;
  top: 50%;
  margin-top: -10px;
  padding-top: 5px;
  padding-right: 10px;
  padding-bottom: 20px;
  padding-left: 10px;
}

/* good */
div {
  transition: 1s;
  top: calc(50% - 10px);
  padding: 5px 10px 20px;
}
```

### 语言编码

只能是英语和数字

```css
/* bad */
:nth-child(2n + 1) {
  transform: rotate(360deg);
}

/* good */
:nth-child(odd) {
  transform: rotate(1turn);
}
```

### 前缀

积极除掉过时的前缀。如果你需要使用它们,插入他们的标准属性之前


```css
/* bad */
div {
  transform: scale(2);
  -webkit-transform: scale(2);
  -moz-transform: scale(2);
  -ms-transform: scale(2);
  transition: 1s;
  -webkit-transition: 1s;
  -moz-transition: 1s;
  -ms-transition: 1s;
}

/* good */
div {
  -webkit-transform: scale(2);
  transform: scale(2);
  transition: 1s;
}
```

### Animations

Favor transitions over animations. Avoid animating other properties than
`opacity` and `transform`.

```css
/* bad */
div:hover {
  animation: move 1s forwards;
}
@keyframes move {
  100% {
    margin-left: 100px;
  }
}

/* good */
div:hover {
  transition: 1s;
  transform: translateX(100px);
}
```

### Units

Use unitless values when you can. Favor `rem` if you use relative units. Prefer seconds over
milliseconds.

```css
/* bad */
div {
  margin: 0px;
  font-size: .9em;
  line-height: 22px;
  transition: 500ms;
}

/* good */
div {
  margin: 0;
  font-size: .9rem;
  line-height: 1.5;
  transition: .5s;
}
```

### Colors

If you need transparency, use `rgba`. Otherwise, always use the hexadecimal format.

```css
/* bad */
div {
  color: hsl(103, 54%, 43%);
}

/* good */
div {
  color: #5a3;
}
```

### Drawing

Avoid HTTP requests when the resources are easily replicable with CSS.

```css
/* bad */
div::before {
  content: url(white-circle.svg);
}

/* good */
div::before {
  content: "";
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
}
```

### Hacks

Don't use them.

```css
/* bad */
div {
  // position: relative;
  transform: translateZ(0);
}

/* good */
div {
  /* position: relative; */
  will-change: transform;
}
```

## JavaScript

### 性能
代码的可读性，正确性，可表达性优于性能。JavaScript 基本上不会有性能上的瓶颈。需要优化的东西像 图片优化，网络请求优化，DOM 渲染优化。如果你要在这个文档记住一条，那就记住这个吧。

```javascript
// bad (albeit way faster)
const arr = [1, 2, 3, 4];
const len = arr.length;
var i = -1;
var result = [];
while (++i < len) {
  var n = arr[i];
  if (n % 2 > 0) continue;
  result.push(n * n);
}

// good
const arr = [1, 2, 3, 4];
const isEven = n => n % 2 == 0;
const square = n => n * n;

const result = arr.filter(isEven).map(square);
```

### Statelessness

Try to keep your functions pure. All functions should ideally produce no side-effects, use no outside data and return new objects instead of mutating existing ones.

```javascript
// bad
const merge = (target, ...sources) => Object.assign(target, ...sources);
merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }

// good
const merge = (...sources) => Object.assign({}, ...sources);
merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }
```

### 原生方法
尽可能的使用语言自带的方法

```javascript
// bad
const toArray = obj => [].slice.call(obj);

// good
const toArray = (() =>
  Array.from ? Array.from : obj => [].slice.call(obj)
)();
```

### 类型转换（隐式转换）

请放心使用类型隐式转换当那样做有意义的时候，虽然说是要避免使用它，但是也不要盲目相信权威。

```javascript
// bad
if (x === undefined || x === null) { ... }

// good
if (x == undefined) { ... }
```

### 循环

Don't use loops as they force you to use mutable objects. Rely on `array.prototype` methods.


```javascript
// bad
const sum = arr => {
  var sum = 0;
  var i = -1;
  for (;arr[++i];) {
    sum += arr[i];
  }
  return sum;
};
sum([1, 2, 3]); // => 6

// good
const sum = arr =>
  arr.reduce((x, y) => x + y);

sum([1, 2, 3]); // => 6
```
If you can't, or if using `array.prototype` methods is arguably abusive, use recursion.

```javascript
// bad
const createDivs = howMany => {
  while (howMany--) {
    document.body.insertAdjacentHTML("beforeend", "<div></div>");
  }
};
createDivs(5);

// bad
const createDivs = howMany =>
  [...Array(howMany)].forEach(() =>
    document.body.insertAdjacentHTML("beforeend", "<div></div>")
  );
createDivs(5);

// good
const createDivs = howMany => {
  if (!howMany) return;
  document.body.insertAdjacentHTML("beforeend", "<div></div>");
  return createDivs(howMany - 1);
};
createDivs(5);
```

Here's a [generic loop function](https://gist.github.com/bendc/6cb2db4a44ec30208e86) making recursion easier to use.

### Arguments

Forget about the `arguments` object. The rest parameter is always a better option because:

1. it's named, so it gives you a better idea of the arguments the function is expecting
2. it's a real array, which makes it easier to use.

```javascript
// bad
const sortNumbers = () =>
  Array.prototype.slice.call(arguments).sort();

// good
const sortNumbers = (...numbers) => numbers.sort();
```

### Apply
忘了 `apply()`吧， 使用 spread operator 代替.

```javascript
const greet = (first, last) => `Hi ${first} ${last}`;
const person = ["John", "Doe"];

// bad
greet.apply(null, person);

// good
greet(...person);
```

### Bind

Don't `bind()` when there's a more idiomatic approach.

```javascript
// bad
["foo", "bar"].forEach(func.bind(this));

// good
["foo", "bar"].forEach(func, this);
```
```javascript
// bad
const person = {
  first: "John",
  last: "Doe",
  greet() {
    const full = function() {
      return `${this.first} ${this.last}`;
    }.bind(this);
    return `Hello ${full()}`;
  }
}

// good
const person = {
  first: "John",
  last: "Doe",
  greet() {
    const full = () => `${this.first} ${this.last}`;
    return `Hello ${full()}`;
  }
}
```

### Higher-order functions

Avoid nesting functions when you don't have to.

```javascript
// bad
[1, 2, 3].map(num => String(num));

// good
[1, 2, 3].map(String);
```

### Composition

Avoid multiple nested function calls. Use composition instead.

```javascript
const plus1 = a => a + 1;
const mult2 = a => a * 2;

// bad
mult2(plus1(5)); // => 12

// good
const pipeline = (...funcs) => val => funcs.reduce((a, b) => b(a), val);
const addThenMult = pipeline(plus1, mult2);
addThenMult(5); // => 12
```

### Caching

Cache feature tests, large data structures and any expensive operation.

```javascript
// bad
const contains = (arr, value) =>
  Array.prototype.includes
    ? arr.includes(value)
    : arr.some(el => el === value);
contains(["foo", "bar"], "baz"); // => false

// good
const contains = (() =>
  Array.prototype.includes
    ? (arr, value) => arr.includes(value)
    : (arr, value) => arr.some(el => el === value)
)();
contains(["foo", "bar"], "baz"); // => false
```

### 变量

赞同使用 `const` 代替 `let`,`let` 代替 `var`。

```javascript
// bad
var me = new Map();
me.set("name", "Ben").set("country", "Belgium");

// good
const me = new Map();
me.set("name", "Ben").set("country", "Belgium");
```

### 条件
赞同用 匿名执行函数返回语句 代替 if,else,switch 语句。
```javascript
// bad
var grade;
if (result < 50)
  grade = "bad";
else if (result < 90)
  grade = "good";
else
  grade = "excellent";

// good
const grade = (() => {
  if (result < 50)
    return "bad";
  if (result < 90)
    return "good";
  return "excellent";
})();
```

### 对象迭代

尽可能的避免使用 `for .. in`

```javascript
const shared = { foo: "foo" };
const obj = Object.create(shared, {
  bar: {
    value: "bar",
    enumerable: true
  }
});

// bad
for (var prop in obj) {
  if (obj.hasOwnProperty(prop))
    console.log(prop);
}

// good
Object.keys(obj).forEach(prop => console.log(prop));
```

### 使用 Map 创建对象

在使用对象的时候，Map 是个更好的选择

```javascript
// bad
const me = {
  name: "Ben",
  age: 30
};
var meSize = Object.keys(me).length;
meSize; // => 2
me.country = "Belgium";
meSize++;
meSize; // => 3

// good
const me = new Map();
me.set("name", "Ben");
me.set("age", 30);
me.size; // => 2
me.set("country", "Belgium");
me.size; // => 3
```

### 柯里化

柯里化很强大，但是很多开发者不是很熟悉。不要滥用它，适当的使用是很不错的。

```javascript
// bad
const sum = a => b => a + b;
sum(5)(3); // => 8

// good
const sum = (a, b) => a + b;
sum(5, 3); // => 8
```

### 可读性

不要用一些看似聪明的小技巧混淆代码的可读性

```javascript
// bad
foo || doSomething();

// good
if (!foo) doSomething();
```
```javascript
// bad
void function() { /* IIFE */ }();

// good
(function() { /* IIFE */ }());
```
```javascript
// bad
const n = ~~3.14;

// good
const n = Math.floor(3.14);
```

### 代码复用

不要害怕创造许多小的，高度组合可重复使用的功能

```javascript
// bad
arr[arr.length - 1];

// good
const first = arr => arr[0];
const last = arr => first(arr.slice(-1));
last(arr);
```
```javascript
// bad
const product = (a, b) => a * b;
const triple = n => n * 3;

// good
const product = (a, b) => a * b;
const triple = product.bind(null, 3);
```

### 依赖

减少依赖，你不熟悉第三方代码，不要为了一个简单的方法加载一个库。

```javascript
// bad
var _ = require("underscore");
_.compact(["foo", 0]));
_.unique(["foo", "foo"]);
_.union(["foo"], ["bar"], ["foo"]);

// good
const compact = arr => arr.filter(el => el);
const unique = arr => [...Set(arr)];
const union = (...arr) => unique([].concat(...arr));

compact(["foo", 0]);
unique(["foo", "foo"]);
union(["foo"], ["bar"], ["foo"]);
```


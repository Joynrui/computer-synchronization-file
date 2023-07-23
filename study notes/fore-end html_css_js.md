



# 结构html,样式CSS，逻辑JS

[**fore-end format standard**](https://segmentfault.com/a/1190000009636665)

# Javascript



<font color="gree">What can JavaScript do?</font>

<font color="red">JavaScript Can Change HTML Content</font>

**javascript可以改变html的内容**

```html
<!DOCTYPE html>
<html>
<body>

<h2>What Can JavaScript Do?</h2>

<p id="demo">JavaScript can change HTML content.</p>

<button type="button" onclick='document.getElementById("demo").innerHTML = "Hello JavaScript!"'>Click Me!</button>

</body>
</html>

```



<font color="red">JavaScript Can Change HTML Attribute Values</font>

**javascript 可以改变html属性值**

```html
<body>
	<p id="pid">Hello</p>
	<button οnclick="demo()">按钮</button>
	<script>
		function demo(){
			var nv = document.getElementById("pid");
			nv.innerHTML="World";
		}
	</script>
</body>
```



<font color="red">JavaScript Can Change HTML Styles (CSS)</font>

**javascript可以改变html样式**

```html
<!DOCTYPE html>
<html>
<body>

<h2>What Can JavaScript Do?</h2>

<p id="demo">JavaScript can change the style of an HTML element.</p>

<button type="button" onclick="document.getElementById('demo').style.fontSize='35px'">Click Me!</button>

</body>
</html> 
```





<font color="red">JavaScript Can Hide HTML Elements</font>

**javascript可以隐藏html元素**

```html
<!DOCTYPE html>
<html>
<body>

<h2>What Can JavaScript Do?</h2>

<p id="demo">JavaScript can hide HTML elements.</p>

<button type="button" onclick="document.getElementById('demo').style.display='none'">Click Me!</button>

</body>
</html> 

```





<font color="red">JavaScript Can Show HTML Elements</font>

**javascript可以展示html元素**

```html
<!DOCTYPE html>
<html>
<body>

<h2>What Can JavaScript Do?</h2>

<p>JavaScript can show hidden HTML elements.</p>

<p id="demo" style="display:none">Hello JavaScript!</p>

<button type="button" onclick="document.getElementById('demo').style.display='block'">Click Me!</button>

</body>
</html> 

```



<font color="gree">How to use JavaScript?</font>

javascript y有三种使用方法：

1. **External file，外链式** ：单独创建一个文件写javascript（最推荐）

```html
<script type="text/JavaScript" src="JavaScript文件的路径"></script>
```



2. **insertion , 嵌入式** ：

```html
<script type="text/JavaScript">
				JavaScript语句; 
			</script>
```



3. **inline，行内式**  ：

```html
<a href="JavaScript:alert('Hello');">test</a>
			<input type="button" onclick="alert('Hello');" value="test">
```



<font color="red">Basic Syntax</font>

1. Output 输出: 

```javascript
alert("hahhahaha ");
document.write("哈哈哈哈哈");
console.log("哈哈哈哈哈");
```

2. Annotation 注释：

```javascript
//单行注释

/*
 *多行注释
 * multi-line annotation
 *
 */
```

3. variable 变量：

```javascript
JavaScript是一种弱类型的语言，即数据（变量或常量）在定义时不必指明数据类型，其数据类型可以通过为数据赋值时根据其值来确定是什么类型。
		//变量类型(基本数据类型)： 
        var variable = 1000;//数值型Number
        var variable = "SunShineY"//字符串型String
        var variable = false;//布尔类型Boolean
        var variable = null;//空型Null
        var variable; //未定义型Undefined
		
```

4. constant常量:

```javascript
const PI = 3.14;
```

 

**note 注释规范 ：**



- 现阶段多多写注释。

- 注释只写做什么，不写怎么做的。

- 标识符

    由数字、字母、下划线和美元$符号来构成，首字符不能是数字。

    见名识意

    一行只写一个表达式，并且每个表达式后面都有;结尾



5. function

1) definition: 独立功能代码块。
2) eval()
3) parseFloat(): 若参数为一个小数，则输出小数，若参数开头为小数，结尾为字母，则忽略字母输出小数；若参数开头为字母，结尾为小数，则输出NaN。 



- 命名规则

由   ：  数字， 字母， 下划线  ，$组成（不常用），首字母不用数字

建议： 见名知意， 驼峰。

example: string_length  stringLength StringLength







# ES6

ES6即ECMAScript 6, 是JavaScript的标准版本。

 

## Let and const

### let

1. base function:

```javascript
{
    let a = 0;
    // a = 0
    a
}
// ReferenceError: a is not defined
a 
```

2. let variable only available in speacify block, var variable available in global range. 

```javascript
{
    let a = 1;
    var b = 9;
    // a = 1
    console.log(a);
    // b = 9
    console.log(b);
}
// b = 0
console.log(b);
// ReferenceError
console.log(a);
```

3. let variable can't assert multiple times but assert only once. var variable can assert multiple times.

```javascript
let a = 1;
let a = 22;
let b = 3;
let b = 4;
// Identifier 'a' has already been declared
a
// b = 4
b
```

4. let is very suitable for for loop:

```javascript
// output 10 ten times
for (var i = 0; i < 10; i++) {
    setTimeout(function() {
        console.log(i);
    })
}
// output 0123456789
for (let j = 0; j < 10; j++) {
    setTimeout(function() {
		console.log(j);
    })
}
```

变量 i 是用 var 声明的，在全局范围内有效，所以全局中只有一个变量 i, 每次循环时，setTimeout 定时器里面的 i 指的是全局变量 i ，而循环里的十个 setTimeout 是在循环结束后才执行，所以此时的 i 都是 10。

变量 j 是用 let 声明的，当前的 j 只在本轮循环中有效，每次循环的 j 其实都是一个新的变量，所以 setTimeout 定时器里面的 j 其实是不同的变量，即最后输出 12345。（若每次循环的变量 j 都是重新声明的，如何知道前一个循环的值？这是因为 JavaScript 引擎内部会记住前一个循环的值）。

5. let 不存在变量提升，var 会变量提升

```javascript
// ReferenceError: a is not defined
console.log(a);
let a = "cyberbase":
// undefined
console.log(b);
var b = "hello cyberbase";
```

变量 b 用 var 声明存在变量提升，所以当脚本开始运行的时候，b 已经存在了，但是还没有赋值，所以会输出 undefined。

变量 a 用 let 声明不存在变量提升，在声明变量 a 之前，a 不存在，所以会报错。



### const

const declare a read only variable, it can't changed after declaration. It also means const variable should initialize while declare it, but error.

```javascript
const PI = "3.1415926";
// 3.1415926
PI
// Syntax Error: Missing Intializer in const declaration
const CYBER;
```

<font color="red">Temporal Dead Area</font>

```javascript
var PI = "a";
if (true) {
    // Cannot access 'PI' before initialization
	console.log(PI);  
	const PI = "3.1415926";
}
```

ES6 明确规定，代码块内如果存在 let 或者 const，代码块会对这些命令声明的变量从块的开始就形成一个封闭作用域。代码块内，在声明变量 PI 之前使用它会报错。



## 解构赋值

### 解构模型

在解构中，有下面两部分参与：

- 解构的源，解构赋值表达式的右边部分。

- 解构的目标，解构赋值表达式的左边部分。

1. 数组模型的解构（Array）

**base 解构**

``` javascript
let [a, b, c] = [1, 2, 3];
// a = 1
// b = 2
// c = 3
```

**可嵌套**

```javascript
let [a, [[b], c]] = [1, [[2], 3]];
// a = 1
// b = 2
// c = 3
```

**可忽略**

```javascript
let [a, , b] = [1, 2, 3];
// a = 1
// b = 3
```

**不完全解构**

```javascript
let [a = 1, b] = []; // a = 1, b = undefined
```

**剩余运算符**

```javascript
let [a, ...b] = [1, 2, 3];
//a = 1
//b = [2, 3]
```

**字符串等**

在数组的解构中，解构的目标若为可遍历对象，皆可进行解构赋值。可遍历对象即实现 Iterator 接口的数据。

```javascript
let [a, b, c, d, e] = 'hello';
// a = 'h'
// b = 'e'
// c = 'l'
// d = 'l'
// e = 'o'
```

**解构默认值**

```javascript
let [a = 2] = [undefined]; // a = 2
```

当解构模式有匹配结果，且匹配结果是 undefined 时，会触发默认值作为返回结果。

```javascript
let [a = 3, b = a] = [];     // a = 3, b = 3
let [a = 3, b = a] = [1];    // a = 1, b = 1
let [a = 3, b = a] = [1, 2]; // a = 1, b = 2
```

- a 与 b 匹配结果为 undefined ，触发默认值：**a = 3; b = a =3**

- a 正常解构赋值，匹配结果：a = 1，b 匹配结果 undefined ，触发默认值：**b = a =1**
- a 与 b 正常解构赋值，匹配结果：**a = 1，b = 2**



### 对象模型解构

**base解构**

```javascript
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
// foo = 'aaa'
// bar = 'bbb'
 
let { baz : foo } = { baz : 'ddd' };
// foo = 'ddd'
```

**可嵌套解构**

```javascript
let obj = {p: ['hello', {y: 'world'}] };
let {p: [x, { y }] } = obj;
// x = 'hello'
// y = 'world'
let obj = {p: ['hello', {y: 'world'}] };
let {p: [x, {  }] } = obj;
// x = 'hello'
```

**不完全解构**

```javascript
let obj = {p: [{y: 'world'}] };
let {p: [{ y }, x ] } = obj;
// x = undefined
// y = 'world'
```

**剩余运算符**

```javascript
let {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40};
// a = 10
// b = 20
// rest = {c: 30, d: 40}
```

**解构默认值**

```javascript
let {a = 10, b = 5} = {a: 3};
// a = 3; b = 5;
let {a: aa = 10, b: bb = 5} = {a: 3};
// aa = 3; bb = 5;
```



## Symbol

ES6 引入了一种新的原始数据类型 Symbol ，表示独一无二的值，最大的用法是用来定义对象的唯一属性名。

ES6 数据类型除了 Number 、 String 、 Boolean 、 Object、 null 和 undefined ，还新增了 Symbol 。

[Symbol](https://www.runoob.com/w3cnote/es6-symbol.html)



## Map and Set

### Map

Map 对象保存键值对。任何值(对象或者原始值) 都可以作为一个键或一个值。



**Maps 和 Objects 的区别**

- 一个 Object 的键只能是字符串或者 Symbols，但一个 Map 的键可以是任意值。
- Map 中的键值是有序的（FIFO 原则），而添加到对象中的键则不是。
- Map 的键值对个数可以从 size 属性获取，而 Object 的键值对个数只能手动计算。
- Object 都有自己的原型，原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。



<font color="gree">Map 中的 key</font>

**key 是字符串**

```javascript
var myMap = new Map();
var keyString = "a string"; 
 
myMap.set(keyString, "和键'a string'关联的值");
 
myMap.get(keyString);    // "和键'a string'关联的值"
myMap.get("a string");   // "和键'a string'关联的值"
                         // 因为 keyString === 'a string'
```

**key是对象**

```javascript
var myMap = new Map();
var keyObj = {}, 
 
myMap.set(keyObj, "和键 keyObj 关联的值");
﻿
myMap.get(keyObj); // "和键 keyObj 关联的值"
myMap.get({}); // undefined, 因为 keyObj !== {}
```

**key是函数**

```javascript
var myMap = new Map();
var keyFunc = function () {}, // 函数
 
myMap.set(keyFunc, "和键 keyFunc 关联的值");
 
myMap.get(keyFunc); // "和键 keyFunc 关联的值"
myMap.get(function() {}) // undefined, 因为 keyFunc !== function () {}
```

**key是NaN**

```javascript
var myMap = new Map();
myMap.set(NaN, "not a number");
 
myMap.get(NaN); // "not a number"
 
var otherNaN = Number("foo");
myMap.get(otherNaN); // "not a number"
```

虽然 NaN 和任何值甚至和自己都不相等(NaN !== NaN 返回true)，NaN作为Map的键来说是没有区别的。

<font color="red">Map 的迭代</font>

对 Map 进行遍历，以下两个最高级。

**for...of**

```javascript
var myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
 
// 将会显示两个 log。 一个是 "0 = zero" 另一个是 "1 = one"
for (var [key, value] of myMap) {
  console.log(key + " = " + value);
}
for (var [key, value] of myMap.entries()) {
  console.log(key + " = " + value);
}
/* 这个 entries 方法返回一个新的 Iterator 对象，它按插入顺序包含了 Map 对象中每个元素的 [key, value] 数组。 */
 
// 将会显示两个log。 一个是 "0" 另一个是 "1"
for (var key of myMap.keys()) {
  console.log(key);
}
/* 这个 keys 方法返回一个新的 Iterator 对象， 它按插入顺序包含了 Map 对象中每个元素的键。 */
 
// 将会显示两个log。 一个是 "zero" 另一个是 "one"
for (var value of myMap.values()) {
  console.log(value);
}
/* 这个 values 方法返回一个新的 Iterator 对象，它按插入顺序包含了 Map 对象中每个元素的值。 */
```

**forEach()**

```javascript
var myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
 
// 将会显示两个 logs。 一个是 "0 = zero" 另一个是 "1 = one"
myMap.forEach(function(value, key) {
  console.log(key + " = " + value);
}, myMap)
```



<font color="red">Map 对象的操作</font>

**Map 与 Array的转换**

```javascript
var kvArray = [["key1", "value1"], ["key2", "value2"]];
 
// Map 构造函数可以将一个 二维 键值对数组转换成一个 Map 对象
var myMap = new Map(kvArray);
 
// 使用 Array.from 函数可以将一个 Map 对象转换成一个二维键值对数组
var outArray = Array.from(myMap);
```



**Map 的克隆**

```javascript
var myMap1 = new Map([["key1", "value1"], ["key2", "value2"]]);
var myMap2 = new Map(myMap1);
 
console.log(original === clone); 
// 打印 false。 Map 对象构造函数生成实例，迭代出新的对象。
```



**Map 的合并**

```javascript
var first = new Map([[1, 'one'], [2, 'two'], [3, 'three'],]);
var second = new Map([[1, 'uno'], [2, 'dos']]);
 
// 合并两个 Map 对象时，如果有重复的键值，则后面的会覆盖前面的，对应值即 uno，dos， three
var merged = new Map([...first, ...second]);
```



### Set

Set 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。



**Set 中的特殊值**

Set 对象存储的值总是唯一的，所以需要判断两个值是否恒等。有几个特殊值需要特殊对待：

- +0 与 -0 在存储判断唯一性的时候是恒等的，所以不重复；
- undefined 与 undefined 是恒等的，所以不重复；
- NaN 与 NaN 是不恒等的，但是在 Set 中只能存一个，不重复。

```javascript
let mySet = new Set();
 
mySet.add(1); // Set(1) {1}
mySet.add(5); // Set(2) {1, 5}
mySet.add(5); // Set(2) {1, 5} 这里体现了值的唯一性
mySet.add("some text"); 
// Set(3) {1, 5, "some text"} 这里体现了类型的多样性
var o = {a: 1, b: 2}; 
mySet.add(o);
mySet.add({a: 1, b: 2}); 
// Set(5) {1, 5, "some text", {…}, {…}} 
// 这里体现了对象之间引用不同不恒等，即使值相同，Set 也能存储
```



<font color="red">类型转换</font>

**Array**

```javascript
// Array 转 Set
var mySet = new Set(["value1", "value2", "value3"]);
// 用...操作符，将 Set 转 Array
var myArray = [...mySet];
String
// String 转 Set
var mySet = new Set('hello');  // Set(4) {"h", "e", "l", "o"}
// 注：Set 中 toString 方法是不能将 Set 转换成 String
```



<font color="red">Set 对象作用</font>

**数组去重**

```javascript
var mySet = new Set([1, 2, 3, 4, 4]); 
[...mySet]; // [1, 2, 3, 4]
```



**并集**

```javascript
var a = new Set([1, 2, 3]);
var b = new Set([4, 3, 2]);
var union = new Set([...a, ...b]); // {1, 2, 3, 4}
```

**交集**

```javascript
var a = new Set([1, 2, 3]); 
var b = new Set([4, 3, 2]); 
var intersect = new Set([...a].filter(x => b.has(x))); // {2, 3}
```

**1、[...a]**

[...a] 就是将 set 转换成 array。以后需要将 set 转换成 array 基本都使用这种方法。

**2、[...a].filter()**

Array.filter(function(x)) 把传入的函数 function(x) 依次作用于每个元素，x 为元素的值，然后根据返回值是 true 还是 false 决定保留还是丢弃该元素。

意思就是遍历当前数组，当遍历到某个元素时，返回值为 false 就将该元素从数组中剔除。

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

**3、 => 则是一种简写方法。**(箭头函数)

```javascript
x => x * x 
```

相当于：

```javascript
function(x) {
    return x * x
}
```

所以 **x => b.has(x)** 本质是一个函数相当于 **function(x){return b.has（x)}**。

**4、b.has(x)**

Set.has(x) 是 set 中的一个方法。即判断当前 set 中是否含有 x，如果有返回 true，没有返回 false。

所以这段程序也可以写成：

```javascript
var a = new Set([1, 2, 3]); 
var b = new Set([4, 3, 2]);
//将a转换成数组
var arr = [...a];
//使用filter过滤数组，并将新数组返回到fArr
var fArr = arr.filter(function(x) {
    //判断b中是否含有a中的元素，没有则返回false
    return b.has(x);        
})
//将fArr转换成set
var intersect = new Set(fArr);
console.log(fArr);
```

**差集**

```javascript
var a = new Set([1, 2, 3]); 
var b = new Set([4, 3, 2]); 
var difference = new Set([...a].filter(x => !b.has(x))); // {1}
```

1 为 a 与 b 的差集。

4 为 b 与 a 的差集。



## Reflect and Proxy

Proxy 与 Reflect 是 ES6 为了操作对象引入的 API 。

Proxy 可以对目标对象的读取、函数调用等操作进行拦截，然后进行操作处理。它不直接操作对象，而是像代理模式，通过对象的代理对象进行操作，在进行这些操作时，可以添加一些需要的额外操作。

Reflect 可以用于获取目标对象的行为，它与 Object 类似，但是更易读，为操作对象提供了一种更优雅的方式。它的方法与 Proxy 是对应的。



### Proxy

一个 Proxy 对象由两个部分组成： target 、 handler 。在通过 Proxy 构造函数生成实例对象时，需要提供这两个参数。 target 即目标对象， handler 是一个对象，声明了代理 target 的指定行为。

```javascript
let target = {
    name: 'Tom',
    age: 24
}
let handler = {
    get: function(target, key) {
        console.log('getting '+key);
        return target[key]; // 不是target.key
    },
    set: function(target, key, value) {
        console.log('setting '+key);
        target[key] = value;
    }
}
let proxy = new Proxy(target, handler)
proxy.name     // 实际执行 handler.get
proxy.age = 25 // 实际执行 handler.set
// getting name
// setting age
// 25
 
// target 可以为空对象
let targetEpt = {}
let proxyEpt = new Proxy(targetEpt, handler)
// 调用 get 方法，此时目标对象为空，没有 name 属性
proxyEpt.name // getting name
// 调用 set 方法，向目标对象中添加了 name 属性
proxyEpt.name = 'Tom'
// setting name
// "Tom"
// 再次调用 get ，此时已经存在 name 属性
proxyEpt.name
// getting name
// "Tom"
 
// 通过构造函数新建实例时其实是对目标对象进行了浅拷贝，因此目标对象与代理对象会互相
// 影响
targetEpt
// {name: "Tom"}
 
// handler 对象也可以为空，相当于不设置拦截操作，直接访问目标对象
let targetEmpty = {}
let proxyEmpty = new Proxy(targetEmpty,{})
proxyEmpty.name = "Tom"
targetEmpty // {name: "Tom"}
```



### Reflect



## String

### 子串识别

ES6 之前判断字符串是否包含子串，用 indexOf 方法，ES6 新增了子串的识别方法。

- **includes()**：返回布尔值，判断是否找到参数字符串。
- **startsWith()**：返回布尔值，判断参数字符串是否在原字符串的头部。
- **endsWith()**：返回布尔值，判断参数字符串是否在原字符串的尾部。

以上三个方法都可以接受两个参数，需要搜索的字符串，和可选的搜索起始位置索引。

```javascript
let string = "apple,banana,orange";
string.includes("banana");     // true
string.startsWith("apple");    // true
string.endsWith("apple");      // false
string.startsWith("banana",6)  // true
```

**注意点：**

- 这三个方法只返回布尔值，如果需要知道子串的位置，还是得用 indexOf 和 lastIndexOf 。
- 这三个方法如果传入了正则表达式而不是字符串，会抛出错误。而 indexOf 和 lastIndexOf 这两个方法，它们会将正则表达式转换为字符串并搜索它。

### String 重复

**repeat()**：返回新的字符串，表示将字符串重复指定次数返回。

```javascript
console.log("Hello,".repeat(2));  // "Hello,Hello,"
```

- 如果参数是小数，向下取整

- 如果参数是 0 至 -1 之间的小数，会进行取整运算，0 至 -1 之间的小数取整得到 -0 ，等同于 repeat 零次

- 如果参数是 NaN，等同于 repeat 零次

- 如果参数是负数或者 Infinity ，会报错:

```javascript
console.log("Hello,".repeat(-1));  
// RangeError: Invalid count value

console.log("Hello,".repeat(Infinity));  
// RangeError: Invalid count value
```

- 如果传入的参数是字符串，则会先将字符串转化为数字

```javascript
console.log("Hello,".repeat("hh")); // ""
console.log("Hello,".repeat("2"));  // "Hello,Hello,"
```



### String 补全

- **padStart**：返回新的字符串，表示用参数字符串从头部（左侧）补全原字符串。
- **padEnd**：返回新的字符串，表示用参数字符串从尾部（右侧）补全原字符串。

以上两个方法接受两个参数，第一个参数是指定生成的字符串的最小长度，第二个参数是用来补全的字符串。如果没有指定第二个参数，默认用空格填充。

```javascript
console.log("h".padStart(5,"o"));  // "ooooh"
console.log("h".padEnd(5,"o"));    // "hoooo"
console.log("h".padStart(5));      // "    h"
```

- 如果指定的长度小于或者等于原字符串的长度，则返回原字符串:

```javascript
console.log("hello".padStart(5,"A"));  // "hello"
```

- 如果原字符串加上补全字符串长度大于指定长度，则截去超出位数的补全字符串:

```javascript
console.log("hello".padEnd(10,",world!"));  // "hello,worl"
```

- <font color="red">常用于补全位数</font>

```javascript
console.log("123".padStart(10,"0"));  // "0000000123"
```



### Template String 

模板字符串相当于加强版的字符串，用反引号 **`**,除了作为普通字符串，还可以用来定义多行字符串，还可以在字符串中加入变量和表达式。

```javascript
let string = `Hello'\n'world`;
console.log(string); 
// "Hello'
// 'world"
```

- 多行String

```javascript
let string1 =  `Hey,
can you stop angry now?`;
console.log(string1);
// Hey,
// can you stop angry now?
```

- 字符串插入变量和表达式。变量名写在 ${} 中，${} 中可以放入 JavaScript 表达式。

```javascript
let name = "Mike";
let age = 27;
let info = `My Name is ${name},I am ${age+1} years old next year.`
console.log(info);
// My Name is Mike,I am 28 years old next year.
```

- 字符串中调用函数

```javascript
function f(){
  return "have fun!";
}
let string2= `Game start,${f()}`;
console.log(string2);  // Game start,have fun!
```

**注意**

模板字符串中的换行和空格都是会被保留的

```javascript
innerHtml = `<ul>
  <li>menu</li>
  <li>mine</li>
</ul>
`;
console.log(innerHtml);
// 输出
<ul>
 <li>menu</li>
 <li>mine</li>
</ul>
```

### Tag Template 

标签模板，是一个函数的调用，其中调用的参数是模板字符串。

```javascript
alert`Hello world!`;
// 等价于
alert('Hello world!');
```

当模板字符串中带有变量，会将模板字符串参数处理成多个参数。

```javascript
function f(stringArr,...values){
 let result = "";
 for(let i=0;i<stringArr.length;i++){
  result += stringArr[i];
  if(values[i]){
   result += values[i];
        }
    }
 return result;
}
let name = 'Mike';
let age = 27;
f`My Name is ${name},I am ${age+1} years old next year.`;
// "My Name is Mike,I am 28 years old next year."
 
f`My Name is ${name},I am ${age+1} years old next year.`;
// 等价于
f(['My Name is',',I am ',' years old next year.'],'Mike',28);
```

#### **应用**

过滤 HTML 字符串，防止用户输入恶意内容。

```javascript
function f(stringArr,...values){
 let result = "";
 for(let i=0;i<stringArr.length;i++){
  result += stringArr[i];
   if(values[i]){
     result += String(values[i]).replace(/&/g, "&amp;")
               .replace(/</g, "&lt;")
               .replace(/>/g, "&gt;");
    }
 }
 return result;
}
name = '<Amy&MIke>';
f`<p>Hi, ${name}.I would like send you some message.</p>`;
// <p>Hi, &lt;Amy&amp;MIke&gt;.I would like send you some message.</p>
```

**国际化处理（转化多国语言）**

```javascript
i18n`Hello ${name}, you are visitor number ${visitorNumber}.`;  
// 你好**，你是第**位访问者
```



## 数值

### 数值的表示

二进制表示法新写法: 前缀 0b 或 0B 

```javascript
console.log(0b11 === 3); // true
console.log(0B11 === 3); // true
```

八进制表示法新写法: 前缀 0o 或 0O 

```javascript
console.log(0o11 === 9); // true
console.log(0O11 === 9); // true
```

**常量**

```javascript
Number.EPSILON
```

Number.EPSILON 属性表示 1 与大于 1 的最小浮点数之间的差。

它的值接近于 2.2204460492503130808472633361816E-16，或者 2-52。

测试数值是否在误差范围内:

```javascript
0.1 + 0.2 === 0.3; // false
// 在误差范围内即视为相等
equal = (Math.abs(0.1 - 0.3 + 0.2) < Number.EPSILON); // true
```

**属性特性**

```javascript
writable：false
enumerable：false
configurable：false
```

**最大/最小安全整数**

1. 安全整数

安全整数表示在 JavaScript 中能够精确表示的整数，安全整数的范围在 2 的 -53 次方到 2 的 53 次方之间（不包括两个端点），超过这个范围的整数无法精确表示。

2. 最大安全整数

安全整数范围的上限，即 2 的 53 次方减 1 

```javascript
Number.MAX_SAFE_INTEGER + 1 === Number.MAX_SAFE_INTEGER + 2; // true
Number.MAX_SAFE_INTEGER === Number.MAX_SAFE_INTEGER + 1;     // false
Number.MAX_SAFE_INTEGER - 1 === Number.MAX_SAFE_INTEGER - 2; // false
```

3. 最小安全整数

安全整数范围的下限，即 2 的 53 次方减 1 的负数

```javascript
Number.MIN_SAFE_INTEGER + 1 === Number.MIN_SAFE_INTEGER + 2; // false
Number.MIN_SAFE_INTEGER === Number.MIN_SAFE_INTEGER - 1;     // false
Number.MIN_SAFE_INTEGER - 1 === Number.MIN_SAFE_INTEGER - 2; // true
```

**属性特性**

```javascript
writable：false
enumerable：false
configurable：false
```

#### 方法

**Number 对象新方法**

```javascript
Number.isFinite()
```

用于检查一个数值是否为有限的（ finite ），即不是 Infinity

```javascript
console.log( Number.isFinite(1));   // true
console.log( Number.isFinite(0.1)); // true
 
// NaN 不是有限的
console.log( Number.isFinite(NaN)); // false
 
console.log( Number.isFinite(Infinity));  // false
console.log( Number.isFinite(-Infinity)); // false
 
// Number.isFinate 没有隐式的 Number() 类型转换，所有非数值都返回 false
console.log( Number.isFinite('foo')); // false
console.log( Number.isFinite('15'));  // false
console.log( Number.isFinite(true));  // false

Number.isNaN()
用于检查一个值是否为 NaN 。
console.log(Number.isNaN(NaN));      // true
console.log(Number.isNaN('true'/0)); // true
 
// 在全局的 isNaN() 中，以下皆返回 true，因为在判断前会将非数值向数值转换
// 而 Number.isNaN() 不存在隐式的 Number() 类型转换，非 NaN 全部返回 false
Number.isNaN("NaN");      // false
Number.isNaN(undefined);  // false
Number.isNaN({});         // false
Number.isNaN("true");     // false
```

**从全局移植到 Number 对象的方法**

逐步减少全局方法，用于全局变量的模块化。

方法的行为没有发生改变。

```javascript
Number.parseInt()
```

用于将给定字符串转化为指定进制的整数。

```javascript
// 不指定进制时默认为 10 进制
Number.parseInt('12.34'); // 12
Number.parseInt(12.34);   // 12
 
// 指定进制
Number.parseInt('0011',2); // 3
 
// 与全局的 parseInt() 函数是同一个函数
Number.parseInt === parseInt; // true
Number.parseFloat()
用于把一个字符串解析成浮点数。
Number.parseFloat('123.45')    // 123.45
Number.parseFloat('123.45abc') // 123.45
 
// 无法被解析成浮点数，则返回 NaN
Number.parseFloat('abc') // NaN
 
// 与全局的 parseFloat() 方法是同一个方法
Number.parseFloat === parseFloat // true
Number.isInteger()
用于判断给定的参数是否为整数。
Number.isInteger(value)
Number.isInteger(0); // true
// JavaScript 内部，整数和浮点数采用的是同样的储存方法,因此 1 与 1.0 被视为相同的值
Number.isInteger(1);   // true
Number.isInteger(1.0); // true
 
Number.isInteger(1.1);     // false
Number.isInteger(Math.PI); // false
 
// NaN 和正负 Infinity 不是整数
Number.isInteger(NaN);       // false
Number.isInteger(Infinity);  // false
Number.isInteger(-Infinity); // false
 
Number.isInteger("10");  // false
Number.isInteger(true);  // false
Number.isInteger(false); // false
Number.isInteger([1]);   // false
 
// 数值的精度超过 53 个二进制位时，由于第 54 位及后面的位被丢弃，会产生误判
Number.isInteger(1.0000000000000001) // true
 
// 一个数值的绝对值小于 Number.MIN_VALUE（5E-324），即小于 JavaScript 能够分辨
// 的最小值，会被自动转为 0，也会产生误判
Number.isInteger(5E-324); // false
Number.isInteger(5E-325); // true
Number.isSafeInteger()
用于判断数值是否在安全范围内。
Number.isSafeInteger(Number.MIN_SAFE_INTEGER - 1); // false
Number.isSafeInteger(Number.MAX_SAFE_INTEGER + 1); // false
```



### Math 对象的扩展

ES6 在 Math 对象上新增了 17 个数学相关的静态方法，这些方法只能在 Math 中调用。

**普通计算**

```javascript
Math.cbrt
```

用于计算一个数的立方根

```javascript
Math.cbrt(1);  // 1
Math.cbrt(0);  // 0
Math.cbrt(-1); // -1
// 会对非数值进行转换
Math.cbrt('1'); // 1
 
// 非数值且无法转换为数值时返回 NaN
Math.cbrt('hhh'); // NaN
```

...continue



## Object

### 对象字面量

**属性的简洁表示法**

ES6允许对象的属性直接写变量，这时候属性名是变量名，属性值是变量值。

```javascript
const age = 12;
const name = "Amy";
const person = {age, name};
person   //{age: 12, name: "Amy"}
//等同于
const person = {age: age, name: name}
```

**方法名也可以简写**

```javascript
const person = {
  sayHi(){
    console.log("Hi");
  }
}
person.sayHi();  //"Hi"
//等同于
const person = {
  sayHi:function(){
    console.log("Hi");
  }
}
person.sayHi();//"Hi"
```

(generator后续会涉及)如果是Generator 函数，则要在前面加一个星号:

```javascript
const obj = {
  * myGenerator() {
    yield 'hello world';
  }
};
//等同于
const obj = {
  myGenerator: function* () {
    yield 'hello world';
  }
};
```

**属性名表达式**

ES6允许用表达式作为属性名，但是一定要将表达式放在方括号内。

```javascript
const obj = {
 ["he"+"llo"](){
   return "Hi";
  }
}
obj.hello();  //"Hi"
```

注意点：属性的简洁表示法和属性名表达式不能同时使用，否则会报错。

```javascript
const hello = "Hello";
const obj = {
 [hello]
};
obj  //SyntaxError: Unexpected token }

const hello = "Hello";
const obj = {
 [hello+"2"]:"world"
};
obj  //{Hello2: "world"}
```



## Array

### Create Array

1. Array.of():将参数中所有值作为元素形成数组。

```javascript
const hello = "Hello";
const obj = {
 [hello]
};
obj  //SyntaxError: Unexpected token }
 
const hello = "Hello";
const obj = {
 [hello+"2"]:"world"
};
obj  //{Hello2: "world"}
```



2. Array.from():将类数组对象或可迭代对象转化为数组。

```javascript
// 参数为数组,返回与原数组一样的数组
console.log(Array.from([1, 2])); // [1, 2]
 
// 参数含空位
console.log(Array.from([1, , 3])); // [1, undefined, 3]
```

parameter:`Array.from(arrayLike[, mapFn[, thisArg]])`

返回值为转换后的数组。

> - **arrayLike**
>
> 想要转换的类数组对象或可迭代对象。
>
> console.log(Array.from([1, 2, 3])); // [1, 2, 3]
>
> - **mapFn**
>
> 可选，map 函数，用于对每个元素进行处理，放入数组的是处理后的元素。
>
> `console.log(Array.from([1, 2, 3], (n) => n * 2)); // [2, 4, 6]`
>
> - **thisArg**
>
> 可选，用于指定 map 函数执行时的 this 对象。
>
> ```javascript
> let map = {
>     do: function(n) {
>         return n * 2;
>     }
> }
> let arrayLike = [1, 2, 3];
> console.log(Array.from(arrayLike, function (n){
>     return this.do(n);
> }, map)); // [2, 4, 6]
> ```
>
> 



3. **类数组对象**

一个类数组对象必须含有 length 属性，且元素属性名必须是数值或者可转换为数值的字符。

```javascript
let arr = Array.from({
  0: '1',
  1: '2',
  2: 3,
  length: 3
});
console.log(arr); // ['1', '2', 3]
 
// 没有 length 属性,则返回空数组 (即默认将length视为0)
let array = Array.from({
  0: '1',
  1: '2',
  2: 3,
});
console.log(array); // []
 
// 元素属性名不为数值且无法转换为数值，返回长度为 length 元素值为 undefined 的数组  
let array1 = Array.from({
  a: 1,
  b: 2,
  length: 2
});
console.log(array1); // [undefined, undefined]
```



**转换可迭代对象**

- convert map

```javascript
let map = new Map();
map.set('key0', 'value0');
map.set('key1', 'value1');
console.log(Array.from(map)); 
// [['key0', 'value0'],['key1', 'value1']]
```

- convert set

```javascript
let arr = [1,2,3];
let set = new Set(arr);
console.log(Array.from(set));
```

- convert String 

```javascript
let str = "cyberbase";
console.log(Array.from(str));
```







## Function



## Class



## Module



## Promise object



## Generator function



## async function

async 是 ES7 才有的与异步操作有关的关键字，和 Promise ， Generator 有很大关联的。



# Question Resolve

## Http cache feild

http缓存字段

>1. Cache-Control
>2. Expires
>3. ETag / If-None-Match
>4. Last-Modified / If-Modified-Since


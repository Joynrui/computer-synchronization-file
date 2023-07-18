



## 结构html,样式CSS，逻辑JS



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



[**fore-end format standard**](https://segmentfault.com/a/1190000009636665)



# I. What can JavaScript do?

## JavaScript Can Change HTML Content

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



## JavaScript Can Change HTML Attribute Values

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



## JavaScript Can Change HTML Styles (CSS)

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





## JavaScript Can Hide HTML Elements

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





## JavaScript Can Show HTML Elements

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



# II. How to use JavaScript?

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







# Basic Syntax

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



# III. 命名规则

由   ：  数字， 字母， 下划线  ，$组成（不常用），首字母不用数字

建议： 见名知意， 驼峰。

example: string_length  stringLength StringLength








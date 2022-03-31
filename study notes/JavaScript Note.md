# JavaScript Note



[**JavaScript format standard**](https://segmentfault.com/a/1190000009636665)



#  I. What can JavaScript do?

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





## 结构html,样式CSS，逻辑JS



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








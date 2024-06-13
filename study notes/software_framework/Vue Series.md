# Vue Series

### Vue3 Basic function

#### basetest.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!--import vue.js script-->
    <script src="http://unpkg.com/vue@next"></script>
</head>
<body>
    <!--declare the DOM area which will be controlled with vue-->
    <div id ="app">
        <!--model syntax-->
        {{message}}
    </div>

    <!--create vue  instance object-->
    <script>
        const hello = {
            data: function() {
                return {
                    message: "Weclome to Cyberbase!"
                }
            }
        }
        const app = Vue.createApp(hello)
        app.mount('#app')
    </script>
</body>
</html>
```

#### content.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="http://unpkg.com/vue@next"></script>
</head>
<body>
    <div id="app">
        <!--模板语法-->
        <p>姓名：{{username}}</p>
        <p>性别：{{gender}}</p>
        <!--super link 字符串不会直接渲染-->
        <p>{{desc}}</p>
        <!--使用 v-html parameter渲染超链接字符串-->
        <!--“v-html”称指令-->
        <p v-html="desc"></p>

    </div>
    <script>
        const vm = {
            data: function() {
                return {
                    username:'cyberbase',
                    gender: '男',
                    desc:'<a herf="http://www.baidu.com">百度</a>'
                }
            }
        }
        const app = Vue.createApp(vm)
        app.mount('#app')
    </script>
</body>
</html>
```

#### parameter_binding.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="http://unpkg.com/vue@next"></script>
</head>

<body>
    <div id="app">
        <!--v-bind:用于将参数绑定-->
        <!--"v-bind:herf" 与 ":herf" 等效，（v-bind 可以省略）-->
        <a v-bind:herf="link">baidu</a>
        <input type="text" :placeholder="inputValue">
         <!--This method only change page element but unchanged with parameter which is to transmit.-->
        <!--When page elements changing by user, v-model command will update parameter value that should be transmitting synchronously.-->
        <img :src="imgSrc" :style="{width:w}" alt="">
    </div>
    <script>
        const vm = {
            data: function () {
                return {
                    link: "http://www.baidu.com",
                    inputValue: "Please input content:",
                    imgSrc: "D:/Files/插画/89532340_p0.jpg",
                    w: '500px'
                }
            }
        }
        const app = Vue.createApp(vm)
        app.mount('#app')
    </script>
</body>

</html>
```

#### js_expression.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="http://unpkg.com/vue@next"></script>
</head>
<body>
    <div id="app">
        <p>{{number + 18}}</p>
        <p>{{ok ? 'True' : 'False'}}</p>
        <p>{{message.split('').reverse().join('')}}</p>
        <p :id="'list-' + id">xxx</p>
        <p>{{user.name}}</p>
    </div>
    <script>
        const vm = {
            data: function() {
                return {
                    number: 10,
                    ok: false,
                    message:'ABC',
                    id: 3,
                    user: {
                        name: 'max',
                    }
                }
            }
        }
        const app = Vue.createApp(vm)
        app.mount('#app')
    </script>
</body>
</html>
```

#### action_binding.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
     <!--import vue.js script-->
    <script src="http://unpkg.com/vue@next"></script>
</head>
<body>
    <div id="app">
        <h2>count value: {{count}}</h2>
        <button v-on:click="subtractCount">-1</button>
        <button @click="count+=1">+1</button>
    </div>

    <script>
        const vm = {
            data:function() {
                return{
                    count: 0,
                }
            },
            methods: {
                subtractCount() {
                    this.count -= 1
                },
            },
        }
        const app = Vue.createApp(vm)
        app.mount('#app')
    </script>
</body>
</html>
```

#### condition_rendering.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
     <!--import vue.js script-->
    <script src="http://unpkg.com/vue@next"></script>
</head>
<body>
    <div id="app">
        <button @click="flag = !flag">Toggle Flag</button>
        <!-- If 'v-if' value is false.it will not create label-->
        <p v-if="flag">请求被v-if控制</p>
        <!-- If 'v-show' value is false it will create label but dont show it on the page.-->
        <p v-show="flag">请求被v-show控制</p>
    </div>
    <script>
        const vm ={
            data: function(){
                return {
                    flag: false,
                }
            }
        }
        const app = Vue.createApp(vm)
        app.mount('#app')
    </script>
</body>
</html>
```

#### v-else_and_v-else-if.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
     <!--import vue.js script-->
    <script src="http://unpkg.com/vue@next"></script>
</head>
<body>
    <div id="app">
        <p v-if="num > 0.5">random number > 0.5</p>
        <p v-else>random <= 0.5</p>
        <hr />
        <p v-if="type === 'A' ">excellent</p>
        <p v-else-if="type === 'B' ">well</p>
        <p v-else-if="type === 'C' ">normal</p>
        <p v-else>bad</p>
    </div> 
    <div v-show="a">
        test
    </div>
    <button @click="!a">click</button>
    <script>
        const vm = {
            data: function(){
                return {
                    num:Math.random(),
                }
            }
        }
        const app = Vue.createApp(vm);
        app.mount("#app");
    </script>
</body>
</html>
```

#### list_rendering.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
     <!--import vue.js script-->
    <script src="http://unpkg.com/vue@next"></script>
</head>

<body>
    <div id="app">
        <ul>
            <li v-for="(user, i) in userList">index: {{i}}< name: {{user.name}}</li>
        </ul>
    </div>
    <script>
        const vm = {
            data: function () {
                return {
                    userList:[
                        {id: 1, name:"Cyberbase corporation"},
                        {id: 2, name:"Max Croft"},
                        {id: 3, name:"Sunshine.Y"}
                    ],
                }
            },
        }
        const app = Vue.createApp(vm);
        app.mount('#app');
    </script>
</body>
```



### Create new Vue project

1. download node.js
2. use:

- It's Vue 手脚架

```shell
npm install -g @Vue-cli
```

- create Vue project

```shell
vue create [options] <app-name>
```

- run Vue project

```shell
npm run serve
```



### Vue project content

- `package.json` is project dependency catalog.
- `App.vue` is project root component.

- `node-modules` is project dependency file, it could be delete, and synchronizing next time.



## `Vue Router`

Vue2.x corresponding Vue router3.x

Vue3.x corresponding Vue router4.x 

router3.x and router.4.0 just have a little bit of difference.



```shell
npm install vue-router@3.6.5
```





## `Vuex`



install version 3 of `Vuex`(Please install it in Vue Project directory)

```shell
npm install vuex@3
```







## `Mockjs`

Frontend intercept Ajax request and create random data tools, used to simulate  server response.

1. install

```shell
npm install mockjs
```



## Element UI

1. install

```shell
npm i element-ui
```

2. import `element-ui` into Vue project

    a. add statements in main.js

```javascript
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
// This is Vue2 syntax, Vue3 has a bit of different
Vue.use(ElementUI);
```

## Third Party Gallery

[`Fontawesome4`](http://fontawesome.dashgame.com/)

[`Fontawesome5`](https://fa5.dashgame.com/#/)

[`Fontawesome6`](https://fa6.dashgame.com/)

- install

```shell
npm install font-awesome
```

- import

```javascript
import 'font-awesome/css/font-awesome.min.css'
```



## `Axios`

An Ajax framework, `Axios` is a *[promise-based](https://javascript.info/promise-basics)* HTTP Client for [`node.js`](https://nodejs.org/) and the browser. 



- install

```shell
npm install axios
```

- import

```javascript
import axios from 'axios';
```



- 一般在组件创建时调用请求，或需要某些动作时调用请求。

### Configure Axios

Import `axios` in main.js, and set `baseUrl`, associate axios

```javascript
import axios from 'axios';
axios.defaults.baseURL = 'http://localhost:8081'
// Set axios to a global custom attribute, every componentscan access directly inside.
Vue.prototype.$http = axios
```

## Axios CRUD

```js
axios.get(url, config);
axios.delete(url, config);
axios.post(url, data, config);
axios.put(url, data, config);
axios.patch(url, data, config);
```

### notice： Data format of Axios response is res.data





1. GET

```js
// then mode
function getList() {
    axios.get("url").then((res:  AxiosResponse<ObjectType[]>) => {
        console.log(res.data)
        data.list = res.data
    })
}
// async mode 
async function getList() {
    let res: AxiosResponse<ObjectType[]> = await axios.get("url") 
}

async functiongetDetail(id: number) {
    let res = await axios.get("url", + id)
    console.log("详情", res.data)
} 
```

2. POST

```js
async function postCreate() {
    // body 为变量本身 userCreateType 为变量类型别名
 	let body :userCreateType(){
     	name: "",
     	age: "",
     	addr:"",
 	}
	let res = await axios.post("url", body)
    console.log("添加"，res.data)
}
```

3. PUT 全量更新

```js
async function putUpdate(item: ObjectType) {
    let body: userCreateType = {
        name: "",
        age: "",
        addr: "",
    }
    let res = await axios.put("url", item.id, body)
    getList()
}
```

4. DELETE 

```js
async function deleteRemove(id: number){
    let res = await axios.delete("url" + id)
    console.log("删除"，res.data)
    getList()
}
```









### Question

使用请求时，因存在回调函数， 而回调函数的作用域会发生变化，故以下代码会出现异常：

此处因回调函数function作用域发生变化， this. 与created不同导致异常。

```javascript
 created:function(){
    axios.get("http://localhost:8081/userquery")
        .then(function(response){
     		this.tableData = response.data
    })
  },
 data(){
     return {
         tableData:[]
     }
 }
```

solution:使用箭头函数：箭头函数的作用域与其所属的父级函数相同，this. 指向相同

```javascript
 created:function(){
    axios.get("http://localhost:8081/userquery")
        .then((response)=>{
     		this.tableData = response.data
    })
  },
 data(){
     return {
         tableData:[]
     }
 }
```





## Less

CSS framework

- install

```shell
npm install less@4.1.2
npm install less-loader@6.0.0
```





> 自己看视频做的笔记做下记录好自己查看
> 如果需要视频可以到B站：https://space.bilibili.com/13541565/#/
> 百度云链接:https://pan.baidu.com/s/1Xrhtj0aUJC3GnO7ZDOqG0w 提取码:m605
> 感谢B站up主TikkiPon提供资源。

* [一 、vue 的安装及介绍](#一-vue-的安装及介绍)
	* [1.1、安装及构建项目](#11-安装及构建项目)
		* [1.1.1、全局安装webpack](#111-全局安装webpack)
		* [1.1.2、全局安装vue cli](#112-全局安装vue-cli)
		* [1.1.3、检测是否安装成功](#113-检测是否安装成功)
		* [1.1.4、构建项目](#114-构建项目)
		* [1.1.5、运行项目](#115-运行项目)
	* [1.2、vue配置](#12-vue配置)
	* [1.3、vue的基础语法](#13-vue的基础语法)
		* [1.3.1、模板语法](#131-模板语法)
		* [1.3.2、class和style绑定](#132-class和style绑定)
		* [1.3.3、条件渲染](#133-条件渲染)
		* [1.3.4、vue时间处理器](#134-vue时间处理器)
		* [1.3.5、组件和组件通讯](#135-组件和组件通讯)
		* [1.3.6、组件通讯案例](#136-组件通讯案例)
* [二、路由](#二-路由)
	* [2.1、路由基础介绍](#21-路由基础介绍)
	* [2.2、动态路由配置](#22-动态路由配置)
	* [2.3、嵌套路由](#23-嵌套路由)
	* [2.4、编程式路由](#24-编程式路由)
	* [2.5、命名路由和命名视图](#25-命名路由和命名视图)
		* [2.5.1、命名路由](#251-命名路由)
		* [2.5.2、命名视图](#252-命名视图)
* [三、Vue-resource和Axios](#三-vue-resource和axios)
	* [3.1、vue-resourse使用](#31-vue-resourse使用)
	* [3.2、axios介绍](#32-axios介绍)
* [四、ES6常用语法](#四-es6常用语法)
	* [4.1、ES6简介](#41-es6简介)
	* [4.2、Rest参数和扩展](#42-rest参数和扩展)
	* [4.3、import和export](#43-import和export)
	* [4.4、Promise讲解](#44-promise讲解)
	* [4.5、AMD、CMD、CommonJS和ES6差异](#45-amd-cmd-commonjs和es6差异)
		* [4.5.1、CommonJS](#451-commonjs)
		* [4.5.2、AMD](#452-amd)
		* [4.5.3、CMD](#453-cmd)
		* [4.5.4、ES6](#454-es6)

# 一 、vue 的安装及介绍
## 1.1、安装及构建项目
### 1.1.1、全局安装webpack

``` cmd
npm install webpack -g
```
### 1.1.2、全局安装vue cli
```cmd
npm install --global vue-cli
```
### 1.1.3、检测是否安装成功
```cmd
vue -V
```
### 1.1.4、构建项目
```cmd
vue init webpack demo（项目名称）
```
安装完成后目录
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541693281966.png)
### 1.1.5、运行项目
```cmd
cnpm init
cnpm run dev
```
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541693382295.png)

## 1.2、vue配置
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541771053661.png)

build.js：构建生产环境的文件，其原理是加载webpack.base.cof.js等配置文件去构建打包正产环境。
webpack.base.conf.js：打包配置文件，加载项目的一些插件。
index.js：也是项目的配置文件，在这里这也对生产环境做一些配置，如端口、静态资源路径配置等
main.js：整个项目的入口。
## 1.3、vue的基础语法
### 1.3.1、模板语法
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541781826892.png)
### 1.3.2、class和style绑定
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541781905905.png)
### 1.3.3、条件渲染
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541781945878.png)
### 1.3.4、vue时间处理器
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541782007572.png)
### 1.3.5、组件和组件通讯
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541782060533.png)
### 1.3.6、组件通讯案例
父组件代码
```html
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <!--
      使用子组件
      v-bind:num="num" ：绑定数据传给子组件，当父组件的num值变动的时候，子组件的值跟着变动
      v-on:aa="increment" ：自定义一个事件aa，让子组件去调用改事件，从而改变父组件的值
    -->
    <counter v-bind:num="num" v-on:aa="increment" v-on:bb="decrement"></counter>
    <p>parent : {{ num }}</p>
  </div>
</template>

<script>
  /*引入子组件*/
  import Counter from './test'
export default {

  name: 'HelloWorld',
  data () {
    return {
      num:10,
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods:{
    increment(){
      this.num++;
    },
    decrement(){
      this.num--;
    }
  },
  /*注册子组件*/
  components:{
    Counter
  }
}
</script>
```
子组件代码
```html
<template>
    <div>
        <button @click="increment">+</button>
        <button v-on:click="decrement">-</button>
        <p><span>{{ num }}</span></p>
    </div>
</template>

<script>
    export default {
      props:["num"],//接收父组件传过来的值
        data() {
            return {
              num : 0
            }
        },
      methods:{
          increment(){
//            this.num++;
            this.$emit('aa');//触发父组件事件，aa是在父组件上定义的事件
          },
          decrement(){
//            this.num--;
            this.$emit('bb');//触发父组件事件
          }
      }
    }
</script>

```
效果
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541782707244.png)
总结：
1、组件使用的有四个步骤
	（1）新建子组件
	（2）在父组件中引入子组件，import
	（3）注册子组件
	（4）使用子组件
2、组件的通讯是单向的，父组件可以向子组件传值，子组件使用props:["num"],接收值。
	  子组件不能直接向父组件传值，可以通过this.$emit('bb')触发父组件的方法改变父组件的值。

----------


# 二、路由
## 2.1、路由基础介绍
什么是前端路由？
路由是根据不同的url地址展示不同的内容或页面
前端路由就是吧不同路由对应不同的内容或页面的任务交给前端来做，之前是通过服务端根据url的不同返回不同的页面实现的
前端路由的优点和缺点？
优点：
		用户体验号，不需要每次都从服务器全部获取，快速展现给用户
缺点：
		不利于SEO（搜索引擎搜索）
		使用浏览器的前进后退键的时候会重新发请求，没有合理的利用缓存
		单页面无法记住之前滚动的位置，无法前进、后退的时候记住滚动的位置
vue-router用来构建SAP
```html
<router-link></router-link>或者this.$router.push({path})
<router-view></router-view>
```
## 2.2、动态路由配置
什么是动态路由？
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/微信截图_20181110113523.png "微信截图_20181110113523")
案例：
新建一个组件GoodList
```html
<template>
    <div>
      这是一个商品列表
      <!--通过$route.params.goodId（定义的路由id）获取参数-->
      <span>{{$route.params.goodId}}</span><br/>
      <span>{{$route.params.userId}}</span>
    </div>
</template>


<script>
    export default {
        data() {
            return {msg: '这个是Home模板页'}
        }
    }
</script>

```
更改router文件夹下的index.js
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541813343060.png)
```js
import Vue from 'vue'
import Router from 'vue-router'
import GoodList from './../views/GoodList'//引入组件

Vue.use(Router)

export default new Router({
  routes: [
    {
      //设置路由“：”后面的goodId和userId就是我们的参数
      path: '/goods/:goodId/user/:userId',
      name: 'GoodList',
      component: GoodList
    }
  ]
})
````
显示效果
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541813540915.png)
## 2.3、嵌套路由
什么是嵌套路由？
就是根路由下面可以建立很多子路由，子路由对应的不同的组件，通过子路由可以访问到不同的子组件。
案例：
新建两个子路由Title和Image
Title.vue
```html
<template>
    <div>
      标题子组件
    </div>
</template>

<style>
</style>

<script>
    export default {
        data() {
            return {msg: '这个是Home模板页'}
        }
    }
</script>
```
Image.vue
```html
<template>
    <div>
       图片子组件
    </div>
</template>

<style>
</style>

<script>
    export default {
        data() {
            return {msg: '这个是Home模板页'}
        }
    }
</script>
```
更改index.js中的路由配置，引入子组件和，在根路由的基础上建立子路由
```js
import Vue from 'vue'
import Router from 'vue-router'
import GoodList from './../views/GoodList'//引入组件
//引入标题子组件和图片子组件
import Title from '@/views/Title'
import Image from '@/views/Image'

Vue.use(Router)

export default new Router({
  routes: [
    {
      //设置路由“：”后面的goodId和userId就是我们的参数
      path: '/goods',
      name: 'GoodList',
      component: GoodList,
      //设置子路由
      children:[
        {
          path:'title',
          name:Title,
          component:Title
        },
        {
          path:'img',
          name:Image,
          component:Image
        }
      ]
    }
  ]
})
```
更改GoodList.vue，建立router-link和router-view
```html
<template>
    <div>
      这是一个商品列表
      <!--通过$route.params.goodId（定义的路由id）获取参数-->
      <span>{{$route.params.goodId}}</span><br/>
      <span>{{$route.params.userId}}</span>
      <!--建立两个router-link跳转标签-->
      <router-link to="/goods/title">标题</router-link>
      <router-link to="/goods/img">图片</router-link>
      <!--建立一个router-view表现用于加载组件-->
      <div>
        <router-view></router-view>
      </div>
    </div>
</template>


<script>
    export default {
        data() {
            return {msg: '这个是Home模板页'}
        }
    }
</script>
```
效果：
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541815092243.png)
## 2.4、编程式路由
什么是编程式路由？
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541815865959.png)
案例：
建立一个购物城Cart.vue
```html
<template>
    <div>
      这是购物车页面
    </div>
</template>

<style>
</style>

<script>
    export default {
        data() {
            return {msg: '这个是Home模板页'}
        }
    }
</script>
```
更改index.js，引入购物车组件和添加路由映射
```js
import Vue from 'vue'
import Router from 'vue-router'
import GoodList from './../views/GoodList'//引入组件
//引入标题子组件和图片子组件
import Title from '@/views/Title'
import Image from '@/views/Image'
import Cart from '@/views/Cart'

Vue.use(Router)

export default new Router({
  routes: [
    {
      //设置路由“：”后面的goodId和userId就是我们的参数
      path: '/goods',
      name: 'GoodList',
      component: GoodList,
      //设置子路由
      children:[
        {
          path:'title',
          name:Title,
          component:Title
        },
        {
          path:'img',
          name:Image,
          component:Image
        }
      ]
    },
    {
      path:'/cart',
      name:Cart,
      component:Cart
    }

  ]
})

```
更改GoodList.vue，增加一个跳转方法
```html
<template>
    <div>
      这是一个商品列表
      <!--通过$route.params.goodId（定义的路由id）获取参数-->
      <span>{{$route.params.goodId}}</span><br/>
      <span>{{$route.params.userId}}</span>
      <!--建立两个router-link跳转标签-->
      <router-link to="/goods/title">标题</router-link>
      <router-link to="/goods/img">图片</router-link>
      <!--建立一个router-view表现用于加载组件-->
      <div>
        <router-view></router-view>
      </div>
      <!--建立一个router-link和一个button分别演示-->
      <router-link to="/cart">跳转购物车</router-link>
      <button @click="jupm">buttom 跳转购物车</button>
    </div>
</template>
<script>
    export default {
        data() {
            return {msg: '这个是Home模板页'}
        },
      methods:{
          jupm(){
            this.$router.push("/cart?goodId=123");
          }
      }
    }
</script>

```
效果：
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/xiaogouyanzs.gif "xiaogouyanzs")
## 2.5、命名路由和命名视图
命名路由：通过router-link定义名字和参数跳转指定视图
命名视图：router-view定义名字渲染指定子组件
### 2.5.1、命名路由
案例：
修改GoodList.vue定义带有参数的router-link
```html
<router-link v-bind:to="{name:'cart',params:{cartId:123}}">跳转购物车</router-link>
```
修改index.js，路由的名字要和router-link中的名字对应
```js
import Vue from 'vue'
import Router from 'vue-router'
import GoodList from './../views/GoodList'//引入组件
//引入标题子组件和图片子组件
import Title from '@/views/Title'
import Image from '@/views/Image'
import Cart from '@/views/Cart'

Vue.use(Router)

export default new Router({
  routes: [
    {
      //设置路由“：”后面的goodId和userId就是我们的参数
      path: '/goods',
      name: 'GoodList',
      component: GoodList
    },
    {
      path:'/cart/:cartId',
      name:'cart',
      component:Cart
    }

  ]
})
```
效果：可以看到url连接中参数也传过来了
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/xiaogouyanzs.gif "xiaogouyanzs")
### 2.5.2、命名视图
案例：
在App.vue中增加两个router-view标签
```html
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
    <router-view class="left" name="title"></router-view>
    <router-view class="right" name="img"></router-view>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
  .left,.right{
    float: left;
    width: 49%;
    border: 1px solid gray;
  }
</style>
```
修改路由index.js，在根路由中设置组件名称，与App.vue中router-view的name相同
```js
import Vue from 'vue'
import Router from 'vue-router'
import GoodList from './../views/GoodList'//引入组件
//引入标题子组件和图片子组件
import Title from '@/views/Title'
import Image from '@/views/Image'
import Cart from '@/views/Cart'

Vue.use(Router)

export default new Router({
  routes: [
    {
      //设置路由“：”后面的goodId和userId就是我们的参数
      path: '/goods',
      name: 'GoodList',
      components:{
        default:GoodList,
        title:Title,
        img:Image
      }
    },
    {
      path:'/cart/:cartId',
      name:'cart',
      component:Cart
    }

  ]
})
```
效果：页面根据不同的组件渲染页面
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541819097420.png)

---
# 三、Vue-resource和Axios
## 3.1、vue-resourse使用
vue-resourse是vue异步请求的插件，特点体积小
安装vue-resourse
```cmd
cnpm i vue-resource --save
```
支持的HTTP方法
vue-resource的请求API是按照REST风格设计的，它提供了7种请求API：
- get(url, [options])
- head(url, [options])
- delete(url, [options])
- jsonp(url, [options])
- post(url, [body], [options])
- put(url, [body], [options])
- patch(url, [body], [options])

options对象
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541842333739.png)

response对象
response对象包含以下属性
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541842364669.png)

案例：
新建一个vue-resource.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
    <script src="../node_modules/vue/dist/vue.js"></script>
    <script src="../node_modules/vue-resource/dist/vue-resource.js"></script>
</head>
<body>
  <div id="app" class="container">
    <h1>vue-resource插件讲解</h1>
    <a href="javascript:;" class="btn btn-primary" @click="get">get请求</a>
    <a href="javascript:;" class="btn btn-primary" @click="post">post请求</a>
    <div>{{msg}}</div>
  </div>
  <script>
    new Vue({
      el:'#app',
      data:{
          msg:''
      },
      //设置请求根路径
      http:{
        root:"http://localhost:63342/dome1/"
      },
      //全局拦截器
      mounted(){
        Vue.http.interceptors.push(function (request,next) {
          console.log("request init!")
          next(function (response) {
            //请求通过往下一步流转
            console.log("response init!");
            return response;
          })
        })
      },
      methods:{
        //get请求演示
        get(){
          this.$http.get("package.json",{
            params:{
              userId:'101'
            },
            headers:{
              token:'abcd'
            }
          }).then(res=>{
            console.log("success!");
            this.msg =res.data;
          },error=>{
            this.msg = error;
            console.log('fail!');
          })
        },
        //post请求演示
        post(){
          this.$http.post("package.json",{
            userId:'102'
          },{
            headers:{
              access_token:"abcde"
            }
          }).then(res=>{
            console.log("success!");
            this.msg = res.data;
          },error=>{
            console.log('fail!');
            this.msg = error;
          })
        }
      }
    })
  </script>
</body>
</html>
```
效果：
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/sdsd.gif "sdsd")

## 3.2、axios介绍
axios同样是一部请求的插件，是目前官方推荐使用的插件。
安装：
```cmd
cnpm i axios --save
```
```js
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```
API
- axios.request(config)
- axios.get(url[, config])
- axios.delete(url[, config])
- axios.head(url[, config])
- axios.post(url[, data[, config]])
- axios.put(url[, data[, config]])
- axios.patch(url[, data[, config]])

案例：
新建一个vue-axios.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
    <script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
    <script src="../../node_modules/vue-resource/dist/vue-resource.js"></script>
    <script src="../../node_modules/axios/dist/axios.js"></script>
</head>
<body>
  <div id="app" class="container">
    <h1>vue-axios插件讲解</h1>
    <a href="javascript:;" class="btn btn-primary" @click="get">get请求</a>
    <a href="javascript:;" class="btn btn-primary" @click="post">post请求</a>
    <a href="javascript:;" class="btn btn-primary" @click="http">http</a>
    <div>{{msg}}</div>
  </div>
  <script>
    new Vue({
      el:'#app',
      data:{
          msg:''
      },
      //全局拦截器
      mounted(){
        axios.interceptors.request.use(function(config){
          console.log("init request")
          return config;
        });
        axios.interceptors.response.use(function (response) {
          console.log("init response");
          return response;
        })
      },
      methods:{
        //get请求演示
        get(){
          axios.get("../../package.json",{
            params:{
              userId:"111"
            },
            headers:{
              token:"jack"
            }
          }).then(res=>{
            this.msg = res.data;
          }).catch(function (error) {
            console.log("error:"+error);
          })
        },
        //post请求演示
        post(){
          axios.post("../../package.json",{
            userId:"999"
          },{
            headers:{
              token:"tom"
            }
          }).then(res=>{
            this.msg = res.data;
          }).catch(function (error) {
            console.log(error);
          })
        },
        //http请求
        http(){
          axios({
            url:"../../package.json",
            method:"get",
            params:{
              userId:"101"
            },
            headers:{
              token:"abcd"
            }
          }).then(res=>{
            this.msg = res.data;
          }).catch(function (error) {
            console.log(error);
          })
        }
      }
    })
  </script>
</body>
</html>
```
效果：
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541849283846.png)


---
# 四、ES6常用语法
## 4.1、ES6简介

## 4.2、Rest参数和扩展
在ES6中，“...” 称为Rest参数
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
</body>
<script>
  function sum(x,y,z) {
    let total =0;
    if(x)total+=x;
    if(y)total+=y;
    if(z)total+=z;
    console.log(`total:${total}`);
  }
  sum(5,"",9);//结果：14

  //Rest参数方式
  function sum2(...m) {
    let total = 0;
    for (var i of m){
      total += i;
    }
    console.log(`total:${total}`);
  }
  sum2(1,4,22,10);//结果：37

  //ES6中使用箭头函数
  let sum3 = (...m)=> {
    let total = 0;
    for (var i of m){
      total += i;
    }
    console.log(`total:${total}`);
  }
  sum2(1,4,22,10);//结果：37

  //...数组解构
  let [x,y] = [4,5];
  console.log(...[4,5]);//结果 4 5

  //数组合并
  let arr1 = [1,3];let arr2 = [4,5];
//  console.log(arr1.concat(arr2));//结果：[1, 3, 4, 5]
  console.log(...arr1,...arr2);//结果：1 3 4 5

  //...作用在数组中
  var [w,...u] = [1,8,6,7];
  console.log("w:"+w+",u:"+u);//结果：w:1,u:8,6,7

  //...作用在变量上
  let [a,b,c] = "ES6";
  console.log(a,b,c);//结果：E S 6
  let j = [..."ES6"];
  console.log(j);//结果：["E", "S", "6"]
</script>
</html>
```
## 4.3、import和export
export：暴露方法、参数对象
import：加载文件，对象
案例：新建一个util.js
```js
export let sum = (x,y)=>{
  return x+y;
}

export let minus = (x,y)=>{
  return x-y;
}
```
在main.js中引入
```js
import {sum,minus} from './util'
console.log(`sum:${sum(5,8)}`);
console.log(`minus:${minus(10,8)}`);
```
效果：控制台打印结果
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541905089484.png)

## 4.4、Promise讲解
Promise解决的问题是：异步的多重调用问题，当我们异步请求数据的时候，往往要在返回的回调函数中嵌套回调函数，代码臃肿不好维护
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
  <a href="javascript:checkLogin();">登陆</a>
</body>
<script>
  //定义一个登陆函数
  let checkLogin = function (){
    return new Promise((resolve,reject)=>{
	//resolve请求成功回调函数
        resolve({
          status:0,
          result:true
        })
    })
  }
  //定义一个获取用户信息函数
  let getUserInfo = ()=>{
    return new Promise((resolve,reject)=>{
      let userInfo={
        userId:"101"
      }
      resolve(userInfo);
    })
  }
  //调用函数
  checkLogin().then((res)=>{
    if(res.status==0){
      console.log("login success")
      return getUserInfo();
    }
  }).catch((error)=>{
    console.log(error);
  }).then((res2)=>{
    console.log("userId:"+res2.userId);
  })
  //执行多个Promise函数
  Promise.all([checkLogin(),getUserInfo()]).then(([res1,res2])=>{
    console.log(`result1:${res1.result},result2:${res2.userId}`)
  })
</script>
</html>
```
效果：
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1541869054772.png)
## 4.5、AMD、CMD、CommonJS和ES6差异
### 4.5.1、CommonJS

 1. 为JS的表现来制定规范，因为js没有模块的功能所以CommonJS应运而生，它希望js可以在任何地方运行，不只是浏览器中。
同步
 2. CommonJS规范 通过model.exports定义的，在前端浏览器中并不支持
 3. NodeJS是CommonJS规范的实现，webpack 也是以CommonJS的形式来书写的。
 4. CommonJS定义的模块分为: 模块引用(require) ； 模块定义(exports) ； 模块标识(module)

```js
	var foo = require('foo.js');
	var count = 1;
	var plusCount = () => {
	  foo.add(count);
	};
	module.exports = {
	  count,
	  plusCount
	};
```
### 4.5.2、AMD
基于commonJS规范的nodeJS出来以后，服务端的模块概念已经形成，很自然地，大家就想要客户端模块。而且最好两者能够兼容，一个模块不用修改，在服务器和浏览器都可以运行。但是，由于一个重大的局限，使得CommonJS规范不适用于浏览器环境。因为会有一个很大的问题：
```js
	var math = require('math');

　math.add(2, 3);
 ```
 第二行math.add(2, 3)，在第一行require(‘math’)之后运行，因此必须等math.js加载完成。也就是说，如果加载时间很长，整个应用就会停在那里等。您会注意到 require 是同步的。
 因此，浏览器端的模块，不能采用”同步加载”（synchronous），只能采用”异步加载”（asynchronous）。这就是AMD规范诞生的背景。
 CommonJS是主要为了JS在后端的表现制定的，他是不适合前端的，AMD(异步模块定义)出现了，它就主要为前端JS的表现制定规范。
 ```js
define(['./package/lib.js'], function(lib) {
  function say(){
    lib.log('this is fn');
  }
  return {
    say:say
  };
});
```
1.  ./package/lib.js使我们依赖的模块，回调函数中参数lib表示的是引入的模块的所有方法和属性，我们可以调用
2.  后来我们又在当前模块定义了say方法，并return输出
3.  可以看到我们是先引入的模块，后使用的引用模块的方法，所以我们称之为依赖前置

### 4.5.3、CMD
Cmd是SeaJs在推广过程中对模块定义的规范化产出
Cmd： 同步模块定义，是一个概念
SeaJs： SeaJS的作者是前淘宝UED,现支付宝前端工程师玉伯。
原则： 依赖就近原则
```js
// 所有的模块通过define定义 
define(function (require, exports, module) {
  //通过require引入依赖，并不是AMD的前置依赖，
  //而是依赖就近原则，在哪里使用，在哪里引入，就是同步的概念，即用即返回 
  var $ = require('jquery');
  //输出模块中定义的方法 
  exports.sayHello = function () {
    $('#hello').toggle('slow');
  };
});
```
### 4.5.4、ES6
上面的AMD,CMD,CommonJs都是ES5时期的。
ES6中无需引入别的js文件，ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。
ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。

---
# 五、商品列表模块实现
## 5.1、商品列表组件拆分
## 5.2、商品列表数据渲染
## 5.3、实现图片懒加载

---
# 六、Node
## 6.1、linux环境搭建
## 6.2、创建httpserver
## 6.3、通过node加载静态资源
## 6.4、搭建基于expres框架的运行环境
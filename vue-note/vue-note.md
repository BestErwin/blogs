
> 自己看视频做的笔记做下记录好自己查看
> 如果需要视频可以到B站：https://space.bilibili.com/13541565/#/
> 百度云链接:https://pan.baidu.com/s/1Xrhtj0aUJC3GnO7ZDOqG0w 提取码:m605
> 感谢B站up主TikkiPon提供资源。


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
简单的做一个httpserver服务
node.js是遵循common语法规范的，同时也支持ES6的大部分语法
首先建立一个User.js文件
```js
module.exports  = {
 userName:"Jack",
 sayHello: function () {
     return 'Hello';
 }
}

exports.userName = "Tom";
exports.sayHello = function () {
  return 'World';
}
```
exports是将js中的对象输出，供其他文件调用
接着建立一个server.js，建立我们的服务
```js
let user = require('./User');

console.log(`userName:${user.userName}`);

console.log(`I'm ${user.userName},I say ${user.sayHello()}`);

let http = require('http');
let url = require('url');
let util = require('util');

let server = http.createServer((req,res)=>{
  res.statusCode = 200;

  res.setHeader("Content-Type","text/plain; charset=utf-8");
  res.end(util.inspect(url.parse(req.url)));
});

server.listen(3000,'127.0.0.1', ()=>{
  console.log("服务器已经运行，请打开浏览,输入:http://127.0.0.1:3000/ 来进行访问.")
});

```
我们可以通过request()去调用我们需要的模块
server.js中http，url，util等这些事nodjs中自带的模块，具体用法可以查看nodejs官网
写好了服务，别忘了通过listen去监听服务的端口
接着cd进入服务所在的文件夹，通过命令启动服务
```cmd
node server.js
```
效果：
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542122217976.png)
这样我们nodejs的服务demo就完成了。
## 6.3、通过node加载静态资源
### 6.3.1、加载html静态文件
上一节我们我们演示了如何搭建服务和运行服务，一般我们的服务都是需要去访问资源的，那么这个demo就演示node.js如何加载静态资源。
新建一个index.html静态文件；
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h2>hello,测试一下,能否访问到</h2>
</body>
</html>
```
接着新建一个server.js服务
```js
let http = require('http');
let url = require('url');
let util = require('util');
let fs = require('fs');//node.js提供的文件访问模块

let server = http.createServer((req,res)=>{
  //截取url后面的文件名称，如index.html
  var pathname = url.parse(req.url).pathname;
  //把名称打印出来
  console.log("file:"+pathname.substring(1))
  //通过文件模块去加载静态问价
  fs.readFile(pathname.substring(1), function (err,data) {
      if(err){
          res.writeHead(404,{
            'Content-Type':'text/html'
          });
      }else{
        res.writeHead(200,{
          'Content-Type':'text/html'
        });
        //将文件信息写入
        res.write(data.toString());
      }
      //最后监听请求结束
      res.end();
  });
});

server.listen(3000,'127.0.0.1', ()=>{
  console.log("服务器已经运行，请打开浏览,输入:http://127.0.0.1:3000/ 来进行访问.")
});
```
接着我们启动一下服务，在浏览器窗口输入http://127.0.0.1:3000/ index.html可以看到如下效果。
控制台输出
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542426701929.png)
页面输出
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542426719089.png)
这样我们就成功的访问到静态资源了
### 6.3.2、node.js调用第三方接口
刚刚是node.js作为服务端去加载静态资源，那么node.js要作为客户端去
调用第三方的接口获取数据，应该如何做呢？
建一个client.js文件
```js
let http = require('http');//http模块
let util = require('util') //util模块：主要用于打印输出结果

//建议一个get请求，去请求第三方的接口
http.get("http://www.imooc.com/u/card", function (res) {

  /*
  * res.on-->data用于监听接口返回数据，
  * 数据不是一次加载出来的，而是多次，
  * 因此需要用一个变量进行累加
  * */
    res.setEncoding('utf8');
    let data = '';

    res.on('data', function (chunk) {
        data += chunk;
    });
    /*
    * 监听结束，将数据转换成一个对象，便于我们使用
    */
    res.on('end', function () {
        let result = JSON.parse(data);

        console.log("result:"+util.inspect(result))

    })
});

```
启动client.js 看到返回结果
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542428119764.png)

## 6.4、搭建基于express框架的运行环境
express是一个node.js的后台开发框架，底层也是封装了基础的server
下面我们介绍如何搭建一个express的框架
首先全局安装一个express-generator
```cmd
cnpm i -g express-generator
```
安装完检查一下，是否安装成功
```cmd
express --version
```
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542430061477.png)

安装成功，进入项目文件夹构建一个express server
```cmd
express server
```
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542430176337.png)
构建成功会看到项目中多了一个server文件夹
结构如下
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/20181117125907.png)
加载依赖
```cmd
cnpm i
```
启动服务
```cmd
cnpm start 或者 node ./bin/www
```
浏览器输入http://127.0.0.1:3000/
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542430520407.png)
到此express框架就构建好了

---
# 7、MongoDB介绍
## 7.1、window下mongodb环境搭建
## 7.2、2linux平台下的搭建
## 7.3、给mogodb创建用户
## 7.4、mogodb基本语法
## 7.5、表数据设计和插入

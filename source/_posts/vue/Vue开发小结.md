---
layout: '[vue]'
title: Vue开发小结
date: 2019-11-11 19:03:36
tags: vue
categories:
  - vue
---
vue是一套用于构建用户界面的渐进式JavaScript框架，与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，方便与第三方库或既有项目整合。
>数据监听的原理，依赖追踪，数据劫持: vue.js 则是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调

### 1、slot 分发，相当于react的this.props.children 可以把内容 分别发送到 template的指定	 的位置
```html
<v-header title="首页" >
        <a slot="left"> 三 </a>
        <a slot="right">user</a>
</v-header>
<template id="header">
    <div class="header">
        <ul>
            <li><slot name="left"><</slot></li>
            <li class="header-tit">{{title}}</li>
            <li><slot name="right">默认内容</slot></li>
        </ul>
    </div>
</template>
```
### 2、组件通信
- a) 传递：<v-list  :list-data="listData"></v-list>  （注意驼峰命名，在html里面要改成 "-" 连接）
组件内部接收：
```js
props:{
  listData:{
  type:Array,
  default (){
  return [1,2,3,4] //数组和对象需要通过函数返回
  }
  }
}
```
- b) 父组件通过事件传递方法:
```js
  //<v-button @change-num="changeNum"></v-button>
  this.$emit("change-num",num); //子组件通过事件触发父子组件的方法 :
```
- c) Global eventbus
```
  var Event = new Vue();
  Event.$on("changeNum",(num)=>{}) 监听
  Event.$emit("changeNum",num) 触发
```
### 3、数组操作
- a)
```js
this.listData.splice(index,1,{}) //在vue里面，如果直接改变数组的某一项，视图不	会自动更新
//解决方法 ：this.$set(数组，下标, 目标值)   this.$set(this.listData,index,{})
```

### 4、基本路由
- a) 使用路由插件  Vue.use(Router)
- b) 配置路由
```js
const routes =  [
    {
      path: '/',
      name: 'Hello',
      component: Hello
    }
  ]
```
- c) 把配置传入router
```js
const router =  new Router({
  routes
})
```
- d) 对外提供路由接口 `export default router`
- e) `router-link` 可以自动加active选择的样式

### 5、公用组件在main.js全局导入注册,所有页面都可以使用
```js
import Header from './components/Header.vue'
import Content from './components/Content.vue'
Vue.component("v-header",Header)
Vue.component("v-content",Content)
```
### 6、私有的组件 局部注册使用
```js
import CartList from './cart-list'
export default {
  name: 'header',
  components:{
     "v-cart-list": CartList
  }
}
```
### 7、Vue-resource
- a) 安装 `cnpm i vue-resource --save`
- b) 导入Import `VueResource from ‘vue-resource’`
- c) 使用插件 `Vue.use(VueResource )`
- d) 组件内部使用 `this.$http.get()`

### 8、Axios
- a) 安装`cnpm i axios --save`
- b) 导入`import VueResource from ‘axios ’`
- c) 设置 `Vue.prototype.$http= axios`
- d) 组件内部使用this.$http.get()

### 9、服务器代理数据请求
打开config/index.js配置：
```js
  proxyTable: {
    "/api": {
    "target": "http://aura.maizuo.com/api",
    "changeOrigin": true,
    "pathRewrite": {
    "^/api": ""
    }
    },
    "/beibei": {
    "target": "http://api.beibei.com/",
    "changeOrigin": true,
    "pathRewrite": {
    "^/beibei": ""
    }
  }
}
```
### 10、在vue项目中使用Vuex
- a) 安装`vuex`
- b) 创建`store`目录 ，引入`vuex`和`vue`
- c) 使用插件： `Vue.use(Vuex)`
- d) 创建并暴露`store` ： `const store = new Vuex.store({ ...state,...mutations})`
- e) 全局导入`store :  main.js` 导入`store`，传人 `new Vue（{el:’#app’,store,router,....}）`
- f) 在组件内部使用`store`： 通过`this.$store`使用
- g) 怎么用：
      1.通过`computed` 获取数据；
      2.通过`methods`方法修改数据

### 11.组件需要详情数据 detailData（vuex异步的数据操作）

  - 1、在 store里面 添加 detailData:{}
  - 2、在组件内部通过computed获取数据
  - 3、当组件mounted的时候， 发起一个 请求 （action） ，获取商品的真实数据
  - 4、store里面的actions接收到请，get获取服务器数据,获取到数据以后，提交给mutations
  - 5、mutation接收提交的数据，改变store的state，组件会自动更新 =》detailData


### 12、Vuex模块化
- a) 把每一个页面（模块）的内容拆分到不同的js文件，再引入
- b) 在组件内部获取数据时，需要加模块名
```js
computed:{
    cartData(){
        return this.$store.state.cart(模块名).cartData
    }
}
```
### 13、Vuex, mapGetters (传递数据到组件),mapActions（传递方法到组件）
- a) getters 数据解析分拣
传递数据到组件：

```js
computed:{
  ...mapGetters([‘cartData’])
}
```
- b) `mapActions`可以传递`actions`方法到组件的`methods`（组件可以直接调用`action`的方法，不需要`dispatch`了）;
```js
methods:{ //传递action方法给组件
...mapActions([’changeCartDataAction’])
}
@click=”changeCartDataAction({type:1,index})” //事件绑定
```

### 14、异步组件加载`AMD=>require.js）`;

a) 为什么使用:模块过多，打包文件体积过多，加载缓慢
b) 怎么用：
```js
path: '/product', component: resolve => require(['../modules/Product'], resolve;
```
### 15、路由缓存keep-alive
- a) `keep-alive`是vue自带的组件,路由每次改变的时候,vue会重新渲染组件,导致重新请求数据了,`keep-alive`就可以,缓存数据路由变化的时候不重新请求数据了;
- b)   使用方法,就是加在路由属兔中就可以了
```html
<keep-alive >
<router-view/>
<keep-alive >
```
- c)  如果路由加载需要重新加载数据的话在生命周期里面放入`activated`函数,就会执行  而`Mounted`不会执行的;
- d)  除了添加生命周期函数还可以在根标签上加一个 `exclude`
```html
<keep-alive  exclude ="组件名字 例如home"/>
<router-view/>
<keep-alive >
```

### 16丶路由跳转默认是a标签怎么改变成li标签
```html
<router-link to="/index/+ele.id" tag="li"> 	<router-link/>
```

### 16丶如果页面滚动进入其他页面这时滚动会传递处理方法
将代码加入router页面的选项
```js
scrollBehavior(to,from,savePosition){
  return {x:0,y:0}
}
```

### 17丶处理移动端300毫秒的延迟
- a) `fastClick`  main 文件中安装 `npm install fastclick --save`
- b) `import Fastclick from "fastclick"`
- c) 使用`fastClick.attach(document.body)`

### 18丶vue.js项目中，出现css调用background背景图无效？如何解决？
 - a) 正确的代码，示例如下
 ```vue
 <template>
  <div class="demo">
    <!-- 成功引入的三种方法： -->
    <!-- 图1 -->
    <div class="img1"></div>
    <!-- 图2 -->
    <div class="img2" :style="{backgroundImage: 'url(' + bg2 + ')' }"></div>
    <!-- 图3 -->
    <img src="~@/../static/images/logo3.png" width="100">
  </div>
</template>

<script>
import Bg2 from '@/../static/images/logo2.png'

export default {
    name: 'App',
    data () {
        return {
            bg2: Bg2,
        }
    }
}
</script>

<style>
    .demo{width: 100px;margin: 50px auto;}
    .img1{
        width: 100px;
        height: 100px;
        background: url('~@/../static/images/logo1.png') center center no-repeat;
        background-size: 100px auto;
    }
    .img2{
        width: 100px;
        height: 100px;
        background-position: center center;
        background-repeat:  no-repeat;
        background-size: 100px auto;
    }
</style>
```
具体参考官方文档： [Class 与 Style 绑定](https://cn.vuejs.org/v2/guide/class-and-style.html);

>如果你用了vue-cli脚手架，在build/utils.js中找到ExtractTextPlugin位置在对象中加入这句publicPath: ../../就行了(本人未测试)。
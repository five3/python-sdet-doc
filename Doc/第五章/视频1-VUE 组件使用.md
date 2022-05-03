# VUE 组件使用

`VUE`中组件类似于`Python`中函数的作用，主要是组织通用的代码块便于复用。其使用方式与函数也是类似。
1. 组件定义（定义）
1. 组件复用（调用）
1. 向组件传递数据(传参)
1. 监听组件事件（回调）
1. 组件插槽（重写）

## 组件定义
语法
```html
Vue.component(tagName, options)
```
示例
```html
Vue.component('btn', { 
 data: function () { 
   return { 
    count: 0 
   } 
 }, 
 template: '<button v-on:click="count++">单击次数：{{ count }}</button>' 
})
```

## 组件复用
```html
<div id="app"> 
  <btn></btn> 
</div> 
<script type="text/javascript"> 
 // 组件定义与注册
 Vue.component('btn', { 
   data: function () { 
     return { 
      count: 0 
     } 
   }, 
   template: '<button v-on:click="count++">单击次数：{{ count }}</button>' 
 }) 
 // VUE实例化
 var app = new Vue({ 
 el: '#app' 
 })
</script>
```

## 向组件传递数据
```html
<div id="app"> 
 <btn name="Python"></btn> 
 <btn name="Java"></btn> 
</div> 
<script type="text/javascript"> 
 // 组件定义与注册
 Vue.component('btn', { 
   props: ['name'], 
   template: '<button>{{ name }}</button>' 
 }) 
 // VUE实例化
 var app = new Vue({ 
   el: '#app' 
 }) 
</script>
```

## 监听组件事件
```html
<div id="app"> 
 <btn v-on:incr="count++"></btn>
 <span>计数：{{ count }}</span>
</div> 
<script type="text/javascript"> 
 // 组件定义与注册
 Vue.component('btn', { 
   props: ['name'], 
   template: '<button v-on:click="$emit('incr')">单击增加</button>' 
 }) 
 // VUE实例化
 var app = new Vue({ 
   el: '#app',
   data: {
    count: 0
   }
 }) 
</script>
```

## 组件插槽
```html
<div id="app"> 
 <tips>
   这是插槽内容
 </tips>
</div> 
<script type="text/javascript"> 
 // 组件定义与注册
 Vue.component('tips', { 
   template: ' 
     <div class="demo-alert-box"> 
     <strong>Error!</strong> 
     <slot></slot> 
     </div> 
   ' 
 })
 // VUE实例化
 var app = new Vue({ 
   el: '#app'
 }) 
</script>
```

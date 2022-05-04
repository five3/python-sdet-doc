# ajax 请求全局配置

## 库安装
```bash
npm install axios -g
```

## 前端使用
```html
<!-- 引入 Vue 库 --> 
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script> 
<!-- 引入 axios 库 --> 
<script src="https://cdn.staticfile.org/axios/0.18.0/axios.min.js"></script> 
<div id="app">
 <input type="button" @click=sendHTTP value="发送请求" /> 
 <div>响应数据：{{ responseData }}</div> 
</div> 
<script type="text/javascript"> 
 var app = new Vue({ 
   el: '#app', 
   data: { 
    responseData: null 
   }, 
   methods: { 
     sendHTTP () { 
       // 发送 HTTP 请求
       axios 
       .get('http://httpbin.org/get') 
       .then(response => (this.responseData = response)) 
       .catch(function (error) { 
          console.log(error) 
       }) 
     } 
   } 
 }) 
</script>
```

## 全局配置
```javascript
// 默认基础url配置
axios.defaults.baseURL = 'https://api.example.com';
// 默认请求头配置
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;  // 对所有请求生效
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';  // 仅对post请求生效
```

## 实例配置
```javascript
// 创建时配置
const instance = axios.create({
  baseURL: 'https://api.example.com'
});
// 实例对象配置
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
instance.defaults.timeout = 2500;
```

## 配置优先级
调用配置 > 实例配置 > 全局配置

## 拦截配置
```javascript
// 请求拦截
axios.interceptors.request.use(function (config) {
    // 请求发送前触发
    return config;
  }, function (error) {
    // 请求错误时触发
    return Promise.reject(error);
  });

// 响应拦截
axios.interceptors.response.use(function (response) {
    // 2xx 状态触发此回调
    return response;
  }, function (error) {
    // 非2xx 状态处罚法此回调
    return Promise.reject(error);
  });
```

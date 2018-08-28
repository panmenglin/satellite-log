# 基于 axios 的 Vue 项目 http 请求优化

对于需要大量使用 `http` 请求的项目，我们通常会选择对 `http` 请求的方法进行二次封装，以便增加统一的拦截器，或者统一处理阻止重复提交之类的逻辑。`Vue.js` 的项目中我们选择使用了 `axios` 这样一个 `http` 库，下面也就简述下基于 `axios` 做的简单二次封装

## 依赖

首先引入 `axios` ，对于 `ie9` 这样不支持 `promise` 的浏览器还需引入 `es6-promise` 模块

```javascript
require('es6-promise').polyfill();
var axios = require('axios');
```

### `axios` 初始化

初始化我们要实现两个需求：
1.发送请求时带上 `cookies `
2.重发发送请求时，如果前一次相同请求还未结束则中止前一次请求

```
const httpServer = axios.create({
    responseType: 'json',
    withCredentials: true,  // 设置 withCredentials 使请求带上 `cookies`
    cancelToken: new axios.CancelToken(function (c) {
        cancel = c  // 记录当前请求的取消方法
    })
})
```

### `http` 请求二次封装

```javascript
var promiseArr = {}  // 用于记录每个请求的取消方法

const gUtils = {
    getData: function () {
        let cancel
        const httpServer = axios.create({
            responseType: 'json',
            withCredentials: true,  // 设置 withCredentials 使请求带上 `cookies`
            cancelToken: new axios.CancelToken(function (c) {
                cancel = c  // 记录当前请求的取消方法
            })
        })
        
        // 设置一个拦截器，每次发起请求前取消掉在进行中的相同请求
        httpServer.interceptors.request.use(function (config) {
          if (promiseArr[config.url]) {
            promiseArr[config.url]('操作取消')
            promiseArr[config.url] = cancel
          } else {
            promiseArr[config.url] = cancel
          }
    
          return config
        }, function (err) {
          // return Promise.reject (error)
        })
    
        return httpServer
    }
}

```


这样我们在对接服务时候直接使用我们封装好的 `http` 请求方法即可
# 小程序问题

1. 小程序跳转其他小程序，需要两个小程序同时关联统一个微信公众号，即便两个小程序关联了同一个开放平台账号，即open账号，也是不行的

2. 原跳转其他小程序接口 `wx.navigateToMiniProgram` 即将下线，建议均使用 `navigator` 组件替代

```
<navigator target="miniProgram" app-id="{{item.appId}}" version="develop"></navigator>

```

其中 target 指定 miniProgram, app-id 为跳转至小程序的 appid，version 指定跳转至小程序的版本，develop 为开发版，trial 为体验版，release 为正式版

无论该参数怎么设置，如果当前小程序是正式版，则打开的必定是正式版
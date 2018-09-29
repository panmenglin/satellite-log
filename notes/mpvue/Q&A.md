# mpvue 问题

1. 多个页面的 `created` 事件在首页被一次性触发

2. 小程序 `onReady` 后，再去触发 `vue` `mounted` 生命周期

3. 有且只能使用单文件组件（`.vue` 组件）的形式进行支持。其他的诸如：动态组件，自定义 `render`，和 `<script type="text/x-template">` 字符串模版等都不支持。原因很简单，因为我们要预编译出 `wxml`。

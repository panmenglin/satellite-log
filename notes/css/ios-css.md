# ios 兼容性

1. 页面设置了 `overflow: auto/scroll` 滚动不流畅

```css
-webkit-overflow-scrolling: touch
```

2. ios 8.1 无法执行 css3 动画

增加 webkit 前缀

```
-webkit-transform

-webkit-animation
```
# ios 兼容性

1. 页面设置了 `overflow: auto/scroll` 滚动不流畅

```css
-webkit-overflow-scrolling: touch
```

2. ios 8.1 无法执行 css3 动画

增加 webkit 前缀

```css
-webkit-transform

-webkit-animation
```

3. 清除 select 默认样式, 统一 safari 和 chrome 样式

```css
select {
  -webkit-appearance: none;
  appearance: none;
}
```
# 位移动画使用 translate 替代其他位移属性

translate 在实现移动时不会发生原始元素重绘，也不会触发其他元素的绘制

css animation 使用 left 时的帧率图以及、事件耗时情况，

帧率波动明显，rendering 耗时长

![图片描述](./css-translate/01.png)

css animation 使用 translateX 时的帧率图以及、事件耗时情况

帧率波动平滑，rendering 耗时短

![图片描述](./css-translate/02.png)



css animation 使用 left 时页面事件执行情况，

update layer 在重复执行

![图片描述](./css-translate/03.png)

css animation 使用 translateX 时页面事件执行情况，

update layer 只执行一次

![图片描述](./css-translate/04.png)

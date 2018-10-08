# 基础

## this

作为对象的方法调用。 

作为普通函数调用。 

构造器调用。 new 

Function.prototype.call 或 Function.prototype.apply 调用。


## Function.prototype.call 和 Function.prototype.apply


## 闭包

变量的生存周期

```javascript
var nodes = document. getElementsByTagName( 'div' ); 

for ( var i = 0, len = nodes. length; i < len; i++ ){ 
  nodes[ i ].onclick = function(){ 
    console.log( i ); 
  } 
};
```

```javascript
for ( var i = 0, len = nodes. length; i < len; i++ ){ 
  (function( i ){ 
    nodes[ i ].onclick = function(){ 
      console.log( i ); 
    } 
  })( i ) 
};

```

闭包的作用

1.封装变量

2.延续局部变量的寿命

```javascript
var report = function( src ){ 
  var img = new Image(); 
  img.src = src; 
}; 

report( 'http://xxx.com/getUserInfo' );
```

```javascript
var report = (function(){ 
  var imgs = []; 
  return function( src ){ 
    var img = new Image(); 
    imgs.push( img ); 
    img.src = src; 
  } 
})();
```

高阶函数

函数可以作为参数被传递； 
函数可以作为返回值输出。


曾探. JavaScript设计模式与开发实践 (图灵原创) (p. 24). 人民邮电出版社. Kindle 版本. 
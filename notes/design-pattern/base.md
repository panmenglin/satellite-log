# 基础

读书笔记

曾探. JavaScript设计模式与开发实践 (图灵原创). 人民邮电出版社. Kindle 版本. 

---

## this

this 的指向大致分以下 4 中情况

1. 作为对象的方法调用

this 指向该对象

2. 作为普通函数调用

this 指向全局对象

3. 构造器调用

例如 new 运算符

构造函数通常会返回一个对象，this 指代这个对象

4. Function.prototype.call 或 Function.prototype.apply 调用

可以动态改变 this

## call 和 apply

### 用途

1. 改变 this 指向

2. 实现 bind 

3. 借用其他对象的方法

例如：借用 map 方法, 循环并返回一个数组

```javascript
let len = 5;
let start = -3;

let list = Array.apply(null, {length: len}).map(() => { start++; return start })

console.log(list) // [-2, -1, 0, 1, 2]
```

## 闭包

### 变量的生存周期

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

### 闭包的作用

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

## 高阶函数

函数可以作为参数被传递 或者 函数可以作为返回值输出。

### 高阶函数实现 AOP

通过扩展 Function.prototype 来实现面向切面编程

```javascript
Function.prototype.before = function( beforefn ){ 
  var __self = this; // 保存 原函数 的 引用 
  return function(){ // 返回 包含 了 原函数 和 新 函数 的" 代理" 函数 
    beforefn.apply( this, arguments ); // 执行 新 函数， 修正 this 
    return __self.apply( this, arguments ); // 执行 原函数 
  } 
}; 

Function.prototype.after = function( afterfn ){ 
  var __self = this;
  return function(){ 
    var ret = __self.apply( this, arguments ); 
    afterfn.apply( this, arguments ); 
    return ret; 
  } 
}; 

var func = function(){ 
  console.log( 2 ); 
}; 

func = func.before( 
  function(){ 
    console.log( 1 ); 
  }
).after( 
  function(){ 
    console.log( 3 ); 
  }
); 
  
func();
```

### 函数柯里化 - currying

```javascript
var currying = function( fn ){ 
  var args = []; 
  return function(){ 
    if ( arguments.length === 0 ){ 
      return fn.apply( this, args ); 
    }else{ 
      [].push.apply( args, arguments ); 
      return arguments.callee; 
    } 
  } 
};
```

### 反柯里化 - uncurrying

```javascript
Function.prototype.uncurrying = function () { 
  var self = this; // self 此时是 Array.prototype.push 
  return function() { 
    var obj = Array.prototype.shift.call( arguments ); 
    // obj 是 { 
    // "length": 1, 
    // "0": 1 
    // } 
    // arguments 对象的第一个元素被截去，剩下[2] 
    return self.apply( obj, arguments ); // 相当于 Array.prototype.push.apply( obj, 2 ) 
  }; 
};

var push = Array.prototype.push.uncurrying(); 
var obj = { 
  "length": 1, 
  "0": 1 
}; 

push( obj, 2 ); 
console. log( obj ); // 输出：{ 0: 1, 1: 2, length: 2}
```

### 节流函数

### 分时函数

### 惰性加载函数
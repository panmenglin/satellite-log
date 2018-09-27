# 原型模式

读书笔记

曾探. JavaScript设计模式与开发实践 (图灵原创). 人民邮电出版社. Kindle 版本. 

---

原型模式不单是一种设计模式，也被称为一种编程范型，在某种程度上它构成了 `JavaScript` 的根本

其特点主要有以下几点：

## 1. 所有的数据都是对象。 

虽然严格意义上不能说 `JavaScript` 中所有数据都是对象，但绝大部分数据都是对象

nummber、boolean、string 这几种基本类型数据也可以通过 包装类 的方式编程对象处理

## 2. 要得到一个对象，不是通过实例化类，而是找到一个对象作为原型并克隆它。

每一个对象都是基于另一个对象的克隆，而克隆是创建对象的手段

`JavaScript` 中有着跟对象 `Object.prototype` 对象，我们遇到的所有对象，以及上都是从  `Object.prototype` 克隆而来，也就是说  `Object.prototype` 是他们的原型

```javascript
var obj1 = new Object(); 
var obj2 = {};
```

```javascript
console. log( Object. getPrototypeOf( obj1 ) === Object. prototype ); // 输出： true 

console. log( Object. getPrototypeOf( obj2 ) === Object. prototype ); // 输出： true
```

可以看到这里定义对象的两种方式，原型都是 `Object.prototype`

## 3. 对象会记住它的原型。 

`JavaScript` 给对象提供了一个名为 `__ proto__` 的隐藏属性，某个对象的 `__ proto__` 属性默认会指向它的构造器的原型对象


## 4. 如果对象无法响应某个请求，它会把这个请求委托给它自己的原型。

这其实对应着原型链委托机制

当一个对象无法响应某个请求的时候，它会顺着原型链把请求传递下去，直到遇到一个可以处理该请求的对象为止

```javascript
Object.getPrototypeOf(a) === Object.prototype
```

```javascript
function Person( name ){
   this.name = name; 
}; 

Person.prototype.getName = function(){ 
  return this.name; 
}; 

var a = new Person( 'sven' ) // 构造函数

console. log( a.name ); // 输出： sven 
console. log( a.getName() ); // 输出： sven 
console. log( Object. getPrototypeOf( a ) === Person. prototype ); // 输出： true
```


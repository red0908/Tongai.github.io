## 【JS基础】深浅拷贝的札记

前段时间一直忙着面试，现在稳定下来，回过头整理这段时间的一些心得感悟。这篇文章讲的是**深拷贝**这个话题，这在面试中是一个高频问题，回顾自己答题的过程，发现对于这个问题的理解还是不够全面透彻的，所以特意搜集了一些精选博文，做了一次汇总学习札记，并以此作为本人技术写作之路上的第一篇博文。

### 什么是深拷贝？

看问题最佳的方式就是需要透过现象看本质，找到事物最本质的定义，理解它的起承转合，才能将它理解透彻。所以我们这边来讲讲什么是深拷贝，弄清晰它最本质的定义。

拷贝其实通俗的讲法就是做副本，亦或者可以简单的理解为做一个一模一样的克隆体。在前端领域中，JS的深拷贝有它同于一些常见编程语言的特殊之处。讲清楚这个就不得不提到，和它息息相关的兄弟——“浅拷贝”。

#### 浅拷贝

关于浅拷贝的定义：

> 当我们以一个对象作为本体，拷贝一个具有相关属性和值得副本对象时，像一些Number、String之类的原始类型的属性值都是存储于计算机内存中的某处，在做对象拷贝的时候，给新对象的相关属性值进行一个简单的赋值，可以将变量的内容复制到另外一个变量内存中。
>
> 但对于项Object或者Array这类的引用类型来说，对象的属性值实际描述的其实是一个内存地址。假如源属性值是一个对象的引用，它仅仅会复制其引用值，当它改变会进而影响到另一个对象（原对象相关属性）。

#### 深拷贝

借用掘金上一篇精选博文的话，我们得到以下定义：

> 将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且修改新对象不会影响原对象。

### 怎么实现深浅拷贝？

在说深拷贝实现方法之前我们先来记录一些常见的浅拷贝实现方式。

#### 1. Object.assign()

> 定义：`Object.assign()` 方法用于将所有可枚举属性的值从一个或多个源对象分配到目标对象。它将返回目标对象。

```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }

```

使用Object.assign()做对象拷贝需要注意的点：

* 无法进行深拷贝，假如源值是一个对象的引用，它仅仅会复制其引用值。
* 继承属性和不可枚举属性是不能拷贝的
* 原始类型会被包装为对象
* 异常会打断后续拷贝任务

####  2. 函数库lodash的_.clone方法

创建一个 `value` 的浅拷贝。

**注意**: 这个方法参考自[structured clone algorithm](https://mdn.io/Structured_clone_algorithm) 以及支持 arrays、array buffers、 booleans、 date objects、maps、 numbers， `Object` 对象, regexes, sets, strings, symbols, 以及 typed arrays。 `arguments`对象的可枚举属性会拷贝为普通对象。 一些不可拷贝的对象，例如error objects、functions, DOM nodes, 以及 WeakMaps 会返回空对象。

Eg :

```js
var objects = [{ 'a': 1 }, { 'b': 2 }];
 
var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true

```

#### 3. ...扩展运算符

对象的扩展运算符（`...`）用于取出参数对象的所有可遍历属性，拷贝到当前对象之中。

```js
let z = { a: 3, b: 4 };
let n = { ...z };
n // { a: 3, b: 4 }
```

#### 4. Array.prototype.concat()

`concat()` 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。数组和/或值，将被合并到一个新的数组中。如果省略了所有 `valueN` 参数，则 `concat` 会返回调用此方法的现存数组的一个浅拷贝。

```js
const array1 = ['a', 'b', 'c'];
const array2 = ['d', 'e', 'f'];
const array3 = array1.concat(array2);

console.log(array3);
// expected output: Array ["a", "b", "c", "d", "e", "f"]
```

#### 5.Array.prototype.slice()

``slice()`` 方法返回一个新的数组对象，这一对象是一个由 `begin` 和 `end` 决定的原数组的**浅拷贝**（包括 `begin`，不包括`end`）。原始数组不会被改变。

```js
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// expected output: Array ["camel", "duck"]

console.log(animals.slice(1, 5));
// expected output: Array ["bison", "camel", "duck", "elephant"]
```

说完上面，下面就到我们的重头戏，深拷贝实现方式了。

#### 基础版深拷贝

首先，我们要看的是经常用到的做深拷贝的，``JSON.stringfy ``和 ``JSON.parse``。

```js
let obj = {
  a: 1,
  b: {c: 2}
}
let objClone = JSON.parse(JSON.stringfy(obj))
```

这样的做法在实现一些简单场景下的深拷贝，是非常方便的。

但在一些复制或者被将被频繁使用到的业务场景里，我们要避免使用它，因为它会有一些缺点，如不能处理函数，以及正则对象。这两者基于JSON.stringify和JSON.parse处理后，得到的正则就不再是正则（变为空对象），得到的函数就不再是函数（变为null）了。

**重点来了👇🏻：**

以个人经验来说，在面试过程中如果想要在深拷贝这个问题里，达到一个普通答得上的标准（即不够惊艳深入，初级合格程度），那么至少要能够写出（描述）下面的深拷贝代码。

```js
function deepClone (Obj) {
  if (typeof obj === 'Object') {
    let newObj = Obj instansof Array ? [] : {}
    for (let key  in obj) {
      newObj[key] = deepClone(obj[key])
    }
    return newObj
  } else {
    return obj
  }
}
```

**函数库lodash的_.cloneDeep方法**

这个方法类似[`_.clone`](https://www.lodashjs.com/docs/lodash.cloneDeep#clone)，除了它会递归拷贝 `value`。（注：也叫深拷贝）。

```js
var objects = [{ 'a': 1 }, { 'b': 2 }];
 
var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

#### 高级版深拷贝

不过经验身后的大佬都看得出来，基础版的深拷贝并不完美，比如以下几点：

* 循环引用
* 性能优化
* 其它类型

**循环引用**

如果我们要复制的对象存在循环引用的结构（即对象的属性间接或直接的引用了自身的情况），那使用上面的深拷贝函数，就会将它绕成了一个死循环。

这个问题我们可以看一篇[精选博文](https://juejin.cn/post/6844903929705136141#heading-3)给出的解答：

> 解决循环引用问题，我们可以额外开辟一个存储空间，来存储当前对象和拷贝对象的对应关系，当需要拷贝当前对象时，先去存储空间中找，有没有拷贝过这个对象，如果有的话直接返回，如果没有的话继续拷贝，这样就巧妙化解的循环引用的问题。
>
> 这个存储空间，需要可以存储`key-value`形式的数据，且`key`可以是一个引用类型，我们可以选择`Map`这种数据结构：
>
> - 检查`map`中有无克隆过的对象
> - 有 - 直接返回
> - 没有 - 将当前对象作为`key`，克隆对象作为`value`进行存储
> - 继续克隆

```js
function clone(target, map = new Map()) {
    if (typeof target === 'object') {
        let cloneTarget = Array.isArray(target) ? [] : {};
        if (map.get(target)) {
            return map.get(target);
        }
        map.set(target, cloneTarget);
        for (const key in target) {
            cloneTarget[key] = clone(target[key], map);
        }
        return cloneTarget;
    } else {
        return target;
    }
};
```

而如果将`WeakMap`提代`Map`来使代码达到画龙点睛的作用。详情请查阅原始[博文](https://juejin.cn/post/6844903929705136141#heading-3)

这里只是对``weakMap``和弱引用做一个简单的笔记：

> WeakMap 对象是一组键/值对的集合，其中的键是弱引用的。其键必须是对象，而值可以是任意的。

什么是弱引用呢？

> 在计算机程序设计中，弱引用与强引用相对，是指不能确保其引用的对象不会被垃圾回收器回收的引用。 一个对象若只被弱引用所引用，则被认为是不可访问（或弱可访问）的，并因此可能在任何时刻被回收。

**进阶优化**

我们遍历数组和对象都使用了`for in`这种方式，实际上`for in`在遍历时效率是非常低的，具体参见原始[博文](https://juejin.cn/post/6844903929705136141#heading-3)

```js
function clone(target, map = new WeakMap()) {
    if (typeof target === 'object') {
        const isArray = Array.isArray(target);
        let cloneTarget = isArray ? [] : {};

        if (map.get(target)) {
            return map.get(target);
        }
        map.set(target, cloneTarget);

        const keys = isArray ? undefined : Object.keys(target);
        forEach(keys || target, (value, key) => {
            if (keys) {
                key = value;
            }
            cloneTarget[key] = clone2(target[key], map);
        });

        return cloneTarget;
    } else {
        return target;
    }
}

```

**其它类型**

在上面的代码中，我们其实只考虑了普通的`object`和`array`两种数据类型，实际上所有的引用类型远远不止这两个，像是`function`和`null`、`Symbol`、`Map`，`Set`...

具体可以参见原始[博文](https://juejin.cn/post/6844903929705136141#heading-3)和[代码](https://github.com/ConardLi/ConardLi.github.io/blob/master/demo/deepClone/src/clone_6.js)

### 小结

对于一个问题的解答，通常能反应出我们在哪些方面的知识是掌握的较好，哪些方面是有所欠缺，或是还未曾了解的。

我们要学会一个将一个问题从广度方面去理解，学会一题多解，发散思维看问题；也要将一个问题的某一种解答方式想透，深入其本质源头去纵向分析，学会追根溯源。

由此可见，一个小小的深拷贝还是隐藏了很多的知识点：

基本实现

- 递归能力

循环引用

- 考虑问题的全面性
- 理解weakmap的真正意义

多种类型

- 考虑问题的严谨性
- 创建各种引用类型的方法，JS API的熟练程度
- 准确的判断数据类型，对数据类型的理解程度

通用遍历：

- 写代码可以考虑性能优化
- 了解集中遍历的效率
- 代码抽象能力

拷贝函数：

- 箭头函数和普通函数的区别

- 正则表达式熟练程度

  

### 附录

[如何写出一个惊艳面试官的深拷贝?](https://juejin.cn/post/6844903929705136141#heading-1)

[浅拷贝与深拷贝](https://juejin.cn/post/6844904197595332622#heading-7)

[JavaScript浅拷贝和深拷贝](https://www.kancloud.cn/ljw789478944/interview/397319)

[Object.assign](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

[lodash](https://www.lodashjs.com/)

[ECMAScript 6 入门](https://es6.ruanyifeng.com/#docs/object)

### 后记

我是彤爱，一个在沉溺于寂寞代码海洋里的前端程序员👨🏻‍💻

欢迎各位大佬的赐教🙏

期待与同样在努力摸索的小伙伴们交流🙌
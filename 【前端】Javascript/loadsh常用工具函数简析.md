# loadsh 常用工具函数札记

### loadsh 简介

[Lodash](https://www.lodashjs.com/) 是一个一致性、模块化、高性能的 JavaScript 实用工具库。

**安装**

浏览器环境

```html
<script src="lodash.js"></script>
```

通过 npm：

```sh
$ npm i -g npm
$ npm i --save lodash
```

Node.js：

```js
// Load the full build.
var _ = require('lodash');
// Load the core build.
var _ = require('lodash/core');
// Load the FP build for immutable auto-curried iteratee-first data-last methods.
var fp = require('lodash/fp');
 
// Load method categories.
var array = require('lodash/array');
var object = require('lodash/fp/object');
 
// Cherry-pick methods for smaller browserify/rollup/webpack bundles.
var at = require('lodash/at');
var curryN = require('lodash/fp/curryN');
```

**为什么选择 Lodash?** 

Lodash 通过降低 array、number、objects、string 等等的使用难度从而让 JavaScript 变得更简单。 Lodash 的模块化方法 非常适用于：

- 遍历 array、object 和 string
- 对值进行操作和检测
- 创建符合功能的函数

#### 数组

[_.drop](https://www.lodashjs.com/docs/lodash.drop): 创建一个切片数组，去除`array`前面的`n`个元素。（`n`默认值为1。）

[_.flatten](https://www.lodashjs.com/docs/lodash.flatten#_flattenarray): 减少一级`array`嵌套深度。

[_.flattenDeep](https://www.lodashjs.com/docs/lodash.flattenDeep#_flattendeeparray): 将`array`递归为一维数组。

[_.nth](https://www.lodashjs.com/docs/lodash.nth): 获取`array`数组的第n个元素。如果`n`为负数，则返回从数组结尾开始的第n个元素。

[_.reverse](https://www.lodashjs.com/docs/lodash.reverse): 反转`array`，使得第一个元素变为最后一个元素，第二个元素变为倒数第二个元素，依次类推。

[_.slice](https://www.lodashjs.com/docs/lodash.slice): 裁剪数组`array`，从 `start` 位置开始到`end`结束，但不包括 `end` 本身的位置。

[_.remove](https://www.lodashjs.com/docs/lodash.remove): 移除数组中`predicate`（断言）返回为真值的所有元素，并返回移除元素组成的数组。

[_.pull](https://www.lodashjs.com/docs/lodash.pull):移除数组`array`中所有和给定值相等的元素，使用[`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 进行全等比较。

[_.pullAt](https://www.lodashjs.com/docs/lodash.pullAt): 根据索引 `indexes`，移除`array`中对应的元素，并返回被移除元素的数组。

[_.fill](https://www.lodashjs.com/docs/lodash.fill): 使用 `value` 值来填充（替换） `array`，从`start`位置开始, 到`end`位置结束（但不包含`end`位置）。

[_.concat](https://www.lodashjs.com/docs/lodash.concat): 创建一个新数组，将`array`与任何数组 或 值连接在一起。

#### 集合

[_.groupBy](https://www.lodashjs.com/docs/lodash.groupBy#_groupbycollection-iteratee_identity): 创建一个对象，返回一个组成聚合的对象。

[_.keyBy](https://www.lodashjs.com/docs/lodash.keyBy#_keybycollection-iteratee_identity)： 创建一个对象组成， 返回一个组成聚合的对象。

[_.flatMap]([#](https://www.lodashjs.com/docs/lodash.flatMap#_flatmapcollection-iteratee_identity)): 创建一个扁平化（注：同阶数组）的数组。

[_.flatMapDeep](https://www.lodashjs.com/docs/lodash.flatMapDeep#_flatmapdeepcollection-iteratee_identity): 这个方法类似_.flatMap，不同之处在于它会继续扁平化递归映射的结果。

[_.reduce](https://www.lodashjs.com/docs/lodash.reduce#_reducecollection-iteratee_identity-accumulator): 压缩集合为一个值, 返回累加后的值。

[_.every](https://www.lodashjs.com/docs/lodash.every#_everycollection-predicate_identity): 检查集合内是否**所有**元素都满足一个条件函数。

[_.some](https://www.lodashjs.com/docs/lodash.some#_somecollection-predicate_identity) : 检查集合内是否**存在**元素都满足一个条件函数。

#### 函数

[_.after](https://www.lodashjs.com/docs/lodash.after#_aftern-func): [`_.before`](https://www.lodashjs.com/docs/lodash.after#before)的反向函数;此方法创建一个函数，当他被调用`n`或更多次之后将马上触发`func` 。

[_.before](https://www.lodashjs.com/docs/lodash.before#_beforen-func): 创建一个调用`func`的函数，通过`this`绑定和创建函数的参数调用`func`，调用次数不超过 `n` 次。 之后再调用这个函数，将返回一次最后调用`func`的结果。

[_.debounce](https://www.lodashjs.com/docs/lodash.debounce#_debouncefunc-wait0-options) :创建一个 debounced（防抖动）函数, 该函数会从上一次被调用后，延迟 xxxx毫秒后调用 `func` 方法。

[_.throttle](https://www.lodashjs.com/docs/lodash.throttle#_throttlefunc-wait0-options): 创建一个节流函数，在 wait 秒内最多执行 `func` 一次的函数。

#### 语言

[_.clone](https://www.lodashjs.com/docs/lodash.clone#_clonevalue) :创建一个 `value` 的浅拷贝。

[_.cloneDeep](https://www.lodashjs.com/docs/lodash.cloneDeep#_clonedeepvalue) : 这个方法类似[`_.clone`](https://www.lodashjs.com/docs/lodash.cloneDeep#clone)，除了它会递归拷贝 `value`。

[_.isEmpty](https://www.lodashjs.com/docs/lodash.isEmpty#_isemptyvalue) : 检查 `value` 是否为一个空对象，集合，映射或者set。

[_.isEqual](https://www.lodashjs.com/docs/lodash.isEqual#_isequalvalue-other) :执行深比较来确定两者的值是否相等。

[_.isArray](https://www.lodashjs.com/docs/lodash.isArray#_isarrayvalue) : 检查 `value` 是否是 `Array` 类对象。

[_.isNaN](https://www.lodashjs.com/docs/lodash.isNaN#_isnanvalue): 检查 `value` 是否是 `NaN`。

[_.isNil](https://www.lodashjs.com/docs/lodash.isNil#_isnilvalue) : 检查 `value` 是否是 `null` 或者 `undefined`。

[_isNull](https://www.lodashjs.com/docs/lodash.isNull#_isnullvalue): 检查 `value`alue 是否是 `null`。

[_.isUndefined](https://www.lodashjs.com/docs/lodash.isUndefined#_isundefinedvalue): 检查 `value` 是否是 `undefined`.

[_.isObject](https://www.lodashjs.com/docs/lodash.isObject#_isobjectvalue):检查 `value` 是否为 `Object` 的[language type](http://www.ecma-international.org/ecma-262/6.0/#sec-ecmascript-language-types)。

[_.toArray](https://www.lodashjs.com/docs/lodash.toArray#_toarrayvalue) : 转换 `value` 为一个数组。

[_.toFinite](https://www.lodashjs.com/docs/lodash.toFinite#_tofinitevalue) : 转换 `value` 为一个有限数字。

[_.toInteger](https://www.lodashjs.com/docs/lodash.toInteger#_tointegervalue): 转换 `value` 为一个整数。

#### 数学

[_.ceil](https://www.lodashjs.com/docs/lodash.ceil#_ceilnumber-precision0): 根据 `precision`（精度） 向上舍入 `number`。

[_.floor](https://www.lodashjs.com/docs/lodash.floor): 根据 `precision`（精度） 向下舍入 `number`。

[_.min](https://www.lodashjs.com/docs/lodash.min):  计算 `array` 中的最小值。 如果 `array` 是 空的或者假值将会返回 `undefined`。

[_.max](https://www.lodashjs.com/docs/lodash.max):  计算 `array` 中的最大值。 如果 `array` 是 空的或者假值将会返回 `undefined`。

[_.mean](https://www.lodashjs.com/docs/lodash.mean): 计算 `array` 的平均值。

#### 数字

[_.random](https://www.lodashjs.com/docs/lodash.random#_randomlower0-upper1-floating): 产生一个包括 `lower` 与 `upper` 之间的数。

#### 对象

[_.create](https://www.lodashjs.com/docs/lodash.create)：创建一个继承 `prototype` 的对象。 如果提供了 `prototype`，它的可枚举属性会被分配到创建的对象上。

[_.assign](https://www.lodashjs.com/docs/lodash.assign)：分配来源对象的可枚举属性到目标对象上。 来源对象的应用规则是从左到右，随后的下一个对象的属性会覆盖上一个对象的属性。

[_.forIn](https://www.lodashjs.com/docs/lodash.forIn): 使用 `iteratee` 遍历对象的自身和继承的可枚举属性。 

[_.has](https://www.lodashjs.com/docs/lodash.has): 检查 `path` 是否是`object`对象的直接属性。

[_.keys](https://www.lodashjs.com/docs/lodash.keys): 创建一个 `object` 的自身可枚举属性名为数组。

[_.valuse](https://www.lodashjs.com/docs/lodash.values): 创建 `object` 自身可枚举属性的值为数组。

[_.merge](https://www.lodashjs.com/docs/lodash.merge):  该方法类似[`_.assign`](https://www.lodashjs.com/docs/lodash.merge#assign)， 除了它递归合并 `sources` 来源对象自身和继承的可枚举属性到 `object` 目标对象。

[_.pick](https://www.lodashjs.com/docs/lodash.pick): 创建一个从 `object` 中选中的属性的对象。

[_.omit](https://www.lodashjs.com/docs/lodash.omit): 反向版[`_.pick`](https://www.lodashjs.com/docs/lodash.omit#pick); 这个方法一个对象，这个对象由忽略属性之外的`object`自身和继承的可枚举属性组成。

#### 字符串

[_.camelCase](https://www.lodashjs.com/docs/lodash.camelCase): 转换字符串`string`为[驼峰写法](https://en.wikipedia.org/wiki/CamelCase)。

[_.escape](https://www.lodashjs.com/docs/lodash.escape#_escapestring) ：返回转义后的字符串。

[_.trim](https://www.lodashjs.com/docs/lodash.trim): 从`string`字符串中移除前面和后面的 空格 或 指定的字符。

[_.split](https://www.lodashjs.com/docs/lodash.split): 根据`separator` 拆分字符串`string`。

[_.template](https://www.lodashjs.com/docs/lodash.template) : 创建一个预编译模板方法，可以插入数据到模板中 "interpolate" 分隔符相应的位置。

[_.words](https://www.lodashjs.com/docs/lodash.words) : 拆分字符串`string`中的词为数组 。

[_.replace](https://www.lodashjs.com/docs/lodash.replace): 替换`string`字符串中匹配的`pattern`为给定的`replacement` 。

#### 实用函数

[_.flow](https://www.lodashjs.com/docs/lodash.flow) : 创建一个函数。 返回的结果是调用提供函数的结果，`this` 会绑定到创建函数。 每一个连续调用，传入的参数都是前一个函数返回的结果。

[_.times](https://www.lodashjs.com/docs/lodash.times): 调用 iteratee `n` 次，每次调用返回的结果存入到数组中。 iteratee 调用入1个参数： *(index)*。

[_.overEvery](https://www.lodashjs.com/docs/lodash.overEvery): 建一个函数，传入提供的参数的函数并调用 `predicates` 判断是否 **全部** 都为真值。

[_.overSome](https://www.lodashjs.com/docs/lodash.overSome): 创建一个函数，传入提供的参数的函数并调用 `predicates` 判断是否 **存在** 有真值。

[_.mixin](https://www.lodashjs.com/docs/lodash.mixin): 添加来源对象自身的所有可枚举函数属性到目标对象。 如果 `object` 是个函数，那么函数方法将被添加到原型链上。

[_.nthArg](https://www.lodashjs.com/docs/lodash.nthArg#_nthargn0) : 创建一个函数，这个函数返回第 `n` 个参数。如果 `n`为负数，则返回从结尾开始的第n个参数。

### 后记

我是彤爱，一个在沉溺于寂寞代码海洋里的前端程序员👨🏻‍💻

欢迎各位大佬的赐教🙏

期待与同样在努力摸索的小伙伴们交流🙌
# 读书笔记

2018年8月4日

代理模式,装饰者模式
多个对象相互要产生影响的时候如果直接对其余对象操作会使得这些对象强耦合,代理模式的引入可以解决这一问题
装饰者模式在对对象添加或者复写某些属性的时候比较常用,对原本对象进行包装再生成

#

2018年8月5日

inerterviewMap中vue-router解析
router挂载原理,router映射生成细节

#

2018年8月6日

了解选择排序,插入排序和归并排序

#

2018年8月7日
- [x] 了解柯里化的详细信息
> 在计算机科学中，柯里化（Currying）是把接受多个参数的函数变换成接受一个单一参数(最初函数的第一个参数)的函数，并且返回接受余下的参数且返回结果的新函数的技术。这个技术由 Christopher Strachey 以逻辑学家 Haskell Curry 命名的，尽管它是 Moses Schnfinkel 和 Gottlob Frege 发明的。

柯里化预期把多个参数的函数转化为一个参数一个参数传递,在javascript中,可以采用闭包来实现,本质是返回一个函数,该函数能访问上一次传入的参数

举个栗子,就像我们在做算术题的时候求 `y = f(x) + g(y)`,非柯里化的做法是同时传入`x y`的值,而柯里化则是先传入一个x,获得一个`y = a + g(y) // a为传入的x计算得到的值`,从一个2元一次方程变成了一元一次方程,对应到js中,第一次传的参数返回了一个已知第一个参数的函数,这时只要接受第二个参数就能获得结果
```javascript
function sum (x) {
    return function (y) {
        return x + y
    }
}
sum(1)(2)
```
- 反柯里化
反柯里化在javascript中是一种广泛存在的现象
> “当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。” --鸭子测试

通俗的来说就是函数的借用，是函数能够接受处理其他对象，通过借用泛化、扩大了函数的使用范围。在javascript中的体现,就是用apply,call,bind实现的函数借用
```javascript
// 非原型上的实现
function unCurrying(fn) {
  return function(target, ...argu) {
    return fn.apply(target, argu)
  }
}

// 通用实现
Function.prototype.unCurrying = function() {
    return (...args) => {
        return Function.prototype.call.apply(this, args);
    }
}

const push = Array.prototype.push.unCurrying()

const obj = { a: '嘻嘻' }
push(obj, '呵呵', '哈哈', '嘿嘿')
console.log(obj) // { '0': '呵呵', '1': '哈哈', '2': '嘿嘿', a: '嘻嘻', length: 3 }
```
#

2018年8月8日
- [x] 阅读设计模式
- 开放-封闭原则(OCP)
> 软件实体(类 模块 函数)等应该是可以扩展的,但是不可修改

几乎所有的设计模式都遵循了开放-封闭原则
#

2018年8月9日

防抖
```javascript
function now() {
  return +new Date()
}

function debounce (func, wait = 50, immediate = true) {
  let last, timer, context, args
  const timeoutReset = () => setTimeout(() => {
    timer = null
    if (!immediate) {
      func.apply(context, args)
      context = args = null
    }
  }, wait)

  return function(...params) {
    // 每次调用更新最后一次点击的时间
    last = now() + wait
    // 如果没有创建过计时器,则调用函数并开始计时
    // 如果还在计时中
    if (!timer) {
      timer = timeoutReset()
      if (immediate) {
        func.apply(this, params)
      } else {
        context = this
        args = params
      }
    } else if (now() < last) {
      clearTimeout(timer)
      timer = timeoutReset()
    }
  }
}

```

#

2018年8月10日

节流

节流在防抖的基础上,改一个地方就ok了
```javascript
function now() {
  return +new Date()
}

function throttle (func, wait = 50, immediate = true) {
  let last, timer, context, args
  const timeoutReset = () => setTimeout(() => {
    timer = null
    if (!immediate) {
      func.apply(context, args)
      context = args = null
    }
  }, wait)

  return function(...params) {
    // 每次调用更新最后一次点击的时间
    // last = now() + wait 这行代码移动一下就变成节流了
    // 如果没有创建过计时器,则调用函数并开始计时
    // 如果还在计时中
    if (!timer) {
      timer = timeoutReset()
      if (immediate) {
        func.apply(this, params)
      } else {
        context = this
        args = params
      }
    } else if (now() < last) {
      // 节流的情况下,不需要每次都更改last,只在last过期之后才重置
      last = now() + wait
      clearTimeout(timer)
      timer = timeoutReset()
    }
  }
}
```


#

2018年8月11日

阅读
> clean code

#

2018年8月12日

阅读
> 深入理解ES6

#

2018年8月13日

阅读
> 学习javascript数据结构与算法

#

2018年8月14日


#
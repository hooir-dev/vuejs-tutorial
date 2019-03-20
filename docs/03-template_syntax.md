# 第3章 模板语法

## Vue 实例

- 每个 Vue 应用都是通过用 Vue 函数创建一个新的 Vue 实例开始的
- 当创建一个 Vue 实例时，你可以传入一个选项对象
- el 选项
  + 不能是 html、body 标签
- data 选项
  + data 中的数据就是我们平常使用模板引擎所常见的模板数据对象
  + data 中的数据是响应式的，即数据改变之后随之驱动视图发生变化
  + 只有当实例被创建时 data 中存在的属性才是响应式的
  + 注意：动态为实例添加属性是无效的，所以我们要在实例初始化开始的时候初始化我们的 data 选项数据
- methods 选项
- ...
- 不同选项有不同功能作用，更多实例选项参考[官方 API 文档](https://cn.vuejs.org/v2/api/)

## 创建一个 Vue 的实例

每个 Vue 应用都是通过 `Vue` 函数创建一个新的 **Vue 实例**开始的：

```javascript
var vm = new Vue({
  // 选项
});
```

当创建一个 Vue 实例时，你可以传入一个**选项对象**。这篇教程主要描述的就是如何使用这些选项来创建你想要的行为。作为参考，你也可以在 [API 文档](https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E6%95%B0%E6%8D%AE) 中浏览完整的选项列表。

## `el` 选项

> 参考文档：https://cn.vuejs.org/v2/api/#el

提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标。可以是 CSS 选择器，也可以是一个 HTMLElement 实例。

- 不能作用到 `<html>` 或者 `<body>` 上
- 也可以通过 `实例.$mount()` 手动挂载

## `data` 选项

> 参考文档：https://cn.vuejs.org/v2/api/#data

- 响应式数据
- 可以通过 `vm.$data` 访问原始数据对象
- Vue 实例也代理了 data 对象上所有的属性，因此访问 `vm.a` 等价于访问 `vm.$data.a`
- 视图中绑定的数据必须显式的初始化到 data 中

## `methods` 选项

> 参考文档：https://cn.vuejs.org/v2/api/#methods

methods 将被混入到 Vue 实例中。可以直接通过 VM 实例访问这些方法，或者在指令表达式中使用。方法中的 `this` 自动绑定为 Vue 实例。

!> 注意，**不应该使用箭头函数来定义 method 函数** (例如 `plus: () => this.a++`)。理由是箭头函数绑定了父级作用域的上下文，所以 `this` 将不会按照期望指向 Vue 实例，`this.a` 将是 undefined。

示例：

```javascript
var vm = new Vue({
  data: { a: 1 },
  methods: {
    plus: function () {
      this.a++
    }
  }
})
vm.plus()
vm.a // 2
```

---

## 实例生命周期

先来听一段延伸法师的人生感悟：[《绳命》](https://www.youtube.com/watch?v=Ps1Er1BSWyA)。

<iframe width="560" height="315" src="https://www.youtube.com/embed/Ps1Er1BSWyA?rel=0" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

> 生命是如此的美丽，让我们祝福这所有，让我们祝福生命如此的精彩！

---

---

生命周期 这个词挺起来也是挺吓人的，在很多个编程领域都存在着这么一个说法。对于一个萌新来说，确实比较难懂。

> 举个例子就好理解多了，人的一生呐，就是从肚子里钻出来，然后度过童年，青年，中年，老年，然后再钻回肚子，哦不，是钻到土地下，这就是一个人的生命周期，从出生到死亡，有着很多个阶段。

![生命周期](https://ooo.0o0.ooo/2017/03/31/58dd2edfc6e95.png)

同样的，实例，一开始我们说了，需要被 构造 出来，紧接着他也会经历它生命中的各个阶段，然后死掉。

所以，要了解一个人，我们就要从他一生中的各个阶段去了解它，了解实例也一样！

> 进入童年就要上学，青年就要上班，中年就要。。也要上班，老年要退休。

所以说，每进入一个阶段都可以干一件什么事情。Vue 中也是这样的。所以 Vue 提供了一些称之为 钩子(HOOK) 的东西，为我们提供了机会去操作某个阶段的行为。

比如说 进入童年 就可以比喻为一个钩子，上学 就可以比喻为这个阶段要让他做的事情。

![Vue实例生命周期](https://ooo.0o0.ooo/2017/03/31/58dd304f6c094.png)

好了，回过头来再看一下官方的生命周期图：

![Vue实例生命周期](https://cn.vuejs.org/images/lifecycle.png)

我们在里面可以看到几个钩子：

- beforeCreate
  + 在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。
- created
  + 在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。
- beforeMount
  + 在挂载开始之前被调用：相关的 render 函数首次被调用。
- mounted
  + el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。
- beforeUpdate
  + 数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。
  + 你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。
- updated
  + 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。
- activated
- deactivated
- beforeDestroy
- destroyed
- errorCaptured





参考文档：

- [Vue 官网 - 实例生命周期](https://cn.vuejs.org/v2/guide/instance.html#实例生命周期)
- [生命周期钩子函数 API 文档](https://cn.vuejs.org/v2/api/#选项-生命周期钩子)
- 

---

## 插值绑定

---

## 计算属性

---

## Class 与 Style 绑定

---

## 条件渲染

---

## 列表渲染

---

## 事件处理

---

## 表单输入绑定

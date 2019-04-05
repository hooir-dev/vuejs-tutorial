# 第8章 Vue Router

## 安装

## Hello World

---

## 动态路由匹配

> https://router.vuejs.org/zh/guide/essentials/dynamic-matching.html

---

## 嵌套路由

> https://router.vuejs.org/zh/guide/essentials/nested-routes.html

---

## 编程式导航

> https://router.vuejs.org/zh/guide/essentials/navigation.html

---

## 命名路由

---

## 命名视图

---

## 重定向和别名

---

## 相关 API

### 路由对象 this.$route

一个**路由对象 (route object)** 表示当前激活的路由的状态信息，包含了当前 URL 解析得到的信息，还有 URL 匹配到的**路由记录 (route records)**。

路由对象是不可变 (immutable) 的，每次成功的导航后都会产生一个新的对象。

路由对象出现在多个地方:

- 在组件内，即 `this.$route`
- 在 `$route` 观察者回调内
- `router.match(location)` 的返回值

- **$route.path**

  - 类型: `string`

    字符串，对应当前路由的路径，总是解析为绝对路径，如 `"/foo/bar"`。

- **$route.params**

  - 类型: `Object`

    一个 key/value 对象，包含了动态片段和全匹配片段，如果没有路由参数，就是一个空对象。

- **$route.query**

  - 类型: `Object`

    一个 key/value 对象，表示 URL 查询参数。例如，对于路径 `/foo?user=1`，则有 `$route.query.user == 1`，如果没有查询参数，则是个空对象。

- **$route.hash**

  - 类型: `string`

    当前路由的 hash 值 (带 `#`) ，如果没有 hash 值，则为空字符串。

- **$route.fullPath**

  - 类型: `string`

    完成解析后的 URL，包含查询参数和 hash 的完整路径。

- **$route.matched**

  - 类型: `Array<RouteRecord>`

  一个数组，包含当前路由的所有嵌套路径片段的**路由记录** 。路由记录就是 `routes` 配置数组中的对象副本 (还有在 `children` 数组)。

  ```js
  const router = new VueRouter({
    routes: [
      // 下面的对象就是路由记录
      { path: '/foo', component: Foo,
        children: [
          // 这也是个路由记录
          { path: 'bar', component: Bar }
        ]
      }
    ]
  })
  ```

  当 URL 为 `/foo/bar`，`$route.matched` 将会是一个包含从上到下的所有对象 (副本)。

- **$route.name**

  当前路由的名称，如果有的话。(查看[命名路由](https://router.vuejs.org/zh/guide/essentials/named-routes.html))

- **$route.redirectedFrom**

  如果存在重定向，即为重定向来源的路由的名字。(参阅[重定向和别名](https://router.vuejs.org/zh/guide/essentials/redirect-and-alias.html))

### Router 实例

> 我们在组件中访问的 this.$router 就是路由文件中创建的路由实例

| API     | 作用                 | 备注                                                         |
| ------- | -------------------- | ------------------------------------------------------------ |
| push    | 跳转，会形成历史记录 | 想要导航到不同的 URL，则使用 `router.push` 方法。这个方法会向 history 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到之前的 URL。 |
| replace | 路径替换             | 跳过去，别回来了                                             |
| go      | 跳转到指定步骤的路由 |                                                              |
| back    | 后退一步             |                                                              |
| forward | 前进一步             |                                                              |
|         |                      |                                                              |




## Vue 中 v-for 和 v-if 哪个优先级高？如果同时出现应该怎么优化以得到更好的性能？

- 官网**不推荐**同时使用 `v-if` 和 `v-for` ，详细查看官网资料[风格指南]([https://cn.vuejs.org/v2/style-guide/#%E9%81%BF%E5%85%8D-v-if-%E5%92%8C-v-for-%E7%94%A8%E5%9C%A8%E4%B8%80%E8%B5%B7-%E5%BF%85%E8%A6%81](https://cn.vuejs.org/v2/style-guide/#避免-v-if-和-v-for-用在一起-必要))
- 当 `v-if` 与 `v-for` 一起使用时，`v-for` 具有比 `v-if` 更高的优先级。详细查看官网资料[列表渲染指南](https://cn.vuejs.org/v2/guide/list.html#v-for-with-v-if)

1. 情况一：当v-if条件来自于循环条件时，可以考虑借助计算属性computed，把源数据处理完再渲染，减少循环次数

```vue
<ul>
  <li
    v-for="(user, index) in users"
    v-if="user.isActive"
    :key="index">
    {{ user.name }}
  </li>
</ul>
```



2. 情况二：当v-if条件跟循环条件互不干扰，可以在v-for的父级做v-if判断。避免不必要的循环渲染

```vue
<ul v-if="isShow">
  <li
    v-for="(user, index) in users"
    :key="index">
    {{ user.name }}
  </li>
</ul>
```




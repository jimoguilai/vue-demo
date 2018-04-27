# Vue学习笔记

(by <dxz506@163.com>，Github[源码地址](https://github.com/jimoguilai/vue-demo))

## Vue2.x+BootStrap3.x简易留言板(todolist)：

### 特点：

- bootstrap：css框架，跟JQueryMobile一样；
- 只需要给标签赋class、角色；
- 依赖jquery；

### 知识点：

vue2.x版本v-for的key和index获取，跟vue1.x有所区别，查看
[官方说明](https://cn.vuejs.org/v2/api/#v-for)

- vue1.x的v-for：
    ```javascript
    (item, index) in arr/obj(数组或对象)
    {{$key}}、{{$index}}
    ```

- vue2.x的v-for：
    ```javascript
    (item, index) in arr(数组)
    (value, key) in obj(对象)
    (value, key, index) in obj(对象)
    ```

# Vue2.x+BootStrap3.x简易留言板(todolist)：

## 特点：

- bootstrap：css框架，跟JQueryMobile一样；
- 只需要给标签赋class、角色；
- 依赖jquery；

## 知识点：vue2.x版本的v-for循环的key和index跟vue1.x有所区别

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

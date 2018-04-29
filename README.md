# Vue学习笔记

(by <dxz506@163.com>，Github[源码地址](https://github.com/jimoguilai/vue-demo))

## Vue2.x+BootStrap3.x简易留言板(todolist)：

### 特点：

- bootstrap：css框架，跟JQueryMobile类似；
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
    ```js
    (item, index) in arr(数组)
    (value, key) in obj(对象)
    (value, key, index) in obj(对象)
    ```

### 事件：

- 事件简写：
    ```js
    v-on:click/onmouseover...
    可以简写为：
    @click/onmouseover...
    ```

- 事件对象：
    ```js
    @click="show($event, a, b)"
    该$event就是js原生的事件对象，可以.出很多属性，如：e.clientX ...；
    a,b为其他参数，需要注意顺序。
    new Vue({
        el: "#app",
        data: {
        },
        methods: {
            show: function(e, a, b){
                alert(e.clientX);
                //alert(a);
            }
        }
    });
    ```

- 事件冒泡与事件捕获、默认行为（默认事件）、键盘事件：

1. [概念解释](https://www.cnblogs.com/qq9694526/p/5653728.html) 当事件发生后，这个事件就要开始传播(从里到外或者从外向里)。有必要的话我们需要对事件的作用范围进行限制。`绑定事件方法的第三个参数，就是控制事件触发顺序是否为事件捕获。true,事件捕获；false,事件冒泡。默认false,即事件冒泡。Jquery的e.stopPropagation会阻止冒泡，意思就是到我为止，我的爹和祖宗的事件就不要触发了。`
2. 事件冒泡：`自下而上（从内向外）`的去触发事件。

    ```js
    document.getElementById("parent").addEventListener("click",function(e){
        alert("parent事件被触发，"+e.target.id);
    }, false); // 绑定事件方法的第三个参数，false为事件冒泡

    document.getElementById("child").addEventListener("click",function(e){
        alert("child事件被触发，"+e.target.id)
    }, false); // 绑定事件方法的第三个参数，false为事件冒泡
    ```
3. 事件捕获：从document到触发事件的那个节点，即`自上而下（从外向里）`的去触发事件。

    ```js
    document.getElementById("parent").addEventListener("click",function(e){
        alert("parent事件被触发，"+e.target.id);
    }, true); // 绑定事件方法的第三个参数，true为事件捕获

    document.getElementById("child").addEventListener("click",function(e){
        alert("child事件被触发，"+e.target.id)
    }, true); // 绑定事件方法的第三个参数，true为事件捕获
    ```
4. 阻止事件冒泡：如果想阻止事件的传递，我们可以用`event.stopPropagation()`阻止事件的传递行为
    ```js
    JQuery阻止事件冒泡方式及其区别：return false 不仅阻止了事件往上冒泡，而且阻止了事件本身。event.stopPropagation() 则只阻止事件往上冒泡，不阻止事件本身。

    方式一：event.stopPropagation();
    $("#div1").mousedown(function(event){
         event.stopPropagation();
    });

    方式二：return false;
    $("#div1").mousedown(function(event){
    　　return false;
    });
    ```
    ```js
    Vue阻止冒泡事件：
    @click.stop = "show()" // 使用 事件.stop阻止事件冒泡

    或者：
    @click="show($event)"

    new Vue({
        el: "#app",
        data: {},
        methods: {
            show: function(e){
                e.cancelBubble = true; //阻止事件冒泡，引用处需传递参数show($event)
                // 其他处理

            }
        }
    });
    ```
5. 默认行为（默认事件）：网页中的某些元素是有自己的默认行为的，比如果超链接单击后需要跳转，提交按钮点击后需要提交表单，有时需要阻止这些行为，也就是[默认行为](https://baike.baidu.com/item/%E4%BA%8B%E4%BB%B6%E5%86%92%E6%B3%A1/4211429?fr=aladdin)。
    ```js
    Vue阻止默认行为：
    @contextmenu.prevent="show()"

    或者：
    @contextmenu="show2($event)"

    new Vue({
        el: "#app",
        methods: {
            show2: function(e){
                e.preventDefault();
            }
        }
    });
    ```
6. 键盘事件：$event  e.keyCode
    ```js
    注：测试时必须切换为英文输入法
    @keydown="show($event)"

    new Vue({
        el: "#app",
        methods: {
            show: function(e){
                alert(e.keyCode);
            }
        }
    });

    常用键的触发：@事件名.keyCode，就不需要去判断了；

    @keydown.13 或者 @keydown.enter /up/down/left/right
    @keydown.a/b/c/d ...
    数字必须使用keycode，1的keycode=49
    ```

- 属性：v-bind:属性名，简写  :属性名
    ```js
    <img src="{{url}}" alt=""> // 页面效果能出来，但是会提示vue的错误

    <img v-bind:src="url" alt=""> // 这样就不会报错
    简写:
    <img :src="url" alt="">
    ```

    ```css
    class和style属性的特殊用法:
    :class=""   v-bind:class=""
    :style=""   v-bind:style=""

    1. css的用法：
    <style>
        .red{color: red;}
        .blue{background: blue;}
    </style>
    <javascript>
        new Vue({
            el: "#app",
            data: {
                red: "red",
                b: "blue",
                json:{
                    red: true,
                    blue: true
                }
            }
        });
    </javascript>

    :class="[red, b...]"    /* 用法1：red,b是vue中data的数据 */
    或者：
    :class="{red:true, blue:true}"  /* 用法2：red,blue直接是class类名，true-生效，false-不生效 */
    :class="json"

    2. style的用法
    <javascript>
        new Vue({
            el: "#app",
            data: {
                a: {
                    color: "red",
                    fontSize: "25px"
                },
                b: {
                    backgroundColor: "blue"
                }
            }
        });
    </javascript>

    :style="a" // json，推荐使用方式
    :style="[a,b]" // json数组
    ```

- 数据绑定：

    ```js
    1. v-model，双向绑定；
    2. v-once，一次性绑定
    3. v-html，html不转义直接输出

    new Vue({
        el: "#app",
        data: {
            msg: "<i>斜体</i>123abc"
        }
    });
    <input type="text" v-model="msg"><br>
    v-model，双向绑定: <span>{{msg}}</span><br>
    v-once，一次性绑定: <span v-once>{{msg}}</span><br>
    v-html，html不转义直接输出: <span v-html="msg"></span>
    ```

- 过滤器：[vue1.x向2.x迁移](https://cn.vuejs.org/v2/guide/migration.html#%E6%9B%BF%E6%8D%A2-uppercase-%E8%BF%87%E6%BB%A4%E5%99%A8)

    ```js
    toUpperCase() 小写转大写：
    {{"abc".toUpperCase()}}

    toLowerCase() 大写转小写：
    {{"AbC".toLowerCase()}}

    首字母大写：
    {{"abcd"[0].toUpperCase()+"abcd".slice(1)}}
    ```
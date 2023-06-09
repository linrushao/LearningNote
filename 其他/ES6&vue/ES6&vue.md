# 1.ES6语法

## 1.1.let特性

> 特性一：let声明的变量有严格局部作用域

```html
<script>
    // var声明的变量往往会越域
    // let声明的变量有严格局部作用域
    {
        var a = 1;
        let b = 2;
    }
    console.log(a); // 1
    console.log(b); // Uncaught ReferenceError: b is not defined   
</script>
```

> 特性二：let只能声明一次

```html
<script>
    // var可以声明多次
    // let只能声明一次
    var m = 1;
    var m = 2;
    let n = 3;
    let n = 4;
    console.log(m); // 2
    console.log(n); // Uncaught SyntaxError: Identifier 'n' has already been declared
</script>
```

> 特性三：let不存在变量提升

```html
<script>
    // var会变量提升
    // let不存在变量提升
    console.log(x); // undefined
    var x = 10;
    console.log(y); // Uncaught ReferenceError: Cannot access 'y' before initialization
    let y = 20;
</script>
```

## 1.2.const特性

> 特性一：const声明变量会不允许改变

```html
<script>
    // const声明变量会不允许改变
    const a = 1;
    a = 2; // Uncaught TypeError: Assignment to constant variable
</script>
```

> 特性二：const一旦声明必须初始化，否则报错

```html
<script>
	const b; // Uncaught SyntaxError: Missing initializer in const declaration
</script>
```

## 1.3.解构表达式

> 数组解构

```html
<script>
    // 1、数组解构
    let arr = [1,2,3];
    let [a,b,c] = arr;
    // let [a,b,c] = arr; 代替的就是一个一个的赋值语句
    // let a = arr[0];
    // let b = arr[1];
    // let c = arr[2];
    console.log(a); // 1
    console.log(b); // 2
    console.log(c); // 3 
</script>
```

> 对象解构

```html
<script>
    // 2、对象解构
    const person = {
        name: "Tangs",
        age: 18,
    }
    
    // 取出person的name赋值给name;取出person的name赋值给age(age别名为aaa)
    const {name,age:aaa} = person;
    
    console.log(name); // Tangs
    console.log(age); // 18
    
    
</script>
```

## 1.4.字符串扩展

> 几个新的API

```html
<script>
    // 字符串扩展API
    let str = "hello Tangs";
    console.log(str.startsWith("hello")); // true
    console.log(str.endsWith("Tangs")); // true
    console.log(str.includes("o")); // true
    console.log(str.includes("hello")); // true
</script>
```

> 字符串模板

```html
<script>
    // 字符串模板
    let ss = `<div><span>hello Tangs</span></div>`; 
    console.log(ss); // <div><span>hello Tangs</span></div>    
</script>
```

```html
<script>
    // 可以引用上面变量的值
    let username = "Tangs";
    let userAge = 18;
    let info = `我是${username},今年${userAge}岁了`;
    console.log(info); // 我是Tangs,今年18岁了
</script>
```

```html
<script>
    // 可以调用函数
    function iWant() {
        return "我喜欢你";
    }
    let username1 = "Tangs";
    let userAge1 = 18;
    let info1 = `我是${username1},今年${userAge1}岁了,我想说${iWant()}`;
    console.log(info1); // 我是Tangs,今年18岁了
</script>
```

## 1.5.函数优化

> 函数参数的默认值

```html
<script>
    // 在ES6之前,我们无法给一个函数参数设置默认值,只能采用变通写法
    function add(a, b) {
        // 判断b是否为空，为空就给默认值1
        b = b || 1;
        return a + b;
    }
    console.log(add(10)); // 11
    console.log(add(10,5)); // 15

    // 现在可以这样写，直接给参数写上默认值，没传就会使用默认值
    function add1(a, b = 1) {
        return a + b;
    }
    console.log(add1(10)); // 11
    console.log(add1(10, 5)); // 15
</script>
```

> 不定参数

```html
<script>
    function fun(...params) {
        console.log(params.length);
    }
    fun(1,2); // 2
    fun(1,2,3,4); // 4
</script>
```

> 箭头函数

```html
<script>
    /**
     箭头函数等价于
     function print(obj) {
        console.log(obj);
    }
    */
    // 有一个参数的箭头函数
    let print = obj => console.log(obj);
    print({"name": "zhangsan", "age": 18}); // {name: "zhangsan", age: 18}
    
    // 箭头函数求两数之和
    let sum = (a, b) => {return a+ b;}
    console.log(sum(10, 18));  // 23    
</script>
```

> 箭头函数和解构表达式联用

```html
<script>
    // 定义person对象
    let person = {
        "name": "Tangs",
        "age": 18
    };

    // 创建箭头函数并且使用对象解构表达式
    let hello = ({name}) => {
        console.log("hello " + name);
    };

    // 调用方法传入person对象
    hello(person);   // hello Tangs
</script>
```

## 1.6.对象优化

> 新增API

```html
<script>
    const person = {
        "name": "Tangs",
        "age": 18,
    };

    // Object的使用
    console.log(Object.keys(person)); // ["name", "age"]
    console.log(Object.values(person)); // ["Tangs", 18]
    console.log(Object.entries(person));
</script>
```

```html
<script>
    const target = {a: 1};
    const source1 = {b: 2};
    const source2 = {c: 3};

    // 将source1和source2合并到target中
    Object.assign(target, source1, source2);

    console.log(target); // {a: 1, b: 2, c: 3}
</script>
```

> 对象声明的简写

```html
<script>
    // 声明对象简写
    const name = "Tangs";
    const age = 18;
    const person1 = {
        "age": age,
        "name": name
    };

    // 如果属性名和属性值是一样的,那么就可以简写
    const person2 = {age, name};
    
    console.log(person1); // {age: 18, name: "Tangs"}
    console.log(person2); // {age: 18, name: "Tangs"}
</script>
```

> 对象中函数的写法

```html
<script>
    let person3 = {
        "name": "Tangs",
        // 方式一：以前的写法
        eat1: function (food) {
            console.log(this.name + "吃" + food);
        },
        // 方式二：箭头函数中不能使用this
        eat2: food => console.log(person3.name + "吃" + food),
        
        // 方式三：可以和C语言一样写函数
        eat3(food) {
            console.log(this.name + "吃" + food);
        }
    }
    person3.eat1("apple"); // Tangs吃apple
    person3.eat2("banana") // Tangs吃banana
    person3.eat3("orange"); // Tangs吃orange
</script>
```

> 对象扩展运算符

```html
<script>
    // 对象扩展运算符

    // 1、拷贝对象(深拷贝)
    let p1 = {
        "name": "Tangs",
        "age": 18
    };

    let someone = {...p1};
    console.log(someone); // {name: "Tangs", age: 18}

    // 2、合并对象
    let p2 = {
        "name": "Tangs",
        "age": 18
    };
    let fav = {
        "age": 19,
        "sport": "basketball",
        "height": "165cm"
    };

    let person4 = {
        ...p2,
        ...fav
    };
    console.log(person4); // {name: "Tangs", age: 19, sport: "basketball", height: "165cm"}
</script>
```

## 1.7.map、reduce

```html
<script>
    // map()：接收一个函数，将原数组中所有的元素用这个函数处理后放入新数组返回。
    let arr = ['1', '-1', '-5', '20'];
    arr = arr.map((item) => {
        return item * 2;
    });
    console.log(arr); // [2, -2, -10, 40]

    /*
     reduce(callback, [initialValue])
     1.previousValue: 上一次调用回调返回的值，或者是提供的初始值(initialValue)
     2.currentValue: 数组中当前被处理的元素
     3.index: 当前元素在数组中的索引
     4.array: 调用reduce的数组
    */
    // arr = [2, -2, -10, 40]
    // 1、不指定initialValue
    let ret1 = arr.reduce((previousValue, currentValue) => {
        console.log("上一次处理后:" + previousValue);
        console.log("当前正在处理:" + currentValue);
        return previousValue + currentValue;
    });

    // 控制台打印的结果
    /*
        上一次处理后:2
        当前正在处理:-2
        上一次处理后:0
        当前正在处理:-10
        上一次处理后:-10
        当前正在处理:40
    */

    console.log(ret1); // 30

    // 2、指定reduce的initialValue
    let ret2 = arr.reduce((previousValue, currentValue) => {
        console.log("上一次处理后:" + previousValue);
        console.log("当前正在处理:" + currentValue);
        return previousValue + currentValue;
    }, 100);

    // 控制台打印的结果
    /*
    上一次处理后:100
    当前正在处理:2
    上一次处理后:102
    当前正在处理:-2
    上一次处理后:100
    当前正在处理:-10
    上一次处理后:90
    当前正在处理:40
    */
    console.log(ret2); // 130
</script>
```

## 1.8.promise异步编排

### 1.8.1.为什么使用promise

在`JavaScript`的世界中，所有代码都是单线程执行的。由于这个”缺陷“，导致`JavaScript`的所有网络操作，浏览器事件，都必须是异步执行的。异步执行可以使用回调函数实现。一旦有一连串的`ajax`请求，==后面的请求依赖前边请求的结果，就需要层层嵌套==。这种缩进和层层嵌套的方式，非常容易造成上下文代码混乱，我们不得非常小心翼翼处理内层函数与外层函数的数据，一旦内层函数使用了上层函数的变量，这种混乱程度就会加剧.......

### 1.8.2.案例

用户登录，并展示该用户的各科成绩。在页面发送两次请求：

1、查询用户，查询成功说明可以登录。

2、查询用户成功，查询科目。

3、根据科目的查询结果，获取成绩。

> 准备

```json
// user.json
{
    "id": 1,
    "username": "Tangs",
    "password": "123456"
}

// user_corse_1.json
{
    "id": 10,
    "name": "math"
}

// corse_score_10.json
{
    "id": 100,
    "score": 90
}
```

> ajax请求

```html
<script src="./static/jquery-1.12.4.js"></script>
<script>
    // 1、查出当前用户信息
    // 2、按照当前用户的id查出他的课程
    // 3、按照当前课程id查出分数

    $.ajax({
        url: "mock/user.json",
        success(data) {
            console.log("查询用户：", data); // 查询用户： {id: 1, username: "Tangs", password: "123456"}
            $.ajax({
                url: `mock/user_corse_${data.id}.json`,
                success(data) {
                    console.log("查到的课程：", data); // 查到的课程： {id: 10, name: "math"}
                    $.ajax({
                        url: `mock/corse_score_${data.id}.json`,
                        success(data) {
                            console.log("查到的分数：", data); // 查到的分数： {id: 100, score: 90}
                        },
                        error(error) {
                            console.log("出现异常：", error);
                        }
                    });
                }

            });
        }

    });
</script>
```

> promise

```html
<script src="./static/jquery-1.12.4.js"></script>
<script>
    // resolve：解决; reject：拒绝
    let p = new Promise((resolve, reject) => {
        // 1、异步操作
        $.ajax({
            url: "mock/user.json",
            success: function (data) {
                console.log("查询用户成功：", data);
                resolve(data);
            },
            error: function (error) {
                reject(error)
            }
        });
    }).then((obj) => {
        // 得到上一步成功的结果
        return new Promise((resolve, reject) => {
            $.ajax({
                url: `mock/user_corse_${obj.id}.json`,
                success: function (data) {
                    console.log("查询课程成功：", data);
                    resolve(data);
                },
                error: function (error) {
                    reject(error);
                }
            });
        });
    }).then(obj => {
        // 得到上一步成功的结果
        new Promise((resolve, reject) => {
            $.ajax({
                url: `mock/corse_score_${obj.id}.json`,
                success: function(data) {
                    console.log("查询分数成功", data);
                    resolve(data);
                },
                error: function(error) {
                    reject(error);
                }
            });
        });
    });
</script>
```

> promise封装优化

```html
<script>
    function get(url) {
        return new Promise((resolve, reject) => {
            $.ajax({
                url,
                success(data) {
                    resolve(data);
                },
                error(error) {
                    reject(error);
                }
            });
        });
    }

    get("mock/user.json")
        .then((data) => {
            console.log("用户查询成功", data);   // 用户查询成功 {id: 1, username: "Tangs", password: "123456"}
            return get(`mock/user_corse_${data.id}.json`);
        })
        .then((data) => {
            console.log("课程查询成功", data); // 课程查询成功 {id: 10, name: "math"}
            return get(`mock/corse_score_${data.id}.json`);
        })
        .then((data) => {
            console.log("成绩查询成功", data); // 成绩查询成功 {id: 100, score: 90}
        });
</script>
```

## 1.9.模块化

### 1.9.1.什么是模块化？

模块化就是把代码进行拆分，方便重复利用。类似java中的导包，要使用一个包，必须先导包。==而javascript中没有包的概念，换来的是模块。==

模块功能主要由两个命令构成：`export`和`import`

- `export`命令用于规定模块的对外接口。
- `import`命令用于导入其他模块提供的功能。

### 1.9.2.基本使用

> export

```javascript
// hello.js
const util = {
    sum(a, b) {
        return a + b;
    }
}

// export不仅可以导出对象
export {
    util
}
```

```javascript
// user.js
let name = "Tangs";
let age = 18;

function add(a, b) {
    return a + b;
}

export {
    name,
    age,
    add
}
```

> import

```javascript
// main.js
import util from "./hello.js";
import { name, age, add } from './user.js';

let ret = util.sum(1, 2);
console.log(ret);
console.log(name);
console.log(add(3, 5));
```

# 2.vue

## 2.1.MVVM思想

- M，即Model，模型，包括数据和一些基本操作。
- V，即View，视图，页面渲染效果。
- VM，即View-Model，模型与视图间的双向操作（无需开发人员操作）。

## 2.2.vue的简单使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <!--v-model双向绑定！--> 
        <input type="text" v-model="num">

        <!--v-on:click绑定事件！-->
        <button v-on:click="num++">点赞</button>
        <h1>{{name}},非常帅,有{{num}}个人为他点赞</h1>
    </div>
</body>
<!--引入vue-->
<script src="./node_modules/vue/dist/vue.js"></script>
<script>
    // vue的声明式渲染
    let vm = new Vue({
        el: "#app",  // 绑定元素
        data: {   // 绑定数据
            name: "张三",
            num: 1
        }
    });
</script>
</html>
```

Vue的使用步骤：

- 第一步：创建Vue实例，`new Vue()`。关联页面的模板，将自己的数据(datas)渲染到关联的模板，只要data中的数据发生变化，页面就跟着发生变化，这种我们成为响应式的。
- 第二步：使用指令`v-on`等来简化対DOM的一些操作。
- 第三步：可以声明方法来做更复杂的操作。

## 2.3.vue指令

### 2.3.1插值表达式

> 花括号

格式：`{{表达式}}`。**<u>只能用在Html标签体里，不可以`<a href="{{link}}">gogogo</a>`。</u>**

说明：

- 该表达式支持`javascript`语法，可以调用`javascript`内置函数（必须有返回值）。
- 表达式必须有返回结果。例如`1+1`，没有结果的表达式不允许使用，如：`let a = 1 + 1`。
- 可以直接获取Vue实例中定义数据或者函数。

> 插值闪烁

使用`{{}}`的方式在网速较慢时会出现问题。在数据未加载完成时，页面上会出现原始的`{{}}`，加载完毕后才显示正确的数据，我们成为插值闪烁。

我们将网速调慢一点，然后刷新页面，试试看刚刚的案例。

![插值闪烁](ES6&vue.assets/20200718134257181.png)

### 2.3.2.v-html和v-text

`v-html`和`v-text`不会出现插值闪烁的情况！！！！

```html
<body>
    <div id="app">
        <!-- 使用插值表达式取出message的值 -->
        {{message}} <br />

        <!-- v-html将message的值取出来，并且显示Html的格式 -->
        <span v-html="message"></span> <br />

        <!-- v-text将message的值取出来，不会转义 -->
        <span v-text="message"></span> <br />
    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data: {
            message: "<h1>hello</h1>",
        }
    }) 
</script>
```

### 2.3.3.v-bind单向绑定

```html
<body>
    <div id="app">
        <!-- 使用v-bind 单向绑定-->
        <!-- 单向绑定：数据变化引起页面变化，但是页面变化不会改变数据 -->
        <a v-bind:href="link">Go</a> <br/>

        <!-- class、style的增强,动态修改class的内容 -->
        <span v-bind:class="{active: isActive, 'text-danger': hasError}"
              v-bind:style="{color: color, 'font-size': fontSize}">你好</span>
    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>
    let instance = new Vue({
        el: '#app',
        data: {
            link: 'https://www.baidu.com',
            isActive: true,
            hasError: true,
            color: 'red',
            fontSize: '36px'
        }
    });
</script>
```

### 2.3.4.v-model双向绑定

```html
<body>
    <div id="app">
        精通的语言: <br />
        <input type="checkbox" name="language" value="java" v-model="language" />java <br />
        <input type="checkbox" name="language" value="php" v-model="language" />php <br />
        <input type="checkbox" name="language" value="python" v-model="language" />python <br />
        <!-- join()方法可以将数组转成字符串 -->
        选中了<span v-text="language.join(',')"></span>
    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>
    let instance = new Vue({
        el: '#app',
        data: {
            language: []
        }
    })
</script>
```

### 2.3.5.v-on事件

> 基本用法

```html
<body>
    <div id="app">
        <!-- v-on添加事件 -->
        <button v-on:click="number++">点赞</button>
        <!-- 除了可以使用data中的数据外,还可以调用方法 -->
        <button v-on:click="decrement">取消</button>
        {{number}}
    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            number: 0
        },
        methods: {
            decrement() {
                if (this.number > 0) {
                    this.number--;
                }
            }
        }
    })
</script>
```

> 事件修饰符

在事件处理过程中程序调用`event.preventDefault()`或`event.stopPropagation()`是非常常见的需求。尽管我们可以在方法中轻松实现这点，但是更好的方式是：方法只有纯粹的数据逻辑，而不是去处理DOM事件细节。

为了解决这个问题，`vue.js`为`v-on`提供了==事件修饰符==。修饰符是由==点开头==的指令后缀来表示的。

- `.stop`：阻止事件冒泡到父元素。
- `.prevent`：阻止默认事件发生。
- `.capture`：使用事件捕获模式。
- `.self`：只有元素自身触发事件才执行。（冒泡或者捕获的都不执行）。
- `.once`：只执行一次。

```html
<body>
    <div id="app">
        <!-- 事件修饰符 -->
        <div style="border: 1px solid red; padding: 20px;" v-on:click="hello">
            大div
             <!-- 当我们点击小div的时候,会触发两次弹窗,这就是事件冒泡！ -->
            <!-- 这里使用.stop就可以阻止事件的冒泡了 -->
            <div style="border: 1px solid blue; padding: 20px;" v-on:click.stop="hello">
                小div <br />
                <!-- .prevent可以阻止事件的默认行为,就不会去百度了 -->
                <a href="https://www.baidu.com" v-on:click.prevent.stop>去百度</a>
            </div>
        </div>

    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: '#app',
        methods: {
            hello() {
                alert("点击了hello()方法");
            }
        },
    })
</script>
```

> 按键修饰符

在监听键盘事件时，我们经常需要检查常见的键值。Vue允许为`v-on`在监听键盘事件时添加按键修饰符。

```html
<!-- 当选中按钮，按下回车键之后才会有弹窗提示 -->
<button v-on:keyup.enter="hello">键修饰符</button>
```

全部的按键别名：

- `enter`
- `tab`
- `delete`（捕获“删除”和“退格”键）
- `esc`
- `up`
- `down`
- `left`
- `right`

> 组合按钮

可以使用如下修饰符和实现仅在相应按键时才触发鼠标或者键盘事件的监听器。

- `ctrl`
- `alt`
- `shift`

```html
<!-- 测试键盘按键和组合键的绑定 -->
<!-- 初始值是0,按up键是加1,按down键是减1,alt+C是清0 -->
<input type="text" v-on:keydown.alt.67="clear" 
       v-on:keydown.up="size++" 
       v-on:keydown.down="size--" 
       v-model="size"/>
```

### 2.3.6.v-for遍历

```html
<body>
    <!-- 遍历数组 -->
    <div id="app">
        <table border="1px">
            <thead>
                <tr>
                    <th>姓名</th>
                    <th>年龄</th>
                    <th>当前索引</th>
                </tr>
            </thead>
            <!-- 推荐要写上:key="index" -->
            <tr v-for="(item, index) in items" :key="index">
                <td v-text="item.name"></td>
                <td v-text="item.age"></td>
                <td v-text="index"></td>
            </tr>
        </table>
    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            items: [
                { "name": "Tangs", "age": 18 },
                { "name": "Ringo", "age": 19 },
                { "name": "Zhangs", "age": 20 }
            ]
        }
    })
</script>
```

### 2.3.7.v-if和v-show

```html
<body>
    <!-- 
        v-if：顾名思义，条件判断。当得到的结果为true时，所在的元素才会被渲染。
        v-show：当得到的结果为true时，所在的元素才会被显示。

        区别： 
        1、当show等于false的时候v-if是直接不显示dom元素，但是v-show是在样式上添加了display=none
        <h1 style="display: none;">show true 看到我</h1>
        2、v-if经常和v-else-if和v-else联用,也可以和v-for联用完成一些判断功能。
    -->

    <div id="app">
        <button v-on:click="show = !show">点我</button>
        <!-- 1、使用v-if显示 -->
        <h1 v-if="show">if true 看到我</h1>
        <!-- 2、使用v-show显示 -->
        <h1 v-show="show">show true 看到我</h1>
    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            show: true
        }
    })
</script>
```

## 2.4.vue计算属性和侦听器

```html
<body>
    <div id="app">
        <!-- 某些结果是基于之前数据实时计算出来的，我们可以使用计算属性 -->
        <ul>
            <li>西游记, 价格:{{price1}}元, 数量: <input type="number" v-model="number1"></li>
            <li>水浒传, 价格:{{price2}}元, 数量: <input type="number" v-model="number2"></li>
            <li>总价: <span v-text="total"></span> <span v-text="message"></span></li>
        </ul>
    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            price1: 50,
            price2: 60,
            number1: 0,
            number2: 0,
            message: ''
        },
        // 计算属性
        computed: {
            total() {
                if (this.number1 < 0 || this.number2 < 0) {
                    this.number1 = 0;
                    this.number2 = 0;
                }
                let sum = this.price1 * this.number1 + this.price2 * this.number2;
                return sum + '元';
            }
        },
        // 监听器
        watch: {
            // 这里是监听number1这个数据
            number1(newValue, oldValue) {
                console.log("oldValue==>" + oldValue + " newValue==>" + newValue);
                if (newValue > 3) {
                    this.message = '，超出库存限制了';
                    this.number1 = 3;
                }
            }
        },
    })
</script>
```

## 2.5.过滤器

```html
<body>
    <!-- 过滤器常用来处理文本格式的操作。
         过滤器可以用在两个地方：双花括号插值和v-bind表达式
    -->
    <div id="app">
        <ul>
            <li v-for="(user, index) in userList" :key="index">
                <!-- 过滤器需要使用管道符 "|" -->
                {{user.id}} ---> {{user.name}} ---> {{user.gender | genderFilter}} ---> {{user.gender | gFilter}}
            </li>
        </ul>
    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>

    // 全局过滤器就可以在任何vue实例中使用了
    Vue.filter("gFilter", function (gender) {
        if (gender == 1) {
            return '男~~~~~';
        }
        return '女~~~~~~';
    });

    new Vue({
        el: '#app',
        data: {
            userList: [
                { 'id': 1, 'name': 'Tangs', 'gender': 0 },
                { 'id': 2, 'name': 'Ringo', 'gender': 1 }
            ]
        },
        // 局部过滤器
        filters: {
            genderFilter(gender) {
                if (gender == 1) {
                    return '男';
                }
                return '女';
            }
        }
    });
</script>
```

## 2.6.组件化

### 2.6.1.组件化简介

在大型应用开发的时候，页面可以划分成很多部分。往往不同的页面，也会有相同的部分。==例如可能会有相同的头部导航。==

但是如果每个页面都独自开发，这无疑增加了我们开发的成本。所以我们会把页面的不同部分拆分成独立的组件，然后再不同页面就可以共享这些组件，避免重复开发。

**在vue里，所有的vue实例都是组件。**

### 2.6.2.定义组件

```html
<body>
    <div id="app">
        <button v-on:click="count++">我被点击了<span v-text="count"></span>次</button>
        <!-- 使用全局组件 -->
        <couter />
        <couter />

        <!-- 使用局部组件 -->
        <couter-component/>
    </div>

</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">

    // 定义全局组件
    Vue.component("couter", {
        template: `<button v-on:click="count++">我被点击了<span v-text="count"></span>次</button>`,
        data() {
            return {
                count: 0
            }
        }
    });

    new Vue({
        el: '#app',
        data: {
            count: 0
        },
        // 定义局部组件
        components: {
            'couter-component': {
                template: `<button v-on:click="count++">我被点击了<span v-text="count"></span>次</button>`,
                data() {
                    return {
                        count: 0
                    }
                }
            }
        }
    });
</script>
```

**总结：**

- 组件其实也是一个`vue`实例，因此它在定义时也会接收：`data`、`methods`生命周期函数等。
- 不同的是组件不会与页面的元素绑定，否则就无法复用了，因此没有`el`属性。
- 但是组件渲染需要`HTML`模板，所以增加了`template`属性，值就是`HTML `模板。
- 全局组件定义完毕，任何`vue`实例都可以直接在`HTML`中通过组件名称来使用组件了。
- `data`必须是一个函数，不再是一个对象。

### 2.6.3.生命周期和钩子函数

每一个`vue`实例在被创建的时候都要经过一系列的初始化过程：创建实例、装载模板、渲染模板等等。`vue`为生命周期中的每个状态都设置好了钩子函数（监听函数）。每当`vue`实例处于不同的生命周期时，对应的函数就会被触发调用。

![vue生命周期](https://cn.vuejs.org/images/lifecycle.png)

```html
<body>
    <div id="app">
        <span v-text="num" id="num"></span> <br/>
        <button v-on:click="num++">点赞</button>
        <h2><span v-text="name"></span>,有<span v-text="num"></span>个人点赞！</h2>
    </div>
</body>
<script src="../node_modules/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            name: 'Tangs',
            num: 0
        },
        methods: {
            show() {
                return this.name;
            },
            add() {
                return this.num++;
            }
        },
        // 钩子函数
        beforeCreate() {
            console.log("=========beforeCreate=========");
            console.log("数据模型未加载：" + this.name,  this.num);
            console.log("方法未加载：" + this.show());
            console.log("html模板未加载：" + document.getElementById("num"));
        },
        created() {
            console.log("=========created=========");
            console.log("数据模型已加载：" + this.name,  this.num);
            console.log("方法已加载：" + this.show());
            console.log("html模板已加载：" + document.getElementById("num"));
            console.log("html模板未渲染：" + document.getElementById("num").innerText);
        },
        beforeMount() {
            console.log("=========beforeMount=========");
            console.log("html模板未渲染：" + document.getElementById("num").innerText);
        },
        mounted() {
            console.log("=========beforeMount=========");
            console.log("html模板已渲染：" + document.getElementById("num").innerText);
        },
        beforeUpdate() {
            console.log("=========beforeUpdate=========");
            console.log("数据模型已更新：" + this.num);
            console.log("html模板未更新：" + document.getElementById("num").innerText);
        },
        updated() {
            console.log("=========updated=========");
            console.log("数据模型已更新：" + this.num);
            console.log("html模板未更新：" + document.getElementById("num").innerText);
        },
    })
</script>
```

# 2.7.vue模块化开发

### 2.7.1.vue-cli

**官网：https://cn.vuejs.org/**

```shell
# 1、全局安装webpack
npm install webpack -g

# 查看webpack版本
webpack -v

# 2、全局安装vue-cli
npm install -g @vue/cli

# 查看vue-cli的版本
vue --version

# 3、初始化vue项目
vue create hello-world

# 4、启动项目
npm run serve
```

### 2.7.2.Element-UI

**官网：https://element.eleme.io/**

> 安装Element-UI

```shell
# 在vue项目目录下使用npm安装
npm i element-ui -S

# 查看element-ui是否安装成功
# package.json中会出现element-ui版本信息
"dependencies": {
"core-js": "^3.6.5",
"element-ui": "^2.13.2",
"vue": "^2.6.11",
"vue-router": "^3.2.0",
"vuex": "^3.4.0"
},
```

> vue完整引入ElementUI

在 main.js 中写入以下内容：

```js
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```

**具体使用Element-UI查看官网文档即可。**

# 3.前端代码片段

## 3.1.GET请求

```json
"http-get请求": {
    "prefix": "httpget",
    "body": [
        "this.\\$http({",
        "url: this.\\$http.adornUrl(''),",
        "method: 'get',",
        "params: this.\\$http.adornParams({})",
        "}).then(((data))=>{",
        "})"
    ],
    "description": "httpGet请求"
}
```

## 3.2.POST请求

```json
"http-post请求": {
    "prefix": "httppost",
    "body": [
        "this.\\$http({",
        "url: this.\\$http.adornUrl(''),",
        "method: 'post',",
        "data: this.\\$http.adornData(data,false)",
        "}).then(({data})=>{});"
    ],
    "description": "httpPOST请求"
}
```

## 3.3.vue模板

```json
"vue模板":{
    "prefix":"vue", 
    "body":[
        "<template>",
        "<div></div>",
        "</template>",
        "",
        "<script>",
        "export default {",
        "//import 引入的组件需要注入到对象中才能使用",
        "components:{},",
        "props:{},",
        "data(){",
        "//这里存数据",
        "return{};",
        "},",
        "//计算属性",
        "computed: {",
        "",
        "},",
        "//监控data中数据变化",
        "watch: {",
        "",
        "},",
        "//方法",
        "methods: {",
        "",
        "},",
        "//声明周期 - 创建完成（可以访问当前this实例）",
        "created() {",
        "",
        "},",
        "//生命周期 - 挂载完成（可以访问DOM元素）",
        "mounted() {",
        "",
        "},",
        "beforeCreate() {},//生命周期 - 创建之前",
        "beforeMount() {},//生命周期 - 挂载之前",
        "beforeUpdate() {},//声明周期 - 更新之前",
        "updated() {},//生命周期 - 更新之后",
        "beforeDestroy() {},//生命周期 - 销毁之前",
        "destroyed() {},//生命周期 - 销毁之后",
        "activated() {},//缓存keep-alive",
        "};",
        "</script>",
        "",
        "<style scoped>",
        "</style>",
    ],
    "description":"生成vue模板"
}
```




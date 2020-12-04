### 一.  插值操作语法

#### 1.1.Mustache语法

- 将data的文本数据插入HTML中

- 基本使用方法：`{{}}`中放入data里的数据名称，也可以是一个表达式例如`{{counter*2}}`

```js
<body>
    <div id="app">
        <p>{{message}}</p>
        <p>{{firstName+lastName}}</p>
        <p>{{firstName+' '+lastName}}</p>
        <p>{{firstName}} {{lastName}}</p>
        <p>{{counter*2}}</p>

    </div>
    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                message: 'hello vue.js',
                firstName: 'Juice',
                lastName: 'Box',
                counter: 100
            },
        })
    </script>
</body>
```

#### 1.2.v-once指令

- 该指令后面不需要跟表达式

- 使用该指令的元素和组件只会渲染一次，再次修改数据不会随着数据改变而改变

```js
<body>
    
    <div id="app">
        <p>{{message}}</p>
        <p v-once>{{message}}</p>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                message: '我是v-once指令'
            },
        })
    </script>
</body>
```

#### 1.3. v-html指令

- 可以将`{{}}`里面的数据以HTML的格式进行解析
- 该指令后往往跟上一个string类型，然后将其内容中的html解析并渲染到页面
- 不安全，不建议使用

```js
<body>

    <div id="app">
        <p v-html="url"></p>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                url: `<a href="http://www.baidu.com">百度一下</a>`
            }
        })
    </script>
</body>
```

#### 1.4.v-text指令

- 作用与Mustache类似，都是将数据显示到界面(不以HTML格式解析),下例页面显示为`<a href="http://www.baidu.com">百度一下</a>`

```js
<body>
    
    <div id="app">
        <p v-text="url"></p>

    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                url: `<a href="http://www.baidu.com">百度一下</a>`
            },
    </script>
</body>
//url: `<a href="http://www.baidu.com">百度一下</a>`
```

#### 1.5.v-pre指令

- 跳过这个元素及其子元素的编译过程，下例中页面显示效果为`{{url}}`

```js
<body>
    
    <div id="app">
        <p v-pre>{{url}}</p>

    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                url: `<a href="http://www.baidu.com">百度一下</a>`
            },
        })
    </script>
</body>
//url
```

#### 1.6.v-cloak指令

- 因为浏览器在编译`{{}}`里的内容时，会将`{{}}`以快速闪过的方式显示在页面，影响用户体验，所以通过v-cloak指令解决这一问题
- 注意要添加样式来搭配使用

```js
<style>
    [v-cloak] {
        display: none;
    }
</style>

<body>

    <div id="app">
        <p v-cloak>{{url}}</p>

    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                url: `<a href="http://www.baidu.com">百度一下</a>`
            },
        })
    </script>
</body
```



### 二. v-bind(动态绑定属性)

#### 2.1.v-bind的基本使用

- 动态绑定标签的一些属性

```js
<body>

    <div id="app">
        <p><img v-bind:src="imgUrl"></p>
        <!-- 语法糖写法 -->
        <p><img :src="imgUrl"></p>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                imgUrl: '//edu-image.nosdn.127.net/3310f128e53b406f94400f7ae6046db2.png?imageView&quality=100'
            },
        })
    </script>
</body>
```

#### 2.2.动态绑定class

##### 2.2.1.对象语法

- `:class=""`在引号中传入对象

- 用法一：直接通过{}绑定一个类

  `<h2 :class="{'active': isActive}">Hello World</h2>`

- 用法二：也可以通过判断，传入多个值

  `<h2 :class="{'active': isActive, 'line': isLine}">Hello World</h2>`

```js
<style>
    .active {
        width: 100px;
        color: pink;
    }
    
    .bfa {
        width: 100px;
        background-color: #bfa;
    }
</style>
<body>

    <div id="app">
        <h1 :class="{active:isActive,bfa:isBfa}">{{message}}</h1>
        <h1 :class="getClass()">{{message}}</h1>

        <button @click="change">切换</button>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                message: '9527',
                isActive: true,
                isBfa: true,
            },
            methods: {
                change: function() {
                    this.isActive = !this.isActive
                    this.isBfa = !this.isBfa
                },
                getClass: function() {
                    return {
                        active: this.isActive,
                        bfa: this.isBfa
                    }
                }
            },
        })
    </script>
</body>
```

##### 2.2.2.数组语法

- `:class=""`在引号中传入数组

```js
<style>
    .active {
        width: 100px;
        color: pink;
    }
    
    .bfa {
        width: 100px;
        background-color: #bfa;
    }
</style>

<body>

    <div id="app">
        <h1 :class="['active','bfa']">{{message}}</h1>
        <button @click="change">切换</button>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                message: '9527',

            },
        })
    </script>
```

#### 2.3.绑定style

- 我们可以利用v-bind:style来绑定一些CSS内联样式
- n在写CSS属性名的时候，比如`font-size`也可以用驼峰语法`fontSize`

##### 2.3.1.对象语法

- :style="{color: currentColor, fontSize: fontSize + 'px'}"
- 也可以在引号后面直接传一个data里的对象

```js
<body>
    <div id="app">
        <h1 :style="styleObj">动态绑定style（对象方法）</h1>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                styleObj: {
                    color: 'pink',
                    "background-color": ' #bfa',
                    width: '400px'
                }
            },
            methods: {

            },
        })
    </script>
</body>
```



##### 2.3.2.数组语法

- `<div v-bind:style="[baseStyles, overridingStyles]"></div>`

```js
<body>
    <div id="app">
        <h1 :style="[baseStyle,otherStyle]">动态绑定style（数组方法）</h1>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                baseStyle: {
                    color: 'pink',
                    "background-color": ' #bfa',
                    width: '400px'
                },
                otherStyle: {
                    'font-size': '50px'
                }
            },
            },
        })
    </script>
```



### 三. 计算属性

#### 3.1. 什么是计算属性

- 在某些情况，我们可能需要对数据进行一些转化后再显示，或者需要将多个数据结合起来进行显示
- 计算属性是写在vue实例的computed中的

```js
<div id="app">
        <p>{{firstName+' '+lastName}}</p>
        <p>{{firstName}} {{lastName}}</p>
        <p>{{fullName}}</p>
    </div>
    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                firstName: 'Juice',
                lastName: 'box'
            },
            computed: {
                fullName: function() {
                    return this.firstName + ' ' + this.lastName
                }
            },
        })
```



#### 3.2. 计算属性的复杂操作

- 例如数据是一个对象数组，要从数组中的对象中拿到价格再求和

```js
<div id="app">
        <h1>总价格：{{totalPrice}}</h1>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                books: [{
                    id: 1,
                    name: 'JavaScript基础',
                    price: 80
                }, {
                    id: 2,
                    name: 'ES6',
                    price: 98
                }, {
                    id: 3,
                    name: '深入理解计算机原理',
                    price: 98
                }, {
                    id: 4,
                    name: '现代操作系统',
                    price: 87
                }]
            },
            computed: {
                totalPrice: function() {
                    let ret = 0
                    for (let i = 0; i < this.books.length; i++) {
                        ret += this.books[i].price
                    }
                    return ret
                }
            },
        })
    </script>
```

#### 3.3.计算属性的setter和getter

- 每一个计算属性都包含一个getter和一个setter
- 在大多数情况下我们只是用getter，很少用setter

```js
<body>

    <div id="app">
        <!-- 直接拼接 -->
        <p>{{firstName}} {{lastName}}</p>

        <!-- 通过computed -->
        <p>{{fullName}}</p>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                firstName: 'Juice',
                lastName: 'box'
            },
            computed: {
                fullName: {
                    set: function(newVal) {
                        const names = newVal.split(' ')
                        this.firstName = names[0]
                        this.lastName = names[1]
                    },
                    get: function() {
                        return this.firstName + ' ' + this.lastName
                    }
                }
            },
            methods: {

            },
        })
    </script>
</body>
```

#### 3.4.计算属性的缓存

- methods和computed看起来都可以实现我们的功能,那计算属性的作用又是什么？
- 计算属性会进行缓存，如果多次使用时，计算属性只会调用一次

```js
<body>

    <div id="app">
        <!-- 直接拼接 -->
        <p>{{firstName}} {{lastName}}</p>

        <!-- 通过定义的methods的返回值 -->
        <!-- 调用了5次 getFullname()-->
        <p>{{getFullname()}}</p>
        <p>{{getFullname()}}</p>
        <p>{{getFullname()}}</p>
        <p>{{getFullname()}}</p>
        <p>{{getFullname()}}</p>

        <!-- 通过computed -->
        <!-- 调用了1次fullName() -->
        <p>{{fullName}}</p>
        <p>{{fullName}}</p>
        <p>{{fullName}}</p>
        <p>{{fullName}}</p>
        <p>{{fullName}}</p>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                firstName: 'Juice',
                lastName: 'box'
            },
            computed: {
                fullName: function() {
                    console.log('我是computed里的fullName，我被调用了');
                    return this.firstName + ' ' + this.lastName
                }
            },
            methods: {
                getFullname: function() {
                    console.log('我是methods里的getFullname，我被调用了');

                    return this.firstName + ' ' + this.lastName
                }
            },
        })
    </script>
</body>
```

### 四.v-on(事件监听)

- 在前端开发中，会做交互，我们会去监听用户的触发事件的事件

#### 4.1.v-on基础

- 下例是一个基本使用的例子

```js
<body>
    <!-- v-on指令用于绑定事件可简写为@，即语法糖 -->
    <div id="app">
        <p>{{message}}</p>
        <button @click="increment">+</button>
        <button @click="decrement">-</button>

    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                message: 0
            },
            computed: {

            },
            methods: {
                increment() {
                    this.message++
                },
                decrement() {
                    this.message--
                }
            },
        })
    </script>
</body>
```

#### 4.2.v-on的参数

- 如果该方法不需要额外参数，那么方法后的()可以不添加。
- 如果方法本身中有一个参数，而你又省略了(),那么会默认将原生事件event参数传递进去
- 如果需要同时传入某个参数，同时需要event时，可以通过$event传入事件

```js
<body>
    <!-- 事件监听的时候，调用了一个方法，该方法没有传参数可以省略()) -->
    <div id="app">
        <!-- 事件调用的方法没有参数 -->
        <button @click='btn1()'>按钮1</button>
        <button @click='btn1'>按钮1</button>

        <!-- 在事件定义时，写函数时省略了小括号，但方法本身需要一个参数,这个时候Vue会默认
        将浏览器产生的event事件对象传入到该方法 -->
        <button @click='btn2("abc")'>按钮2</button>
        <button @click='btn2'>按钮2</button>

        <!-- 在方法定义时，需要event对象，同时又需要其他参数 -->
        <button @click='btn3'>按钮3</button>
        <!-- 如何手动获取event？使用$event -->
        <button @click='btn3("adwd",$event)'>按钮3</button>

        <button>按钮4</button>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {

            },
            computed: {

            },
            methods: {
                btn1() {
                    console.log('btn1');
                },
                btn2(n) {
                    console.log(n);
                },
                btn3(abc, event) {
                    console.log(`第一个参数：${abc} 第二个参数${event}`);
                }
            },
        })
    </script>
</body>
```

#### 4.3.v-on修饰符

- 部分使用如下

```js
<body>

    <div id="app">
        <!-- 1. .stop的使用：阻止事件冒泡,在事件后加上.stop -->
        <div @click='divClick'>
            <button @click.stop='btnClick'>9527</button>
        </div><br>

        <!-- 2. .prevent的使用：阻止默认行为,在事件后加上.prevent -->
        <form action="9527">
            <input type="submit" value="提交" @click.prevent='submitClick'>
        </form><br>

        <!-- 3监听某个键帽的点击 -->
        <input type="text" @keyup.enter="keyUp">

        <!-- 4. .once 只会触发一次 -->

    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {

            },
            computed: {

            },
            methods: {
                btnClick() {
                    console.log(`this is the click from button`);
                },
                divClick() {
                    console.log(`this is the click from div`);
                },
                submitClick() {
                    console.log(`this is the click from sumbit`);

                },
                keyUp() {
                    console.log(9527);
                }
            },
        })
    </script>
</body>
```



### 五.条件判断(v-if、v-else-if、v-else)

#### 5.1.基本使用

- 这三个指令与JavaScript中的if，elseif，else类似

```js
<body>
    <div id="app">
        <h1 v-if="score>=90">优秀</h1>
        <h1 v-else-if="score>=80">良好</h1>
        <h1 v-else-if="score>=60">及格</h1>
        <h1 v-else>不及格</h1>

    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                score: 90,
            }
        })
    </script>
</body>
```

#### 5.2.v-show

- v-show的用法和v-if非常相似，也用于决定一个元素是否渲染
- 如何区别使用二者：
  - pv-if当条件为false时，压根不会有对应的元素在DOM中。
  - v-show当条件为false时，仅仅是将元素的display属性设置为none而已

```js

```



### 六. v-for(循环遍历)

- 当我们有一组数据需要进行渲染时，我们就可以使用v-for来完成

#### 6.1. 遍历数组

```js
<body>

    <div id="app">
        <ul>
            <li v-for="(item, index) in fruits" :key="index">{{index+1}} {{item}}</li>
        </ul>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                fruits: ['apple', 'banana', 'watermelon', 'peach']
            },
        })
    </script>
</body>
```



#### 6.2. 遍历对象

```js
<body>
    <!-- 遍历对象时，第一个值为value，第二个值为属性名 
        第三个值为index-->
    <div id="app">
        <ul>
            <li v-for="(item, key,index) in info" :key="index"> {{key}}：{{item}} ***索引为：{{index}}</li>
        </ul>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                info: {
                    name: 'JuiceBox',
                    age: 22,
                    hobbies: '摸鱼',
                }
            }
        })
    </script>
</body>
```



#### 6.3. 数组哪些方法是响应式的

- 只有使用了响应式的方法，Vue才能检测到数组做了修改，并将新数据渲染到页面

- push()方法
- pop()
- shift()
- unshift()
- splice()
- sort()
- reverse()

##### v-for与v-bind的结合案例

- 要求：把data中的数据用ul的结构显示到页面，默认第一个有active样式，然后点击哪个li，哪个li就具有active样式，上一个有样式的失去该样式

```js
<style>
    * {
        margin: 0;
        padding: 0;
        font-weight: bold;
        font-size: larger;
    }
    
    .active {
        color: #bfa;
    }
</style>

<body>

    <div id="app">
        <ul>
            <li v-for="(item, index) in movies" :class="{active: currentIndex === index}" @click="liClick(index)">
                {{index}}.{{item}}
            </li>
        </ul>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                movies: ['海王', '海贼王', '加勒比海盗', '海尔兄弟'],
                currentIndex: 0
            },
            methods: {
                liClick(index) {
                    this.currentIndex = index
                }
            },
        })
    </script>
</body>

```



### 七. v-model的使用

- Vue中使用v-model指令来实现表单元素和数据的双向绑定。表单控件在实际开发中是非常常见的。特别是对于用户信息的提交，需要大量的表单

#### 7.1. v-model的基本使用

* 当我们在input框里写入内容时，也同时修改了message的值

```js
<body>

    <div id="app">
        <input type="text" v-model="messgae">
          <h1>{{messgae}} </h1>
    </div>
    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                messgae: '我是双向绑定的数据'
            },
        })
    </script>
</body>
```

#### 7.2原理

- 就是v-bind与v-on的结合,即这两个操作是一样的效果：
  - `<input type="text" v-model="message">`
  - ``<input type="text" v-bind:value="message" v-on:input="message = $event.target.value">`

#### 7.3. v-model和radio/checkbox/select的结合使用

##### 7.3.1.与radio的结合使用

```js
<body>

    <div id="app">
        <label for="">
      <input type="radio" id="male" value="男" v-model="sex">男
    </label>

        <label for="">
      <input type="radio" id="female" value="女" v-model="sex">女
    </label>
        <h2>选择的性别是：{{sex}}</h2>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                sex: '男'
            },
        })
    </script>
</body>

```

##### 7.3.2.与checkbox的结合使用

```js
<body>

    <div id="app">
        
        <!-- <label for="license">
      <input type="checkbox" id="license" v-model="isAgree">同意协议
    </label>
        <h2>你选择的是{{isAgree}}</h2>
        <button :disabled='!isAgree'>下一步</button> -->

        <input type="checkbox" value="篮球" v-model="hobbies">篮球
        <input type="checkbox" value="足球" v-model="hobbies">足球
        <input type="checkbox" value="乒乓球" v-model="hobbies">乒乓球
        <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
        <h2>你选择的爱好是{{hobbies}}</h2>
    </div>

    <script src="/js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                isAgree: false,
                hobbies: []
            },
        })
    </script>
</body>
```

##### 7.3.3.与select的结合使用

```js
<body>

    <div id='app'>
        <!-- 选择一个 -->
        <select name="choice" v-model="fruit">
      <option value="苹果">苹果</option>
      <option value="香蕉">香蕉</option>
      <option value="西瓜">西瓜</option>
      <option value="芒果">芒果</option>
      <option value="葡萄">葡萄</option>
    </select>
        <h2>你选的水果为{{fruit}}</h2>

        <!-- 选择多个 -->
        <select name="choice" v-model="fruits" multiple>
      <option value="苹果">苹果</option>
      <option value="香蕉">香蕉</option>
      <option value="西瓜">西瓜</option>
      <option value="芒果">芒果</option>
      <option value="葡萄">葡萄</option>
    </select>
        <h2>你选的水果为{{fruits}}</h2>
    </div>

    <script src='/js/vue.js'></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                fruit: '香蕉',
                fruits: []
            },
        })
    </script>
</body>
```



#### 7.4. 修饰符

- 部分修饰符如下

```js
<body>

    <div id='app'>
        <!-- 1.修饰符：lazy 失去焦点或者敲击回车时变量才会更新-->
        <input type="text" v-model.lazy="message">
        <h2>{{message}}</h2>

        <!-- 2.修饰符：number -->
        <input type="text" v-model.number="age">
        <h2>{{typeof age}}</h2>

        <!-- 3.修饰符：trim -->
        <input type="text" v-model.number="name">
        <h2>{{name}}</h2>
    </div>

    <script src='/js/vue.js'></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                message: '',
                age: 18,
                name: ''
            },
        })
    </script>
</body>
```



### 八. 组件化开发

- 注册组件的基本步骤：
  - 创建组件构造器
  - 注册组件
  - 使用组件

#### 8.1. 组件的基本使用

```js
<body>

    <div id="app">
        <my-cpn></my-cpn>
        <my-cpn></my-cpn>
    </div>

    <script src='/js/vue.js'></script>
    <script>
        // 1.创建组件构造器对象
        const cpnC = Vue.extend({
            template: `    <div>
        <h2>我是标题</h2>
        <p>我是组件</p>
        <p>我是组件</p>
    </div>`
        })

        // 2.注册组件
        Vue.component('my-cpn', cpnC)

        const app = new Vue({
            el: '#app',
            data: {

            },
        })
    </script>
</body>
```

#### 8.2. 全局组件和局部组件

- 当我们通过调用Vue.component()注册组件时，组件的注册是全局的
- 如果我们注册的组件是挂载在某个实例中, 那么就是一个局部组件

#### 8.3. 父组件和子组件

- p组件和组件之间存在层级关系
- p而其中一种非常重要的关系就是父子组件的关系

```js
<body>

    <div id='app'>
        <cnp1></cnp1>
        <cnp2></cnp2>
    </div>

    <script src='/js/vue.js'></script>
    <script>
        // 创建组件1构造器对象(子组件)
        const cpnC1 = Vue.extend({
            template: `    
    <div>
        <h2>我是cpnC1</h2>
        <p>我是组件1</p>
        <p>我是组件1</p>
    </div>`
        })

        // 创建组件2构造器对象，并在里面注册组件1(父组件)
        const cpnC2 = Vue.extend({
            template: `    
    <div>
        <h2>我是cpnC2</h2>
        <p>我是组件2</p>
        <p>我是组件2</p>
        <cnp1></cnp1>
    </div>`,
            components: {
                cnp1: cpnC1
            }
        })

        const app = new Vue({
            el: '#app',
            data: {
                message: 9527
            },
            components: {
                cnp2: cpnC2,
                // cnp1: cpnC1
            }
        })
    </script>
</body>
```

#### 8.4. 注册的语法糖

```js
<body>

    <div id='app'>
        <cpn1></cpn1>
        <cnp2></cnp2>
    </div>

    <script src='/js/vue.js'></script>
    <script>
        // 全局组件注册的语法糖
        Vue.component('cpn1', {
            template: `    
    <div>
        <h2>我是cpn1</h2>
        <p>我是组件cpn1</p>
        <p>我是组件cpn1</p>
    </div>`
        })

        const app = new Vue({
            el: '#app',
            data: {

            },
            components: {
                'cnp2': {
                    template: `<div>
                    <h2>我是cpn2</h2>
                    <p>我是组件cpn2</p>
                    <p>我是组件cpn2</p>
                    </div>`
                }
            }
        })
    </script>
</body>
```

#### 8.5. 模板的分类写法

```js
<body>

    <div id='app'>
        <cpn1></cpn1>
    </div>

    <!-- <script type="text/x-template">
        <div>
            <h2>模板分离的写法cpn1</h2>
            <p>模板分离的写法cpn1</p>
            <p>模板分离的写法cpn1</p>

        </div>
    </script> -->
    <template id="cpn1">
    <div>
      <h2>模板分离的写法cpn1</h2>
      <p>模板分离的写法cpn1</p>
      <p>模板分离的写法cpn1</p>

    </div>
  </template>
    <script src='/js/vue.js'></script>
    <script>
        Vue.component('cpn1', {
            template: '#cpn1'
        })
        const app = new Vue({
            el: '#app',
            data: {

            },
        })
    </script>
</body>

```



#### 8.6. 数据的存放

* 子组件不能直接访问父组件
* 子组件中有自己的data, 而且必须是一个函数.

```js
<body>

    <div id='app'>
        <cpn1></cpn1>
    </div>

    <template id="cpn1">
        <div>
            <h2>{{message}}</h2>
            <p>{{message}}</p>
            <p>{{message}}</p>

        </div>
    </template>
    <script src='/js/vue.js'></script>
    <script>
        Vue.component('cpn1', {
            template: '#cpn1',
            data() {
                return {
                    message: '我是组件里的data返回的数据'
                }
            }
        })
        const app = new Vue({
            el: '#app',
            data: {

            },
        })
    </script>
</body>
```

#### 8.7. 父子组件的通信

* 父传子: props

```js
<body>

    <div id='app'>
        <!-- 将父组件的数据绑定给子组件的变量 -->
        <cpn :cfruits="fruits" :cmessage="message"></cpn>
    </div>

    <!-- 父传子通过props -->
    <template id="cpn">
    <div>
      <!-- 将获取到的父组件的数据进行渲染 -->
      <span v-for="(item, index) in cfruits" :key="index"> {{item}}</span>
      <p>{{cmessage}}</p>
    </div>
  </template>

    <script src='/js/vue.js'></script>
    <script>
        const cpn = {
            template: '#cpn',
            // 使用数组时
            // props: ['cfruits', 'cmessage'], //里面的字符串为该子组件的变量名

            //使用对象时
            props: {
                cfruits: Array, //可以作传入数据的类型限制
                // cmessage: String,

                cmessage: { //也可以指定默认值
                    type: String,
                    default: '我是默认值',
                    required: true
                }
            },
        }
        const app = new Vue({
            el: '#app',
            data: {
                message: '我是vue实例的数据',
                fruits: ['苹果', '香蕉', '桃子', '西瓜', '草莓', '芒果']
            },
            components: {
                cpn
            }
        })
    </script>
</body>
```

* 子传父: $emit

```js
body>

    <div id='app'>
        <!-- 父组件绑定该事件对传过来的数据做处理，
          cpnClick那边传入的参数不是事件对象，而是子组件传的数据 -->
        <cpn @itemclick="cpnClick"></cpn>
    </div>

    <template id="cpn">
        <div>
            <button v-for="(item, index) in categories" :key="index" @click='btnClick(item)'>{{item.name}}</button>
        </div>
    </template>
    <script src='/js/vue.js'></script>
    <script>
        const cpn = {
            template: '#cpn',
            data() {
                return {
                    categories: [{
                        id: 'aaa',
                        name: '热门推荐'
                    }, {
                        id: 'bbb',
                        name: '手机数码'
                    }, {
                        id: 'ccc',
                        name: '家用家电'
                    }, {
                        id: 'bbb',
                        name: '电脑办公'
                    }]
                }
            },

            methods: {
                btnClick(item) {
                    // 通过该自定义事件发射数据给父组件
                    this.$emit('itemclick', item.id)
                }
            },
        }

        const app = new Vue({
            el: '#app',
            data: {},
            components: {
                cpn
            },
            methods: {
                cpnClick(id) {
                    console.log(id);
                }
            }
        })
    </script>
</body>
```

- 

#### 

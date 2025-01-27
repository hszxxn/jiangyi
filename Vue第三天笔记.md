

# Vue基础第三天笔记

## 反馈 

| ***  | 老高 我觉得还可以再慢点 你太累了 歇会                        |
| ---- | ------------------------------------------------------------ |
| ***  | （疑车无据）--今天讲的太多了，真的，没消化完                 |
| ***  | 需要判断就取反 反着反着就习惯了                              |
| ***  | 老师，慢点吧，没人拦你是因为追不上你。                       |
| ***  | 点歌台吗，我点一首乱世巨星，顺带附赠你两个上课铃，赌神&&《新闻联播》重制版（这开场曲，绝对燃，网易云音乐有） |
| ***  | 懵懵懂懂的，好像明白，又好像不明白，敲代码去了，拜拜         |
| ***  | 过滤器的传参数和串联的使用能不能再讲一遍                     |
| ***  | 似懂非懂的感觉，希望老师在讲一下v-bind v-model map filter some 以及过滤器 |
| ***  | <input type="text" :value="name" name="" id="" /> 我输入内容为啥不会改变变量的值，而前天 <div id="add"> {{ name }}真棒 {{ count + 1 }} {{ list.reverse().join("") }} </div>没有使用v-model 他就影响下边的值形成死循环了 |
| ***  | 老师，以后所有的项目都引用vue.js么,不是的话，我们在学习的时候要不要区分哪些是原生的语法，哪些是Vue专用的语法？教师节忘了祝福，祝老师月饼节快乐！！！ |
| ***  | 东西需要慢慢吸收，有点多，但是又没有办法，硬着头皮去学把，filter，map以前讲过的，可是又忘记了，这可咋整，愁死我了，算了，温故而知新把。 |
| ***  | 努力敲代码吧!多敲才是王道                                    |
| ***  | 讲很不错，但是感觉有些跟不上，不知老高可以体谅一下，我这种基础很稀薄得学子吗，特别是那种链式写法得时候，啊有些转不过弯来。 |
| ***  | prefect两遍确实加强了记忆                                    |
| ***  | 老师讲慢点吧 零基础挺不容易的 当然也努力的在学新知识了 当时懂了 下来敲代码吧也倒是还行 但是整整就懵了 在学几天我估计茶饭不思夜不能寐了 太上头了 |

## 复习 

* 全局过滤器 (所有Vue实例都可使用) /局部过滤器(当前实例)
* {{  表达式 | 过滤器名称 }} 或者 v-bind:
* {{ 表达式 | 过滤器名称(参数1, 参数2) }} =>传入的参数一定是从**`第二个`**参数开始 =>第一个参数永远都是 **`管道`**前面表达式计算的结果的值**`value`**   
* 多个过滤器同时使用  {{ 表达式 |  过滤器1 | 过滤器2 | .... }}
* v-bind  绑定属性 => 动态属性   v-bind:属性名="表达式"  =>:属性="表达式"  => 通过(data)数据的变化来决定属性的变化 => 摆脱了dom操作   
* v-model  绑定表单数据 => 双向绑定 =>  数据变化 => 视图变化 (响应式数据)  视图变化 =>数据变化
* v-model 实现原理   v-bind:value="表达式"
* v-model 实现原理   v-on:值改变事件="方法" => 方法  =>   data数据 =  event.target.value 
* map/filter => map(function(item,index){   return item })  =>返回一个新数组  => 新数组的长度和原数组长度一定相等
* filter =>  筛选  => filter(function(item,index){ return 条件表达式  }) => 条件表达式=> true => 返回当前项
* 条件表达式 => false =>不返回结果  
* filter => 等到一个新数组 =>  相等于 根据条件表达式筛选出符合条件的结果
* some => 和filter是一样的  => 根据条件判断有没有符合条件的数据 =>  布尔值
* some(function(item,index){  return 条件表达式 })
* 插值表达式  
* 指令



## 基础-自定义指令-全局自定义指令

> **`目标`**掌握如何**`全局`**自定义一个指令
>
> * 使用场景:需要对普通 DOM 元素进行操作，这时候就会用到自定义指令 
>
> - 分类:**`全局注册`**和**`局部注册`**
>
> 1. 在创建 Vue 实例之前定义全局自定义指令  Vue.directive()
> 2. Vue.directive('指令的名称',{ inserted: (使用指令的DOM对象,表达式对象) => { 具体的DOM操作 } } );
> 3. 表达式对象 => value  => 表达式计算结果的值
> 4. 在视图中通过"v-自定义指令名"去使用指令

```js
 // 定义指令
//  自定义指令是不需要加v-前缀的
// 第二个参数为一个对象  对象中要实现 inserted的方法
// inserted中的参数为当前指令所在元素的dom对象
Vue.directive("focus", {
        inserted(dom,expression) {
          dom.focus();
        }
 });
```

> * 指令名称要全小写
>
> **`任务`** 实现一个可以自动聚焦input的自定义指令v-focus
>
> * 实现一个类似v-text指令的功能的自定义指令v-textcopy
>
> **`路径`**参照实现代码

## 基础-自定义指令-局部自定义指令

> **`目标:`**掌握如何自定义一个局部指令
>
> * 需要注册在当前实例上
> * filters 
> * directives
>
> ```js
> directives: {
> focus: {
> inserted(dom,expression) {
> dom.focus();
> }
> }
> } // 局部自定义指令实现
> ```
>
> **`任务`** 实现一个可以自动聚焦input的自定义指令v-focus
>
> - 实现一个类似v-html指令的功能的自定义指令v-htmlcopy
>
> 
>
> **`路径`**参照实现代码

## 基础-表格案例-使用自定义指令完成自动获取焦点功能

> **`目标-任务`**在表格案例中 实现自定义指令 完成 输入框自动聚焦功能
>
> **`路径`**参照实现代码

## 基础-实例选项-计算属性-文档分析

**`目标`** 掌握实例选项中计算属性的基本含义

> - 场景:当(插值表达式/v-bind表达式)过于复杂的情况下 可以采用计算属性 对于任何**`复杂逻辑`**都可以采用计算属性,**`简单逻辑也可以采用计算属性`**
> - 使用: 在Vue实例选项中 定义 computed:{ (key)计算属性名: **`带返回值`**的函数 }
> - 说明: 计算属性的值 依赖 数据对象中的值  数据对象发生改变 => 计算属性发生改变=> 视图改变
> - methods 和 计算属性的区别
> - methods 每次都会执行  
> - 计算属性 每计算一次 都会讲结果缓存,如果 data中的数据没变化,则直接从缓存中取数据
> - 如果 data中变化了 , 则会执行 新的计算方法 => 缓存
> - 计算属性 会每次比较**`data更新`**前后的值 如果前后一致 则不会引起视图变化
> - methods每次都会执行 性能较计算属性较差
> - 计算属性是有缓存机制的,更智能化 ,更有效率

## 基础-实例选项-计算属性-基本使用

> **`目标`** 掌握如何使用计算属性完成基本业务
>
> * 由于计算属性中 要return 值 => 立刻返回 => 同步/异步 => 计算属性方法 => **`必须写同步代码`**
> * **`ajax/setTimeout`**  不能写在计算属性中
>
> ​       示例:  通过计算属性实现字符串的翻转
>
> ​        1 定义数据对象 
>
> ​        2 实现计算属性 
>
> ​        3 使用计算属性
>
> ​     -->
>
> ```js	
> computed: {
> nameReverse() {
> return this.name
> .split("")
> .reverse()
> .join("");
> }
> } // 定义计算属性
> ```
>
> 当 数据对象中 name发生变化时  计算属性也会重新计算计算=> 改变页面视图
>
> 计算属性 和 methods方法的区别: 
>
> 计算属性不需要调用形式的写法  而methods方法必须采用 方法() 调用的形式
>
> methods 每次都会执行
>
> 计算属性 会比较data变化 => data不变化 =>  从缓存中取值 => data变化 => 重新计算=> 放入缓存
>
> **`任务1`:**通过计算属性实现**`字符串的翻转`**
>
> **`任务2`**通过计算属性实现 根据**`变量select(布尔值)`**的内容 是否将div标签的class设置为**`select`**
>
> **`路径`**参考代码

## 表格案例-用计算属性实现商品搜索

> **`目标-任务`**在表格案例中使用计算属性实现商品搜索
>
> - 搜索框内容变化=> 列表内容变化
> - 计算属性:  依赖 输入值和 列表的变化实现
>
> ​       使用计算属性实现品牌搜索
>
> ​      1  定义 品牌搜索的内容
>
> ​      2  定义计算属性 
>
> ​      3  实现计算属性的筛选功能
>
> ​      4  计算属性替换原有得列表数据
>
> ```js
> computed: {
> // 实现计算属性
> newList() {
> if (!this.searchValue) return this.list;
> return this.list.filter(item => {
>  return item.name.startsWith(this.searchValue);
> });
> }
> }
> ```
>
> 用到了 数组的filter筛选功能  和 字符串的 startsWith 校验功能

当data中无法完成复杂逻辑时,通通可以在**`计算属性`**中实现

## 在Vue中实现发送网络请求

>**`目标`**: 了解在Vue中发送网络请求  
>
>在Vue.js中发送网络请求本质还是ajax，我们可以使用插件方便操作。
>
>1. vue-resource: Vue.js的插件，已经不维护，不推荐使用
>2. [axios](https://www.kancloud.cn/yunye/axios/234845) :**不是vue的插件**，可以在任何地方使用，**`推荐`**
>
>> 说明: 既可以在浏览器端又可以在node.js中使用的发送http请求的库，**`支持Promise`**，不支持jsonp
>>
>> 如果遇到jsonp请求, 可以使用插件 `jsonp` 实现
>>
>> ```js
>> // promise 是为了解决回调
>> $.ajax({
>>     url:'',
>>     data:{},
>>     success:function(data){
>>         // data为后端响应回来的数据
>>         $.ajax({
>>             url:''
>>             data:data,
>>             success:function(data1){
>>              $.ajax({
>>                  url:'',
>>                  data:data,
>>                  success:function(data2){
>>                      
>>                  }
>>              })  
>>           }
>>         })
>>     }
>> })
>> // 
>>  new Promise(function(resolve,reject){ 
>>     if(flag === 1) {
>>           resolve("success")  // 正确执行  返回一个字符串 success
>>     }else {
>>         reject(new Error("fail")) // reject 抛出错误 throw一个错误
>>     } 
>>  }).then(result => {
>>      return  axios({url,data:result }) // 第一个请求 生成result1
>>  }).then(result1 => {
>>      return axios(url,data:result) // 第二个请求生成result2
>>  }).then(result2 => {
>>      return axios({url,data:result}) //第三个请求result3
>>  }).then(result3 => {
>>      return axios({})
>>  }).catch(err=>{
>>      
>>  })
>> // 链式调用
>> ```
>>
>> //  如果reject  .相当于执行失败 =>  执行失败=>不会进入到then => 会进入到promise的catch
>
>axios 返回的是一个promise对象 
>
>```js
>axios ===  new Promise(function(reslove,reject){
>            
>})
>axios().then(拿到返回数据(接口返回数据)).catch(err=> )
>```
>
>

## 基础-json-server工具的使用

> **`目标`**掌握json-server工具的使用
>
> * 目的: 没有后端的支撑下 ,前端难以为继,json-server可以快速构建一个后台的接口服务,供前端调用
> * mock => 模拟数据 
> *   json-server 是一个命令行工具 可以json文件变成接口文件 
>
> * json-server遵循**`restful`**接口规则
>
> 安装
>
> ```bash
> npm i -g  json-server // 也可以采用yarn 和 cnpm
> ```
>
> 新建一个json文件 db.json,并在相对目录下运行命令行命令
>
> json文件格式  
>
> ```json
> {
>  // brands 相等于 我们数据库中的一个表
> "brands": [
>  {
>    "name": "苹果",
>    "date": "2018-05-30T08:07:20.089Z",
>    "id": 2
>  },
>  {
>    "name": "小米",
>    "date": "2018-07-04T08:59:51.200Z",
>    "id": 4
>  },
>  {
>    "name": "华为",
>    "date": "2019-07-14T04:04:56.599Z",
>    "id": 5
>  },
>  {
>    "name": "75期大神",
>    "date": "2019-07-14T04:31:03.017Z",
>    "id": 7
>  },
>  {
>    "name": "李四",
>    "id": 8
>  }
> ],
>  user:[{
>      
>  }],
>  money:[{}]
> }
> ```
>
> 
>
> ```bash
> json-server --watch db.json
> 
> ```

* 启动完成后=>  通过访问地址访问接口

>**`任务`**
>
>1. 安装json-server
>2. 新建db.json 写入json数据
>3. 启动json-server服务
>4. 通过访问地址访问接口

## 基础-RESTFUL的接口规则

> **`目标`**: 掌握restful接口规则
>
> - RESTful是一套**`接口设计规范`**
> - 用**`不同的请求类型`**发送**`同样一个请求标识`** 所对应的处理是`不同的`
> - 同样的请求标识 => 相同的请求地址**`url`**
> - 通过Http请求的不同类型(POST/DELETE/PUT/GET)来判断是什么业务操作(CRUD ) 
> - CRUD => 增删改查 => C =>Create(增)  R => Read(查)    U => UPDATE(改)  D =>DELETE(删)
> - json-server应用了RESTful规范

**2. HTTP方法规则举例**

| **HTTP方法** | **数据处理** | **说明**                                           |
| ------------ | ------------ | -------------------------------------------------- |
| POST         | Create       | 新增一个没有id的资源                               |
| GET          | Read         | 取得一个资源                                       |
| PUT          | Update       | 更新一个资源。或新增一个含 id 资源(如果 id 不存在) |
| DELETE       | Delete       | 删除一个资源                                       |

1. 查询数据  GET  /brands 获取db.json下brands对应的所有数据 **`列表`**
2. GET /brands/1 查询id=1数据 **`单条`**
3. 删除数据 DELETE   /brands/1 删除id=1数据
4. 修改数据 PUT  /brands/1 请求体对象 {name:'李四' }
5. 上传/添加 POST /brands 请求体  {name:'李四'}

> PUT和POST用法一样  请求体 {name:"张三",age: 18, sex:'男'}

5. 查询 GET /brands?title_like=关键字  -> 模糊搜索

>**`任务`** 在json-server中测试体会restful接口规则
>
>

## 基础-postman测试接口

> **`目标`**学会使用postman测试接口
>
> * 说明:Postman是一款功能强大的网页调试与发送网页HTTP请求的测试工具
>
> **`任务`**安装postman工具,并启动son-server 测试json-server的crud接口
>
> 

## 基础-axios-介绍-及基本使用

>**`目标`**:掌握如何使用axios 
>
>* 除去post请求 ,所有接口的正确请求返回码都是**`200`** 但是post的状态码是**`201`**
>
>* 本地引入axios文件
>
>* 在npm 中引入axios文件
>
>* ```js
>axios.get(url).then((res) => {
>// 请求成功 会来到这  res响应体
>}).catch((err) => {
>// 请求失败 会来到这 处理err对象
>	})	
>	```
>```js
>
>axios.get('http://localhost:3000/brands')
>.then(res => {
>console.log(res.data);
>})
>.catch(err => {
>console.dir(err)
>});
>```
>
>* 发送delete请求
>
>```js
>axios.delete('http://localhost:3000/brands/109')
>.then(res => {
>console.log(res.data);
>})
>.catch(err => {
>console.dir(err)
>});
>```
>
>* 发送post请求

> ```js
>axios.post('http://localhost:3000/brands', {name: '小米', date: new Date()})
>    .then(res => {
>    console.log(res);
>})
>    .catch(err => {
>    console.dir(err)
>});
> ```
>
>注意:post 成功 status===201 其他是200
>
>**`任务`** 启动json-server 完成一个 getlist(获取整个表的数据)接口的访问
>
>**`路径`**参考代码
>
>

## 基础-表格案例-axios-列表

>**`目标-任务`** 将表格案例中列表数据实现用axios请求
>
>​      **`路径`**: 使用axios请求列表
>
>​      1.  引入axios资源
>
>​      2.  在渲染完成时间中请求列表数据
>
>​      3.  赋值给data数据
>
>代码
>
>```js
>mounted() {
>// 渲染完成事件
>axios.get("http://localhost:3000/brands").then(result => {
>  this.list = result.data;
>     });
>   }
>```
>
>**注意** mounted 是一个事件,后面会讲到,指的是渲染完成事件
>
>created 也是一个事件  指的是实例创建完成事件

## 基础-表格案例-axios-删除商品

>**`目标-任务`**` 将表格案例中列表数据实现用axios删除
>
>​      **`路径`**: 使用axios请求列表
>
>​      1.  删除方法中传入ID
>
>​      2.  删除方法中调用删除接口
>
>​      3.  删除完成后重新调用请求接口
>
>代码
>
>```js
>  delItem(id) {
>       if (confirm("确定删除此条记录")) {
>         axios
>           .delete("http://localhost:3000/brands/" + id)
>           .then(result => {
>             this.getList(); // 重新调用拉取数据
>           });
>       }
>     }
>```
>
>​       路径: 使用axios删除商品
>
>​       1 删除方法中传入ID 
>
>​       2 删除方法中调用删除接口
>
>​       3 删除完成后重新调用接口
>
>```js
>delItem(id) {
>       if (confirm("确定删除此条记录")) {
>         axios
>           .delete("http://localhost:3000/brands/" + id)
>           .then(result => {
>             this.getList(); // 重新调用拉取数据
>           });
>       }
>     }
>```
>
>

## 基础-表格案例-axios-添加商品

>**`目标-任务`** 将表格案例中列表数据实现用axios添加
>
>​      **`路径`**: 使用axios请求列表
>
>​      1.  添加方法中调用新增接口 
>
>​      2. 添加成功后 拉取数据
>
>​      3.  清空输入框
>
>代码
>
>```js
>  addItem() {
>       // 添加商品
>       axios
>         .post("http://localhost:3000/brands", {
>           name: this.name,
>           date: new Date()
>         })
>         .then(result => {
>           if (result.status == 201) {
>             this.getList(); // 请求数据
>             this.name = ""; // 清楚文本框内容
>           }
>         });
>```
>
>

## 基础-表格案例-axios-搜索功能-分析

>**`目标`** 通过分析得出 计算属性不能进行搜索功能分析的结论
>
>* 如果**`一个函数有return`** 那么这个函数基本上就是一个**`同步的函数`** 就不能执行任何的异步的业务
>* computed计算属性 return   filter  return 
>
>计算属性=> 异步操作搜索=>返回结果 XXXXX 走不通
>
>结论: 搜索功能不能采用 axios请求 进行解决
>
>计算属性中一定是**`同步操作`**,如果有**`异步`**操作,则该业务逻辑就会失败
>
>新知识: 监听属性 watch

## 基础-实例选项-watch-文档分析

> **`目标`**:掌握watch 选项的基本功能含义
>
> 场景: 当需要根据**`数据变化`** 进行相应业务操作,且该操作是**`异步操作`**时,**`计算属性不能再使用`**,可以使用监听watch特性
>
> * watch=> 是监听data数据 中数据项的变化对象 => data中数据变化  => watch 监控函数执行 =>监控函数 
> * 监控函数 =>  newValue.oldValue
> * watch选项不需要返回值 不需要return  只需要在函数体中执行对应的逻辑即可\
> * watch:  {  data属性名(监视谁写谁的名字): function(newValue(新值),oldValue(旧值)){} } 

## 基础-实例选项-watch-基本使用

>**`目标-任务`**-: 定义一个城市city变量,当城市city变量发生改变时 生成对应城市的一个数组 如  
>
>```json
>【
>```
>
>​      1   实现 city的双向绑定  
>
>​        2  watch监听city的数据项改变 
>
>​        3  改变函数中实现
>
>* 计算属性和watch区别
>* 计算属性 必须要有返回值 所以说不能写异步请求 因为有人用它的返回值(插值表达式)
>* watch选项中可以写很多逻辑 不需要返回值 因为没有人用它的返回值
>
>代码
>
>```js
>watch: {
>//newValue是最新的值 oldValue为后面的旧值
>city(newValue, oldValue) {
>  this.list = this.list.map(item => ({
>    city: item.name,
>    count: newValue
>  }));
>}
>}
>```
>
>

## 基础-表格案例-axios-搜索功能-实现

>**`目标-任务`**使用watch实现前后台搜索功能
>
>​         1. 监听搜索内容框 
>
>​         2. 在监听函数中实现搜索逻辑
>
>​         3.  将返回结果设置给 当前数据对象
>
>​         4.   更换数据对象
>
>代码
>
>```js
>   watch: {
>     searchValue(newValue) {
>            if (newValue) {
>              axios
>                .get("http://localhost:3000/brands?name_like=" + newValue)
>                .then(result => {
>                  this.list = result.data;
>                });
>            } else {
>              this.getList();
>            }
>           }
>        }
>     ```
>     

## 基础-组件-组件体验

> **`目标：`**建立对于组件的认识
>
> 场景: 重复的页面结构,数据,逻辑 都可以抽提成一个组件  
>
> 对于复杂的结构来说 都可以通过抽提组件的方式 来简化开发过程
>
> - 简单 高效 不重复

## 基础-组件-组件特点

> **`目标`**认识组件特点
>
> 组件特点: 组件是一个**`特殊的 Vue实例`**
>
> 和实例相似之处:   data/methods/computed/watch  等一应俱全  
>
> * vue实例有**`el`**选项  组件实例没有el 但是**`templete`**页面结构
>
> **注意** 值得注意的是  data和Vue实例的区别为 组件中data为一个函数   没有el选项 
>
> template 代表其页面结构 (**`有且只要一个根元素`**)
>
> 每个组件都是**`独立`**的 运行作用域  **`数据 逻辑没有任何关联`**
>
> data () {  return {  数据属性 } }

## 基础-组件-全局组件

> **`目标`**掌握如何实现一个全局组件
>
> 路径: 实现一个全局组件
>
> 1  定义一个全局组件
>
> 2   写入组件选项
>
> 3 使用注册组件

```js
 // 注册组件名称 推荐 小写字母 加横向的结构
      Vue.component("content-a", {
        template: `<div>
        {{count}}
        </div>`,
        data() {
          return {
            count: 1
          };
        }
      });
// 注意  data中必须为一个返回对象的函数
// template必须有且只有一个根元素
```

**`任务`** 实现一个全局组件 完成 加减步进器

![./assets/step.png](./assets/step.png)

## 基础-组件-局部组件

> **`目标`**: 掌握 如何实现一个局部组件
>
> 路径: 局部组件的实现
>
> ​        1 定义一个局部组件
>
> ​        2 写入组件选项
>
> ​        3 使用组件
>
> ```js
> new Vue({
> el: "#app",
> data: {},
> methods:{ },
> components:{
>     "content-a": {
>         template: `<div>
>     {{count}}
>     </div>`,
>     data() {
>       return {
>         count: 1
>       };
>     }
> }
> })
> ```
>
> 
>
> **注意**注册组件时,注册名不能为 - 分割的名称
>
> **`任务`** 实现一个局部组件 完成 加减步进器
>
> 

## 基础-组件-组件嵌套

> **`目标`**掌握如何在组件中掌握嵌套
>
> - 我们可以在new Vue()实例中使用自定义组件,
> - 也可以在注册自定义组件时,嵌套另一个自定义组件,也就是父子组件的关系
>
> ```js
> var comA = {
>  template: `<div>我是子组件</div>`
> };
> var parentA = {
>  template: `<div>
>   我是父组件
>   <com-a></com-a>
>  </div>`,
>  components: {'com-a': comA }
> };
> var vm = new Vue({
>  el: "#app",
>  data: {},
>  methods: {},
>  components: {
>    'parent-a":parentA
>  }
> });
> ```
>
> 
>
> **`任务`** 
>
> 1. 实现一个Vue实例
> 2. 自定义一个组件parentB，内容为我是父组件parentB
> 3. 自定义一个组件childA ,内容是我是子组件childA
> 4. 将在父组件中使用childA, 并在页面上实现显示两个parentB
>
> **`路径`**: 实现组件嵌套
>
> ​        1 定义多个组件 
>
> ​        2 组件对组件进行引用 
>
> ​        3 使用根组件
>
> ​       注意: 组件嵌套和全局 及局部组件没关系
>
> **`关于具体实现参考课程提供的代码`**

## 基础-组件-组件通信的几种情况

> **`目标`**：了解组件通信的几种情况（
>
> - 父组件 =》 子组件   需要将数据传给子组件 
> - 子组件 =》 父组件  如果父组件需要 子组件也可以传数据给父组件
> - 兄弟组件1 =》兄弟组件2 

## 基础-组件-父组件给子组件传值Props

> **`目标`**:掌握父组件用Props给子组件传值
>
> - props作用: 接收父组件传递的数据
> - props就是父组件给子组件标签上定义的属性
>
> ```js
> 1. props是组件的选项  定义接收属性
> 2. props的值可以是字符串数组 props:["list"]
> 3. props数组里面的元素称之为prop(属性) 属性=?值
> 4. prop的值来源于外部的(组件的外部)
> 5. prop(我们这里是lists)是组件的属性->自定义标签的属性
> 6. prop的赋值位置(在使用组件时,通过标签属性去赋值)
> 7. prop的用法和data中的数据用法一样
> ```
>
> - **`注意`**: 父组件传递给子组件的数据是**`只读`**的,即**`只可以用,不可以改`**
> - 用props完成父组件给子组件传值  传值的属性都是定义在 子组件的标签上,可以采用v-bind的形式传递动态值
> - 定义props属性 在标签上定义属性  v-bind传递动态值
> - 在子组件中声明接收的属性
> - 在子组件中使用 组件 记住 属性只可以用 不可改
>
> **`任务`** 
>
> 1. 定义子组件
> 2. 在父组件中将 ["北京", "上海","天津"] 传递给子组件
> 3. 在子组件中获取该数据 并采用v-for循环显示在页面上
>
> ```html
>    components: {
>      a: {
>        template: "<b :name1='123'></b>",
>        components: {
>          b: {
>            props: ["name1"],
>            template: "<c :name2='234'></c>",
>            components: {
>              c: {
>                props: ["name2"],
>                template: "<d :name3='345'></d>",
>                components: {
>                  d: {
>                    props: ["name3"]
>                  }
>                }
>              }
>            }
>          }
>        }
>      }
>    }
> ```
>
> 
>
> **`路径`**: 
>
> ```
>   1. 定义父子组件 
>      2. 定义props接受父组件属性
>      3. 父组件中通过属性给子组件传值
>      4. 注册使用子组件
> ```
>
> ```js
> const comA = {
> template: `<div>
> <span v-for="(item,index) in list" :key="index">{{item}}</span>
> </div>
> `,
> props: ["list"] // props可以是数组  也可以是对象
> };
> ```
>
> **`关于具体实现参考课程提供的代码`**

## 基础-组件-子组件给父组件传值(自定义事件)

> **`目标`**:掌握如何通过子组件给父组件传值
>
> ​    父组件如何监听子组件事件?
>
> - 上个小节中,父组件通过props将值传给了子组件,那么子组件如何将数据传给父组件?
> - 可通过在子组件中触发**`$emit`**事件,然后在父组件中监视此事件 进行追踪
> - **`任务`**
>
> 1. 上一小节基础上  实现 点击子组件的城市时,将当前点击的城市传递给父组件,
> 2. 父组件 将 当前点击城市 通过props再次传递给子组件 
> 3. 子组件 根据当前选中和循环项目比对 得出 哪个城市 得到 select class 
> 4. 对 select  class进行样式赋值,使其 字体大小为40px  字体颜色为红色
>
> **`注意`**：抛出事件名必须为全小写
>
> **`路径`**:  点击子组件时  调用父组件的方法  改变当前的select
>
> ​        1  定义子组件 
>
> ​        2  定义props接收 父组件 数据 函数
>
> ​        3  父组件给子组件传值  数据 和函数
>
> ​        4  子组件点击事件绑定 父组件传递prop函数
>
> **注意 !!!!!!!!!!!!!**       如果props有驼峰命名的情况 赋值时  需要拆成- 分割的形式 否则无法传递
>
> 例如
>
> ```html
> <p postTitle="hello world"></p> // 错误
> <p post-title="hello world"></p> //正确
> ```
>
> **`关于具体实现参考课程提供的代码`**

## 复习

* 自定义指令 => 全局(所有Vue实例-组件实例).局部(当前实例=>) => 注册位置不同 应用范围不同
* Vue.directive("指令名称(不用写v-)", {  (元素插值时执行)inserted: function(dom,expressions){}  })
* directives:{ 指令1,指令2.... }
* 计算属性 =>将所有的复杂逻辑抽提出来 =>   计算属性更高效 => 缓存机制 =>  计算一次之后 会将结果放到缓存,如果 data数据没有变化,则直接从缓存中取,  => 更高效的逻辑处理方式
* Vue发送网络请求 => axios => 支持promise => 链式调用 => 回调嵌套 => 代码更优雅
* aixos => restful接口规则 
* 不同的请求类型 同样的请求地址 处理不同的业务逻辑  
* get  /brands 获取brands表的所有数据
* post  /brands 新增一个数据 到brands表
* get /brands/1 查询 id=1单条数据
* delete  /brands/1 删除id=1单条数据
* put /brands/1 修改id=1单条数据
* get  /brands?name_like=关键字
* 表格案例 => axios 请求
* created (钩子函数)=> 执行 请求  axios获取整个表的数据 赋值给本地的数据list  完成后台数据到前端同步 
* 删除数据 => 点击删除时,传入删除数据的id => 得到删除的地址 => 调用删除接口 => then中重新请求数据 完成前后同步
* 新增数据  => 点击新增时 => 调用新增接口 .传入新增数据 => then => 重新请求数据
* 搜索数据 => 计算属性 return 结果 => 同步方法  => ajax请求行不通
* 搜索数据 => watch选项  => 监视某一个属性的数据变化 => 执行相应的函数  => 监听谁就写谁名字 => function(newValue,oldValue){    axios搜索 }
* 组件 => 重复的页面结构 重复的数据 重复的业务逻辑 => 组件 
* 全局组件/局部组件=>特殊的Vue实例 => 没有el  但是又template => template有且只有一个根元素
* data 是一个函数 带返回值的函数   返回值是一个对象 对象里面的内容就是我们的data数据
* 每个组件之间都是独立的作用域 
* Vue.component("组件名称",{    template:data(){} ,methods })abc  abc-d(全小写)
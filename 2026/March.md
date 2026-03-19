## 3.19 Javascript
- **JavaScript基础**
  JavaScript和java是完全不同的东西，只是名称类似
- **JavaScript写在哪里**
  - head部分：用于声明变量，函数，类型，为事件绑定处理函数
  - body部分：调用脚本执行
  - 外部脚本：用于定于函数，类型 
     -将代码封装在一个js文件中，在需要的地方引用，完成一次定义，多出引用的效果，简化代码维护
     -在文件中不需要写标签
- **基本语法**
  - 大小写敏感
  - 弱类型语言 ~大型项目后期难维护
  - 分句结尾
  - 注释（单行  多行 方法） 
  - 字符串既可以用单引号 也可以用双引号
    ~~~
//var s="helloWorld!"
/*var s="helloWorld!"
var s="helloWorld!"
var s="helloWorld!"*/
var s="helloWorld!";

fun1 (12)
/**
 * 方法一
 * @param {string} param1 这是参数一
 */
function fun1(param1){

}
    ~~~
	
## 3.18 CSS
### 定位
- position: absolute | 
  - 绝对定位absolute是以浏览器为参考系，但是如果绝对定位的元素在 非静态定位（static）的元素中，那就以这个元素为参考,绝对定位与left right top bottom连用
  - fixed
     - 无论浏览器如何滚动，窗口都位于指定位置
  - relative让我们的元素可以在不脱离文档流的情况下 使用left right top bottom，而移动的位置是相对于其本身的位置
  - sticky 粘滞定位，滚动界面当标签相对于浏览器界面 等于指定定位时 标签粘滞
### 盒子的层次
- **z-index 数值越高标签越在上层**
  ~~~
    <body>
    <div style="background-color: thistle; z-index: 10;"></div>
    <div style="background-color: aquamarine;z-index: 11;"></div>
    </body>
  ~~~
- **呈现形式 display：none | block | inline | inline-block**
  - block 块级标签 可设置宽 ,高，元素独占一行
  - inline 行级标签 不可设置宽，高，元素自适应内部内容
  - inline-block 介于block与line之间 可以设置宽，高 但是不会独占一行
- **表格线框**
  

## 3.17  CSS
### 背景样式
- background-image 设置背景图片
- background-repeat 设置背景重复
- background-position:top left；第一个值是Y轴上，第二个值是X轴上
- background-size 设置背景图片大小
~~~
<style>
     div {
        width: auto;
        height: 600px;
        border: 1px solid red;
        background-image: url("C:\\Users\\15283\\source\\repos\\htmldemo\\header.png");
        background-repeat: no-repeat;
        background-position:top left ;
        background-size: cover;
     }
    </style>
~~~
### 图片样式
- vertical-align 其他元素相对于图片的对齐方式
~~~
<style>
        img{
            vertical-align: top;
        }
    </style>
~~~
### 布局样式
- 文档流
  - 既文档的排列方式：在同一个平面中 从左往右，从上往下排列
- 脱离文档流 简单理解为盒子脱离原有的文档排列浮起来，从同一平面浮起来，根据一定的要求排列。
- 浮动
  - float：left | right
~~~
style>
        div{
            width:100px;
            height: 100px;
            background-color: aquamarine;
            margin: 10px;
        }
    </style>
</head>
<body>
    <div></div>
    <div></div>
    <div></div>
    <div style="background-color: chocolate;float: left; margin-left: 10px; margin-right: 10px;"></div>
    <div style="float: left;  margin-right: 10px;"></div>
    <div style="float: left; margin-right: 10px;"></div>
    <!--给最后一个方块设置清除浮动 不受前面浮动的影响-->
    <div style="clear:both"> </div>
</body>
~~~
### 菜单栏和电商物品选择实现

## 3.16 CSS
- css用于设置元素的特征（决定样式）
- css一般写在3个地方
   1. 元素标签的style 属性中设置
~~~
<div style=" width: 100px; height: 100px; background-color: forestgreen">div</div>
~~~
   2. html文档的<style></style> 标签中设置
   ~~~
   style>
        div {
            width: 100px;
            height: 100px;
            background-color: brown
        }
    </style>
   ~~~
   3. 在.css文件中设置
~~~
<!--在头文件中引用已经定义好了的css-->>
<link rel="stylesheet" href="demo.css">

<!--定义css文件-->
p {
    width: 200px;
    height: 100px;
    background-color: lightblue;
}
~~~
- 通过元素id属性获取
  - css根据id获取标签，需要在id名前添加 #
~~~
<style>
    div {
        width: 100px;
        height: 100px;
        background-color: brown
    }

    #div1 {
        width: 100px;
        height: 100px;
        background-color: blue
    }
</style>
~~~
- 通过元素class属性获取
~~~
<div class="div-test">div</div> 
<div class="div-test">div</div>

<style>
    .div-test {
        width: 100px;
        height: 100px;
        background-color: cyan
    }
</style>
~~~
- 其他选择器
  - 空格 所有子集（包括子集中的子集）
~~~
<style>
    .test1 div {
        border-width: 2px;
        border-style: solid;
        border-color: forestgreen;
        color: blue;
    }

    .test2 > div {
        border-width: 2px;
        border-style: solid;
        border-color: forestgreen;
        color: blue;
    }
</style>
~~~
- 父级>子集 父级下面的子一级标签
-  .test3~.test4  test3以后的所有同级test4
- **伪类选择器**
  - 鼠标徘徊选择器 .ul-test li:hover   hover经过就改变样式
  - .ul-test li:active   点下去改变样式
  - a:visited  浏览过改变样式
- **CSS优先级**
  - style属性中定义样式优先级最高
  - 就近原则
  - id选择器>class选择器>标签选择器
#### 常用样式
- **盒子模型**
  - 标签元素排列规则是 *从左往右 从上往下*
   ![[Pasted image 20260315171601.png|196]]
  蓝颜色是真正可以写字的部分，浅一点的黄颜色是边框，绿色是可写字部分和边框的距离
称为内边距，margin外边距
- 盒子的水平排列
 ![[Pasted image 20260315171944.png|421]]
- 盒子的垂直排列
 ![[Pasted image 20260315172140.png|220]]
 - **盒子样式**
   - margin  4个参数上左下右，2个 上下 左右
- **文本样式**
~~~
 <style>
     div {
         font-family: "微软雅黑";
         font-size: 20px;
         font-weight: bold;
         text-align: center;
         background-color: lightblue;
         height: 100px;
         line-height: 5;
     }

     s {
         text-decoration: none;
     }

     a {
         text-decoration: none;
         color: red;
     }
 </style>
~~~

## 3.15 Html
**列表标签**
- **无序列表**
	无序列表是工作中最常用的列表，ul是定义无序状态的标签，li是具体的列表项
- **type属性 circle/disk/square**
~~~
   <ul >
       <li type="circle">无序列表1</li>
       <li type="disk">无序列表2</li>
       <li type="square">无序列表3</li>
   </ul>
   <ul>
    <li type="circle">无序列表1</li>
    <li type="disk">无序列表2</li>
    <li type="square">无序列表3</li>
  </ul>
    <li>无序列表1</li>
    <li>无序列表2</li>
    <li>无序列表3</li>
  </ul>
~~~
	无序标签之中可以嵌套其他内容,如图片 超链接 
 - **有序列表 自定义列表**
~~~
	 <!--无序标签-->

<!--有序列表标签-->
<ol>
    <li>有序列表1</li>
    <li>有序列表2</li>
    <li>有序列表3</li>
</ol>
<ol type="i">
    <li>有序列表1</li>
    <li>有序列表2</li>
    <li>有序列表3</li>
</ol>
<ol type="I">
    <li>有序列表1</li>
    <li>有序列表2</li>
    <li>有序列表3</li>
</ol>
<ol type="a">
    <li>有序列表1</li>
    <li>有序列表2</li>
    <li>有序列表3</li>
</ol>
<ol type="A">
    <li>有序列表1</li>
    <li>有序列表2</li>
    <li>有序列表3</li>
</ol>
~~~
- **自定义列表标签**
~~~
<!--dl定义自定义列表的标签，dt设置标题，dd具体列-->
<dl>
    <dt>自定义标题1</dt>
    <dd>自定义列1</dd>
    <dd>自定义列2</dd>
    <dt>自定义标题2</dt>
    <dd>自定义列1</dd>
    <dd>自定义列2</dd>
</dl>
<!--表格标签 table定义表格 tr定义表格行 td定义单元格-->
<!--colspan="2" 表格跨2列-->
<!--rowspan="2" 表格跨2行-->
<table width="300" height="300" border="1">
<tr>
    <td>A</td>
    <td colspan="2">B</td>
</tr>
<tr>
    <td rowspan="2">C </td>
    <td>D</td>
    <td>D</td>
</tr>
<tr>
    <td>E</td>
    <td>F</td>
</tr>
</table>
~~~
- **表单标签**
	- 侧重于向后端发送数据
	- 主要已input**标签为主** 辅之以name属性，通过form表单向后端发送数据
	- input 不需要闭标签 因为xhtml
~~~
	 <!--表单标签-->>
 <form action="后端URL" method="提交方式">
     <input type="text" name="与后端参数名一直" value="">
     <br>
     <input type="count" name="与后端参数名一直" value="">
     <br>
     <input type="date" name="与后端参数名一直" value="">
     <br>
     <input type="radio" name="与后端参数名一直" value="">
     <br>
     <input type="checkbox" name="与后端参数名一直" value="boy">
     <br>
     <input type="hidden" name="与后端参数名一直" value="">
     <br>
     <select name="class">
         <option>class one</option>
         <option>class two</option>
     </select>
     <br>
     <input type="submit" value="提交" />
     <input type="reset" value="重置" />
 </form>
~~~
- **iframe 标签**
  - 用于在一个页面中嵌入另一个页面
  - 配合a标签使用时，可以用a标签指定iframe指向的页面
~~~
<!--iframe标签 网址禁用ifrma嵌入的情况也有-->
<a href="https://www.google.com" target="iframe-test  ">show google in iframe</a><br>
<iframe name="iframe-test" width="600" height="600"></iframe>
<!--div&span 容器标签 重要-->
<!--div是块状容器，独占一行，主要用于搭建网页布局，页面整体布局就靠它-->
<!--span是行级容器，其大小自适应于包裹的对象-->
<div>
    <span>这是span标签</span>
    <span>hello</span>
</div>
<div>
    <span>这是span标签</span>
    <span>world</span>
</div>
<input type="text"> <br>
<input type="checkbox" checked> <br>
<input type="button" value="button"> <br>
<input type="password" placeholder="please input password"> <br>
<input type="tel">
<br>
<textarea name="message" rows="10" cols="30">sss</textarea
~~~

## 3.14 Html
**框架级标签**
1.  !DOCTYPE html 定义文档的类型
2.  html 定义html文档
3.  head 定义文档的头部
	- base   
	- title   
	- meta
4.  body 定义文档的主体
~~~
    <b>这是加粗标签(bold)</b><strong></strong>  <br>
    2<sup>2</sup>这是上标标签
    <br>
    2<sub>2</sub>这是下标标签
    <br>
    <s>strikethrough</s>这是删除线标签
    <u>underline</u>这是下划线标签
    <br>
    <i>italics</i><em></em> 这是斜体标签
    <br>
    <code></code>这是代码标签
    <br>
    <cite>cite</cite>  这是引用标签
    <p>p标签独占一行</p><p>p标签独占一行</p>
    <hr>分割线标签
    <pre>按照输入格式
    显示文本
</pr>
~~~
**链接标签**  
   href属性可以存放图片，文件路径，网址，锚点；
~~~
 <a href="header.png">诗歌剧的照片</a><br>
 <a href="111.zip">文件</a><br>
 <a href="https://www.google.com">google</a>
~~~
- id
标签身份的唯一标识
~~~
<h1 id="h111">标题1</h1>
<br>
<br>
//锚点
<a href="#h111">跳转到id为h111锚点<>
~~~
 - targe
 ~~~
 //self 本页面跳转
 //bank 打开新页面跳转
 <a href="https://www.google.com" target="_self">google本页面跳转</a><br>
 <a href="https://www.google.com" target="_bank">google新面跳转</a>
 ~~~
**图片标签**
~~~
 <!--图标标签-->
 <img src="header.png" alt="图片失效（失效代替）">诗歌剧
~~~

## 3.13 WebApi
- 如何做自己的API
控制器继承于父类ControllerBase
- 构建器 和app配置
~~~
var builder = WebApplication.CreateBuilder(args);

// 1. 注册控制器服务 (必选)
builder.Services.AddControllers();

var app = builder.Build();

// 2. 配置中间件管道 (顺序也很重要)
app.UseHttpsRedirection();
app.UseAuthorization();

// 3. 映射控制器路由 (必选)
app.MapControllers();

app.Run();
~~~

## 3.12 MVC 创建表单及表单验证
- **MVC**    
能够返回View方法的前提是 类必须是Controller类的子类
如何添加衬衫创建表单Form
在MVC view中如果有用到tagHelper则会显示为绿色

- **asp-validation-for**
~~~
<span class="text-danger" asp-validation-for="Size"></span>
~~~
属性验证 为单个属性准备 与span配套使用  

- **validation**
~~~
protected override ValidationResult? IsValid(object? value, ValidationContext validationContext)
~~~
 vlaue是只附加验证的那个属性的值  例如Size ，而ValidationContext是传进来的整个对象 


- **括号强转**  
double转换成int会丢失小数部分  
unboxing 拆箱只能转换成原来的类型 负责会抛出InvalidCastException异常   

- **顶级语句**   
顶级语句遇到class namespace enum struct 就结束，顶级语句默认在 static void Main()中
~~~
static void Main(string[] args)
{
顶级语句
}
~~~

## 3.11 MVC 创建表单
**Bootstrap**
~~~
<a class="btn btn-primary">
~~~
这里的‘a’ 代表超链接 ，通过在html标签 class属性中添加特定的字符串 ，告诉浏览器
按Bootstrap定义好的规则来渲染这个按钮

Css可以改变如何标签的外观

**Tag helper**
允许在View(html)中使用类似HTML 标签的语法来编写服务器端代码
~~~
<a href="/Shirt/Details/5">查看详情</a> 

<a asp-controller="Shirt" asp-action="Details" asp-route-id="5">查看详情</a>
~~~
这个超文本链接显示‘查看详情’，
href是根据路径去访问控制器和方法，而taghelper是根据目的地 自动生成路径
*访问控制器的URL（路径）可以由我们自定义，哪怕URL中不带控制器名称*

虽然dotNET core路由默认不区分大小写，但是在编写代码和配置路由时保持首字母大写（PascalCse）是微软官方的推荐方法


## 03.10 WebApi

~~~
builder.Services.AddTransient<IWebApiExecuter, WebApiExecuter>();
~~~
注册WebApiExecuter（服务）接口以及（服务）接口的具体实现
 自定义服务 想要手动注册 
`IHttpClientFactory`是系统已经在框架里注册好了的，所以我们只需要配置就能够使用


~~~
     private readonly IWebApiExecuter webApiExecuter;

     public ShirtsController(IWebApiExecuter webApiExecuter)
     {
         this.webApiExecuter = webApiExecuter;
     }
     public async Task<IActionResult> Index()
     {
         var shirts = await webApiExecuter.InvokeGet<List<Shirt>>("shirts");
         return View(shirts);

     }
~~~
依赖注入向框架请求服务，异步方法调用WebApiExecute中的InvokeGet方法
readonly和get属性只能在声明时或初始化时被赋值
## 03.09 WebApi
native AOT 原生，编译时可以编译为本机代码（性能要求很高的类库，底层是C++）
**控制器与路由**
一个类继承于ControllerBase那么就具有了控制器的能力和行为

**如何在项目中调用访问其他api**
1.  配置
向生成器配置名为“ShirtsApi” 客户端 ，定义该客户端的根地址，和请求头
https://localhost:7025/api/Controller   协议，域名，端口 ，路由前缀，控制器
```
builder.Services.AddHttpClient("ShirtsAPi",client =>
{
    client.BaseAddress = new Uri("https://localhost:7025/api");
    client.DefaultRequestHeaders.Add("Accept","Appliaction/Json");
});

```

2. 使用
通过依赖注入来向框架请求IHttpClientFactory实例
使用实例方法CreatClient向容器请求已经配置好的客户端
使用客户端的GetFromJsonAsync方法访问端点返回Json文件
*(将发送请求转换为二进制发送，并接收二进制流编码按Json格式进行解析)*
~~~
private const string apiName = "ShirtsApi";
private readonly IHttpClientFactory httpClientFactory;

public WebApiExecuter(IHttpClientFactory httpClientFactory)
{   
    this.httpClientFactory = httpClientFactory;
}
 public async Task<T?> InvokeGet<T>(string relativerUrl)
 {   
     var httpClient = httpClientFactory.CreateClient(apiName);
     return await httpClient.GetFromJsonAsync<T>(relativerUrl);
 }
~~~


## 03.08 Multi Threading
**多线程的缺点
- 缺乏原子性  
什么是原子性：单线程下任务要么执行完成，要么执行过程不被其他因素打断，要么完全不执行。
- 竞态性
由于多线程的竞态性，导致其缺乏原子性（谁竞争到上下文谁执行）
例如：两个线程都对10进行++操作，并写入11，进程A和B都进行了写入操作，2次++后结果为11
- 死锁
A占用A的资源同时访问B资源，线程B占用B资源同时访问A的资源

**WhenAll**
- 返回值为Task或Task泛型集合代表所有任务都将完成的任务
- 异步等待，可以使用await关键字，不阻塞线程
- 如果内部有异常则会在等待的任务上抛出，异常收集在AggregateException中

<img width="310" height="34" alt="Pasted image 20260308102452" src="https://github.com/user-attachments/assets/22bfcd53-a934-47af-90a9-aef037a0dfba" />   

 这种用法和同步没有区别，一样阻塞线程

**死锁**
关键字：Lock（锁对象），lock线程锁只能锁住线程，对多线程有效，而不能阻止主线程如何调用其他子线程
**同步方法（阻塞式）** 阻塞线程，线程一直等待任务完成
**await Task.Run()（异步串行）** 不会阻塞当前线程，线程返回线程池，而是挂起任务等结束后由线程继续执行
**TasK.Run()（异步并发）** 多个任务同时进行，不等当前任务完成，同时进行下个任务

**await和lock**
await 当前线程内同时只有一个任务在执行，任务执行完成后再开启下一个
lock  锁住资源 只能有一个线程访问到资源 其他任务排队等待

**线程休眠**
- Thread Sleep
- Task.Delay
这两个方法都可以实现线程休眠，但是区别是Thread Sleep是当前线程休眠但是不释放任务
而Task Delay 是会在线程上释放当前任务，后续哪个线程会接手当前任务
1，Thread Sleep 会阻塞线程，虽然在休眠但是在这段时间内该线程无法执行其他工作而Task,.Delay则相反
2， Thread Sleep 是同步，Task,.Delay是异步，Task,.Delay最好配合await和async使用

**顺序执行线程**
如果我们需要线程执行有一个先后顺序，需要用一个叫ContinueWith方法，来在子线程执行完成之后顺序执行后面的线程

## 03.07
## Multi Threading
**Task.Run()**
- 将任务交由线程池中的线程运行  
- Task.Run()执行一个委托，可以是匿名委托。默认返回值为Task类型
- _= 下划线加等于号可以 忽略返回值（Discards）
- 加了await  
  如果时IO操作，则后台线程会返回线程池，如果时需要线程的技术操作后台线程继续执行，主线程继续向下，程序会一直运行到await拿回结果
- 不加await
  任务交由线程池中的线程执行，主线程继续向下运行，主线程结束时不会等待结果
  <img width="400" height="442" alt="image" src="https://github.com/user-attachments/assets/34b9cc5c-d340-4a4f-97ec-3fba555c8606" />
- 主线程 线程池 后台线程 前台线程
  主线程：通常是只有一个,通常程序运行时自动开启（主线程是前台线程）
  线程池：由CLR管理，线程池中都是后台线程。（可复用的劳动力），当所有前台线程关闭时后台线程自动关闭
  前台线程：new Thread创建的都为前台线程，只要存在前台线程程序就不会关闭


**Task.WaitAll(taskA,TaskB);**
- 1 返回值类型为void（同步方法），
- 2 同步等待，阻塞线程直到所有任务完成，
- 3 如果内部有异常会在wait all结束后抛出。（异常会被收集在AggregateException中）
<img width="300" height="400" alt="image" src="https://github.com/user-attachments/assets/640c1e92-de89-4aec-b391-7d18572480af" />

  


## 03.05
## bootstrap
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/1f07112a-c51b-48c6-960b-dc6faa97b8a1" />     

  提供cdn链接 用于访问css和js， 

## MVC-AddHttpClient
<img width="800" height="219" alt="image" src="https://github.com/user-attachments/assets/d1026677-0c9e-4d06-be57-1925cb552380" />

往服务池里注册httoclient服务，httpClient：能够通过登录第三方api，并通过依赖注入的方式来调用
# 03.04
## MVC
   scaffolding 脚手架  
   - 安装Microsoft.VisualStudio.Web.CodeGeneration.Design  
   - 可以通过dotnet 命令或者VS界面操作追加scaffolding
   - 如何工作：通过反射的方式读取当前模型和数据库上下文，将读取到的模型信息和数据库上下文填入模板中，生成控制器以及view.cs文件
     <img width="399" height="257" alt="image" src="https://github.com/user-attachments/assets/8d3c2478-bad1-4c41-811a-05e41860a032" />

   
## 03.03
## entity framework core
- dotnet ef  migrations add Initial  
  确保在add后使用大写字母开头的单词 
## MVC
- @model IEnumerable<SelfAspNet_MVC.Models.Book>  
  -定义了模型的类型，例如该模型为Book类
- @{Viewdata["Title"]="List";}  
  -在页面标签上显示List
- 路由 Routing  
  -解析URL决定将请求转到哪个控制器Controller，及操作方法 action

## 03.02
## entity framework core
了解了如何通过端点工具 添加nugetpack，并且添加ef tools
<img width="1198" height="171" alt="image" src="https://github.com/user-attachments/assets/546ef25c-fef9-43ee-8b8c-b247d40ec1df" />

连接如何通过命令添加生成migrations 文件 并通过codeFirst方式将对象映射成到数据库中的表
- dotnet ef migrations add Initial
- dotnet ef database update
  
## postgreSQL
- 连接字符串名，可以与数据库名不同
- pqsql中用true 和 false给bool类型赋值而非0和1

## powershell
- 设置环境变量 setx ConnectionStrings__MyContext "Host= ;Port= ;Datebase= ;Username= ;Password= "
- 确认环境变量 echo $Env:ConnectionStrings__MyContext
- 查看当前环境变量 win+R 输入sysdm.cpl 或者设置-系统-系统信息-高级系统设置



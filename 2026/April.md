## 04.08 webApi
- 一个程序中不能有2个一模一样的路由
- 需要通过不同动词或者路由结尾区分
~~~
//设置路由地址的两种方式
//通过通配路由设置 路由地址等于方法名
[Route("api/[Controller]/[Action]")]
[ApiController]

//通过动词中指定路由地址
[Route("api/[controller]")]
[ApiController]
public class MyNewTwoController : ControllerBase
{
    [HttpPost("A")]
~~~
- 要求路由地址必须要带参数
~~~
//在地址中 大括号带参数
 [HttpGet("GetUserName/{id}/{showCN}")]
 public string GetUserName(long id, string? showCN)
~~~

## 04.07 webApi
- webApi中的Query传参
	~~~
	//请求路径中带多个参数，第一个用？后面都用&隔开
	http://localhost:5299/api/mynew/GetUserName?id=1&name=abc&age=18
	~~~
### 400 Badrequest
- 请求参数个数不正确
- 请求参数类型不正确
- Get请求URL长度超过浏览器或者web服务器限制
- 为什么参数为布尔类型时，不传参数也不报错---因为布尔类型 默认为false
- string 类型默认为null，null就是没有
~~~
//方法参数加了URL 可以不传参数也不报错
 public string GetUserName(long id, string? showCN)
~~~
### RESTful 风格的四种传参方式
- GET--读取，获取数据  
- POST--添加数据
- PUT--修改数据
- DELETE--删除数据
*对应数据库中的CRUD*
*JSON格式中的对象，键和值都要双引号*
~~~
{"name": "Gemini"}
~~~

## 04.06  Vue3 webApi
- Vue3 中的视图属性  v-html
~~~

<h1 v-html="getMessage()"></h1>
function getMessage(){
                return `<h1><u>${message}</u></h1>`;
            }
~~~
### webAPI 路由地址
- 路由通过Route中的特性来定义
	通配符 
	~~~
	//控制器通配符   
	[Controller]
	//方法通配符
	[Action]
	~~~
- 如何开启热加载 在端口中输入 dotnet watch ，关闭ctrl+c，重启ctrl+R
	热加载donet watch run 默认监听http端口，要想其监听https端口运行如下代码
	~~~
	dotnet watch run --launch-profile "https"
	~~~
- 请求路径中附带多个对象
~~~
http://localhost:5299/api/mynew/GetUserName?id=1&name=abc&age=18
~~~

## 04.05 Vue3
### 函数中的超时
- setTimeout
~~~
 function updateLuckNumer(){
                setTimeout(() => {
                    luckNumber.value=77;
                }, 2000);
~~~
- 对象上的ref
~~~
//ref用于处理数字或者字符串那种原始类型
let employee=ref({
                name:"Cks",
                age:28,
                salay:1900
            });
            
     function updateLuckNumer(){
                setTimeout(() => {
                    luckNumber.value=77;
                    employee.value.salay=10000;
                }, 2000);
        
~~~
- reactive 用于处理对象
~~~
//使用时不像ref那样用value进行修饰
//reactive是处理复杂对象时应该使用的方法
let employee=reactive({
                name:"Cks",
                age:28,
                salay:1900
            });
            function updateLuckNumer(){
                setTimeout(() => {
                    luckNumber.value=77;
                    employee.salay=10000;
                }, 2000);
                 
            }
~~~
## 04.02 Vue3
- 在VS code中安装Vue扩展包才能看到{{ }}中的代码颜色
- Vue的插值表达式{{}}中可以直接写JS
~~~
//Math是对象
//Math.floor(数字); 向下取整
//Math.random();随机返回(0,1),0~1中的一个数字 不包括1
<body>
    <div id="vue3Demo">
    <h1>{{message}}</h1>
    <p>The luckNumber is {{luckNumber}}</p>
    <p>The luckNumber is {{luckNumber%2==0?"even luckNumber":"odd luckNumber"}}</p>
    <p>{{luckNumbers}}</p>
    <p>{{employee.name}} is {{employee.age}} years old!</p>
    <p>Random Number  from:1-10:{{Math.floor(Math.random()*10)}}</p>
    //取0到9再减去1=-1~8
    <p>{{Math.floor(Math.random()*10-1)}}</p>
    </div>
</body>
~~~
- 在插值表达式中使用方法
~~~
//message.toLowerCase();
//message.toUpperCase();
<p>Random Number  from:1-10:{{getLuckNumer()}}</p>

 function getLuckNumer(){
                return Math.floor(Math.random()*10+1);
            }
~~~
### ref
- 使用ref前需要从视图导入
- 对ref变量值进行更新，对变量的value属性进行赋值
  ~~~
  const {ref}=Vue;
   let luckNumber=ref(7);
     function getLuckNumer(){
                 luckNumber.value=Math.floor(Math.random()*10+1);
                return Math.floor(Math.random()*10+1);
            }
  ~~~

## 04.01 vue3
- node_modules 所有依赖文件的包
- index.html静态文件夹
- src/assets 资源
###  setup方法是应用开发中的主方法
- vue 脚本文件要写在script 尖括号中
	~~~
	<script src="https://unpkg.com/vue@3.5.31/dist/vue.global.js"></script>
	~~~
 


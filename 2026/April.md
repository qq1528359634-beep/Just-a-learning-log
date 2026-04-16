## 04.16 webApi-管道短路器
- 若context.Result已经有结果则直接返回结果
- 不经过Action也不经过Filter
~~~
 ObjectResult _result=null;
  public void OnResourceExecuted(ResourceExecutedContext context)
  {
      _result = context.Result as ObjectResult;
     context.HttpContext.Items.Clear();   
  }

  public void OnResourceExecuting(ResourceExecutingContext context)
  {
      if (_result != null)
      {
          context.Result=_result;
      }
      context.HttpContext.Items[GlobalValues.ItemKey]= "Cks";
  }
~~~

## 04.15 webApi-SourceFilter
- 前端传进来的数据，在与控制器绑定模型之前，只是2进制数据。绑定后才从混乱的原始数据变成了有序的业务对象。
### HttpContext 
- Controller构造函数执行完之后，才对HttpContext进行赋值
~~~
public class MyResourceFilter : Attribute, IResourceFilter
{
    public void OnResourceExecuted(ResourceExecutedContext context)
    {
           
    }

    public void OnResourceExecuting(ResourceExecutingContext context)
    {
      //这里的字符串区分大小写
        context.HttpContext.Items["Name"]= "Cks";
    }
}
~~~
- const 不能和static一起使用，因为const就是静态
### 请求周期
- 前端传入请求→OnResourceExecuting→controller构造函数→OnActionExecuting→Action→OnActionExecuted→OnResourceExecuted


## 04.14 webApi
### 过滤器获取context上下文信息
~~~
    public class MyActionFilterAttribute :Attribute,IActionFilter
    { 
        //在Action方法执行之后执行
        public void OnActionExecuted(ActionExecutedContext context)
        {
            var result=context.Result as ObjectResult;
            //想要拿到方法返回的结果，需要将Result转化成ObjectResult
            Console.WriteLine("Action方法执行之后"+ result.Value);
        }

        //在Action方法执行之前执行   
        public void OnActionExecuting(ActionExecutingContext context)
        {
            var argDic=context.ActionArguments;
            //方法传入参数中声明id，则可以在方法所在语句块中使用
            var isSuccess=argDic.TryGetValue("id", out object? id);
        
            Console.WriteLine($"Action方法执行前，请求的参数有{id}");
        }
    }
~~~

## 04.13 webApi 过滤器
- AOP面向切面编程
- Action Filter 过滤器
	- 过滤器应该与控制器平级
	- 要成为执行方法的过滤器，需要继承IActionFilter接口，并实现OnActionExecuted和OnActionExecuting 两个方法
- 特性Attribute（特性名称后面加Attribute）
	~~~
public class MyActionFilterAttribute :Attribute,IActionFilter
{ 
    //在Action方法执行之后执行
    public void OnActionExecuted(ActionExecutedContext context)
    {
        Console.WriteLine("Action方法执行之后");
    }

    //在Action方法执行之前执行   
    public void OnActionExecuting(ActionExecutingContext context)
    {
        Console.WriteLine("Action方法执行之前");
    }
}	
	~~~
- 常用特性
~~~
//追加此特性，表示该控制器为WebAPI控制器。开启自动验证模型，绑定推断等高级功能
[ApiController] 

//表示该方法接收的请求动词，该方法只允许Get请求
[HttpGet]

//定义方法的访问地址
[Route("api/[Controller]/[Action]")]

//自定义逻辑（检查监控）
[MyActionFilter]
~~~

## 04.10 webApi
- 用接口作为服务，类作为实现，提高代码可读性，符合依赖倒置
	降低耦合度,注册服务时使用接口而非具体类
~~~
//注册IProductServices，其实现为ProductServices (依赖倒置)
builder.Services.AddTransient<IProductServices,ProductServices>();

//服务和实现都为其本身
builder.Services.AddTransient<ProductServices>();
~~~
- 注册的不同方式
	- 泛型注册
		~~~
		builder.Services.AddTransient<IProductServices,ProductServices>();
		~~~
	- 类型注册
	~~~
	builder.Services.AddTransient(typeof(ITransientServices),typeof(TransientServices));
	~~~

## 04.09 webApi
### 依赖注入是实现控制反转的技术手段
- 不使用依赖注入时，需要在当前类中创建其他类的实例对象，使得当前类与其他类高度耦合
~~~
 [Route("api/[controller]")]
 [ApiController]
 public class ProductController : ControllerBase
 {
     ProductServices productServices = new ProductServices();
     [HttpGet]
     public string GetName(long id)
     {
       return  productServices.GetProductName(id);
     }
 }
~~~
- 依赖注入
~~~
//向DI容器中注册服务
//告诉系统，每当有地方需要 `ProductServices` 这个类时，请为它创建一个新的实例
builder.Services.AddTransient<ProductServices>();


[Route("api/[controller]")]
[ApiController]
public class ProductController : ControllerBase
{
    private readonly ProductServices _productServices;

    public ProductController(ProductServices productServices)
    {
        _productServices= productServices;
    }

    [HttpGet]
    public string GetName(long id)
    {
        return _productServices.GetProductName(id);
    }
}
~~~
- 依赖注入的三种生命周期
~~~
//瞬时生命周期   瞬态 只用一次就结束（每次都创建新的实例。使用后就销毁）
builder.Services.AddScoped<ScopedServices>();

//Addscoped 作用域生命周期
builder.Services.AddTransient<TransientServices>();

//AddSingleton 单例生命周期，只注册一次之后就使用这个单例
builder.Services.AddSingleton<SingletonServices>();
~~~
- 三种生命周期的使用场景
	无状态的服务使用Transient
	一次请求中，上一次调用服务与下一次调用服务有关联Scoped
	单例，不会被系统销毁，不同请求要有关联
- Singleton单例服务不好的点
	不同单例服务如果太多，会占用内存
	哪怕被调用的服务时瞬时服务，只要该服务中调用了单例服务，则该服务不会被回收

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
 


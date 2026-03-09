
## 03.09
## webAPi
native AOT 原生，编译时可以编译为本机代码（性能要求很高的类库，底层是C++）
**控制器与路由**
一个类继承于ControllerBase那么就具有了控制器的能力和行为

**如何在项目中调用访问其他api**

Program.cs 启动  
↓  
AddHttpClient("ShirtsApi") 注册配置  
↓  
DI容器保存配置  
↓  
某处请求 HttpClient  
↓  
httpClientFactory.CreateClient("ShirtsApi")  
↓  
框架创建 HttpClient  
↓  
执行 client => {...}  
↓  
返回配置好的 HttpClient

1.  配置
通过AddHttpClient向builder容器添加名为“ShirtsApi” 的HttpClient配置规则 ，
*返回IHttpClientBuilder（配置对象）类型可以用来进行链式调用，不过这里被忽略了*
```
//注册HttpClient服务，命名为ShirtApi，设置基础地址和默认请求头
builder.Services.AddHttpClient("ShirtsApi", client =>
{ 
    client.BaseAddress=new Uri("https://localhost:7025/api/");
    client.DefaultRequestHeaders.Add("Accept", "application/json");
});

```

2. 依赖注入-通过构造函数
```
private const string apiName = "ShirtsApi";
private readonly IHttpClientFactory httpClientFactory;

public WebApiExecuter(IHttpClientFactory httpClientFactory)
{   
    this.httpClientFactory = httpClientFactory;
}
```
3. 创建对应不同http动词的不同方法
~~~
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

# 03.07
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



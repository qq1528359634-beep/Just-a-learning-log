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


**Task.Wait(taskA,TaskB);**
- 1 返回值类型为void（同步方法），
- 2 同步等待，阻塞线程直到所有任务完成，
- 3 如果内部有异常会在wait all结束后抛出。（异常会被收集在AggregateException中）
<img width="300" height="400" alt="image" src="https://github.com/user-attachments/assets/640c1e92-de89-4aec-b391-7d18572480af" />

  


# 03.05
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

   
# 03.03
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

# 03.02
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



## 3.31 Vue3
### NPM方法创建项目
- npm install -g @vue/cli 往电脑里安装vue施工队
- vue create myproject --在npm前端中，不能使用大写命名项目，可以使用中划线或者下划线的方式命名
- npm run server
### vue ui创建项目
 - powershell 运行命令vue ui

### 使用vite创建项目 推荐使用这个
- npm create vite@latest
- npm install 安装依赖包
- npm run dev

## 3.30 Vue3
- 从外部引入脚本 ，或者直接引用脚本网址都可以
	~~~
	<script src="./vue3.global.js"></script>
	~~~
- 挂载渲染节点
- button标签中通过@来触发方法
- 要动态修改对象值，需要用ref和. value来修饰
~~~
<div id="indexPage">
    <!-- 插值表达式，将脚本中返回的message值，填入这个变量-->
    {{message}}
    <button @click="changeText">ChangeData</button>
  </div>
  <script>
    //从右边对象中找到名为createApp的属性并赋值给同名变量
    const {createApp,ref}=Vue;
   const app= createApp({
   //这里的setup与生命周期相关，在vue3中绝大多数逻辑代码
   //都写在setup中
      setup(){
        const message=ref("hello World!");
        const changeText=()=>{
          message.value="GoodBye World!";
        }
        return{
          message,
          changeText
        } 
      }
    })
    //挂载点选择器
    app.mount("#indexPage");
~~~
- node js的运行环境，npm插件安装管理库
- npm -v 查看当前npm版本
- node -v 查看当前node版本
- vue -v查看Vue CLI (Command Line Interface)版本


## 3.28 TS
### 常量
- const定义变量 本身不能赋值或者修改，但如果他是一个对象则内部的属性可以被修改
	~~~
	const userName="Cks";
const user={
    name:"Cks",
    age:18
}
user.name ="Ace";
user.age=19;
	~~~
### 解构与拓展
~~~
//解构与扩展
 let input=[1,2];
 let [first,second]=input;
 console.log(first);
 console.log(second);

 let input1=[1,2];
 function f([f,s]:[number,number]){
 console.log(f);
 console.log(s);
 }
 f(input1 as [number,number]);

let [f]=[1,2,3,4];
console.log(f);
let [one,...others]=[1,2,4,5];
console.log(one);
console.log(others);
~~~
### 对象解构 扩展
~~~
let object={
    a:"a",
    b:2,
    c:true
}
let {a,b}=object;
console.log(a);
console.log(b);
//扩散运算符
let {c,...d}=object;
console.log(b);
console.log(d);
~~~
### 接口
- TS中独有，JS没有，作用1.约束：继承接口就必须实现接口中的所有内容 2.对接 3.多态
- 前端中string不可以为null，但是后端中string可以为null
- 接口定义中变量名后加? 可以为undefined，而问号后面加 |null可以为空
- 只读属性 在前面追加readnoly   -readnoly场景在属性，而const作用与变量
	~~~
	interface  IUser{
    userName?:string,
    age:number|null
}
let user:IUser={
    age:null
}
function print(user:IUser){
   console.log(user.userName);
   console.log(user.age);
}
print(user);
	~~~
- ReadnolyArray 类型不能执行如何操作，包括赋值给另一个数组
~~~
let arr1:ReadonlyArray<number>=[1,2,3,4]
let arr2:number[]=arr1 as number[];
console.log(arr2);
~~~
### 口浮动属性与索引类型
- 接口中浮动属性，可以用于容错
~~~
interface IUserName{
    userName:string,
    age?:20,
    [propName:string]:any
}
function getUser(user:IUserName){
    console.log(user.ag);
    console.log(user.userName);  
}
let user:IUserName={
    userName:"Cks",
    ag:20
}
getUser(user);
~~~
- 接口索引类型
	~~~
	interface IStringArray{
    [index:number]:string
}
let strArray:IStringArray=["Cks","Tim","Ai"];
let str=strArray[0];
console.log(str);
	~~~
### 接口继承类
- 关键字extends 将类中的属性，方法保留声明部分 传给接口
	~~~
	class User{
    userName:string;
    /**
     *
     */
    constructor() {
       this.userName="Cks" 
    }
    addUser(name:string){
        this.userName=name;
    }
}

interface IUser extends User{
    age:number;
}

class Person implements IUser{
    age: number=10;
    userName: string="hello";
    addUser(name: string): void {
        throw new Error("Method not implemented.");
    }
}
	~~~
### TS类的继承
- 子类想要重写父类中的方法或者属性，必须使在构造函数中使用super（）
- TS在子类中重写父类方法 就是重写了父类方法
	~~~
	class Person {
    height;
    Weight;
    /**
     *
     */
    constructor() {
        this.Weight = 70;
        this.height = 186;
    }
    eat() {
        console.log("eat");
    }
}
class Student extends Person {
    /**
     *
     */
    constructor() {
        super();
        this.Weight = 100;
    }
    eat() {
        console.log("student eat");
    }
}
let student = new Student();
student.eat();
console.log(student.Weight);
	~~~
### TS中的访问级别
- public：公共类型 外部可以访问，子类也可以访问
- private：私有类型，内部可以访问，但外部或子类无法访问
- protected：保护类型，本类的内部可以访问，子类也可以访问
### 代理模式  C#中的get set
~~~
class User{
    private _weight:number;
    /**
     *
     */
    constructor() {
        this._weight=70;
    }
    get weight():number{
        return this._weight
    }
    set weight(value:number){
        this._weight=value;
    }
}
let user=new User();
console.log(user.weight);
user.weight=199;
console.log(user.weight);
~~~
### 静态类型
- 静态类型 static 保持不变 不被初始化
~~~
class User{
    static weight:number=60;

}
console.log(User.weight);
User.weight=100;
console.log(User.weight);
~~~
- 单例 实例
	~~~
	class UserAppService{
    userName:string="Cks";
   server(){
    console.log(this.userName+"接入服务");
    
   }
}

class UserAppServiceFactory{
    static userApp?:UserAppService;
    getUseAppService(){
    if(UserAppServiceFactory.userApp==null){
    UserAppServiceFactory.userApp=new UserAppService();
    } 
    return UserAppServiceFactory.userApp;
    }
}
class UserController{
    userFac:UserAppServiceFactory=new UserAppServiceFactory();
    server(){
        let userApp:UserAppService=this.userFac.getUseAppService();
        userApp.server();
    }
}
new UserController().server();
	~~~
### 抽象类
	抽象类
	只有抽象类能够有抽象方法
	一个类继承这个抽象类 则必须实现其抽象方法
### 泛型
- 泛型T 能够保持传入类型，能够点出原有属性 而any不可以
~~~
class User {
    userName = "Cks";
}
class Department {
    department = "department1";
}
function insert(model) {
    return model;
}
let res = insert(new Department);
console.log(res.department);
class DbHelper {
    insert(model) {
        return model;
    }
}
let dbHelper = new DbHelper();
let res1 = dbHelper.insert(new User);
console.log(res1.userName);
~~~
### 泛型约束
- T extends User
~~~
class DbHelper<T extends User>{
    insert<T>(model:T){
    return model;
    }
}

//用父类进行类型约束可以传入子类，并且保留子类特征
class DbHelper<T extends BaseModel >{
    insert(model:T){
    return model;
    }
}
let dbHelper=new DbHelper();
let res1=dbHelper.insert(new Department);
console.log(res1.id);
~~~

## 3.27 TypeScript
### Object
- 大写object和 小写object的区别
	大写object是类，他又成员对象和成员方法
	小写object是声明类型的关键字，二者都可以对变量进行声明但是用起来是不一样的
	~~~
	//大写Object和小写
	let o:Object="Hello";
	o=1;
	let o1:object={
	userName:"Cks"
	};
	~~~
### 类型断言 显示转化
- 和C#中的括号强制是一样的，唯一不同的就是用尖括号来代替圆括号。
	推荐使用as
~~~
// 类型断言 显示转化
let anyValue:any="HelloWorld!";
let str:number=(<string>anyValue).length;
str=(anyValue as string).length;
console.log(str);
~~~
### 声明变量
- var和let
	var声明的变量可以重复声明，var可以跨作用域声明在语句块内部也可以被从外部被访问


## 3.26 TypeScript
~~~
/数组
let arr1:number[]=[1,2,3,4,5];
let arr2:Array<number>=[1,2,3,4,5]
//元组 Tuple
//这以后只能前一个是字符串，后一个是数字
let dg:[string,number,string];
dg=["hello",10,"string"]; 
console.log(dg[0]);
console.log(dg[1]);
console.log(dg[2]);

//枚举类型
enum Color {Red,Green,Blue};
let c1:Color=Color.Green;
console.log(c1);
console.log(Color);

enum Color1{Red,Blue=100,yellow}
let c2:Color1=Color1.yellow;
console.log(c2);

//any=>dynamic
//少用any类型
let any:any="Hello";
any=1;
any=false;
any=100;
let num:number=any.toFixed();
console.log(num);

//object 
let objectOne:Object=9;
objectOne="Hello";
objectOne=false;
//object不能使用toFixed方法
//objectOne.toFixed();

let list:any=[1,"Cks",3,4,5];
console.log(list[1]);

//void
let voidValue:void=undefined;
let u:undefined=undefined;
let n:null=null;
~~~
## 3.25 TypeScript
- 确保已按照node.js 且设置系统允许运行脚本
~~~
//Windows PowerShell 允许当前系统运行脚本
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
//安装TS包
npm install -g typescript
//将TS文件转化JS文件
tsc .\test.ts
//运行js 脚本
node test.js
//创建tsconfig.js文件
tsc --init
//在tsc文件中设置“outDir”
 "outDir": "./js"
 //VScode 中运行任务-TS-监视
~~~
- TS中的几种基本类型
	- boolean
		~~~
		let isDone:boolean=false;
		console.log(isDone);
		~~~
	- number
	~~~
	//数字类型 number
	let n0:number=6;
	let n1:number=0xf00d;
	~~~
	- string
	~~~
	//字符串
	let name:string="Ace";
	name="Cks";
	let msg:string="hello"+name+"World";
	msg=`hello ${name} World!`;
	~~~

## 3.24 JS Csharp混讲
- JS中的every方法等价于C#中的All
	- All：当对象集合所有元素都符合判断条件则返回true
	~~~
	Console.WriteLine(striList.All(m => m != "ace"));
	~~~
	- JS：every
	~~~
	var allWrong=strList.every(m=>m!="ace");
	~~~
- JS中的includes方法等价于Csharp中的contains方法
	- contains
	~~~
	//contains如果包含某人就返回true，否则返回false
	Console.WriteLine(striList.Contains("Ace"));
	//如果字符串中包含指定字符就返回true，否则返回false
	string str = "hello world!";
	Console.WriteLine(str.Contains("world"));	
	~~~
	
- includes
	~~~
	var strList=["Taro","Zoffy","Man","Seven","Jack","Ace"];
	var allWrong=strList.every(m=>m!="ace");
	var bool=strList.includes("Ace");
	console.log(bool);
	var str="Hello World!";
	str.includes("Hello");
	console.log(str.includes("Hello"));
	~~~
- contact
	- JS
	~~~
	var list1=[1,2,3,4]
    var list2=[5,6,7,8]
    var list=list1.concat(list2);
	~~~
	- Csharp
	~~~
	 string[] striArr = { "A", "B" };
     string[] striArr2 = { "C", "D" };
	 string[] striArr3 = striArr.Concat(striArr2).ToArray();
	~~~
	- push unshift splice
	~~~
	//push从尾部添加 
	//unshift从头部添加
	list.push(9);
	list.unshift(0);
	//splice 既可以删除数据，也可以添加数据
	list.splice(0,1);
	list.splice(1,0,9);
	console.log(list);
	~~~
### JS中的拓展运算符
- ...  相当于C#中的params
	~~~
	//...表示扩展运算符
function add(array,...array2){
   let sum=0;
   for (let i = 0; i < array2.length; i++) {
    sum+=array2[i];
   }
   return sum;
}
var res=add(2,3,4,5);
console.log(res);
var [list1,...list2]=[1,2,3,4];
console.log(list1);
console.log(list2);
	~~~
### 字符串转换为 字符数组
- JS
~~~
var str="Hello World!";
var chars=[...str];
console.log(chars);
//三种匹配方式
document.querySelectorAll("div");
document.querySelectorAll(".my-class");
document.querySelectorAll("#myID");
~~~
- Csharp
~~~
string str = "hello world!";
str.ToCharArray();
~~~

## 3.23 JS Csharp混讲
- JS中的some方法等价于C#中any方法
- JS中的Filter方法  返回集合中所有符合条件的对象
~~~
//filter方法
us=strList.filter(m=>m=="Taro");
//手写filter方法
function myFilter(array,fun){
  let newArray=[];
  for (let index = 0; index < array.length; index++) {
       var item = array[index];
       var bool=fun(item);
       if(bool) newArray.push(item); 
  }
  return newArray;
}
~~~
- Csharp中的FindAll方法
~~~
var str= striList.FindAll(m=>m=="Ace");
//手写FindAll方法
static class Extension
{
    static public List<T> MyFindAll<T>(this List<T> list, Func<T, bool> func)
    {
        List<T> newList = new();
        foreach (var item in list)
        {
            if (func(item)) newList.Add(item);

        }
        return newList;
    }
}
~~~

## 3.21 JS操作标签样式
### 操作style属性
- style属性可以设置或放回样式
- style属性css特征值时，需要把特征的 短横线命名法改为驼峰命名法后使用
	- float时js的保留关键字，设置标签float属性时写cssFloat
	~~~
	<body>
    <p id="p1">Hello World!</p>
    <p id="p2">Hello World!</p>
    <input type="button" id="button1" value="change">
    <script>
        document.getElementById("button1").onclick=function(){
            // 通过js给标签赋予样式
            document.getElementById("p1").style.backgroundColor="green";
            document.getElementById("p1").style.color="blue";
            document.getElementById("p1").style.fontFamily="Arial";
            document.getElementById("p1").style.fontSize="20px";
            document.getElementById("p1").style.cssFloat="right";
            //通过js获取标签样式
            var backColor=document.getElementById("p1").style.color;
            console.log(backColor);
        }
    </script>
	~~~
### 操作className属性
- className 属性设置或返回元素的class属性
	- 获取属性值：HTMLElementObject.className
	- 设置属性值：HTMLElementObject.className=classname
	~~~
	 <script>
        document.getElementById("button1").onclick=function(){
	         document.getElementById("p1").className="ppp";
            alert(document.getElementById("p1").className);
        }
    </script>
	~~~
	- 获取标签对象
		~~~
		    //通过标签名获取标签对象集合
            var els=document.querySelectorAll("p");
            //通过class获取标签对象集合
            var els=document.querySelectorAll(".pp");
            //通过id获取标签对象集合
            var els=document.querySelectorAll("#pp");
		~~~
### BOM
- BOM 即Browser Object Model，用于控制浏览器行为，
- 操作BOM对象，一般使用window关键字调用
**常用方法**
- alert()：弹出提示对话框
- confirm（）:弹出确认对话框，返回bool值类型
~~~
  var result=confirm("您确定要关闭浏览器吗");
        if (result) {
            alert("关闭浏览器");
            window.close();
        } else {
            alert("保持浏览器开启")
        }
~~~
- prompt（）：弹出用户输入对话框，返回输入的内容，如果取消输入则返回null
~~~
var text=prompt("please input content！"); 
        alert(text);
~~~
- setInterval (code.milliseconds);计时器按照指定的周期来调用函数或者表达式
~~~ var i=0;
       var setIntervalId= setInterval(() => {
            console.log(++i);
        }, 1000);
        function clearTime(){
            clearInterval(setIntervalId);
        };
        document.getElementById("button1").onclick=clearTime;

~~~

## 3.20 JS集合
### 数组
#### 数组的定义 赋值
  ~~~
     <script>
        var array=new Array(1);
        array[0]=1;
        array[1]="Hello";
        console.log(array);

        var array1=[];
        array1[0]=1;
        array1[1]="Hello";
        console.log(array1);

        var array2=[1,"hello"];
        console.log(array2);
    </script>
  ~~~
#### 键值对
  ~~~
   <script>
        var kv={};
        console.log(kv);
        kv["a"]="A";
        kv["b"]="B";
        console.log(kv);
        kv.c="C";
        kv.d="D";
        console.log(kv);
        
        var kv2={a:"A"};
        console.log(kv2);

        var kv3;
        kv3=kv2;
        console.log(kv3);
    </Script>
  ~~~
#### 对象数组
  - JS对象和Json对象的区别
  ~~~
   var kv1={a:"A",b:"B"};//js对象

   var kv2={"aa":"AA","bb":"BB"};//Json格式对象
  ~~~
#### Array 对象属性
 - length 设置或返回数组中元素的数目
#### Array 对象方法
- contact（）连接2个或者更多数组并返回结果
- join（）把数组的所有元素放入一个字符串 。元素通过指定的分隔符进行分隔
- push（）向数组的末尾添加一个或更多元素，并返回新的长度
- reverse（）颠倒数组中的元素顺序
- sort（）对数组中的元素进行排序
- splice（）删除元素，并向数组添加元素
   splice 3个参数  第一个参数要删除的元素下标  第二个 要删除后面几个元素 第三个 要插入的内容
~~~
 <script>
        //splice 删除元素，并向数组添加元素
        //1.删除一个元素
        var ar1=[1,2,3,4]
        ar1.splice(1,1);
        console.log(ar1);
        //2.删除多个元素
        var ar2=[1,2,3,4]
        ar2.splice(1,2);
        console.log(ar2);
        //3.删除指定元素之后的所有元素
        var ar3=[1,2,3,4]
        ar3.splice(1);
        console.log(ar3);
        //4.添加元素  添加于下标之前
        var ar4=[1,2,3,4]
        ar4.splice(0,0,0)
        console.log(ar4);
        //5.替换元素（删了添加）
        var ar4=[1,2,3,4];
        ar4.splice(1,1,111);
        console.log(ar4);
    </script>
~~~
#### 类型转化
- parseInt  parseFloat
~~~
 <script>
        var str="9876.6";
        var num=parseInt(str);
        console.log(num);
        num=parseFloat(str);
        console.log(num);
        console.log(typeof(num));
    </script>
~~~
#### 方法使用
- 使用关键字function 定义方法
- 方法名使用驼峰法命名（lowerCamelCase）
- 方法可以设置参数及返回值
    - js是弱类型语言 方法参数无需指定变量类型
    - 方法返回值关键字return 后如果不跟返回内容，则简单理解为中断方法执行
    - js中不存在方法重载,"重载"会覆盖之前的方法
    - 从方法中获取参数还可以用argument 关键字 他是一个数组
~~~
<script>
        function add(a,b){
       if(a>1&&b>1) return a+b;
       return;
        };
        var c=add(2,3);
        console.log(c);
    </script>
~~~
#### 匿名方法
- 匿名方法  不需要写方法名的方法
- 匿名方法的2种写法
  - 在方法中调用
~~~
 <script>
    //匿名方法
  var fun = function(p1){
        alert(p1);
    };
   // fun("helloWorld");
    //使用匿名方法
    var ar1=[2,1,5,3,4]
    var sortFun=function(a,b){
        return b-a;
    }
    ar1.sort(sortFun);
    console.log(ar1);
 </script>
~~~
  - 直接调用匿名方法
~~~
//直接调用匿名方法
  (function (a,b){
   console.log(a+b);
  })(1,2);
 </script>
~~~
### 闭包
- 可以简单理解为子方法可以使用父方法中的变量（不建议使用闭包，变量不易释放）
### DOM
- DOM即Document Object Model
- DOM用于操作html文档，准确说是操作html标签内的内容
- JavaScript中将每一个标签 当作对象处理
- html中，每个标签都有自己的属性，如style id class等，也拥有触发事件，方法。同样在js中作为
    对象处理别的标签也拥有属性，事件，方法等成员。
- 操作DOM对象，一般使用document关键字调用
### js获取元素的方法
- document.getElementById(id); 根据id获取元素节点
-  document.getElementsByClassName(className); 根据class的值获取一组元素节点
-  document.getElementByName(name); 根据name获取一组元素节点
-  document.getElementByTagName(tag); 根据标签名获取一组元素节点
### 注册事件
- 事件注册常用的方式右很多种，此处先结束两种最常用的方法。一种为直接在元素上注册事件，另一种为在获取的对象上注册触发事件。
	- 元素注册法
	- 对象注册法-（对象注册法 实现了html与js的分离，更符合现在的编程思想 ）
	~~~
	<body>
    <input type="text" name="" id="txt1" value="阿猫">
      <script>
        var changeMe=function(){
            alert(event.target.value);
        }
        document.getElementById("txt1").onchange=changeMe;
    </script>
    </body>
	~~~
### 动态操作元素
- document.createElement();创建元素
    - document.createElement( );创建元素
    - document.appendchild( ); 添加子元素
    - document.insertBefore(newEl,orgEl)在某元素前添加元素
    - document.firstChild;获取第一个子元素
    - document.childNodes;获取所有子节点元素
    - document.removeChild();移除所有子节点元素
      脚本空白处也算节点
    ~~~
    <body>
    <ul id="ulist"><li>1</li><li>2</li><li>3</li></ul>
    <script>
        var list=document.getElementById("ulist");
       // list.removeChild(list.childNodes[0]);
        //list.removeChild(list.firstChild);
        list.removeChild(list.lastChild);
       var newTag=document.createElement("div");
       newTag.innerHTML="Hello World!";
       document.body.appendChild(newTag);
    </script>
  </body>
    ~~~
### 获取元素内容
- innerHTML
	- innerHTML用于获取与赋值拥有开闭标签的元素中完整内容
	  *innerHTML 可以获取到 指定开闭标签内的全部内容*
	- innerHTML赋值可以识别并添加HTML标签
- innerText
	- 只获取纯文字内容
	- 添加元素时无法识别标签，将标签视作纯文本
   
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



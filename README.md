# ES6

## 历史

1. ECMAScript和JavaScript
	- ECMA是标准，JS是实现
		- 类似于HTML5是标准，IE10、Chrome、FF都是实现
		- 换句话说，将来也能有其他XXXScript来实现ECMA
	- ECMAScript简称**ECMA或ES**
	- 目前版本
		- 低级浏览器主要支持ES 3.1
		- 高级浏览器正在从ES 5过渡到ES 6
2. 历史版本

|时间|ECMA|JS|解释|
|---|---|---|---|
|1996.11|ES 1.0|JS稳定|Netscape将JS提交给ECMA组织，ES正式出现|
|1998.06|ES 2.0||ES2正式发布|
|1999.12|ES 3.0||ES3被广泛支持|
|2007.10|ES 4.0||ES4过于激进，被废了|
|2008.07|ES 3.1||4.0退化为严重缩水版的3.1<br/>因为吵得太厉害，所以ES 3.1代号为Harmony(和谐)|
|2009.12|ES 5.0||ES 5.0正式发布<br/>同时公布了JavaScript.next也就是后来的ES 6.0|
|2011.06|ES 5.1||ES 5.1成为了ISO国际标准|
|2013.03|ES 6.0||ES 6.0草案定稿|
|2013.12|ES 6.0||ES 6.0草案发布|
|2015.06|ES 6.0||ES 6.0预计发布正式版<br/>JavaScript.next开始指向ES 7.0|

## 兼容性

http://kangax.github.io/compat-table/es5/
http://kangax.github.io/compat-table/es6/

### 解决兼容性
1. 在线转换

使用babel转化
```html
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<!--babel其实就是browser.js-->
        <script src="browser.js" charset="utf-8" ></script>
        <script type="text/babel">
            let a=12;
            let b=5;
            alert(a+b);
        </script>

	</head>
	<body>
		<input type="button" value="按钮1">
		<input type="button" value="按钮2">
		<input type="button" value="按钮3">
	</body>
</html>
```


2. 提前编译


##  变量

### 使用 var 存在的问题：
1. 没有块级作用域

由于作用域是相同的，所以最后赋值到每个按钮上的值都是相同的
```html
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script>
		// 点击按钮之后输出3
		window.onload=function(){
            var aBtn = document.getElementsByTagName('input');
            
            for(var i=0;i<aBtn.length;i++){
                aBtn[i].onclick=function(){
                    alert(i);
                };
            }
		};
		</script>
	</head>
	<body>
		<input type="button" value="按钮1">
		<input type="button" value="按钮2">
		<input type="button" value="按钮3">
	</body>
</html>
```

之前的解决方案：使用function来封闭作用域
```html
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script>
		window.onload=function(){
            var aBtn = document.getElementsByTagName('input');
            //使用function作为封闭作用域
            for(var i=0;i<aBtn.length;i++){
                (function(i){
                	aBtn[i].onclick=function(){
                    alert(i);
                	};
                })(i);
            }
		};
		</script>
	</head>
	<body>
		<input type="button" value="按钮1">
		<input type="button" value="按钮2">
		<input type="button" value="按钮3">
	</body>
</html>
```


2. 可以重复定义
3. 无法限制修改

### 使用let

1. 不能重复声明

```javascript
<script>
let a = 12;
let a = 12;//会报错，重复定义
</script>
```

2. 有块级作用域
```html
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script>
		window.onload=function(){
            var aBtn = document.getElementsByTagName('input');
            // 正常输出
            for(let i=0;i<aBtn.length;i++){
                aBtn[i].onclick=function(){
                    alert(i);
                };
            }
		};
		</script>
	</head>
	<body>
		<input type="button" value="按钮1">
		<input type="button" value="按钮2">
		<input type="button" value="按钮3">
	</body>
</html>
```

### 使用const

1. 不能赋值

```javascript
<script>
const a = 12;
a = 12;//会报错，不能对const变量赋值
</script>
```

2. 有块级作用域


## 函数

### 箭头函数

普通函数：
```javascript
function(){

}
```

箭头函数：
```javascript
()=>{

}
```

之前函数的写法：
```html
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script>
		let show=function(){
            alert('show')
		}
		
		show();
		</script>
	</head>
	<body>
	</body>
</html>
```

使用箭头函数之后的写法：
```html
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script>
		let show=()=>{
            alert('show')
		}
		
		show();
		</script>
	</head>
	<body>
	</body>
</html>
```

两个参数，一个返回值的情况：
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
    let arr=[12, 5, 8, 99, 33, 14, 26];
    /*arr.sort(function (n1, n2){
      return n1-n2;
    });*/

    arr.sort((n1, n2)=>{
      return n1-n2;
    });

    alert(arr);
    </script>
  </head>
  <body>

  </body>
</html>
```


1.如果只有一个参数，()可以省
2.如果只有一个return，{}可以省


### 参数

#### 剩余参数

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
		function show(a,b,...args){
			alert(a);
			alert(b);
			alert(args);
		}
		
		show(12,13,14,15,16);
	</script>
  </head>
  <body>

  </body>
</html>
```

#### 默认参数

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
		function show(a,b=3,c=4){
			alert(a);
			alert(b);
			alert(c);
		}
		
		show(12,13);
	</script>
  </head>
  <body>

  </body>
</html>
```

## 解构赋值
1. 左右两边结构必须一样（两边是数组都是数组，两边是json都是json）
2. 右边必须是一个东西
3. 声明和赋值不能分开


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
		let [a,b,c]=[1,2,3];
		alert(a);
		alert(b);
		alert(c);
		
		let {d,e,f}={d:123,e:"hello",f:true};
		alert(d);
		alert(e);
		alert(f);
		
		let [num,arr,str]=[12,[1,2,3],"hello world"];
		console.log(num,arr,str);
	</script>
  </head>
  <body>

  </body>
</html>
```


## 数组
> 主要是添加了若干种方法

### map 映射
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
		let arr = [1,2,3];
		let res = arr.map(function(item){
            alert(item);
            return item * 2;
		});
		alert(res);
		
		//使用箭头函数
		let res2 = arr.map(item=>item*3);
		alert(res2);
		
		//使用箭头函数
		let scores = [12,60,99]
		let res3 = scores.map(item=>item>=60?"及格":"不及格");
		alert(res3);
	</script>
  </head>
  <body>

  </body>
</html>
```

### reduce 汇总
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
		let arr = [1,2,3];
		//a: 临时结果
		//b: 每次处理的item
		//c: 下标，从1开始
		let res = arr.reduce(function(a,b,c){
           alert(a+" "+b+" "+c); 
           return a+b;
		});
		alert(res);
		
		
		let res1 = arr.reduce(function(temp,item,index){
           if(index!=arr.length-1){
               return temp + item;
           }else{
               return (temp+item)/arr.length;
           }
		});
		alert("平均值"+res1);
	</script>
  </head>
  <body>

  </body>
</html>
```

### filter 过滤器

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
		let arr = [
            {title:"男士衬衫",price:23},
            {title:"女士鞋",price:99},
            {title:"男士包",price:1},
            {title:"女士鞋",price:2223}
		];
		
		let res = arr.filter(json=>json.price>=50);
		
		alert(res);
        alert(res[0]["title"]);
		alert(res[0]["price"]);
	</script>
  </head>
  <body>

  </body>
</html>
```


### forEach 循环


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
		let arr = [1,2,3]
		
		arr.forEach(function(item，index){
            alert(item);
		});
	</script>
  </head>
  <body>

  </body>
</html>
```


## 字符串

### 多了两个方法:
startsWith(str) 判断一个字符串是不是以str开头
endsWith(str) 判断一个字符是不是以str结束

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
		let str="http://baidu.com";
		
		if(str.startsWith("http")){
            alert("普通网址");
		}else if(str.startsWith("https")){
            alert("加密网址");
		}else{
            alert("其他网站");
		}
	</script>
  </head>
  <body>

  </body>
</html>
```

### 字符串模板

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
		let title = "我的标题";
		let content = "我的内容";
		let str = `
			<title>${title}</title>
			<content>${content}</content>
		`;
		alert(str);
	</script>
  </head>
  <body>

  </body>
</html>
```


## 面向对象

### 之前面向对象的写法：
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
    	//问题1：类和构造函数不区分
		function User(name,pass){
            this.name = name;
            this.pass = pass;
		}
		
		//问题2：类分开了，把函数放在了后面
		User.prototype.showName=function(){
            alert(this.name);
		}
		
		User.prototype.showPass = function(){
            alert(this.pass);
		}
		
		var u1 = new User("john","zhangzhongjun");
		u1.showName();
		u1.showPass();
		
		function Student(name,pass,cla){
            User.call(this,name,pass);
            this.cla = cla;
		}
		//继承方法
		Student.prototype=new User();
		Student.prototype.constructor=Student;
		
		//新增的方法
		Student.prototype.showCla=function(){
            alert(this.cla);
		}
		
		var s = new Student("john","zhangzhongjun","3年2班");
		s.showName();
		s.showPass();
		s.showCla();
		
	</script>
  </head>
  <body>

  </body>
</html>
```

### ES6中的类

1. class关键字
2. 构造器和类分离
3. class中直接加方法


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script>
    	class User{
    		constructor(name,pass){
                this.name = name;
                this.pass = pass;
			}
		
            showName(){
                alert(this.name);
            }
		
            showPass(){
                alert(this.pass);
            }
 		}
		
		var u1 = new User("john","zhangzhongjun");
		u1.showName();
		u1.showPass();
		
		class Student extends User{
            constructor(name,pass,cla){
                super(name,pass);
                this.cla = cla;
            }
            
            showCla(){
                alert(this.cla);
            }
		}
		
		var s = new Student("john","zhangzhongjun","3年2班");
		s.showName();
		s.showPass();
		s.showCla();
		
	</script>
  </head>
  <body>

  </body>
</html>
```

### 一个面向对象的实例

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
        <script src="react.js" charset="utf-8" ></script>

        <script src="react-dom.js" charset="utf-8" ></script>		
		<!--react依赖于JSX -->
        <script src="browser.js" charset="utf-8" ></script>
       

        
        <script type="text/babel">
        
        	// 自定义组件
        	class MyItem extends React.Component{
                constructor(...args){
                    super(...args);
                }
                render(){
                    return <li>{this.props.str}</li>;
                }
        	}
        
			class MyList extends React.Component{
			  constructor(...args){
				super(...args);
			  }

			  render(){
				return <ul>
				  {this.props.arr.map(a=><MyItem str={a}></MyItem>)}
				</ul>;
			  }
			}

			window.onload=function (){
			  let oDiv=document.getElementById('div1');

			  ReactDOM.render(
				<MyList arr={['abc', 'erw', 'sdfasdf', 'dfasdfsdfds']}></MyList>,
				oDiv
			  );
			};
        </script>

	</head>
	<body>
		<div id="div1" >
		
		</div>
		
		
	</body>
</html>
```

## JSON对象

JSON的标准写法：
1. 只能用双引号
2. 所有的key必须用双引号包起来

JSON的简写:
1. 函数中的 冒号 和 function关键词 可以同时省略
2. 如果名字和值一样，则可以只写一个
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
        <script>
        	let str = "{\"name\":\"john\",\"age\":12}";
        	let json = JSON.parse(str);
        	console.log(json);
        	
			let j = {"name":"ads","age":1};
			console.log(JSON.stringify(j));
			
			let j2 = {
				//名字和值一样，只写一个
				str,
				"a":12,
				show(){
					alert(this.a);
				},
				add:function(b){
                    alert(this.a+b);
				},
				showStr(){
                    alert(this.str);
				}
			};
			j2.show();
			j2.add(12);
			j2.showStr();
        </script>

	</head>
	<body>
		<div id="div1" >
		
		</div>
	</body>
</html>
```


## generator

普通函数 中间不能停
generator 中间可以使用yield

可以有下面三种写法：
function * 函数名
function* 函数名
function *函数名

yield: 停止
next() 函数：向前推动一步

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
        <script>
			function * show(){
                alert(12);
                alert(14);
                yield;
                alert(13);
			}
			// 创建一个生成器对象
			let genObj=show();
			// 输出12 14
			genObj.next();
			// 输出13
			genObj.next();
        </script>

	</head>
	<body>
		<div id="div1" >
		
		</div>
	</body>
</html>
```

## yield

* 使用next传参：
1. 不能给第一个过程（函数开始到遇到第一个yield）传参。可以使用函数参数给第一个参数传参。
2. 第一个next方法是给第二个过程（第一个yield到第二个yield）传参
3. 第二个next方法是给第三个过程（第二个yield到第三个yield）传参

* 使用yield返回，使用next接收：
1. 第一个next接收到的是第一个过程的输出
2. 第二个next接收到的是第二个过程的输出
3. 最后一个过程的输出应该由return返回


```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
        <script>
			function * show(){
                alert(12);
                alert(14);
                let res = yield [1,2,3];
                alert(13);
                alert(res);
			}
			// 创建一个生成器对象
			let genObj=show();
			// 输出12 14
			let aa = genObj.next("a");
			// 输出13
			let bb = genObj.next("b");
			// 输出 {value: Array(3), done: false}
			alert(aa);
			console.log(aa);
			// 输出 {value: undefined, done: true}
			alert(bb);
			console.log(bb);
        </script>

	</head>
	<body>
		<div id="div1" >
		
		</div>
	</body>
</html>
```

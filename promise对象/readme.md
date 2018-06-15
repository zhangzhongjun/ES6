# Promise对象

> 同步的写法逻辑简单，写法简单，但是页面容易卡死；异步的写法写法复杂。而Promise的目的就是取同步和异步的优点
> 

本文的所有实验，因为涉及到了ajax，所以必须在服务器的环境中才能运行。本人在实验时使用的是TOMCAT。

## Promise对象的使用

resolve——成功了
reject——失败了

```javascript
    <script>
        // Promise对象
    let p=new Promise(function (resolve, reject){
      //异步代码
      //resolve——成功了
      //reject——失败了

      $.ajax({
        url: &#39;data/arr.txt&#39;,
        dataType: &#39;json&#39;,
        success(arr){
          resolve(arr);
        },
        error(err){
          reject(err);
        }
      })
    });

        // then: ajax结束之后执行
    p.then(function (arr){
      alert(&#39;成功&#39;+arr);
    }, function (err){
      console.log(err);
      alert(&#39;失败了&#39;+err);
    });
    
</script>
```

## 两个Promise对象

Promise.all 方法：表示全部的promise运行完成之后执行的

```javascript
    <script>
    let p1=new Promise(function (resolve, reject){
      $.ajax({
        url: &#39;data/arr.txt&#39;,
        dataType: &#39;json&#39;,
        success(arr){
          resolve(arr);
        },
        error(err){
          reject(err);
        }
      })
    });
    let p2=new Promise(function (resolve, reject){
      $.ajax({
        url: &#39;data/json.txt&#39;,
        dataType: &#39;json&#39;,
        success(arr){
          resolve(arr);
        },
        error(err){
          reject(err);
        }
      })
    });

        // 全部都成功
    Promise.all([
      p1, p2
    ]).then(function (arr){
      let [res1, res2]=arr;

      alert(&#39;全都成功了&#39;);
      alert(res1);
      alert(res2);
    }, function (){
      alert(&#39;至少有一个失败了&#39;);
    });
    
</script>
```

## jquery中使用Promise

jquery中已经帮助我们实现了Promise

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script src="jquery.js" charset="utf-8"></script>
    <script>
    Promise.all([
      $.ajax({url: 'data/arr.txt', dataType: 'json'}),
      $.ajax({url: 'data/json.txt', dataType: 'json'})
    ]).then(function (results){
      let [arr, json]=results;

      alert('成功了');
      console.log(arr, json);
    }, function (){
      alert('失败了');
    });
    </script>
  </head>
  <body>

  </body>
</html>

```
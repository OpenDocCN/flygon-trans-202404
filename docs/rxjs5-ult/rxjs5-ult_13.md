# 运算符和Ajax

# 运算符和Ajax

Rx对象上有一个`ajax`运算符。

## 使用`ajax()`运算符

index.html

```
<html>
    <body>
        <div id="result">

        </div>
        <script src="https://unpkg.com/@reactivex/rxjs@5.0.1/dist/global/Rx.js"></script>
        <script src="app.js"></script>
    </body>
</html> 
```

app.js

```
let person$ = Rx.Observable
  .ajax({
      url : 'http://swapi.co/api/people/1',
      crossDomain: true, 
      createXHR: function () {
        return new XMLHttpRequest();
     }
    })
  .map(e => e.response);

const subscription = person$
  .subscribe(res => {
      let element = document.getElementById('result');
      element.innerHTML = res.name
      console.log(res)
  }); 
```

从这里引发的一个小注意事项是我们如何调用`ajax()`运算符，我们显然指定了除了`url`属性之外的一堆东西。之所以这样做是因为`ajax`运算符执行以下操作：

> ajaxObservable中的XHR的默认工厂默认将withCredentials设置为true

所以我们在自定义工厂中提供了一个解决方案，并且它有效。我明白这是一个当前正在关注的问题。

## 使用fetch API

```
const fetchSubscription = Rx.Observable
.from(fetch('http://swapi.co/api/people/1'))
.flatMap((res) => Rx.Observable.from(res.json()) )
.subscribe((fetchRes) => {
    console.log('fetch sub', fetchRes);
}) 
```

这里发生了几件值得一提的事情

+   fetch api是基于promise的，但是使用`.from()` Rxjs允许我们将promise作为参数插入并将其转换为Observable。

+   但是返回的结果是一个响应对象，我们需要将其转换为Json。调用`json()`会为您完成此操作，但该操作会返回一个Promise。因此，我们需要使用另一个`from()`运算符。但在observable内部创建一个Observable会创建一个observable列表，而我们不希望如此，我们想要Json。所以我们使用一个称为`flatMap()`的运算符来解决这个问题。在[这里](operators-observable-in-an-observable.html)阅读更多关于`flatMap()`的内容。

最后，我们获得了我们期望的Json，没有CORS的问题，但是需要写更多的代码。

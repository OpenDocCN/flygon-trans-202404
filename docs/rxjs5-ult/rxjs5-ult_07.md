# 生产者

# 生产者

一个生产者的任务是产生Observable发出的值。

```
 class Producer {
    constructor(){
      this.i = 0;
    }

    nextValue(){
      return i++;
    }
 } 
```

而要使用它

```
 let stream$ = Rx.Observable.create( (observer) => {
       observer.next( Producer.nextValue() )
       observer.next( Producer.nextValue() )
    }) 
```

在[可观察对象解剖](observable-anatomy.html)章节中，示例中没有`Producer`，但大多数通过辅助方法创建的`Observables`都会有一个内部的`Producer`来产生观察者使用`observer.next`方法发出的值。

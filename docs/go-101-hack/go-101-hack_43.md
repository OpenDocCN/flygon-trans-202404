# 使用`sync.WaitGroup`来同步goroutines

# 使用`sync.WaitGroup`来同步goroutines

* * *

（本文是[在Golang中使用sync.WaitGroup](http://nanxiao.me/en/use-sync-waitgroup-in-golang/)的修改版）。

[sync.WaitGroup](https://golang.org/pkg/sync/#WaitGroup)提供了一个goroutine同步机制，用于等待一组goroutines完成。在`sync.WaitGroup`结构体内部，有一个`counter`记录着当前有多少个需要等待的goroutines。

`sync.WaitGroup`提供`3`个方法：`Add`、`Done`和`Wait`。`Add`方法用于标识需要等待多少个goroutines，并且会增加`counter`值。当一个goroutine退出时，必须调用`Done`，它会将`counter`值减少`1`。`main` goroutine在`Wait`上阻塞，一旦`counter`变为`0`，`Wait`将返回，主goroutine可以继续运行。

让我们看一个例子：

```
package main

import (
    "sync"
    "time"
    "fmt"
)

func sleepFun(sec time.Duration, wg *sync.WaitGroup) {
    defer wg.Done()
    time.Sleep(sec * time.Second)
    fmt.Println("goroutine exit")
}

func main() {
    var wg sync.WaitGroup

    wg.Add(2)
    go sleepFun(1, &wg)
    go sleepFun(3, &wg)
    wg.Wait()
    fmt.Println("Main goroutine exit")

} 
```

因为`main` goroutine需要等待`2`个goroutines，所以`wg.Add`的参数是`2`。执行结果如下：

```
goroutine exit
goroutine exit
Main goroutine exit 
```

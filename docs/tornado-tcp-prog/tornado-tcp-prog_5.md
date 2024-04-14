# 解读Tornado

# 解读Tornado

前几章主要是针对TCP编程中，tornado中常用的函数进行简单的解读。本章主要对tornado性能进行分析，来看一看我们到底为什么要在tornado的基础上进行tcp编程。

# epoll

## epoll

我们知道tornado通过非阻塞的方式以及对epoll的运用，才使得性能上得到了很大的提升。那么epoll到底是什么，它在tornado中扮演着怎样的角色呢？

1.epoll解读

说到epoll，就得先说说阻塞和非阻塞，这里大家自行百度或者脑补。 我们通常处理数据流可能是这样的

```
While true：
    for i in stream:
        if i has data:
            Do something with i 
```

这种方式显然很差劲，他会一直轮询，不管数据流中是否有IO事件。针对这种情况就出现了select， 它可以甄别数据流是否有IO，当无IO的时候，就阻塞在那里，直到下一次IO发生，在进行操作。

```
While true：
    select（stream）
    for i in stream：
        if i has data：
            Do something 
```

虽然我们不用白白的轮询，也知道了是否发生IO，，但却并不知道是那几个流（可能有一个，多个，甚至全部），我们只能无差别轮询所有流，找出能读出数据，或者写入数据的流，对他们进行操作。 因此epoll就诞生了，epoll全称就是event poll，和咱们平常用的轮询不同，基于事件的epoll会把哪个数据流发生了怎样的事件告诉我们。

```
while true 
    active_stream[] = epoll_wait(epollfd)
    for i in active_stream[]：
        read or write till unavailable 
```

# epoll的CPU和内存消耗

## 2.epoll的性能优势

#### 前面说了epoll的特点，那么这些特点能带来什么好处呢？Epoll 在绝大多数情况下性能都远超 select 或者 poll，但是除了速度之外，三者之间的 CPU 开销，内存消耗情况又怎么样呢？

##### 以下来自stackoverflow网友的问答翻译

##### 问:

##### 我读过所有的关于tornado的书告诉我在epoll是可以替代select和poll的，特别是对twisted(twsited是python的另一个十分有名的网络库)。查阅epoll以及其他的(select等)相关资料表明，epoll速度很快并且拓展性很强，这是否表明在CPU和内存消耗上，epoll仍然很强？

##### 答：

##### 在socket数量很少的时候，select在内存消耗以及运行效率上都超过epoll，当然，这个差距是非常小的，以至于在绝大多数环境下都可以忽略。但是，无论是选择select还是epoll，在不同场景下面临的api复杂度是不一样的。如果你选择了一个单一的fd，100，那么它的性能会高于两倍���上的fd，50.

##### Epoll的成本接近于fd(文件描述符)，如果你监控200个fd，其中只有100个有IO事件，那么你只需要支付这100个fd的消耗，而不用在乎另外的100个，这就是epoll提供的优势。相反，当你使用select的时候，如果1000个fd都处于空闲，你仍然要监控这1000个fd(简单的来讲，就是epoll只为有io的fd支付。你干活，我付钱给你；你不干活，那么我就不给你钱)。那么这就意味着更少的CPU使用率。

##### 关于内存使用率，简单来说，使用select的话，你要花384字节监视一个文件描述符，但它的价值是1024，而用epoll你只花20个字节。不过，所有这些数字都很小，所以没有太大的区别。

# tornado在TCP层里的工作

## tornado 在TCP里的工作

首先是关于 TCP 协议。这是一个面向连接的可靠交付的协议。由于是面向连接，所以在服务器端需要分配内存来记忆客户端连接，同样客户端也需要记录服务器。为了安全所以有了三次握手机制，这里给出一张图-- 状态转换图(UNIX网络编程)![](2013_12_06_01.png)

对于 TCP 编程的总结就是：创建一个监听 socket，然后把它绑定到端口和地址上并开始监听，然后不停 accept。这也是 tornado 的 TCPServer 要做的工作。

TCPServer 类的定义在 tcpserver.py。它有两种用法：bind+start 或者 listen。

简言之，基于事件驱动的服务器（tornado）要干的事就是：创建 socket，绑定到端口并 listen，然后注册事件和对应的回调，在回调里accept 新请求。

创建监听 socket 后为了异步，设置 socket 为非阻塞（这样由它 accept 派生的socket 也是非阻塞的），然后绑定并监听之。add_sockets 方法接收 socket 列表，对于列表中的 socket，用 fd 作键记录下来，并调用add_accept_handler 方法。它也是在 netutil 里定义的。

add_accept_handler 方法的流程：首先是确保ioloop对象。然后调用 add_handler 向 loloop 对象注册在fd上的read事件和回调函数accept_handler。该回调函数是现成定义的，属于IOLoop层次的回调，每当事件发生时就会调用。回调内容也就是accept得到新socket和客户端地址，然后调用callback向上层传递事件。从上面的分析可知，当read事件发生时，accept_handler被调用，进而callback=_handle_connection被调用。

# tornado TCPServer的设计解读

## TcpServer类的解读

##### 在TCPServer类的注释中，首先强调了它是一个non-blocking, single-threaded TCP Server.

那么如何理解non-blocking呢？ non-blocking，就是说，这个服务器没有使用阻塞式API。 通常来说，我们socket的读写都是阻塞式的,不管有没有数据，服务器都派API去读，读不到，API就不会回来交差。而非阻塞区别在于没有数据可读时，它不会在那死等，它直接就返回了。 而single-thread，说的是服务器是单线程模式，一个线程可以监视成千上万的连接，因此不需要多线程。在ubuntu上用的是epoll，bsd用的是kqueue。

在使用方面，tcpserver这个类一般不直接使用，而是派生出子类，然后让子类实例化。可以看到作者是强制去继承tcpserver，handle_stream并没有实现，如果你不去覆盖，就会报错。

```
def handle_stream(self, stream, address):

    """Override to handle a new `.IOStream` from an incoming connection."""

    raise NotImplementedError() 
```

# ioloop分析

## ioloop分析

###### 咱们先来简单说一下ioloop的源码

```
while True:
    poll_timeout = 3600.0

    # Prevent IO event starvation by delaying new callbacks
    # to the next iteration of the event loop.
    with self._callback_lock:
        ＃上次循环的回调列表
        callbacks = self._callbacks
        self._callbacks = []
    for callback in callbacks:
        ＃执行遗留回调
        self._run_callback(callback)

    if self._timeouts:
        now = self.time()
        while self._timeouts:
            ＃超时回调
            if self._timeouts[0].callback is None:
                # 最小堆维护超时事件
                heapq.heappop(self._timeouts)
            elif self._timeouts[0].deadline <= now:
                timeout = heapq.heappop(self._timeouts)
                self._run_callback(timeout.callback)
            else:
                seconds = self._timeouts[0].deadline - now
                poll_timeout = min(seconds, poll_timeout)
                break

    if self._callbacks:
        # If any callbacks or timeouts called add_callback,
        # we don't want to wait in poll() before we run them.
        poll_timeout = 0.0

    if not self._running:
        break

    if self._blocking_signal_threshold is not None:
        # clear alarm so it doesn't fire while poll is waiting for
        # events.
        signal.setitimer(signal.ITIMER_REAL, 0, 0)

    try:
        ＃这里的poll就是epoll，当有事件发生，就会返回，详情参照tornado里e＃poll的代码
        event_pairs = self._impl.poll(poll_timeout)
    except Exception as e:
        if (getattr(e, 'errno', None) == errno.EINTR or
            (isinstance(getattr(e, 'args', None), tuple) and
             len(e.args) == 2 and e.args[0] == errno.EINTR)):
            continue
        else:
            raise

    if self._blocking_signal_threshold is not None:
        signal.setitimer(signal.ITIMER_REAL,
                         self._blocking_signal_threshold, 0)

    ＃如果有事件发生，添加事件，
    self._events.update(event_pairs)
    while self._events:
        fd, events = self._events.popitem()
        try:
            ＃根据fd找到对应的回调函数，
            self._handlers[fd](fd, events)
        except (OSError, IOError) as e:
            if e.args[0] == errno.EPIPE:
                # Happens when the client closes the connection
                pass
            else:
                app_log.error("Exception in I/O handler for fd %s",
                              fd, exc_info=True)
        except Exception:
            app_log.error("Exception in I/O handler for fd %s",
                          fd, exc_info=True) 
```

##### 简单来说一下流程，首先执行上次循环的回调列表，然后调用epoll等待事件的发生，根据fd取出对应的回调函数，然后执行。IOLoop基本是个事件循环，因此它总是被其它模块所调用。

##### 咱们来看一下ioloop的start方法，start 方法中主要分三个部分：一个部分是对超时的相关处理；一部分是 epoll 事件通知阻塞、接收；一部分是对 epoll 返回I/O事件的处理。

1.超时的处理，是用一个最小堆来维护每个回调函数的超时时间，如果超时，取出对应的回调，如果没有则重新设置poll_timeout的值

2.通过 self._impl.poll(poll_timeout) 进行事件阻塞，当有事件通知或超时时 poll 返回特定的 event_pairs，这个上面也说过了。

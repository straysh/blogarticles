{
    "id": 68,
    "user_id": 1,
    "category_id": 1,
    "author": "straysh",
    "title": "laravel队列的使用(三)-beanstalk-driver",
    "slug": "php_laravel队列的使用(三)_beanstalk_driver",
    "hits": 130,
    "published_at": "1467795854",
    "created_at": 1467795854,
    "updated_at": 1504919705,
    "deleted_at": null
}
## Beanstalk驱动的队列示例
Beanstalk驱动示例分为两部分,第一部分介绍Beanstalk的安装和使用,第二部分介绍在Laravel中如何使用 `pda/pheanstalk api`

Beanstalkd的主要使用场景是,在模块间及使用队列消息的worker之间管理工作流.这和另外一个常用的方案RabbitMQ相似,但Beanstalkd被设计为一个独立的服务.

并不像其他的解决方案,Beanstalkd本质上被设计为一个工作队列,而不是解决各种需求的急救工具.为此,它是用C语言构建的轻量且高效的应用.而且,其精简的结构也使他安装方便,使用简单,非常的适合绝大部分的使用场景.

### 特点
* 持久化 - Beanstalkd队列运行在内存中但也提供了持久化存储.
* 优先级 - Beanstalkd能为队列作业设置优先级,以便在需要紧急处理时可以及时处理.
* 分布式 - 类似Memecached的分布式(注:实际上是client分布式).
* Burying - 调用->bury()接口可以永久挂起一个作业.
* 三方工具 - Beanstalkd有大量的第三方管理工具,包括CLI的和Web的.
* 过期时间 - 任务可以设置过期时间并自动入队(TTR - time To Run).

### Beanstalkd使用场景
* 允许web服务器快速响应,而不是被强迫当场处理长时请求(被阻塞的请求)
* 每隔一段时间执行任务(如网络爬虫)
* 将任务分发给多个客户处理
* 让离线用户可以在之后通过worker重新读取数据而不会丢失
* 为后端系统引入了完整的异步功能
* 顺序的/优先级的任务
* 在worker之间负载均衡
* 极大的提高了应用程序的可靠性和运行时间
* 将CPU密集型任务延后执行(如视频处理、图片处理)
* 群发邮件
* 等等

### Beanstalkd的基本概念
#### Tubes/Queues
Beanstalkd将其他消息系统中的Tube翻译为Queue.它们是job(或message)传输到消费者的途径
#### Jobs/Messages
Beanstalkd是一个工作队列,在管道(tube)中传输的就是job - 和被发送出去的message类似
#### Producers/Senders
生产者,类似高级消息队列规范所述,是制造并发送job(或message)(job/message被消费者使用)的应用程序.
#### Consumers/Receivers
接收者是另一个应用程序,他从tube中获取job(job是生产者制造的),

### 安装Beanstalkd
* `git clone https://github.com/kr/beanstalkd`
* `cd beanstalkd && cat README`
```bash
QUICK START
$ make
$ ./beanstalkd
also try,
$ ./beanstalkd -h
$ ./beanstalkd -VVV
$ make CFLAGS=-O2
$ make CC=clang
$ make check
$ make install
$ make install PREFIX=/usr
```

```bash
$beanstalkd -h
Use: beanstalkd [OPTIONS]
Options:
 -b DIR   write-ahead log directory
 -f MS    fsync at most once every MS milliseconds (use -f0 for "always fsync")
 -F       never fsync (default)
 -l ADDR  listen on address (default is 0.0.0.0)
 -p PORT  listen on port (default is 11300)
 -u USER  become user and group
 -z BYTES set the maximum job size in bytes (default is 65535)
 -s BYTES set the size of each write-ahead log file (default is 10485760)
            (will be rounded up to a multiple of 512 bytes)
 -c       compact the binlog (default)
 -n       do not compact the binlog
 -v       show version information
 -V       increase verbosity
 -h       show this help
 
#本地测试使用
beanstalkd -l 127.0.0.1 -p 11301 &
```

### Beanstalkd扩展支持的客户端/语言:
[https://github.com/kr/beanstalkd/wiki/client-libraries](https://github.com/kr/beanstalkd/wiki/client-libraries)
* C
* C/C++
* C++
* Chrome App
* Clojure
* Django
* Common Lisp
* Erlang
* Go
* Haskell
* Io
* Java
* Lua
* Nim
* Node.js
* OCaml
* Perl
* <span style="color:red;">PHP</span>
* Python
* Rails
* Ruby
* Ruby EventMachine
* Rust
* Scheme
* Scheme (Chicken)
* .NET/C#

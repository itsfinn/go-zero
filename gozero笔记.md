记录了一下每个目录大概包含哪些内容

go-zero

├── core

│  ├── bloom 基于redis bit map 做了一个boolm filter ，没地方用到

│  ├── breaker 客户端负载 google breaker 客户端节流机制（操作redis mongo mysql都用到了）

​              生成sdk没看到有

│  ├── cmdline 读取命令行输入的，不用看

│  ├── codec 加解密 rsa base64 解压缩 gzip

│  ├── collection 滑动窗口rollingwindow(sum cnt)（breaker ，load 的 adaptiveshedder 用了）

​              时间轮 timingwhell https://www.yuque.com/tal-tech/go-zero/iwimew

│  ├── conf 配置文件加载工具，支持了 json yaml proterties

│  ├── contextx

│  ├── discov 服务发现

│  │  ├── internal watch etcd

│  │  └── kubernetes

│  ├── errorx atomicerror MapReduce waitgroup errgroup

│  ├── executors 没地方用到

│  ├── filex 文件工具，没地方用到

│  ├── fs 没地方用到

│  ├── fx 并发 重试 超时 流（map reduce filter reverse sort count group; Just生成器）

│  ├── hash 一致性hash （数据缓存配多redis时用到）

│  ├── iox io相关

│  ├── jsontype 不用看

│  ├── jsonx json unmarshall

│  ├── lang 没东西 PlaceholderType struct{}

│  ├── limit 基于redis

​				periodlimit ：period 秒内允许发生quota次

​				Tokenlimit ：控制事件允许在一秒钟内发生的频率。

│  ├── load 服务端负载 adaptiveshedder 

​				5*50的 rollingwindow 内，根据 cpu负载

​				allow 拿到一个 promise，反馈fail/pass

│  ├── logx

│  ├── mapping

│  ├── mathx

│  ├── metric prometheus

│  ├── mr 并发用的 MapReduce 

https://github.com/tal-tech/zero-doc/blob/main/doc/mapreduce.md

│  ├── naming

│  ├── netx

│  ├── proc 环境变量，实现 dump profile gracefulStop 通过三个信号 SIGUSR1，SIGUSR2，SIGTERM

​					仅支持（+build linux darwin）

│  ├── prof

│  ├── prometheus

│  ├── queue 没地方用

│  ├── rescue 封了一下 Golang 的 recover

│  ├── search 二叉搜索树，web 路由用到

│  ├── service webService metrics Prometheus

│  ├── stat

│  │  └── internal cpuusage 仅支持linux

│  ├── stores

│  │  ├── cache 数据缓存按照primary key 增删改查，调 redis 模块具体命令

​              套了（dispatcher 一致性hash）

│  │  ├── clickhouse 空的，没支持

│  │  ├── kv 接口封装了 redis 常见命令，工具，没地方用到

​              套了（dispatcher 一致性hash）

│  │  ├── mongo 常见mongo操作

│  │  │  └── internal

│  │  ├── mongoc redis cache 结合了mongo

│  │  ├── postgres 空的，没支持

│  │  ├── redis redis 具体操作，用到了 breaker

│  │  │  └── redistest

│  │  ├── sqlc redis cache 结合了 sql

│  │  └── sqlx

│  ├── stringx Trie 字典树/前缀树 https://juejin.cn/post/6844903750490914829

​              内容安全用到

│  ├── syncx 太多了，看一下sharedcalls 防止缓存击穿之进程内共享调用

​           https://github.com/tal-tech/zero-doc/blob/main/doc/sharedcalls.md

│  ├── sysx

│  ├── threading 主要是一个 RunSafe函数， panic 的时候logx然后recover

│  ├── timex

│  ├── trace

│  │  └── tracespec

│  └── utils

├── doc

│  └── images

├── rest

│  ├── handler 一堆middleware，鉴权，breaker服务端负载，加密，压缩，日志，超时，链路追踪

│  ├── httpx http request response 工具

│  ├── internal

│  │  ├── context

│  │  └── security

│  ├── router

│  └── token 基于go-zero实现JWT认证

​					https://github.com/tal-tech/zero-doc/blob/main/doc/jwt.md

​					什么是JWT https://www.jianshu.com/p/576dbf44b2ae

└── zrpc

  └── internal

​    ├── auth

​    ├── balancer

​    │  └── p2c

​    ├── clientinterceptors

​    ├── codes

​    ├── mock

​    ├── resolver

​    └── serverinterceptors
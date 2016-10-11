# cooklive

直播服务
推流及播放对接七牛直播云服务，即时通讯采用融云。

技术实现主要采用Vert.x异步应用开发库框架，技术选型主要考虑服务端请求主要在点赞，发送消息以及即时通讯相关的请求（加入/离开聊天室，获取token等),属于I/O密集型业务，且对于直播的即时性要求信息的交互要保持低延时。而Vert.x是一个异步、可伸缩、并发应用的框架，最初的了解是在了解协程（纤程）是看到对它的介绍，旨在为JVM提供一个Node.js的替代方案。

其它技术选择包括Redis，旨在快速读取/存储直播中先关的数据信息，例如点赞数量，用户数量,用户信息等。MondgoDB主要用于存储用户发送的先关聊天信息，以json形式存储。选用MongoDB的主要原因是，对于一个文档数据库，每一个直播对应一个文档，而不会因数据量影响其它直播文档，且其索引类型和Mysql一样采用B-tree索引，这对回放时根据时间读取范围内的数据非常适用。

结构介绍：

主要划分为接口交互，即时通讯，直播数据服务，数据统计等模块。
根目录下CookLiveHttpServer 为接口入口，主要和客户端通讯。
CookLiveInitializer 服务启动后发布Vert.x服务。
im 包 ，内部对接融云,对外提供即时通讯先关服务。
live包，内部对接七牛，对外提供创建直播，结束直播等对应的直播流服务。
redis包，实现Vert.x提供的Redisclient异步接口，提供针对Redis集群下的存储服务。
robot包，这个是..不介绍了。
statistic包，直播数据统计服务。
utils包，工具类服务。




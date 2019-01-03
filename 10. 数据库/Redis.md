# redis

## redis 的概念

Redis 是一个速度极快的非关系数据库，也就是我们所说的 NoSQL 数据库(non-relational database)，它可以存储键(key)与 5 种不同类型的值(value)之间的映射(mapping)，可以将存储在内存的键值对数据持久化到硬盘，可以使用复制特性来扩展读性能，还可以使用客户端分片来扩展性能，并且它还提供了多种语言的 API。

| 名称      | 类型                                  | 数据存储选项                                                                               | 查询类型                                               | 附加功能                                            |
| --------- | ------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------ | --------------------------------------------------- |
| Redis     | 使用内存存储的非关系数据库            | 字符串、列表、集合、散列表、有序集合                                                       | 每种数据类型专属的命令，以及批量操作和不完全的事务支持 | 发布与订阅，主从复制，持久化，脚本                  |
| memcached | 使用内存存储的键值缓存                | 键值之间的映射                                                                             | 创建、读取、删除、更新等命令                           | 多线程服务器，用于提升性能                          |
| MySQL     | 关系数据库                            | 每个数据库可以包含多个表，每个表可以包含多个行；可以处理多个表的视图；支持空间和第三方扩展 | SELECT、INSERT、UPDATE、DELETE、函数、存储过程         | 支持 ACID 性质(需要使用 InnoDB)，主从复制，主主复制 |
| MongoDB   | 使用硬盘存储(on-disk)的非关系文档存储 | 每个数据库可以包含多个表，每个表可以包含多个无 schema 的 BSON 文档                         | 创建、读取、更新、删除、条件查询等命令                 | 支持 map-reduce 操作，主从复制，分片，空间索引      |

## redis 的安装(windows)

下载地址：[https://github.com/MicrosoftArchive/redis/releases](https://github.com/MicrosoftArchive/redis/releases)

## redis 的应用场景

缓存（数据查询、短连接、新闻内容、商品内容等等）。（最多使用） 分布式集群架构中的 session 分离。 聊天室的在线好友列表。 任务队列。（秒杀、抢购、12306 等等） 应用排行榜。 网站访问统计。 数据过期处理（可以精确到毫秒）

## redis 的用法

koa 的两个中间件
koa-generic-session 处理 session 的
koa-redis 连接 redis

```js

const Store = new Redis().client

router.get('/fix', async function(ctx) {
  const st = await Store.hset('fix', 'name', Math.random())
})
app.keys=['keys', 'keyskeys']
app.use(session{
  key: 'mt',
  prefix: 'mtpr',
  store: new Redis({

  })
})
```

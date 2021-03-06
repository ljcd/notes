> 参考：[Redis 教程 | 菜鸟教程](http://www.runoob.com/redis/redis-tutorial.html)  
[Redis命令中心 -- Redis中国用户组](http://redis.cn/commands.html)

# Ubuntu 下安装
`sudo apt install redis-server`

# 命令行登录 Redis

### 本地连接

- 无密码：`redis-cli`

- 有密码：`redis-cli -a 密码`

- 若登录有密码的 redis 服务器时没有提供密码，则后续操作需要通过 AUTH 命令进行密码验证：`127.0.0.1:6379> AUTH 密码`

### 远程连接

- `redis-cli -h host -p port -a password`

- `redis-cli -h 127.0.0.1 -p 6379 -a "mypass"`

# Redis 配置

> Redis 的配置文件位于 Redis 安装目录下，文件名为 redis.conf

`/etc/redis/redis.conf`

> 可以通过 CONFIG 命令查看或设置配置项  
> 也可以通过修改 redis.conf 文件修改配置项

### 查看配置

- `127.0.0.1:6379> CONFIG GET CONFIG_SETTING_NAME`

- `127.0.0.1:6379> CONFIG GET loglevel`

- 获取所有配置项：`127.0.0.1:6379> CONFIG GET *`

### 修改配置

- `127.0.0.1:6379> CONFIG SET CONFIG_SETTING_NAME NEW_CONFIG_VALUE`

- `127.0.0.1:6379> CONFIG SET loglevel "notice"`

# Redis keys 相关命令

- `KEYS pattern`  
  查找所有符合给定模式的 key
  
    例：`KEYS *`(查看所有的 key)

- `EXISTS key`  
  检查给定 key 是否存在

- `DEL key`  
  在 key 存在时删除 key

- `TYPE key`  
  返回 key 所储存的值的类型

- `EXPIRE key seconds`  
  为给定 key 设置过期时间

- `PERSIST key`  
  移除 key 的过期时间，key 将持久保持

- `TTL key`  
  以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)

- `RENAME key new_key`  
  修改 key 的名称

- `RENAMENX key new_key`  
  仅当 newkey 不存在时，将 key 改名为 newkey

# Redis 字符串类型相关命令

- `GET key`    
  获取指定 key 的值

- `SET key value`  
  设置指定 key 的值

- `GETRANGE key start end`  
  返回 key 中字符串值的子字符

- `GETSET key value`  
  将给定 key 的值设为 value ，并返回 key 的旧值

- `MGET key1 [key2..]`  
  获取所有(一个或多个)给定 key 的值

- `MSET key value [key value ...]`  
  同时设置一个或多个 key-value 对

- `SETEX key seconds value`  
  将值 value 关联到 key ，并将 key 的过期时间设为 seconds (以秒为单位)

- `SETNX key value`  
  只有在 key 不存在时设置 key 的值

- `MSETNX key value [key value ...]`  
  同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在

- `STRLEN key`  
  返回 key 所储存的字符串值的长度

- `INCR key`  
  将 key 中储存的数字值增一

- `DECR key`  
  将 key 中储存的数字值减一

- `INCRBY key increment`    
  将 key 所储存的值加上给定的增量值

- `DECRBY key decrement`  
  key 所储存的值减去给定的减量值

- `INCRBYFLOAT key increment`    
  将 key 所储存的值加上给定的浮点增量值

- `APPEND key value`  
  如果 key 已经存在并且是一个字符串， APPEND 命令将 value 追加到 key 原来的值的末尾

# Redis 字典(哈希)类型相关命令

- `HMSET key field1 value1 [field2 value2 ]`  
  同时将多个 field-value (域-值)对设置到哈希表 key 中
  
    例：`127.0.0.1:6379>  HMSET myinfo name "lijiac" address "Guangzhou" age 26`

- `HMGET key field1 [field2]`  
  获取所有给定字段的值

- `HGETALL key`  
  获取在哈希表中指定 key 的所有字段和值

- `HKEYS key`  
  获取所有哈希表中的字段

- `HVALS key`  
  获取哈希表中所有值

- `HSET key field value`  
  将哈希表 key 中的字段 field 的值设为 value

- `HGET key field`  
  获取存储在哈希表中指定字段的值

- `HLEN key`  
  获取哈希表中字段的数量

- `HEXISTS key field`   
  查看哈希表 key 中，指定的字段是否存在

- `HDEL key field2 [field2]`   
  删除一个或多个哈希表字段

- `HINCRBY key field increment`   
  为哈希表 key 中的指定字段的整数值加上增量 increment

- `HINCRBYFLOAT key field increment`  
  为哈希表 key 中的指定字段的浮点数值加上增量 increment

- `HSETNX key field value`   
  只有在字段 field 不存在时，设置哈希表字段的值

- `HSCAN key cursor [MATCH pattern] [COUNT count]`  
  迭代哈希表中的键值对

# Redis 列表类型相关命令

- `RPUSH key value1 [value2]`  
  在列表中添加一个或多个值

- `LPOP key`  
  移出并获取列表的第一个元素

- `LLEN key`  
  获取列表长度

- `LINDEX key index`  
  通过索引获取列表中的元素

- `LSET key index value`  
  通过索引设置列表元素的值

- `LINSERT key BEFORE|AFTER pivot value`  
  在列表的元素前或者后插入元素

- `LPUSH key value1 [value2]`  
  将一个或多个值插入到列表头部

- `LPUSHX key value`  
  将一个或多个值插入到已存在的列表头部

- `RPUSHX key value`  
  为已存在的列表添加值

- `RPOP key`  
  移除并获取列表最后一个元素

- `BLPOP key1 [key2 ] timeout`   
  移出并获取列表的第一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止

- `BRPOP key1 [key2 ] timeout`  
  移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止

- `RPOPLPUSH source destination`  
  移除列表的最后一个元素，并将该元素添加到另一个列表并返回

- `BRPOPLPUSH source destination timeout`  
  从列表中弹出一个值，将弹出的元素插入到另外一个列表中并返回它； 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止

- `LRANGE key start stop`  
  获取列表指定范围内的元素

-	`LTRIM key start stop`  
  对一个列表进行修剪(trim)，就是说，让列表只保留指定区间内的元素，不在指定区间之内的元素都将被删除。

- `LREM key count value`  
  从存于 key 的列表里移除前 count 次出现的值为 value 的元素

    - count > 0: 从头往尾移除值为 value 的元素。
    - count < 0: 从尾往头移除值为 value 的元素。
    - count = 0: 移除所有值为 value 的元素。

# Redis 集合类型相关命令

- `SADD key member1 [member2]`  
  向集合添加一个或多个成员

- `SREM key member1 [member2]`  
  移除集合中一个或多个成员

- `SPOP key`  
  移除并返回集合中的一个随机元素

- `SISMEMBER key member`  
  判断 member 元素是否是集合 key 的成员

- `SMEMBERS key`  
  返回集合中的所有成员

- `SCARD key`  
  获取集合的成员数

- `SINTER key1 [key2]`  
  返回给定所有集合的交集

- `SUNION key1 [key2]`  
  返回所有给定集合的并集

- `SDIFF key1 [key2]`  
  返回给定所有集合的差集

- `SINTERSTORE destination key1 [key2]`  
  返回给定所有集合的交集并存储在 destination 中

- `SUNIONSTORE destination key1 [key2]`  
  所有给定集合的并集存储在 destination 集合中

- `SDIFFSTORE destination key1 [key2]`  
  返回给定所有集合的差集并存储在 destination 中

- `SMOVE source destination member`  
  将 member 元素从 source 集合移动到 destination 集合

- `SRANDMEMBER key [count]`  
  返回集合中一个或多个随机元素

- `SSCAN key cursor [MATCH pattern] [COUNT count]`  
  迭代集合中的元素

# Redis 有序集合类型相关命令

- `ZADD key score1 member1 [score2 member2]`  
  向有序集合添加一个或多个成员，或者更新已存在成员的分数

- `ZSCORE key member`  
  返回有序集中，成员的分数值

- `ZRANK key member`  
  返回有序集合中指定成员的索引

- `ZCARD key`  
  获取有序集合的成员数

- `ZCOUNT key min max`  
  计算在有序集合中指定区间分数的成员数

- `ZLEXCOUNT key min max`  
  用于计算有序集合中指定成员之间的成员数量

- `ZINCRBY key increment member`  
  有序集合中对指定成员的分数加上增量 increment  

- `ZRANGE key start stop [WITHSCORES]`  
  通过索引区间返回有序集合中指定区间内的成员

- `ZRANGEBYLEX key min max [LIMIT offset count]`  
  通过字典区间返回有序集合的成员

- `ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT]`  
  通过分数返回有序集合指定区间内的成员

- `ZREM key member [member ...]`  
  移除有序集合中的一个或多个成员

- `ZREMRANGEBYLEX key min max`  
  移除有序集合中给定的字典区间的所有成员

- `ZREMRANGEBYRANK key start stop`  
  移除有序集合中给定的排名区间的所有成员

- `ZREMRANGEBYSCORE key min max`  
  移除有序集合中给定的分数区间的所有成员

- `ZREVRANGE key start stop [WITHSCORES]`  
  返回有序集中指定区间内的成员，通过索引，分数从高到底

- `ZREVRANGEBYSCORE key max min [WITHSCORES]`  
  返回有序集中指定分数区间内的成员，分数从高到低排序

- `ZREVRANK key member`  
  返回有序集合中指定成员的排名，有序集成员按分数值递减(从大到小)排序

- `ZINTERSTORE destination numkeys key [key ...]`  
  计算给定的 numkeys 个有序集合的交集，并且把结果放到 destination 中

- `ZUNIONSTORE destination numkeys key [key ...]`  
  计算给定的 numkeys 个有序集合的并集，并且把结果放到 destination 中

- `ZSCAN key cursor [MATCH pattern] [COUNT count]`  
  迭代有序集合中的元素（包括元素成员和元素分值）

# Redis 发布订阅命令

- `PUBLISH channel message`  
  将信息发送到指定的频道

- `SUBSCRIBE channel [channel ...]`  
  订阅给定的一个或多个频道的信息

- `UNSUBSCRIBE [channel [channel ...]]`  
  退订给定的频道

- `PSUBSCRIBE pattern [pattern ...]`  
  订阅一个或多个符合给定模式的频道

- `PUNSUBSCRIBE [pattern [pattern ...]]`  
  退订所有给定模式的频道

- `PUBSUB subcommand [argument [argument ...]]`  
  查看订阅与发布系统状态

- `PUBSUB CHANNELS [pattern]`  
  Lists the currently active channels

- `PUBSUB NUMSUB [channel-1 ... channel-N]`  
  Returns the number of subscribers (not counting clients subscribed to patterns) for the specified channels

- `PUBSUB NUMPAT`  
  Returns the number of subscriptions to patterns (that are performed using the PSUBSCRIBE command). Note that this is not just the count of clients subscribed to patterns but the total number of patterns all the clients are subscribed to

# Redis 查看／设置密码

- `127.0.0.1:6379> CONFIG get requirepass`

- `127.0.0.1:6379> CONFIG set requirepass "密码"`

redisDemo
=========

introduce something about redis jedis

##redis 简介
Redis 是完全开源免费的，遵守BSD协议，先进的key - value持久化产品。它通常被称为数据结构服务器，因为值（value）可以是 字符串(String), 哈希(Map), 列表(list), 集合(sets) 和 有序集合(sorted sets)等类型。 
##redis 下载安装
####下载wget  http://download.redis.io/releases/redis-2.8.13.tar.gz
假设当前下载到  /home/michael/soft 路径
####解压：tar -xvzf redis-2.8.13.tar.gz
####编译：  cd redis-2.8.13  <br/>make
####创建启动链接
sudo ln -s /home/michael/soft/redis-2.8.13/src/redis-server                      &nbsp;&nbsp;     /usr/bin/redis-server
sudo ln -s /home/michael/soft/redis-2.8.13/src/redis-cli&nbsp;&nbsp;/usr/bin/redis-cli
####启动
在命令行中输入  redis-server 即可启动redis 服务器端
新开一个控制台，输入redis-cli 即可启动 redis 客户端，如果不带任何参数，redis客户端可默认连接到本机上 6379默认端口上的服务端。如需连接到其他非默认服务器端，可以使用以下参数 
-h host -p point -a password   
详细说明，可以在命令行中输入 redis-cli --help获取。
详细帮助如下：
redis-cli 2.6.17

Usage: redis-cli [OPTIONS] [cmd [arg [arg ...]]]<br/>
  -h <hostname>     Server hostname (default: 127.0.0.1)<br/>
  -p <port>         Server port (default: 6379)<br/>
  -s <socket>       Server socket (overrides hostname and port)<br/>
  -a <password>     Password to use when connecting to the server<br/>
  -r <repeat>       Execute specified command N times<br/>
  -i <interval>     When -r is used, waits <interval> seconds per command.
                    It is possible to specify sub-second times like -i 0.1<br/>
  -n <db>           Database number<br/>
  -x                Read last argument from STDIN <br/>
  -d <delimiter>    Multi-bulk delimiter in for raw formatting (default: \n) <br/>
  -c                Enable cluster mode (follow -ASK and -MOVED redirections)<br/>
  --raw             Use raw formatting for replies (default when STDOUT is
                    not a tty)<br/>
  --latency         Enter a special mode continuously sampling latency<br/>
  --latency-history Like --latency but tracking latency changes over time.
                    Default time interval is 15 sec. Change it using -i.<br/>
  --slave           Simulate a slave showing commands received from the master<br/>
  --rdb <filename>  Transfer an RDB dump from remote server to local file.<br/>
  --pipe            Transfer raw Redis protocol from stdin to server<br/>
  --bigkeys         Sample Redis keys looking for big keys<br/>
  --eval <file>     Send an EVAL command using the Lua script at <file><br/>
  --help            Output this help and exit<br/>
  --version         Output version and exit<br/>

Examples:<br/>
  cat /etc/passwd | redis-cli -x set mypasswd<br/>
  redis-cli get mypasswd<br/>
  redis-cli -r 100 lpush mylist x<br/>
  redis-cli -r 100 -i 1 info | grep used_memory_human:<br/>
  redis-cli --eval myscript.lua key1 key2 , arg1 arg2 arg3<br/>
  (Note: when using --eval the comma separates KEYS[] from ARGV[] items)<br/>

When no command is given, redis-cli starts in interactive mode.<br/>
Type "help" in interactive mode for information on available commands.<br/>

在打开的客户端进行简单的测试：

info  
>查看系统信息

set hello "world"  
>存入一个 key 和 value均为 String 的记录
 
get hello 
> 获取一个key为 ‘hello’ 的string 记录

##redis常用配置
** 提示：redis的默认配置文件位于 **/redis/conf/redis.conf  如需修改前，请先备份当前配置文件
说明，如redis.conf.demo 所示

##常用的数据类型以及命令
### String
最简单也是最常用的一种存贮数据类型。其他类型的数据结构都是基于string类型发展而来的。
要点：字符串必须二进制安全，
常用命令：
http://www.redis.cn/commands.html#string
BITCOUNT key [start] [end]统计字符串指定起始位置的字节数<br/>
BITOP operation destkey key [key ...]Perform bitwise operations between strings<br/>
DECR key整数原子减1<br/>
DECRBY key decrement原子减指定的整数<br/>
GET key获取key的值<br/>
GETBIT key offset返回位的值存储在关键的字符串值的偏移量。<br/>
GETRANGE key start end获取存储在key上的值的一个子字符串<br/>
GETSET key value设置一个key的value，并获取设置前的值<br/>
INCR key执行原子加1操作<br/>
INCRBY key increment执行原子增加一个整数<br/>
INCRBYFLOAT key increment执行原子增加一个浮点数<br/>
MGET key [key ...]获得所有key的值<br/>
MSET key value [key value ...]设置多个key value<br/>
MSETNX key value [key value ...]设置多个key value,仅当key存在时<br/>
PSETEX key milliseconds valueSet the value and expiration in milliseconds of a key<br/>
SET key value设置一个key的value值<br/>
SETBIT key offset valueSets or clears the bit at offset in the string value stored at key<br/>
SETEX key seconds value设置key-value并设置过期时间（单位：秒）<br/>
SETNX key value设置的一个关键的价值，只有当该键不存在<br/>
SETRANGE key offset valueOverwrite part of a string at key starting at the specified offset<br/>
STRLEN key获取指定key值的长度<br/>
使用场景：
计数器应用
Redis的命令都是原子性的，你可以轻松地利用INCR，DECR命令来构建计数器系统。

### List
要点：
有序，其顺序为插入到到list的顺序，一个list的最大长度一个列表最多可以包含2的32次方-1个元素（4294967295，每个表超过40亿个元素）。
常用的命令：
http://www.redis.cn/commands.html#list
BLPOP key [key ...] timeout删除，并获得该列表中的第一元素，或阻塞，直到有一个可用<br/>
BRPOP key [key ...] timeout删除，并获得该列表中的最后一个元素，或阻塞，直到有一个可用<br/>
BRPOPLPUSH source destination timeout弹出一个列表的值，将它推到另一个列表，并返回它;或阻塞，直到有一个可用<br/>
LINDEX key index获取一个元素，通过其索引列表<br/>
LINSERT key BEFORE|AFTER pivot value在列表中的另一个元素之前或之后插入一个元素<br/>
LLEN key获得队列(List)的长度<br/>
LPOP key从队列的左边出队一个元素<br/>
LPUSH key value [value ...]从队列的左边入队一个或多个元素<br/>
LPUSHX key value当队列存在时，从队到左边入队一个元素<br/>
LRANGE key start stop从列表中获取指定返回的元素<br/>
LREM key count value从列表中删除元素<br/>
LSET key index value设置队列里面一个元素的值<br/>
LTRIM key start stop修剪到指定范围内的清单<br/>
RPOP key从队列的右边出队一个元素<br/>
RPOPLPUSH source destination删除列表中的最后一个元素，将其追加到另一个列表<br/>
使用场景：
可以用作消息队列（生产者和消费者），存取指定大小的内容。比如：网站主页的最新若干条的榜单，保存指定条数的日志等。
### Set
无序，不可重复，
最大长度：2的32次方-1个元素
常用的命令：
http://www.redis.cn/commands.html#set
SADD key member [member ...]添加一个或者多个元素到集合(set)里<br/>
SCARD key获取集合里面的元素数量<br/>
SDIFF key [key ...]获得队列不存在的元素<br/>
SDIFFSTORE destination key [key ...]获得队列不存在的元素，并存储在一个关键的结果集<br/>
SINTER key [key ...]获得两个集合的交集<br/>
SINTERSTORE destination key [key ...]获得两个集合的交集，并存储在一个关键的结果集<br/>
SISMEMBER key member确定一个给定的值是一个集合的成员<br/>
SMEMBERS key获取集合里面的所有key<br/>
SMOVE source destination member移动集合里面的一个key到另一个集合<br/>
SPOP key删除并获取一个集合里面的元素<br/>
SRANDMEMBER key [count]从集合里面随机获取一个key<br/>
SREM key member [member ...]从集合里删除一个或多个key<br/>
SSCAN key cursor [MATCH pattern] [COUNT count]迭代set里面的元素<br/>
SUNION key [key ...]添加多个set元素<br/>
SUNIONSTORE destination key [key ...]合并set元素，并将结果存入新的set里面<br/>

类似于数学中的
交集（SINTER，SINTERSTORE），并集(SUNION,SUNIONSTORE)，差集(SDIFF,SDIFFSTORE)  查找某个元素是否存在于 集合中

可以使用的场景：
大量的数据去重，判断是否首次访问等。
### Hashes
  以java为例，可以将一个bean中的各个字段同时保存为一个hash元素。类似mongo db。并且支持对单个字段（可以转换为数字）的加减等操作。适合作为缓存。
  关于hash的命令列表：
  HDEL key field [field ...]删除一个或多个哈希域<br/>
HEXISTS key field判断给定域是否存在于哈希集中<br/>
HGET key field读取哈希域的的值<br/>
HGETALL key从哈希集中读取全部的域和值<br/>
HINCRBY key field increment将哈希集中指定域的值增加给定的数字<br/>
HINCRBYFLOAT key field increment将哈希集中指定域的值增加给定的浮点数<br/>
HKEYS key获取hash的所有字段<br/>
HLEN key获取hash里所有字段的数量<br/>
HMGET key field [field ...]获取hash里面指定字段的值<br/>
HMSET key field value [field value ...]设置hash字段值<br/>
HSCAN key cursor [MATCH pattern] [COUNT count]迭代hash里面的元素<br/>
HSET key field value设置hash里面一个字段的值<br/>
HSETNX key field value设置hash的一个字段，只有当这个字段不存在时有效<br/>
HVALS key获得hash的所有值<br/>

使用场景：作为缓存的使用。可以实现多个系统中的单点登陆。

### SortSet
redis的高级功能。set，但是可以排序。sortSet中的排序依据首先根据每个元素对应的权值。如果权值相等，则以元素按照词典序进行排列。
相关命令：
ZADD key score member [score member ...]添加到有序set的一个或多个成员，或更新的分数，如果它已经存在<br/>
ZCARD key获取一个排序的集合中的成员数量<br/>
ZCOUNT key min max给定值范围内的成员数与分数排序<br/>
ZINCRBY key increment member增量的一名成员在排序设置的评分<br/>
ZINTERSTORE destination numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE<br/> SUM|MIN|MAX]相交多个排序集，导致排序的设置存储在一个新的关键<br/>
ZRANGE key start stop [WITHSCORES]返回的成员在排序设置的范围，由指数<br/><br/>
ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT offset count]返回的成员在排序设置的范围，由得分<br/>
ZRANK key member确定在排序集合成员的索引<br/>
ZREM key member [member ...]从排序的集合中删除一个或多个成员<br/>
ZREMRANGEBYRANK key start stop在排序设置的所有成员在给定的索引中删除<br/>
ZREMRANGEBYSCORE key min max删除一个排序的设置在给定的分数所有成员<br/>
ZREVRANGE key start stop [WITHSCORES]在排序的设置返回的成员范围，通过索引，下令从分数高到低<br/>
ZREVRANGEBYSCORE key max min [WITHSCORES] [LIMIT offset count]返回的成员在排序设置的范围，由得分，下令从分数高到低<br/>
ZREVRANK key member确定指数在排序集的成员，下令从分数高到低<br/>
ZSCAN key cursor [MATCH pattern] [COUNT count]迭代sorted sets里面的元素<br/>
ZSCORE key member获取成员在排序设置相关的比分<br/>
ZUNIONSTORE destination numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE<br/> SUM|MIN|MAX]添加多个排序集和导致排序的设置存储在一个新的关键<br/>
使用场景：
排行榜，带优先级的消息队列



## 其他功能
### 事务
支持多个操作的事务，提交回滚

### 订阅，发布
每个客户端可以订阅1个或者多个频道， 或者订阅模式  （类似于模糊匹配的模式）
但是当一个客户端在处于订阅模式时，无法进行其他操作

### 主从复制
可以使用多个服务器实现读写分离。使用单个主节点接收写入，使用若干个从节点接受读取操作请求。配置文件。

### 认证

## 持久化方式
### BDR
### AOF





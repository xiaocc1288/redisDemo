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
在配置文件中添加。。。也可以在sever运行的时候加入，如果想要实现待下次server启动的时候也可以实现认证，则必须在配置文件也修改相关的配置。

## 持久化方式


提供了多种不同级别的持久化方式:一种是RDB,另一种是AOF.

RDB 持久化可以在指定的时间间隔内生成数据集的时间点快照（point-in-time snapshot）。

AOF 持久化记录服务器执行的所有写操作命令，并在服务器启动时，通过重新执行这些命令来还原数据集。 AOF 文件中的命令全部以 Redis 协议的格式来保存，新命令会被追加到文件的末尾。 Redis 还可以在后台对 AOF 文件进行重写（rewrite），使得 AOF 文件的体积不会超出保存数据集状态所需的实际大小。Redis 还可以同时使用 AOF 持久化和 RDB 持久化。 在这种情况下， 当 Redis 重启时， 它会优先使用 AOF 文件来还原数据集， 因为 AOF 文件保存的数据集通常比 RDB 文件所保存的数据集更完整。你甚至可以关闭持久化功能，让数据只在服务器运行时存在。


了解 RDB 持久化和 AOF 持久化之间的异同是非常重要的， 以下几个小节将详细地介绍这这两种持久化功能， 并对它们的相同和不同之处进行说明。

RDB 的优点:
RDB 是一个非常紧凑（compact）的文件，它保存了 Redis 在某个时间点上的数据集。 这种文件非常适合用于进行备份： 比如说，你可以在最近的 24 小时内，每小时备份一次 RDB 文件，并且在每个月的每一天，也备份一个 RDB 文件。 这样的话，即使遇上问题，也可以随时将数据集还原到不同的版本。RDB 非常适用于灾难恢复（disaster recovery）：它只有一个文件，并且内容都非常紧凑，可以（在加密后）将它传送到别的数据中心，或者亚马逊 S3 中。RDB 可以最大化 Redis 的性能：父进程在保存 RDB 文件时唯一要做的就是 fork 出一个子进程，然后这个子进程就会处理接下来的所有保存工作，父进程无须执行任何磁盘 I/O 操作。RDB 在恢复大数据集时的速度比 AOF 的恢复速度要快。


RDB 的缺点:
如果你需要尽量避免在服务器故障时丢失数据，那么 RDB 不适合你。 虽然 Redis 允许你设置不同的保存点（save point）来控制保存 RDB 文件的频率， 但是， 因为RDB 文件需要保存整个数据集的状态， 所以它并不是一个轻松的操作。 因此你可能会至少 5 分钟才保存一次 RDB 文件。 在这种情况下， 一旦发生故障停机， 你就可能会丢失好几分钟的数据。每次保存 RDB 的时候，Redis 都要 fork() 出一个子进程，并由子进程来进行实际的持久化工作。 在数据集比较庞大时， fork() 可能会非常耗时，造成服务器在某某毫秒内停止处理客户端； 如果数据集非常巨大，并且 CPU 时间非常紧张的话，那么这种停止时间甚至可能会长达整整一秒。 虽然 AOF 重写也需要进行 fork() ，但无论 AOF 重写的执行间隔有多长，数据的耐久性都不会有任何损失。


AOF 的优点:
使用 AOF 持久化会让 Redis 变得非常耐久（much more durable）：你可以设置不同的 fsync 策略，比如无 fsync ，每秒钟一次 fsync ，或者每次执行写入命令时 fsync 。 AOF 的默认策略为每秒钟 fsync 一次，在这种配置下，Redis 仍然可以保持良好的性能，并且就算发生故障停机，也最多只会丢失一秒钟的数据（ fsync 会在后台线程执行，所以主线程可以继续努力地处理命令请求）。AOF 文件是一个只进行追加操作的日志文件（append only log）， 因此对 AOF 文件的写入不需要进行 seek ， 即使日志因为某些原因而包含了未写入完整的命令（比如写入时磁盘已满，写入中途停机，等等）， redis-check-aof 工具也可以轻易地修复这种问题。
Redis 可以在 AOF 文件体积变得过大时，自动地在后台对 AOF 进行重写： 重写后的新 AOF 文件包含了恢复当前数据集所需的最小命令集合。 整个重写操作是绝对安全的，因为 Redis 在创建新 AOF 文件的过程中，会继续将命令追加到现有的 AOF 文件里面，即使重写过程中发生停机，现有的 AOF 文件也不会丢失。 而一旦新 AOF 文件创建完毕，Redis 就会从旧 AOF 文件切换到新 AOF 文件，并开始对新 AOF 文件进行追加操作。AOF 文件有序地保存了对数据库执行的所有写入操作， 这些写入操作以 Redis 协议的格式保存， 因此 AOF 文件的内容非常容易被人读懂， 对文件进行分析（parse）也很轻松。 导出（export） AOF 文件也非常简单： 举个例子， 如果你不小心执行了 FLUSHALL 命令， 但只要 AOF 文件未被重写， 那么只要停止服务器， 移除 AOF 文件末尾的 FLUSHALL 命令， 并重启 Redis ， 就可以将数据集恢复到 FLUSHALL 执行之前的状态。


AOF 的缺点:
对于相同的数据集来说，AOF 文件的体积通常要大于 RDB 文件的体积。根据所使用的 fsync 策略，AOF 的速度可能会慢于 RDB 。 在一般情况下， 每秒 fsync 的性能依然非常高， 而关闭 fsync 可以让 AOF 的速度和 RDB 一样快， 即使在高负荷之下也是如此。 不过在处理巨大的写入载入时，RDB 可以提供更有保证的最大延迟时间（latency）。AOF 在过去曾经发生过这样的 bug ： 因为个别命令的原因，导致 AOF 文件在重新载入时，无法将数据集恢复成保存时的原样。 （举个例子，阻塞命令 BRPOPLPUSH 就曾经引起过这样的 bug 。） 测试套件里为这种情况添加了测试： 它们会自动生成随机的、复杂的数据集， 并通过重新载入这些数据来确保一切正常。 虽然这种 bug 在 AOF 文件中并不常见， 但是对比来说， RDB 几乎是不可能出现这种 bug 的。

RDB 和 AOF ,我应该用哪一个？
一般来说,如果想达到足以媲美 PostgreSQL 的数据安全性， 你应该同时使用两种持久化功能。如果你非常关心你的数据,但仍然可以承受数分钟以内的数据丢失， 那么你可以只使用 RDB 持久化。有很多用户都只使用 AOF 持久化， 但我们并不推荐这种方式： 因为定时生成 RDB 快照（snapshot）非常便于进行数据库备份， 并且 RDB 恢复数据集的速度也要比 AOF 恢复的速度要快， 除此之外， 使用 RDB 还可以避免之前提到的 AOF 程序的 bug 。因为以上提到的种种原因， 未来我们可能会将 AOF 和 RDB 整合成单个持久化模型。 （这是一个长期计划。）

RDB 快照:
在默认情况下， Redis 将数据库快照保存在名字为 dump.rdb 的二进制文件中。你可以对 Redis 进行设置， 让它在“ N 秒内数据集至少有 M 个改动”这一条件被满足时， 自动保存一次数据集。你也可以通过调用 SAVE 或者 BGSAVE ， 手动让 Redis 进行数据集保存操作。比如说， 以下设置会让 Redis 在满足“ 60 秒内有至少有 1000 个键被改动”这一条件时， 自动保存一次数据集：
save 60 1000
这种持久化方式被称为快照（snapshot）。

快照的运作方式:
当 Redis 需要保存 dump.rdb 文件时， 服务器执行以下操作：
Redis 调用 fork() ，同时拥有父进程和子进程。
子进程将数据集写入到一个临时 RDB 文件中。
当子进程完成对新 RDB 文件的写入时，Redis 用新 RDB 文件替换原来的 RDB 文件，并删除旧的 RDB 文件。
这种工作方式使得 Redis 可以从写时复制（copy-on-write）机制中获益。
只进行追加操作的文件（append-only file，AOF）
快照功能并不是非常耐久（durable）： 如果 Redis 因为某些原因而造成故障停机， 那么服务器将丢失最近写入、且仍未保存到快照中的那些数据。尽管对于某些程序来说， 数据的耐久性并不是最重要的考虑因素， 但是对于那些追求完全耐久能力（full durability）的程序来说， 快照功能就不太适用了。
从 1.1 版本开始， Redis 增加了一种完全耐久的持久化方式： AOF 持久化。
你可以通过修改配置文件来打开 AOF 功能：
appendonly yes
从现在开始， 每当 Redis 执行一个改变数据集的命令时（比如 SET）， 这个命令就会被追加到 AOF 文件的末尾。
这样的话， 当 Redis 重新启时， 程序就可以通过重新执行 AOF 文件中的命令来达到重建数据集的目的。

AOF 重写:
因为 AOF 的运作方式是不断地将命令追加到文件的末尾， 所以随着写入命令的不断增加， AOF 文件的体积也会变得越来越大。举个例子， 如果你对一个计数器调用了 100 次 INCR ， 那么仅仅是为了保存这个计数器的当前值， AOF 文件就需要使用 100 条记录（entry）。然而在实际上， 只使用一条 SET 命令已经足以保存计数器的当前值了， 其余 99 条记录实际上都是多余的。为了处理这种情况， Redis 支持一种有趣的特性： 可以在不打断服务客户端的情况下， 对 AOF 文件进行重建（rebuild）。执行 BGREWRITEAOF 命令， Redis 将生成一个新的 AOF 文件， 这个文件包含重建当前数据集所需的最少命令。

AOF 有多耐久？
你可以配置 Redis 多久才将数据 fsync 到磁盘一次。
有三个选项：
每次有新命令追加到 AOF 文件时就执行一次 fsync ：非常慢，也非常安全。
每秒 fsync 一次：足够快（和使用 RDB 持久化差不多），并且在故障时只会丢失 1 秒钟的数据。
从不 fsync ：将数据交给操作系统来处理。更快，也更不安全的选择。
推荐（并且也是默认）的措施为每秒 fsync 一次， 这种 fsync 策略可以兼顾速度和安全性。
总是 fsync 的策略在实际使用中非常慢， 即使在 Redis 2.0 对相关的程序进行了改进之后仍是如此 —— 频繁调用 fsync 注定了这种策略不可能快得起来。

如果 AOF 文件出错了，怎么办？
服务器可能在程序正在对 AOF 文件进行写入时停机， 如果停机造成了 AOF 文件出错（corrupt）， 那么 Redis 在重启时会拒绝载入这个 AOF 文件， 从而确保数据的一致性不会被破坏。


当发生这种情况时， 可以用以下方法来修复出错的 AOF 文件：
为现有的 AOF 文件创建一个备份。
使用 Redis 附带的 redis-check-aof 程序，对原来的 AOF 文件进行修复。
$ redis-check-aof --fix
（可选）使用 diff -u 对比修复后的 AOF 文件和原始 AOF 文件的备份，查看两个文件之间的不同之处。
重启 Redis 服务器，等待服务器载入修复后的 AOF 文件，并进行数据恢复。
AOF 的运作方式
AOF 重写和 RDB 创建快照一样，都巧妙地利用了写时复制机制。

以下是 AOF 重写的执行步骤:
Redis 执行 fork() ，现在同时拥有父进程和子进程。
子进程开始将新 AOF 文件的内容写入到临时文件。对于所有新执行的写入命令，父进程一边将它们累积到一个内存缓存中，一边将这些改动追加到现有 AOF 文件的末尾： 这样即使在重写的中途发生停机，现有的 AOF 文件也还是安全的。当子进程完成重写工作时，它给父进程发送一个信号，父进程在接收到信号之后，将内存缓存中的所有数据追加到新 AOF 文件的末尾。现在 Redis 原子地用新文件替换旧文件，之后所有命令都会直接追加到新 AOF 文件的末尾。

为最新的 dump.rdb 文件创建一个备份。
将备份放到一个安全的地方。
执行以下两条命令：
redis-cli> CONFIG SET appendonly yes
redis-cli> CONFIG SET save ""
确保命令执行之后，数据库的键的数量没有改变。
确保写命令会被正确地追加到 AOF 文件的末尾。
步骤 3 执行的第一条命令开启了 AOF 功能： Redis 会阻塞直到初始 AOF 文件创建完成为止， 之后 Redis 会继续处理命令请求， 并开始将写入命令追加到 AOF 文件末尾。
步骤 3 执行的第二条命令用于关闭 RDB 功能。 这一步是可选的， 如果你愿意的话， 也可以同时使用 RDB 和 AOF 这两种持久化功能。
别忘了在 redis.conf 中打开 AOF 功能！ 否则的话， 服务器重启之后， 之前通过 CONFIG SET 设置的配置就会被遗忘， 程序会按原来的配置来启动服务器。

RDB 和 AOF 之间的相互作用:
在版本号大于等于 2.4 的 Redis 中， BGSAVE 执行的过程中， 不可以执行 BGREWRITEAOF 。 反过来说， 在 BGREWRITEAOF 执行的过程中， 也不可以执行 BGSAVE 。
这可以防止两个 Redis 后台进程同时对磁盘进行大量的 I/O 操作。
如果 BGSAVE 正在执行， 并且用户显示地调用 BGREWRITEAOF 命令， 那么服务器将向用户回复一个 OK 状态， 并告知用户， BGREWRITEAOF 已经被预定执行： 一旦 BGSAVE 执行完毕， BGREWRITEAOF 就会正式开始。当 Redis 启动时， 如果 RDB 持久化和 AOF 持久化都被打开了， 那么程序会优先使用 AOF 文件来恢复数据集， 因为 AOF 文件所保存的数据通常是最完整的。

备份 Redis 数据:
Redis 对于数据备份是非常友好的， 因为你可以在服务器运行的时候对 RDB 文件进行复制： RDB 文件一旦被创建， 就不会进行任何修改。 当服务器要创建一个新的 RDB 文件时， 它先将文件的内容保存在一个临时文件里面， 当临时文件写入完毕时， 程序才使用  原子地用临时文件替换原来的 RDB 文件。这也就是说， 无论何时， 复制 RDB 文件都是绝对安全的。








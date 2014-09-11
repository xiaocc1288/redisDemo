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
BITCOUNT key [start] [end]统计字符串指定起始位置的字节数
BITOP operation destkey key [key ...]Perform bitwise operations between strings
DECR key整数原子减1
DECRBY key decrement原子减指定的整数
GET key获取key的值
GETBIT key offset返回位的值存储在关键的字符串值的偏移量。
GETRANGE key start end获取存储在key上的值的一个子字符串
GETSET key value设置一个key的value，并获取设置前的值
INCR key执行原子加1操作
INCRBY key increment执行原子增加一个整数
INCRBYFLOAT key increment执行原子增加一个浮点数
MGET key [key ...]获得所有key的值
MSET key value [key value ...]设置多个key value
MSETNX key value [key value ...]设置多个key value,仅当key存在时
PSETEX key milliseconds valueSet the value and expiration in milliseconds of a key
SET key value设置一个key的value值
SETBIT key offset valueSets or clears the bit at offset in the string value stored at key
SETEX key seconds value设置key-value并设置过期时间（单位：秒）
SETNX key value设置的一个关键的价值，只有当该键不存在
SETRANGE key offset valueOverwrite part of a string at key starting at the specified offset
STRLEN key获取指定key值的长度
使用场景：
计数器应用
Redis的命令都是原子性的，你可以轻松地利用INCR，DECR命令来构建计数器系统。

### List
要点：
有序，其顺序为插入到到list的顺序，一个list的最大长度一个列表最多可以包含2的32次方-1个元素（4294967295，每个表超过40亿个元素）。
常用的命令：
http://www.redis.cn/commands.html#list
BLPOP key [key ...] timeout删除，并获得该列表中的第一元素，或阻塞，直到有一个可用
BRPOP key [key ...] timeout删除，并获得该列表中的最后一个元素，或阻塞，直到有一个可用
BRPOPLPUSH source destination timeout弹出一个列表的值，将它推到另一个列表，并返回它;或阻塞，直到有一个可用
LINDEX key index获取一个元素，通过其索引列表
LINSERT key BEFORE|AFTER pivot value在列表中的另一个元素之前或之后插入一个元素
LLEN key获得队列(List)的长度
LPOP key从队列的左边出队一个元素
LPUSH key value [value ...]从队列的左边入队一个或多个元素
LPUSHX key value当队列存在时，从队到左边入队一个元素
LRANGE key start stop从列表中获取指定返回的元素
LREM key count value从列表中删除元素
LSET key index value设置队列里面一个元素的值
LTRIM key start stop修剪到指定范围内的清单
RPOP key从队列的右边出队一个元素
RPOPLPUSH source destination删除列表中的最后一个元素，将其追加到另一个列表
使用场景：
可以用作队列，存取指定大小的内容。比如：网站主页的最新若干条的榜单，保存指定条数的日志等。
### Set
无序，不可重复，
最大长度：2的32次方-1个元素
常用的命令：
http://www.redis.cn/commands.html#set
SADD key member [member ...]添加一个或者多个元素到集合(set)里
SCARD key获取集合里面的元素数量
SDIFF key [key ...]获得队列不存在的元素
SDIFFSTORE destination key [key ...]获得队列不存在的元素，并存储在一个关键的结果集
SINTER key [key ...]获得两个集合的交集
SINTERSTORE destination key [key ...]获得两个集合的交集，并存储在一个关键的结果集
SISMEMBER key member确定一个给定的值是一个集合的成员
SMEMBERS key获取集合里面的所有key
SMOVE source destination member移动集合里面的一个key到另一个集合
SPOP key删除并获取一个集合里面的元素
SRANDMEMBER key [count]从集合里面随机获取一个key
SREM key member [member ...]从集合里删除一个或多个key
SSCAN key cursor [MATCH pattern] [COUNT count]迭代set里面的元素
SUNION key [key ...]添加多个set元素
SUNIONSTORE destination key [key ...]合并set元素，并将结果存入新的set里面

类似于数学中的
交集（SINTER，SINTERSTORE），并集(SUNION,SUNIONSTORE)，差集(SDIFF,SDIFFSTORE)  查找某个元素是否存在于 集合中
### Hashes
### SortSet




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




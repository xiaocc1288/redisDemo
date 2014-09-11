redisDemo
=========

introduce something about redis jedis

##redis 简介
Redis 是完全开源免费的，遵守BSD协议，先进的key - value持久化产品。它通常被称为数据结构服务器，因为值（value）可以是 字符串(String), 哈希(Map), 列表(list), 集合(sets) 和 有序集合(sorted sets)等类型。 
##redis 下载安装
wget  http://download.redis.io/releases/redis-2.8.13.tar.gz
假设当前下载到  /home/michael/soft 路径

解压：tar -xvzf redis-2.8.13.tar.gz编译：  cd redis-2.8.13
  make

创建启动链接
sudo ln -s /home/michael/soft/redis-2.8.13/src/redis-server /usr/bin/redis-server
sudo ln -s /home/michael/soft/redis-2.8.13/src/redis-cli /usr/bin/redis-cli

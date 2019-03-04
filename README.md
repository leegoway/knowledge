# 必备知识

## PHP

### 数据类型  

#### 布尔
bool  值有true和false，所有的零值都和false相等（使用==）。判断符号“===”还会区别类型。
#### 字符串
string
#### 整数
int
#### 浮点数
float double 
#### 数组
array []
#### 对象
stdobject
#### 其他
mixed resource null closure 等

### 数组函数 字符串函数 日期类函数

#### 字符串函数
strlen, strpos, substr, explode, implode, mb_strlen, mb_strpos, mb_substr, strstr, strrchr, strtolower, strtoupper, trim
#### 数组函数
count, in_array, array_keys, array_values, array_diff, array_merge, array_push, array_pop, array_shift, array_unshift, array_map, array_filter
#### 日期类函数
date(), strtotime

### 进制转换
二进制是bin，八进制是oct，十进制是dec，十六进制是hex。通用方法base_convert()
### Cookie&Session共享
### PHP-FPM
### PHP配置常用
### 循环引用
### 性能测试

## Mysql
### 数据类型
- enum 枚举
- 整数
> tinyint 1个字节整数  smallint 2个字节证书 mediumint 3个字节整数 int 4字节整数 bigint 8字节整数

- 字符串
> varchar与char 变长与定长，注意长度是指字符的长度，一个汉字是一个字符，一个英文字母也是一个字符，一个数字也是一个字符，并不是字节数。varchar需要单独的一个字节存储结束符。

- 时间类型
> timestamp datetime date time 。 timestamp是时间戳类型，占4个字节，跟时区有关的，存储时内部存的都是0时区的值。datetime占8个字节，最大值‘9999-99-99 99:99:99’（值已经不合法）。

- 二进制
> binary的好处是不存在大小写以及字符编码的问题，对比的时候按照字节对比。

- 文本
> text是文本类型，用于存储内容较多的字段。

### 引擎
- myisam
> 不支持事务；不支持外键；支持表极锁；全文搜索；B+树存储；主键和辅助索引结构相同；表结构frm，数据MYD，索引MYI存储。
- ndb
- innodb
> 支持事务；行级锁；支持外键；共享表空间；优化的B+树存储；聚簇索引；OLTP，全文搜索。

### 进程
Mysql是单进程多线程的软件。线程包括：主线程、Log线程、Insert Buff线程、4个IO读线程、4个IO写线程、错误监控线程、锁监控线程等。

### 内存
Mysql内存占用主要分3块，主缓冲区、日志缓冲区和其他缓冲区。主缓冲区包括数据区、索引区、insert buffer、自适应hash区、锁信息区等

### 文件
- 配置文件、日志文件、PID文件、Sock文件、重做日志文件、表定义相关文件、表数据相关文件。

- 其中Innodb存储引擎的表共享空间文件，存储了数据、索引、重做日志、事务等信息，通过Innodb_data_file_path设置存储位置，通过Innodb_file_per_table设置是否每个表一个共享空间文件。开启Innodb_file_per_table，每个表的数据、索引和插入缓存信息存入各自的表文件，其他还是存入共享的表空间文件。

- 表共享空间文件，在物理存储结构上分为段、区、页和记录组成。页是磁盘上物理存储的最小单位，一个页文件大小为16KB，一个区包含64个页，也就是1MB。

### 规范
- 数据类型占用空间要小
- NOT NULL DEFAULT
- 只查询需要的字段
- 根据查询SQL建立索引
- 最左联合索引原则

### 索引
- B+树结构
- 主键索引&辅助索引
- 在选择项多的列上加索引
- 索引的类型（主键、辅助、联合索引、空间索引等）
- 高性能索引
  1. 多列的联合索引要注意顺序
  2. 多使用覆盖索引
  3. 最左前缀原则
  4. 选择高选择的列
  5. 排序的字段也可以考虑添加索引


### 事务
- ACID
- MVCC 非锁定读的版本号机制，提升查询性能

### 隔离级别
- 隔离级别有读未提交、读已提交、可重复读，串行执行4个隔离级别。隔离是解决并行执行的时候数据竞争的方法。读未提交会导致脏读，所以有了读已提交，但读已提交会出现不可重复读，所以有了可重复读，但会出现幻读，于是乎串行执行是最严格的模式。

### 性能优化
- explain
- slow_log
  slow_query_log=on, long_query_times=10s;来设置慢日志。慢日志分析工具是mysqldumpslow，传递参数筛选日志（mysqldumpslow -s t -t 10 logfile）。

### 锁
- 锁类型
>  innodb提供行级共享锁与排他锁，意向共享锁和意向排它锁。意向锁是在表上建立的，对表级的操作有影响。
>  myisam提供表级锁 
- 一致性的非锁定读
- 锁算法
> Gap Lock
> Record Lock
> Next Key Lock

### 新特性
- Json
- Geo

### 主从同步
1. 开启binlog，同时设置server_id;
2. grant replication slave on db.table to 'username'@'host' identified by 'password';
3. change master to master_host='', master_user='', master_password='', master_log_file='', master_log_pos=''
4. start slave
5. show slave status 会看到slave_io和slave_sql线程正在running方可

### 读写分离
- 这个是应用层来实现的，读写分离要注意的是主从同步延迟，通过show slave status有个字段slave_balabala_seconds显示延迟时间。
- Yii配置

### 分库分区表
- 分区range\list\hash\key
- 分库的时机，分表的时机

### 中间件
- Mycat
- Kingshard
- Atlas

### 分布式事务
- XA

## Redis 

### 基础数据结构
- 动态字符串sdshdr

- 链表 linkedlist和listnode

- 字典表 dict dictht dictentry

- 整数集合 intset

- 压缩列表 ziplist

- 跳跃表 skiplist


### RedisObject
- 内部有type encoding ptr lru refcount 等字段。

### RedisServer/Db
- RedisServer内部有dbnum, redisdb\*，saveparams, 等
- RedisDb内部有 dict\*， expires\*等

### LRU
- 过期键的判定就是扫描expires的dict，找到相对lru比较小的，进行过期删除。redis使用了惰性删除和定期删除。访问的时候，先判断是否过期；定期serverCron的时候删除过期的键。

### 存储rdb/aos
- rdb是二进制方式存储数据，首先记录redis的版本等信息，接着是db的信息，接着是redisDb结构体里的dict内数据。
- AOF是日志方式存储数据，会记录redis的命令历史；重写AOF文件时是遍历redisDb的dict结构体，为数据生成命令并保存到aof文件中。
- 启用并存在AOF，优先从AOF启动redis，否则从rdb启动。
- SAVE命令会阻塞请求，BGSAVE会fork进程来处理保存数据，同时采用COW技术。

### 复制SYNC
- slave of host port；SYNC\PSYNC\PSYNC2
- PSYNC在2.8版本启用，PSYNC2在4.0版本启用。 
- PSYNC主要用来解决网络抖动时，主从重新同步的问题，主redis增加了同步队列replication_backlog，从增加了master的ID和偏移量。
- PSYNC2是在集群的背景下解决主从切换时，其他从redis从新主redis重新同步数据的问题，从存储了当前master的ID和前一个master的ID以及偏移量。

### 集群
- 16384个slot

### 缓存更新顺序

### Redis应用场景
- 缓存（一致性hash）
- 排行榜（zset）
- bitmap
- GEO
- 布隆过滤
- 队列（延迟队列:Job状态，消费队列，推拉）
- 分布式锁

## HTTP权威指南

### URL
< schema>//:user:pass@host:port/path?querystring#fragement
url_encode

### 报文
#### 起始行
- 请求方法  路径 
- HTTP版本  响应code 响应短语

#### 首部
> 通用首部
Connection Date 

> 请求首部
Accept Accept-encoding Accept-language
Host Referer Authorization Cookie
if-modified-since   Cache-Control Pragma

> 响应首部
Content-Type Content-Length Date Server
Set-Cookie Location
ETag Expires Last-Modified

#### 主体
根据content-type的不同，可以传不同类型的参数，常用的有application/json, application/x-www-form-url-encoded, multipart/form-data, text/plain等

### 请求方法与返回码
#### 请求方法
GET POST DELETE PUT PATCH OPTIONS HEAD
#### 返回码
200  201 ； 301  302  304； 400  401  404 ； 500  502  504 

### TCP/IP
- TCP 20字节报文
- IP 20字节报文
- 三次握手、四次挥手、慢启动 

### 缓存
> if-modified-since last_modified HTTP_CODE = 304
> cache-control: max-age  相对时间长度
> expires: 日期   过期的绝对日期时间
> 优先级：cache-control > expire > etag > if-modified-since

### HTTPS
- TLS SSL
- 证书

## Thrift
- 分层: Transport, Protocol, Processor, Service
- thrift文件编写
- Go使用thrift
- PHP使用thrift

## 队列
### Kafka

### RabbitMQ
#### 类型
- basic consume
- multi clients
- fanout
- direct
- topic
#### 插件
- shovel
#### 集群
- 集群
- 持久化
- 

### 延迟队列
### 普通队列

## 设计模式
### 模式原则
1. 单一职责
2. 里式替换
3. 迪米特法则
4. 依赖倒置
5. 接口隔离
6. 开闭原则

### 模式列表  
1. 简单工厂模式
2. 单例模式
3. 模板方法
4. 策略模式
5. 职责链模式
6. 装饰者模式
7. 观察者模式
8. 状态模式
9. 命令模式
10. 代理模式
11. 适配器模式
12. 组合模式
13. 迭代器模式
14. 门面模式

## Nginx
### 常见配置
### 负载均衡

## 微服务
  
### 注册与发现
### 降级
### 限流
### 服务描述文件
### 缓存

## 场景

## 大数据
### ES
### DRUID
### TiDB
### 超出内存的求出现次数最多的n条记录？

## 数据结构与算法
### 二叉平衡树
- 前序遍历、中序遍历、后序遍历
- 遍历算法
### B+树
### Trie前缀树
### Raft算法
### 动态规划

## VueJS


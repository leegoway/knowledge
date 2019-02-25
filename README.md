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
### 进程
Mysql是单进程多线程的软件。线程包括：主线程、Log线程、Insert Buff线程、4个IO读线程、4个IO写线程、错误监控线程、锁监控线程等。
### 文件
> 配置文件、日志文件、PID文件、Sock文件、重做日志文件、表定义相关文件、表数据相关文件。

> 其中Innodb存储引擎的表共享空间文件，存储了数据、索引、重做日志、事务等信息，通过Innodb_data_file_path设置存储位置，通过Innodb_file_per_table设置是否每个表一个共享空间文件。开启Innodb_file_per_table，每个表的数据、索引和插入缓存信息存入各自的表文件，其他还是存入共享的表空间文件。

> 表共享空间文件，在物理存储结构上分为段、区、页和记录组成。页是磁盘上物理存储的最小单位，一个页文件大小为16KB，一个区包含64个页，也就是1MB。

### 规范
- 数据类型占用空间要小
- NOT NULL DEFAULT
- 只查询需要的字段
- 根据查询SQL建立索引
- 最左联合索引原则

### 隔离&锁


### 分库分区表
### 中间件
### 内存
### 引擎
### 性能优化
### 锁算法
### 读写分离
### 新特性
### 数据类型
### 事务
### 索引
### 分布式事务

## Redis 

### 基础数据结构
### RedisObject
### RedisServer/Db
### LUR
### SYNC/PSYNC/PSYNC2
### 存储rdb/aos
### 集群
### 缓存更新顺序

## HTTP

### URL
### 报文
### TCP/IP

## THRIFT

## 队列
### Kafka
### RabbitMQ
### 延迟队列
### 普通队列

## 设计模式
### 模式原则
### 模式列表  

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

## 数据结构与算法

关于TendisPlus

## 	TendisPlus简介

## 	基本功能

​			本文详细介绍 Tendis 具备的基本功能。

​			数据类型

​						string(字符串)：set，get，getall

​						hash(哈希)：hset ，hget，hgetall

​						list(列表)：lpush，rpush

​						set(集合)：sadd，scard，sdiff，spop

​						zset(sorted set:有序集合)：zadd，zcard，zcount，zrank

​			正常服务

​						连接上节点，执行ping，输出pong即为正常

​			配 置

​						CONFIG GET * 获取所有的配置

​						CONFIG SET M N 将M中设置成N

​			备份与恢复

​						SAVE    该命令将在 redis 安装目录中创建dump.rdb文件。

​						CONFIG GET dir  恢复数据

​						BGSAVE

​			集群及槽位的操作

​						cluster addslots 添加槽位

​						cluster delslots	删除槽位

​						cluster info  集群信息

​						cluster meet 添加进集群

​						cluster forget  踢出集群						



## 	性能测试报告

## 	与Redis的兼容性

## 	使用限制

# 快速上手

## 	快速上手指南

​		本文介绍如何快速上手体验 tendis部署集群。有以下2 种体验方式供用户选择。		 		 		

​			<span id='first'>第一种：使用tendisplus-2.0.2-rocksdb-v5.13.4.tgz包部署单机测试环境</span>		

​			<span id='second'>第二种：使用tendisplus-2.0.2-rocksdb-v5.13.4.tgz包联机部署真实生产环境</span>



​		**[第一种：使用tendisplus-2.0.2-rocksdb-v5.13.4.tgz包部署单机测试环境](#first)**

​				适用场景：利用本地 Mac 或者单机 Linux 环境快速部署 Tendis 集群

​				耗时：5分钟

​	   最基础的 Tendis 测试集群通常有3个redis主节点，3个redis从节点来构成。

​			1. 下载tendisplus-2.0.2-rocksdb-v5.13.4.tgz包并解压，进入该目录

​				tar  -zxvf  tendisplus-2.0.2-rocksdb-v5.13.4.tgz

​				![1602298714420](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602298714420.png)

​			![1602298757851](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602298757851.png)

​			2. 复制目录

​					 	复制一个script目录，并重新命名为script_port,port为tendis的端口号如（51003，下面均						 以51003端口为例），根据需要修改，每需要手动建立一个tendis节点就需要复制一个script						 目录

​						 cp -r ./script ./script_51003

​						![1602298832675](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602298832675.png)

​			3. 修改配置文件和停止脚本

​					 	进入script_51003目录，修改tendisplus.conf文件和修改stop.sh文件，将port后面的值改 					 	成51003

​						 vim tendisplus.conf

​						 vim stop.sh		

​						![1602298916508](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602298916508.png)

​			![1602298950422](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602298950422.png) 			4. 删除目录

​						 删除script_51003下面的home目录（没有则忽略该步骤）

​						 rm -rf ./home

​						![1602298999084](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602298999084.png)

​			5. 启动tendis节点

​				sh ./start.sh

![1602299063891](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602299063891.png)

​	    **[第二种：使用tendisplus-2.0.2-rocksdb-v5.13.4.tgz包联机部署真实生产环境](#second)**

​			 准备两台部署主机，确保其软件满足需求：

​				推荐安装 CentOS 7.3 及以上版本

​				Linux 操作系统开放外网访问，用于联机tendis集群

| 实例            | 个数 | IP             | 配置                   |
| --------------- | ---- | -------------- | ---------------------- |
| tendis集群机器A | 1    | 106.52.236.229 | 避免端口和目录冲突     |
| tendis集群机器B | 1    | 106.52.242.48  | 默认端口  全局目录配置 |

**实施部署**

​			1. 登陆tendis集群机器A  106.52.236.229

​			2. 下载tendisplus-2.0.2-rocksdb-v5.13.4.tgz包并解压，进入该目录

​				tar  -zxvf  tendisplus-2.0.2-rocksdb-v5.13.4.tgz

​			3. 复制目录

​					 	复制一个script目录，并重新命名为script_port,port为tendis的端口号如（51009，下面均						 以51009端口为例），根据需要修改，每需要手动建立一个tendis节点就需要复制一个script						 目录

​						 cp -r ./script ./script_51009

​			4. 修改配置文件和停止脚本

​					 	进入script_51009目录，修改tendisplus.conf文件和修改stop.sh文件，将port后面的值改 					 	成51009

​						 vim tendisplus.conf

​						 vim stop.sh		![1602312717406](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602312717406.png)

​			 5. 删除目录

​						 删除script_51009下面的home目录（没有则忽略该步骤）

​						 rm -rf ./home

​			6. 开启集群模式

​						将两个节点中的tendisplus.conf文件的末尾加上cluster-enabled on

​					![1602312657605](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602312657605.png)

​			7. 修改tendispluas.conf配置文件，使tendis节点能外网访问

​				加上bind 0.0.0.0，默认是本地访问，加上后可外网访问![1602312896112](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602312896112.png)

​			7. 启动tendis节点

​				sh ./start.sh

​			8. 登陆集群机器B 106.52.242.48，重复上述所有步骤(新的节点为： 106.52.242.48:51005)

​			9. 加入集群

​						使用redis-cli工具连接106.52.236.229:51009节点

​						 ../bin/redis-cli -h 106.52.236.229 -p 51009![1602313033356](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602313033356.png)

​						然后执行  cluster meet 106.52.242.48 51005

![1602313321656](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602313321656.png)

​						执行cluster nodes查看节点信息，看是否添加进了集群![1602313545400](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602313545400.png)

​		  10. 支持手动添加slot

​						连接上tendis节点，执行 cluster addslots 1  ，槽位号不能重复添加

​						![1602313604560](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602313604560.png)

​						**常见问题小贴士（ERR:18,msg:Slot is already busy）**

​								集群中的一些节点信息不统一，需要登陆上每个节点查看，是否占用了该slot

​		11. 建立主从关系		

​						连接10.0.1.1:51003节点，并且已经通过meet命令，加入了至少两个节点在集群中（例如端口					10.0.1.2:51003，nodeid为：37b8039564fca4dbce16e5216440ce155dc24433)执行以下命令：

​						cluster replicate 37b8039564fca4dbce16e5216440ce155dc24433

​						此命令会将10.0.1.2:51003节点变成10.0.1.1:51003节点的从节点，并且执行该命令时，						10.0.1.2:51003必须是空节点

## 	访问工具

​			    使用原生的redis-cli工具访问

​				redis-cli -h 127.0.0.1 -p 6379 -a "mypass"

​					-h  连接的节点ip

​					-p 连接的节点的port

​					-a 连接的节点密码，没有密码则省略

# 部署指南

## 	软硬件环境要求

## 	安装与启动

### 		部署基本节点

​					   	**需要的包** ：tendisplus-2.0.2-rocksdb-v5.13.4.tgz

​					  	 解压生成tendisplus-2.0.2-rocksdb-v5.13.4目录，并进入该目录

​							tar  -zxvf  tendisplus-2.0.2-rocksdb-v5.13.4.tgz

#### 		  	   复制目录

​					 	复制一个script目录，并重新命名为script_port,port为tendis的端口号如（51003，下面均						 以51003端口为例），根据需要修改，每需要手动建立一个tendis节点就需要复制一个script						 目录

​						 cp -r ./script ./script_51003

#### 			     修改配置文件和停止脚本

​					 	进入script_51003目录，修改tendisplus.conf文件和修改stop.sh文件，将port后面的值改 					 	成51003

​						 vim tendisplus.conf

​						 vim stop.sh		

#### 			    删除目录

​						 删除script_51003下面的home目录（没有则忽略该步骤）

​						 rm -rf ./home		

#### 			    启动节点			

​						 sh ./start.sh

#### 				停止节点

​						 sh ./stop.sh  (此步骤不用执行)

### 		建立集群模式

#### 				开启集群模式

​						将tendisplus.conf文件的末尾加上cluster-enabled on

#### 				加入集群

​						前提：已经部署了多个tendis节点，以51003端口和51004端口为例

​						使用redis-cli工具连接51003节点

​						../bin/redis-cli -h 127.0.0.1 -p 51003

​						然后执行  cluster meet 127.0.0.1 51004

​						执行cluster nodes查看节点信息，看是否添加进了集群

#### 			   支持手动添加slot

​						连接上tendis节点，执行 cluster addslots 1  ，槽位号不能重复添加

​						**常见问题小贴士（ERR:18,msg:Slot is already busy）**

​								集群中的一些节点信息不统一，需要登陆上每个节点查看，是否占用了该slot

#### 			   建立主从关系		

​						连接51002节点，并且已经通过meet命令，加入了至少两个节点在集群中（例如端口51003，

​						nodeid为：37b8039564fca4dbce16e5216440ce155dc24433），执行以下命令：

​						cluster replicate 37b8039564fca4dbce16e5216440ce155dc24433

​						此命令会将51002节点变成51003节点的从节点，并且执行该命令时，51002必须是空节点

#### 			   节点踢出集群

​						cluster forget nodeid  (nodeid为需要剔除集群的节点id)								

## 	验证集群状态

​			本文档介绍如何通过连接集群 检查集群状态，以及登录tendis节点执行简单tendis语句。

### 		查看tendis 集群状态

​				使用redi-cli工具 连接tendis节点，redis-cli -h 127.0.0.1 -p 6379 -a "mypass"，

​				然后执行cluster info  ,输出ok则为正常，为fail

​				![1602234930129](C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602234930129.png)

​				执行cluster nodes,展示的节点，存在fail则为不正常

​				<img src="C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602235021459.png" alt="1602235021459" style="zoom: 50%;" />

### 		登陆集群执行简单的语句

​					执行如下命令集群：

​						redis-cli -h 127.0.0.1 -p 51002 -a "mypass"

​					输出以下样式为登陆成功

​				<img src="C:\Users\v_vhqhuang\AppData\Roaming\Typora\typora-user-images\1602235337393.png" style="zoom:50%;" />

​					set数据类型操作

​						新建string类型	set  key1  value1

​						获取string类型key1的值    get  key1

​					hash数据类型操作

​						新建hash表   hset  field1  key1 value1  

​						获取某个hash表的所有键值  hgetall field1

​						获取某个hash表中某个key的值  hget field1 key1

​					list数据类型

​						左插入数据：lpush  list1  l1

​						右插入数据： rpush list1 l2

​						移除列表第一个元素 lpop l1

​					set数据类型：

​						SCARD key 获取集合的成员数

​						sadd set1 value1  集合插入数据

​						smembers set1 获取集合的所有成员

​					zset数据类型：

​						ZADD runoobkey 1 redis	有序集合插入数据

​					    ZRANGE runoobkey 0 10 WITHSCORES   有序输出0-10分数的成员

​						zcard key  获取有序集合的成员数

## 性能测试方法

# 运维操作

## 	扩缩容

## 	备份与恢复

## 	参数配置

## 	日常运维操作

# 监控与告警

## 	监控采集

## 	告警建议

# 故障诊断

## 	定位慢查询

# 版本发布历史



# 故障诊断


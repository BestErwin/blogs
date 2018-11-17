> MongoDB是一个非关系型数据库，数据类型是json格式的，轻巧方便
> 下面我们看一下在Windows如何安装和配置MongoDB。
# Windows安装配置MongoDB

下载的话网上都有很多，根据自己的电脑是64位还是32位的自行下载就可以了
官网地址：https://www.mongodb.com/download-center/community
这里提供楼主有的版本连接
https://pan.baidu.com/s/1fGzDiTJta-A8OluzLAuqkg
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542458941386.png)
安装也比较简单。直接下载下来安装到本地就可以。
重点我们看一下安装完成后的配置。

---
## 2、配置
安装完成后目录如下，楼主是安装在E盘
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542459368425.png)
在MongoDB文件夹下新建一下几个文件夹
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542459453412.png)
data：数据存放
etc：配置文件存放
logs：日志存放
etc文件夹下新建一个配置文件  mongo.conf
内容如下
```html
#数据库路径
dbpath=E:\MongoDB\data\
#日志输出文件路径
logpath=E:\MongoDB\logs\mongo.log
#错误日志采用追加模式，配置这个选项后mongodb的日志会追加到现有的日志文件，而不是从新创建一个新文件
logappend=true
#启用日志文件，默认启用
journal=true
#这个选项可以过滤掉一些无用的日志信息，若需要调试使用请设置为false
quiet=true
#端口号 默认为27017
port=27017
#指定存储引擎（默认先不加此引擎，如果报错了，大家在加进去）
storageEngine=mmapv1
```
接着配置一下电脑的环境变量，打开本地配置环境变量界面
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542459919296.png)
将MongoDB安装目录中的bin路径添加到path里
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542459978821.png)
这样我们在任何目录下都可以使用mongod命令了
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542460046197.png)

## 3、添加服务
管理员模式打开cmd
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542460884681.png)
cd 进入安装目录的bin文件下
输入
```cmd
mongod --logpath "E:\MongoDB\logs\mongo.log" --logappend --dbpath "E:\MongoDB\data" --directoryperdb --serviceName "MongoDB" --serviceDisplayName "MongoDB" --install
```
打开本地服务可以看到服务，表示成功
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542461023228.png)
这样就可以直接启动mongoDB服务了
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542461141383.png)
浏览器输入：http://127.0.0.1:27017/ ，显示如下表示成功
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542461320561.png)
可以在命令行中输入mongo命令对MongoDB进行操作了
![](https://www.github.com/BestErwin/img/raw/master/xiaoshujiang/1542461436090.png)

---
## mongodb之一些简单的增删改查语句
 

### 数据库操作：
show dbs;#查看数据库
use test;#如果没有就创建一个
db;#查看当前数据库
db.dropDatabase();#删除数据库

### 数据操作：
show collections；#查看集合
创建集合、插入：
create collection;#创建集合
db.student.insert({"name":"张三","age":"22","sex":"男","class":"计算机2班"});#如果数据库中不存在集合，就创建并插入这些数据
db.student.insert({"name":"李四","age":"22","sex":"女","phone":"18513081650","class":"计算机1班"});#里面的key-value不用保持一致
db.student.insert([{"name":"王五","age":"22","sex":"男","class":"计算机2班"},{"name":"赵六","age":"22","sex":"女","phone":"18513081650","class":"计算机1班"}]);#同时插入多条数据

### 更新：
db.student.update({"name":"张三"},{"name":"张三丰"});#如果有多条语句，只修改第一条，会覆盖原有数据
db.student.update({"22":"女"},{"name":"张三丰"});
db.student.update({"name":"张三"},{$set:{"name":"张无忌"}});#只想改某个key的value使用set
db.student.update({"name":"王五"},{$set:{"name":"张无忌"}},{multi:true});#把所有的记录都改了

### 查询：
db.student.find();#查询全部
db.student.find({"name":"李四"});#查询指定记录，返回这一行结果
db.student.update({"name":"张三丰"},{"name":"张无忌","age":"28","sex":"男"});
db.student.find({"name":"张无忌","age":"28"});#and操作
db.student.find({$or:[{"name":"张无忌"},{"name":"李四"}]});#or操作
db.student.find().pretty();#格式化显示
db.student.find().count();#获取结果的行数
db.student.find().sort({"age":-1});#按照sort里面key的值排序，1为正序，-1为倒序

### 删除：
db.student.remove();#删除所有数据
db.student.remove({"22":"女"});#按照条件删除
db.student.remove({"name":"张无忌"},2);#删除几条

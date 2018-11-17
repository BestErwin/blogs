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


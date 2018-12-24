# ServerStatus中文版：   

* ServerStatus中文版是一个酷炫高逼格的云探针、云监控、服务器云监控、多服务器探针~。
* 在线演示：https://status.7colorblog.com   
* 本人博客：https://www.7colorblog.com  
* 七彩杂铺货：https://faka.7colorblog.com  

# 目录介绍：

* clients  客户端文件
* server   服务端文件
* web      网站文件  

# 更新说明：

* 20181224, 将软件仓库全部整合为本人仓库,并加以细节修改
* 20180314, 调整前端，置默认密码为: USER_DEFAULT_PASSWORD，设置ip和user即可上线　　　　　　
* 20180312, 加入失联(被照顾)检测【正常：MH361, 屏蔽：MH370】，校准虚拟化(container)流量统计异常　　　　　　
* 20170807, 更新平均1，5，15负载
* 20170108, 更新支持所有系统
* 20161205, 去掉无用的IPV6信息，增加服务器总流量监控                           

# 系统要求
CentOS 7 / Debian 7+ / Ubuntu 14.04 +

推荐 Debian 7 x64，这个是我一直使用的系统，我的脚本在这个系统上面出错率最低。

> 注意，既然是个 多服务器云监控程序，那么你肯定需要两个以上的服务器（其实一个也可以，客户端和服务端可以同时安装），一个服务器做服务端，脚本会自动安装Caddy并配置好HTTP服务的，然后接收各个客户端实时发来的信息并通过网站显示出来。
> 因为客户端每秒都会发送最新的信息给服务端，所以要保证客户端与服务端直接网络通常，否则网页显示会很抽风。
> 虽然客户端每秒都会发送信息到服务端，但是对流量消耗是很小的，毕竟每次发送的数据都只有几百或上千个字符。

**ServerStatus 客户端需要 Python 2.7版本以上才可以正常运行，如果不是那么请升级（查看版本： `python -V` ）。**

> 注意：CentOS6 系统默认的Python版本是2.6，版本太低，使用客户端会出问题，请升级Python或者更换系统。

# 一键安装脚本：
执行下面的代码下载并运行脚本。
``` bash
wget -N --no-check-certificate https://raw.githubusercontent.com/lizhongnian/ServerStatus/master/status.sh && chmod +x status.sh
```
下载脚本后，根据需要安装客户端或者服务端：
``` mipsasm
# 显示服务端管理菜单
bash status.sh server

# 显示客户端管理菜单
bash status.sh client
```
运行脚本后会出现脚本操作菜单，选择并输入 `1` 就会开始安装。

一开始会提示你输入网站服务器的域名和端口，如果没有域名可以直接回车代表使用 **本机IP:8888**。
## 简单步骤
首先安装服务端，安装过程中会提示：
是否由脚本自动配置HTTP服务(服务端的在线监控网站)[Y/n]
``` vala
# 如果你不懂，那就直接回车，如果你想用其他的HTTP服务自己配置，那么请输入 n 并回车。
# 注意，当你曾经安装过 服务端，同时没有卸载Caddy(HTTP服务)，那么重新安装服务端的时候，请输入 n 并回车。
```
然后 **添加或修改 初始示例的节点配置，注意用户名每个节点配置都不能重复**，其他的参数都无所谓了。

然后安装客户端，根据提示填写 **服务端的IP** 和前面添加/修改 对应的 **节点用户名和密码**（用于和服务端验证），然后启动就好了。
## 使用说明
进入下载脚本的目录并运行脚本：
``` jboss-cli
# 客户端管理菜单
./status.sh c
# 服务端管理菜单
./status.sh s
```
然后选择你要执行的选项即可。
``` markdown
ServerStatus 一键安装管理脚本 [vx.x.x]
-- 7colorblog | https://www.7colorblog.com --
 
————————————
1. 安装 服务端
2. 卸载 服务端
————————————
3. 启动 服务端
4. 停止 服务端
5. 重启 服务端
————————————
6. 设置 服务端配置
7. 查看 服务端信息
8. 查看 服务端日志
————————————
9. 切换为 客户端菜单
 
当前状态: 服务端 已安装 并 已启动
 
请输入数字 [1-9]:
```
## 其他操作
### 客户端
**启动：**`/etc/init.d/status-client start`

**停止：**`/etc/init.d/status-client stop`

**重启：**`/etc/init.d/status-client restart`

**查看状态：**`/etc/init.d/status-client status`
### 服务端
**启动：**`/etc/init.d/status-server start`

**停止：**`/etc/init.d/status-server stop`

**重启：**`/etc/init.d/status-server restart`

**查看状态：**`/etc/init.d/status-server status`
### Caddy（HTTP服务）
**启动：**`/etc/init.d/caddy start`

**停止：**`/etc/init.d/caddy stop`

**重启：**`/etc/init.d/caddy restart`

**查看状态：**`/etc/init.d/caddy status`

**Caddy配置文件：**`/usr/local/caddy/Caddyfile`


----------
**安装目录：**`/usr/local/ServerStatus`

**网页文件：**`/usr/local/ServerStatus/web`

**客户端拓展信息配置文件:**`/usr/local/ServerStatus/customMsg.txt` #注意：不能超过512个字符，否则会出错。可以用html、css的标签去格式化显示(稍微注意双引号要用反斜杠\转义)

**配置文件：**`/usr/local/ServerStatus/server/config.json`

**客户端查看日志：**`tail -f tmp/serverstatus_client.log`

**服务端查看日志：**`tail -f /tmp/serverstatus_server.log`


----------
### 服务端网页显示异常，频繁开启/关闭
这种问题说明系统中的 Python版本低于 2.7（查看版本： `python -V` ），一般常见这种问题的都是 CentOS6 ，因为这个系统默认都是 Python2.6 版本，版本太低，使用客户端会出问题，请升级Python或者更换系统。
### 提示 wget: command not found 的错误
这是你的系统精简的太干净了，wget都没有安装，所以需要安装wget。
``` vala
# CentOS系统:
yum install -y wget
 
# Debian/Ubuntu系统:
apt-get install -y wget
```
### Caddy启动失败，打开 http://ip 显示的是 It works !
一些系统会自带 apache2 ，而 apache2 会占用80端口，导致Caddy无法绑定端口，所以只要关掉就好了。
``` nginx
netstat -lntp
# 我们可以通过这个命令查看是不是被其他软件占用了 80 端口。
```
不过 apache2 会默认开机自启动，如果不需要可以关闭自启动或者卸载 apache2 。
**停止 Apache2**
``` vim
service apache2 stop
# 尝试使用上面这个关闭，如果没效果或者提示什么错误无法关闭，那就用下面这个强行关闭进程。
kill -9 $(ps -ef|grep "apache2"|grep -v "grep"|awk '{print $2}')
```
**取消开机自启动**
``` shell
# CentOS 系统 #
chkconfig --del httpd
# Debian/Ubuntu 系统 #
update-rc.d -f apache2 remove
```
**卸载 Apache2(卸载包括了取消开机启动，无需重复)**
``` shell
# CentOS 系统 #
yum remove httpd
# Debian/Ubuntu 系统 #
apt-get remove --purge apache2
```
关闭 Apache2后，就可以尝试启动 Caddy ，并试试能不能打开网页。
``` ebnf
service caddy start
```


# 手动安装教程：     
   
【克隆代码】:
```
git clone https://github.com/tenyue/ServerStatus.git
```

【服务端配置】（服务端程序在ServerStatus/web下）:  
          
一、生成服务端程序              
```
cd ServerStatus/server
make
./sergate
```
如果没错误提示，OK，ctrl+c关闭；如果有错误提示，检查35601端口是否被占用    

二、修改配置文件         
修改config.json文件，注意username, password的值需要和客户端对应一致                 
```
{"servers":
	[
		{
			"username": "s01",
			"name": "Mainserver 1",
			"type": "Dedicated Server",
			"host": "GenericServerHost123",
			"location": "Austria",
			"password": "some-hard-to-guess-copy-paste-password"
		},
	]
}       
```

三、拷贝ServerStatus/status到你的网站目录        
例如：
```
sudo cp -r ServerStatus/web/* /home/wwwroot/default
```

四、运行服务端：             
web-dir参数为上一步设置的网站根目录，务必修改成自己网站的路径   
```
./sergate --config=config.json --web-dir=/home/wwwroot/default   
```

【客户端配置】（客户端程序在ServerStatus/clients下）：          
客户端有两个版本，client-linux为普通linux，client-psutil为跨平台版，普通版不成功，换成跨平台版即可。        

一、client-linux版配置：       
1、vim client-linux.py, 修改SERVER地址，username帐号， password密码        
2、python client-linux.py 运行即可。      

二、client-psutil版配置:                
1、安装psutil跨平台依赖库      
2、vim client-psutil.py, 修改SERVER地址，username帐号， password密码       
3、python client-psutil.py 运行即可。           
```
### for Centos：
sudo yum -y install epel-release
sudo yum -y install python-pip
sudo yum clean all
sudo yum -y install gcc
sudo yum -y install python-devel
sudo pip install psutil
### for Ubuntu/Debian:
sudo root
apt-get -y install python-setuptools python-dev build-essential
apt-get -y install python-pip
pip install psutil
### for Windows:
打开网址：https://pypi.python.org/pypi?:action=display&name=psutil#downloads
下载psutil for windows程序包
安装即可
```

打开云探针页面，就可以正常的监控。接下来把服务器和客户端脚本自行加入开机启动，或者进程守护，或以后台方式运行即可！例如： nohup python client-linux.py &      

# 为什么会有ServerStatus中文版：

* 有些功能确实没用
* 原版本部署，英文说明复杂
* 不符合中文版的习惯
* 没有一次又一次的轮子，哪来如此优秀的云探针

# 相关开源项目，感谢： 

* ServerStatus：https://github.com/BotoX/ServerStatus
* mojeda: https://github.com/mojeda 
* mojeda's ServerStatus: https://github.com/mojeda/ServerStatus
* BlueVM's project: http://www.lowendtalk.com/discussion/comment/169690#Comment_169690

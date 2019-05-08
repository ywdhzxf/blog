
---
title: linux的基础命令
date: 2019-05-06 12:36:15
tags: linux
---


## linux简介

### 安装 

1. 安装操作系统软件   CentOS6.8-***.iso
2. 密码原则    12位以上    大小写字符  数字   特殊符号
3. DeskTop   图形界面      开发 
4. Basic Server   服务器   没有图形界面   Server
5. 安装Basic Server    701软件包
6. 分区  swap备用内存2000M ，/boot exit 执行内存200M 剩余全部为根目录exit空间
7. setup 设置防火墙之类
8. ifconfig  查看网络状态 
9. 最后service network restart 重启网络服务确定无误

### 常用端口

```
3306   mysql        80 apache（http）    22 ssh
pgrep  应用    得到进程号
```

###  常用命令

```
ls              (显示当前目录下文件)
ls 目录名        (显示指定目录下文件)
ls -l           (长格式显示目录文件)
ls -l 文件名     (长格式显示指定文件)
ls -a           (显示所有文件(包含隐藏文件))
ls -al          (长格式显示当前目录下所有文件)
ls -h           (文件大小显示为常见大小单位 B KB MB ...)
ls -d           (显示目录本身，而不是里面的子文件)
```

```
cd /usr/local/src   切换到指定路径(使用绝对路径方式)
cd ~                进入当前用户的家目录
cd -                进入上次目录
cd ..               进入上一级目录
cd .                进入当前目录
```

```
/bin              命令保存目录（普通用户就可以读取的命令）
/boot             启动目录，启动相关文件
/dev              设备文件保存目录
/etc              配置文件保存目录
/home             普通用户的家目录
/lib              系统库保存目录
/mnt              系统挂载目录
/media            挂载目录
/root             超级用户的家目录
/tmp              临时目录
/sbin             命令保存目录（超级用户才能使用的目录）
/proc             直接写入内存的
/sys              将内核的一些信息映射，可供应用程序所用
/usr              系统软件资源目录
/usr/bin/         系统命令（普通用户）
/usr/sbin/        系统命令（超级用户）
/var              系统相关文档内容
/var/log/         系统日志位置
/var/spool/mail/  系统默认邮箱位置
/var/lib/         默认安装的库文件目录 
```

### 提示符

```
[dragon@localhost ~]$
   ①       ②    ③ ④

①：dragon 代表 当前登录用户
②：localhost 代表 主机名
③：~ 代表 当前所在目录
    ~ 用户家目录；  /root 管理员；  /home/用户名 普通用户
④：$ 代表 当前用户身份
    $ 普通用户；  # 超级用户
```

## linux简单操作

### 追加

```
ls -lR  可以看当前目录文件以及目录里面的文件
/opt  临时应用的SH 可以放置
bd 数据库          bak 备份
last  查看历史登录记录（用户名，时间，登录中断之类）
$0   文件本身      printf 格式化打印
```

### 常用操作

```
mkdir   t1        创建目录
mkdir   -p   t1/t2/t3      递归创建目录
rmdir   t1         删除目录（只能删除空目录）
rm -rf   t1    强制删除目录文件
rm  -r   t1   递归删除文件和目录   
touch  t1.py    创建空文件
touch  -t  20170612   t1    修改文件时间
cat   t1.py       查看文件内容
cat   -n    t1.py      查看文件内容并列出行号
more   t1.py      分屏显示文件内容   空格向上   b 向下      q 退出
head  t1.py   显示文件前几行（默认10行）
head  -n  20   文件名    显示文件前20 行
head   -n  -29  文件名   显示文件最后20行（不常用，有tail）
ln  -s   源文件    目标文件       创建链接文件（必须用绝对路径）
nano    文件名          纳米编辑器
man   ls     帮助命令             ls    --help     帮助命令
date		查看系统时间
	date  -s  20170220		设定日期
	date  -s  09:30:00		设定时间
du  -sh  目录名		统计目录大小
	-s	和
	-h	常见单位 
df  -h       查看系统内存（查看占用内存。以便为后安装程序做准备）
df   -hT      查看系统内存（T 类型）
netstat -an |grep ESTABLISHED | wc -l   查看服务器的连接数
source 文件名      执行这个文件（一般在改配置时使用）
```

```

cp 源文件 目标位置             (复制)
    或
cp 源文件 目标位置/目标名称      (复制并改名)

cp -r       复制目录
cp -p       连带文件属性一起复制
cp -d       若源文件是链接文件，则复制链接属性
cp -a       相当于 cp -pdr
```

```
mv 源文件 目标位置
mv /root/test /tmp/           将/root/下的test文件移动到/tmp/目录下
mv /root/test /root/newtest   将/root/下的test文件改名为newtest
```

### 快捷键

```
ctrl +c      强行终止
ctrl   + l     清屏
tab         命令补全   文件目录名补全（常用）
反撤销  ctrl + r
```

### 权限位

```
-rw-r--r--. 1 root root 44736 7月  18 00:38 install.log

权限位是十位
    第一位：代表文件类型
    -   普通文件
    d   目录文件
    l   链接文件
默认文件   644   默认目录  755     默认链接文件  777
最大  777   最小 000

    其他九位：代表各用户的权限
    (前三位=属主权限u  中间三位=属组权限g  其他人权限o)
    r   读   4
    w   写   2
    x   执行  1
    权限对文件的含义
    r：读取文件内容 如：cat、more、head、tail
    w：编辑、新增、修改文件内容 如：vi、echo 但是不包含删除文件
    x：可执行  /tmp/11/22/abc   ---------    

权限对目录的含义
    r：可以查询目录下文件名 如：ls
    w：具有修改目录结构的权限 如：touch、rm、mv、cp
    x：可以进入目录 如：cd
```

### 权限操作

```
chmod u+x aa      aa文件的属主加上执行权限
chmod u-x aa      aa文件的属主减去执行权限
chmod g+w,o+w aa  aa文件的属组和其他人加上写权限
chmod u=rwx aa    aa文件的用户权限改为所有权限(读+写+执行)

chmod 777 -R aa    给当前文件和子文件都给上权限
另一种表现方式：
chmod 755 aa      aa文件的属主权限是rwx，属组和其他人是rx
chmod 644 aa      aa文件的属主权限是rw，属组和其他人是r
```

```
chown 用户名 文件名      改变文件属主
chown user1 aa         user1必须存在
chown user1:user1 aa   改变属主同时改变属组
```

 ### 用户操作

```
useradd 用户名        功能描述：添加用户
userdel -r  用户名    功能描述： 连同家目录一起删除用户
id -u 检测当前用户的UID

passwd 用户名         功能描述：设定用户密码 
```

### 查找命令

whereis     ls               查找命令所在位置

```
find 查找位置 -name 文件名
find / -name aabbcc    查找/目录下名为 aabbcc的文件

更多选项：
    -name 文件名      按照文件名查找
    -user 用户名      按照属主用户名查找文件
    -group 组名       按照属组组名查找文件
    -nouser          找没有属主的文件 (除了这三个文件：/proc、/sys、/mnt/cdrom)
    -size            按照文件大小k M  如：find / -size +50k
    -type            按照文件类型查找(f=普通  d=目录  l=链接)
    -perm            按照权限查找  如：find /root -perm 644
    -iname           按照文件名查找，不区分大小写
格式  
find   /    -name   index.html
find   /   -user   python
find   /   -group   python
find  /    -nouser
find  /  -type     f
find   /  -perm     777
find / -size +10M -a -size -20M  -exec rm -rf  {} \;
find / -size +10M -a -size -20M  -ok   rm -rf  {} \;
exec  直接执行不提示     OK  提示危险操作
```

```
grep 选项 '字串' 查找路径
grep  '字串'    路径
grep -i "root" /etc/passwd
    -v       反向选择
    -i       忽略大小写
    -n       显示行号
```

### 管道符

 |   连接命令

ls   -l   /etc/    |   more      分屏显示etc里面的目录和文件

cat  -n  install.log   |   grep  "zip"       查看文档显示行号并且查找‘zip’字符

### 压缩和解压

```
tar.gz    
tar  -zcvf       p1.tar.gz     test1.py  install.log    压缩文件
tar   -zxvf     p1.tar.gz    解压缩  
tar  -ztvf    p1.tar.gz  查看不解压
tar   -zxvf   p1.tar.gz   -C   txt     定向解压缩
tar -zcPf   p1.tar.gz test1.py    压缩文件  
-P 保留备份文件的原有权限和属性。常用于备份
```

```
.tar.bz2
tar  -jcvf      txt.tar.bz2    txt    压缩目录
tar  -jxvf    txt.tar.bz2   解压缩
tar  -jtvf    txt.tar.bz2    查看不解压
tar   -jxvf    txt.tar.bz2   -C   /tmp    定向解压缩
```

### 关机重启

```
shutdown  -h  now     现在关机 
init  0  关机
shutdown   -r   now    重启系统 
reboot   重启系统 
init  6  重启
```

### 挂载

```
1. 物理连接    2.手动挂载  3.识别设备使用

   mount     光驱设备名   （/dev/sr0    /dev/cdrom）     挂载点  /media   /mnt  (手动建立挂载点      mkdir  /mnt/cdrom)
   
   mount   /dev/sr0    /media
   cd  /media/
1. 卸载    umount 
   umount  /dev/sr0   
   umount  /media   注意：退出挂载目录，才能卸载
fdisk  -l    查看设备名
mount -t iso9660 /dev/cdrom /mnt/cdrom
```

### 网络命令

```
ping     测试网络连通性
ping   -c   5   192.168.2.222  
ifconfig     查看网络设备    Linux  
ipconfig        windows  
ipconfig   /all
```

## vim操作

![图片1](C:\Users\Administrator\Desktop\图片1.png)

```
vim编辑器
全屏幕纯文本编辑器
vi -> vim (加强版)

三种模式： 
命令模式                插入模式                 末行模式
                       a   i   o  s             Shitft + : 
                         ESC
a  追加   i 插入  o 打开  s 删除当前字符插入 
:wq  保存退出  :w 保存  :q 退出
:q! 不保存退出  :wq! 强制保存退出（root）
vim   test1.py       命令模式
vim   install.log 

光标移动     h  j   k   l             :n   行号   :300      gg  光标移动到第一行   G 移动最后一行
设置行号  :set nu    取消行号  :set nonu            
复制  yy      复制多行  nyy    
粘贴    p   
删除(剪切)单字符   x     删除多字符  nx 
删除（剪切）行  dd      删除多行 ndd            
dG   从当前行到最后全部删除
撤销  u        反撤销  ctrl + r
颜色开关（语法高亮） :syntax off  关闭   :syntax  on   开启 

手动建立配置文件
vim   ~/.vimrc        
 可以写   set nu    让每个文件都显示行号

查找功能
vim  install.log 
/i686   N  向下    n 向上   查找i686 
/root    查找root 

替换功能
vim  install.log
:%s/要替换内容/替换后内容/g    全文替换
:1,20s/要替换内容/替换后内容/g  范围替换

注释   #  
:21,30s/^/#/g    添加注释       :25,30s/^#//g   取消注释
:60,70s/^/\/\//g   添加注释      :65,70s/^\/\///g  取消注释 
```

## 软件包安装

```
一 	软件包分类
源码包:	
        优点：	特点	开源	自由定制
		缺点：	编译时间长，一旦报错，很难解决
二进制包:rpm包
		优点：安装速度快		简易
		缺点：自定义性差		依赖性
				a---->b---->c		树形依赖
				a---b----c---a		环形依赖			
库文件依赖		www.rpmfind.net
```

### rpm手动安装

```
手动RPM命令安装
		1	包命名
			包名-版本号-发布次数-适合linux系统-硬件平台.rpm
	    2	安装
			rpm  -ivh  包名（绝对路径）
				-i  安装	-v	显示详细信息		-h 显示进度
			rpm  -Uvh  包名
				-U  升级
		3	卸载
			rpm  -e  软件名	
		4	查询
			rpm  -q  软件名		        查询包是否安装
			rpm  -qa  | grep  httpd 		显示所有安装包
			rpm  -qi  软件名	查询包的信息		-p  未安装包
			rpm  -qip 包名	查询没有安装包的信息
				-i	information
			rpm  -ql  软件名	查询包中文件的安装位置
			rpm  -qlp  包名	查询没有安装的包，打算安装位置
					-l	list
			rpm  -qf  系统文件名		查询系统文件属于哪个包
```

### yum安装

```
yum  -y  install  软件名		 安装			-y  自动回答yes
yum  -y  remove   软件名	     删除
yum  -y  update   软件名        升级
yum  list			       查询所有可以安装的包
光盘作为yum源：
	1	cd  /etc/yum.repos.d/
		mv  CentOS-Base.repo  CentOS-Base.repo.bak

	2	mount /dev/sr0     /mnt/cdrom
	3	vim  /etc/yum.repos.d/CentOS-Media.repo
			baseurl=file:///mnt/cdrom/	指定yum源位置
			enabled=1					yum源文件生效
			gpgcheck=0					rpm验证不生效
yum  -y  install  gcc 		(gcc是c语言编译器，不装gcc，源码包不能安装)
```

### 源码包安装(apache)

```
！！！  必须先安装gcc  !
apache解析php的效率特别高
1	远程传输工具传输apache到linux。
				httpd-2.2.29.tar.gz
2	安装
	1）解压
	2） cd  解压目录
	3）  查看安装文档
	     INSTALL		README
	4）编译前准备
		./configure  --prefix=/usr/local/apache2
		功能：
			1	检测系统环境，生成Makefile
			2	定义软件选项
	5)编译			
		make
	6）编译安装
		make  install
		报错判断：
			第一：安装过程是否停止
			第二：注意error  warning  no  等错误报警
3	启动
	/usr/local/apache2/bin/apachectl  start
	/usr/local/apache2/bin/apachectl  stop    
4	删除
	直接删除安装目录
```

## 用户和用户组管理

### 用户管理命令

```
一	用户管理命令		
		用户信息文件：	/etc/passwd
	超级用户  uid 0
	普通不需要登录， uid 500 开始 人为用户（系统服务使用）
		影子文件：	/etc/shadow
		组信息文件：	/etc/group
	1	添加用户
		useradd  用户名		
		useradd  选项  用户名
useradd   -g    python   f1     添加f1 同时修改初始组为python
useradd   -G    python   f2    添加f2  同时添加f2为python组的附加组员
useradd   -c    "pyer"    f3    添加f3用户 同时注释
useradd    -d    /home/four    f4    添加用户f4同时修改家目录名
useradd    -s    /bin/nologin   f5    添加用户f5同时禁止登录
	2	设定密码			
		passwd	用户名
		passwd			改变当前用户密码
		passwd   root		改变root密码
	3	删除用户				
		userdel  -r  用户名
		-r  连带家目录一起删除
	4	添加组				
		groupadd  组名
	5	删除组				
		groupdel  组名		
	6	把已经存在的用户加入组			
		gpasswd  -a  用户名  组名		用户加入组
		gpasswd  -d  用户名  组名		把用户从组中删除
```

### 用户相关命令（id和切换）

```
id   用户名     查看用户相关ID号 ，显示用户的UID，初始组和附加组
su  - 用户名    切换用户身份 
```

### ACL权限

```
1.给特殊身份的人设置权限 
  getfacl  文件名  查看文件的acl权限
  setfacl   -m   u:用户名:权限   文件名    设置用户的ACL权限
  ls -l    查看有没有 +
  getfacl   test1.py  

  setfacl   -m   g:组名:权限     文件名     设置组的ACL权限 
  getfacl 文件名    查看权限

  setfacl  -x  u:f2   test1.py   删除f2用户ACL权限
  setfacl  -b  文件名   删除所有ACL权限

2.对目录设置ACL权限
  1）对目录本身设置ACL权限
  setfacl  -m  u:f2:rwx    目录名   

  2）对目录和目录内文件设置ACL权限 
  setfacl  -m  u:f2:rwx   -R   目录名     递归设置 
  
  3）对未来建立的文件设置ACL权限 
  setfacl  -m   d:u:f2:rwx    -R   目录名
  -R  递归
 
 ！！！ 如果给目录赋予ACL权限，2和3 命令都要输入 ！！！
```

### 输出重定向

```
ls   >  name.list
ls  -l  > name.list   覆盖 
ls      >>   name.list   追加
```

## 进程和服务管理

```
进程管理三个主要任务：
		判断服务器健康状态
		查看所有正在运行的进程
		强制终止进程
```

### 进程查看系统运行状况

```
1	ps  aux		查看当前系统所有运行的进程
	-a 	显示前台所有进程
	-u	显示用户名
	-x	显示后台进程

	user： 用户名
	pid：	进程id。PID		 init  系统启动的第一个进程
	%CPU	cpu占用百分比
	%MEM	内存占用百分比
	VSZ	虚拟内存占用量		KB
	RSS	固定内存占有量
	tty	登录终端		本地终端		远程终端		
	stat	状态	S：睡眠 D：不可唤醒	R：运行	  T：停止  
	start	进程触发时间
	time  	占用cpu时间
	command	 进程本身
2	pstree		 查看进程树
3	top  （动态查看）
	第一行：	系统当前时间		系统持续时间		登录用户		1,5,15分钟之前的平均负载
	第二行：进程总数
	第三行：CPU占用率		%id		空闲百分比
	第四行：内存使用：	总共		使用		空闲		缓存
	第五行：swap使用
	操作命令	  M	 内存排序
				P	CPU排序
				q	退出
4    w	查看系统运行情况和登录用户（静态查看）
5	进程管理		终止进程
	kill  -9  PID		结束单个进程
	-9  强制
	killall  -9  进程名		终止进程树
	
	
	pkill  -9  -t  终端号	把某个终端登录的用户踢出
	例：pkill  -9  -t tty1		把本地登录终端1登录用户踢出
```

### 服务管理

```
1	分类
	1）系统默认安装的服务		安装二进制包的服务
	2）源码包安装的服务

（一）系统默认安装的服务
	1	确定服务分类
		chkconfig  --list		查看服务的自启动状态
		运行级别：0-6
		0	关机
		1	单用户模式
		2	不完全多用户，不包含NFS服务
		3	完全多用户	字符界面
		4	未分配
		5	图形界面
		6	重启
	  init  0	关机			init  6	重启
	  runlevel			查询系统当前运行级别
	  vi  /etc/inittab
	  id:3:initdefault:		定义系统默认运行级别
	2	系统默认安装的服务器管理		
		1）启动
			/etc/rc.d/init.d/服务  start|stop|restart|status
			例：	/etc/rc.d/init.d/httpd  start
			service   服务名   start|stop|restart|status
		2)自启动	
		  chkconfig  --list  查看
		  chkconfig  --level  245  服务名  on|off 
 ！！！ 245 都可以   尽量不要写3，因为是系统服务 ！！！
		推荐用下面这种方法
			vi  /etc/rc.local---->/etc/rc.d/rc.local
			/etc/rc.d/init.d/httpd  start
（二）源码包安装的服务
	1）手动管理  绝对路径启动   不可以状态查询
		/usr/local/apache2/bin/apachectl  start
	2)开机自启动
		vi /etc/rc.local
		/usr/local/apache2/bin/apachectl  start
```

### 计划任务

```
crontab  -e		编辑定时任务
		* * * * *  命令（命令一般是绝对路径）
		第一个*：一小时中第几分钟	   0-59
		第二个：一天中第几个小时	   0-23
		第三个：一个月中第几天		    1-31
		第四个：一年第几个月			1-12
		第五个：一周中星期几			0-6		
例：		
	5   3  *  5,7,10  *  命令   5,7和10月每天三点5分执行
	*/10  *  *  *  1-3   命令   星期一到星期三每隔10分钟执行
命令： 开启/关闭服务   service sshd start     
					service sshd stop                               /usr/local/apache2/bin/apachectl restart
       备份文件/目录   cp  -r   /root/bbs   /tmp
crontab  -l		查看系统定时任务
crontab  -r  	删除所有定时任务

注意事项：
选项都不能为空，必须填入，不知道的值使用通配符*表示任何时间 
每个时间字段都可以指定多个值，不连续的值用,间隔，连续的值用-间隔
间隔固定时间执行书写为*/n格式 
命令应该给出绝对路径 
	星期几何第几天不能同时出现
	最小时间范围是分钟，最大时间范围是月
```

## 网络配置

```
IP设置 

ifconfig   eth0   192.168.2.251     临时IP        
setup        设置永久IP  关闭防火墙
service   network   restart      (/etc/rc.d/init.d/network  restart)    重启网络服务

网卡信息文件  vim  /etc/sysconfig/network-scripts/ifcfg-eth0   
  8  IPADDR=192.168.2.251     IP地址
  9  NETMASK=255.255.255.0      掩码
 10  GATEWAY=192.168.2.1        网关
     BOOTPROTO=none			是否自动获取IP。none：不生效	static：手动	 dhcp：动态获取IP
     DEVICE=eth0				网卡设备名
     ONBOOT=yes					    网卡开机启动
     
主机名修改 
  hostname    查看主机名 
  hostname   lampbrother   临时修改主机名
  vim  /etc/sysconfig/network      永久修改主机名
     HOSTNAME=lampbrother
     
DNS设置
  setup  设置DNS
  vim  /etc/resolv.conf
  nameserver  114.114.114.114

网络命令
  vim /etc/services   查看网络端口
  ifup   eth0   开启网卡
  ifdown  eth0   关闭网卡
  netstat  -an   查看网络状态
  netstat  -tlun   查看查看tcp和udp协议监听端口
  	t  tcp   u  udp   l  listen 
  netstat  -rn    查看网关（默认路由default）
  route  del   default   gw   192.168.2.1   删除默认网关
  route   add  default   gw   192.168.2.1  添加默认网关
  ping  192.168.2.250       ICMP协议   测试网络连通协议    
  ping   -c  5  -s   10000   192.168.2.250   -s   发送数据大小  
```

## VSFTP服务

```
一	文件服务器简介
	ftp：在内网和公网使用。	服务器：windows，linux	客户端：		windows，linux
	服务器 用 s 表示    客户端用 c 表示
1	ftp软件
	linux：	wu-ftp		早期，安全一般
	proftp		增强ftp工具
	vsftp		安全，强大
	windows	IIS		windows下网页搭建服务，可以搭建ftp服务
	Serv-U		专用ftp服务器
2	原理
	开启 	21  	命令传输端口
	20	    数据传输端口
3	ftp的用户
	1）ftp允许登录用户	就是系统用户	使用密码也是系统密码
					上传位置：/home/家目录
	2）匿名用户	anonymous	密码：  空  
					下载位置：/var/ftp/pub
二	安装
	mount /dev/sr0 /media
	cd /media/Packages/
	yum -y install  vsftpd  
三 	相关文件（了解）
	/etc/vsftpd/ftpusers	用户访问控制文件(不是必要步骤)
	/etc/vsftpd/vsftpd.conf		配置文件
四	配置文件配置
      vim    /etc/vsftpd/vsftpd.conf
    1主机相关配置
		listen_port=21			         监听端口
		connect_from_port_20=YES		数据传输端口
		ftpd_banner=				    欢迎信息
	2	匿名用户登录			在linux下识别为  ftp  用户
		nonymous_enable=YES			允许匿名用户登录
	3	本地用户
		local_enable=YES			允许系统用户登录
		write_enable=YES			允许上传
		local_umask=022			默认上传权限
	4	限制用户访问目录
		chroot_local_user=YES		所有用户限制在家目录下
	5   关闭防火墙和selinux
		关闭防火墙   setup
		关闭 selinux
		    vim  /etc/selinux/config
		    SELINUX = disabled	
	6  重启生效
	   reboot   重启
五	ftp客户端使用
	1、使用windows窗口
		ftp://用户名@IP
		匿名用户可以不用用户名和密码
		ftp://@ip
	2、使用第三方工具登录
		FileZilla
```

```
实验  限制用户目录权限
vim /etc/vsftpd/vsftpd.conf
96   chroot_local_user = YES
service vdftpd restart   重启服务
FileZilla  登录
```

## Samba服务器

```
文件共享服务
windows  ->  linux 
（一）端口
	smbd：为clinet提供资源访问		tcp  139  445
	nmbd：提供netbios主机名解析		udp  137  138
（二）安装 ISO
	mount /dev/sr0  /media
	yum -y install samba
	samba-common		主要配置文件
	samba-client		客户端文件
(三)修改配置文件
	安全级别     share     无密码
		        user      添加samba用户设置samba密码   
		    	server    需要服务器做解析
		    	
实验1： 安全级别  share    共享目录 /movie    
    1）建立目录/movie
       mkdir   /movie
       chmod  777  /movie
    2）修改配置文件
    vim  /etc/samba/smb.conf
    101         security = share
    263 [movie]    （这步是添加共享文件）
    264         comment = dianying   （说明）
    265         path = /movie		（路径）
    266         browseable = yes	 （目录对用户可见）
    267         guest ok = yes		  （访问）
    268         writable = yes		（可写）
    3）启动服务  测试
    关闭防火墙  关闭selinux
     vim  /etc/selinux/config
		 SELINUX = disabled	
    service  smb  start
    service  nmb  start
    netstat  -tlun   （查看端口是否出现）
  测试     
      \\192.168.2.251
  网络驱动映射
  	  进入共享文件，右键，网络驱动映射，就可以在我的电脑里查看信息
  	 
实验2：安全级别  user     共享  /pub  所有用户能访问上传     			/soft  只有aa能访问上传
1）建立目录
  mkdir  /pub
  mkdir  /soft
  chmod  777  /pub
  chmod  700 /soft
  useradd  aa
  passwd  aa
  chown    aa   /soft
2）修改配置文件
  vim  /etc/samba/smb.conf
  101         security = user
  263 [pub]   
  264         comment = public
  265         path = /pub
  266         browseable = yes
  267         writable = yes
  268 
  269 [soft]
  270         comment = software
  271         path = /soft
  272         browseable = yes
  273         writable = yes
3）添加samba用户
  smbpasswd   -a    aa
  smbpasswd   -a    f1
  pdbedit  -L    查看samba用户
4）重启服务  测试
  service  smb  restart
  service  nmb  restart
测试      f1 登录     
    windows 界面登录 
	    CMD   net  use  *   /del    删除连接缓存
	    aa  登录
```

## SSH安全登录（必会）

```
联机加密工具   非对称钥匙对加密
默认（不用改）：   安装	openssh
				开机自启 service  sshd restart
配置文件     vim  /etc/ssh/sshd.config

远程连接
  ssh    root@192.168.2.251  

网络复制  scp   
  scp   root@192.168.2.140:/root/httpd-2.2.29.tar.gz    /root     下载文件 
  scp  hello.list   root@192.168.2.140:/root/      上传文件
  scp   -r   root@192.168.2.140:/etc/     /root/    下载目录
  scp  -r   /etc   root@192.168.2.140:/root/      上传目录 
SSH密钥登录
   ssh-keygen -t  rsa -P ''   (必须要写)
   -P  表示密码
   cd .ssh  进入自动生成的隐藏目录
   cp  id_rsa.pub   authorized_keys  必须要写（文件49行要求）
   chmod 600    authorized_keys
客户端:
  下载私钥      登录测试
  设置 /etc/ssh/sshd_config  禁止使用密码登录（慎用！！）
  66 PasswordAuthentication no
  重启sshd服务
  service  sshd restart
```

## lamp环境搭建

```
1配置yum源
mount /dev/sr0 /media
 vim /etc/yum.repos.d/CentOS-Media.repo 
[c6-media] 
name=CentOS-$releasever - Media
baseurl=file:///media/   * 修改为光盘挂载点
gpgcheck=0
enabled=1  * 改为1意为启用
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
2）剪切/etc/yum.repos.d/CentOS-Base.repo
  mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
3）依次安装gcc、gcc-c++
 yum -y install gcc  gcc-c++
```

```
关闭防火墙 和 selinux
setup    或
iptables  -F
iptables  -X
iptables  -Z
vim /etc/selinux/config
	SELINUX=disabled
```

```
复制源码包 解压缩
mv  lamp    /lamp
vim   tar.sh
    cd /lamp
    /bin/ls *.tar.gz > ls.list
     	for TAR in `cat ls.list`
     do
    		/bin/tar -zxf $TAR
     done
    /bin/rm ls.list
    
chmod  777  tar.sh
```

./tar.sh    查看磁盘空间（产看安装软件有没有足够的空间）

### 安装辅助软件包

```
安装libxml2
yum -y install python-devel			必须安装

 cd /lamp/libxml2-2.9.1
 ./configure --prefix=/usr/local/libxml2/
 make 
 make install
 
 yum  install  -y  libxml2-devel	如果报错，安装此包后再尝试安装
```

```
安装libmcrypt
cd /lamp/libmcrypt-2.5.8
 ./configure --prefix=/usr/local/libmcrypt/
 make 
 make install
```

```
安装libltdl
cd /lamp/libmcrypt-2.5.8/libltdl
 ./configure --enable-ltdl-install
 make
 make install
```

```
安装mhash
cd /lamp/mhash-0.9.9.9
./configure 
make
make install
```

```
安装mcrypt
cd /lamp/mcrypt-2.6.8
LD_LIBRARY_PATH=/usr/local/libmcrypt/lib:/usr/local/lib  \
./configure --with-libmcrypt-prefix=/usr/local/libmcrypt
make
make install
```

```
安装zlib
cd /lamp/zlib-1.2.3			
./configure
 make
 make install
```

```
安装libpng
 cd /lamp/libpng-1.2.31
 ./configure --prefix=/usr/local/libpng
 make
 make install
```

```
安装jpeg6
 mkdir /usr/local/jpeg6	
 mkdir /usr/local/jpeg6/bin
 mkdir /usr/local/jpeg6/lib
 mkdir /usr/local/jpeg6/include
 mkdir -p /usr/local/jpeg6/man/man1
 ###目录必须手工建立
  cd /lamp/jpeg-6b
 ./configure --prefix=/usr/local/jpeg6/ --enable-shared --enable-static
 make	
 make install
```

```
安装freetype
 cd /lamp/freetype-2.3.5
./configure --prefix=/usr/local/freetype/
 make
 make install
```

### 安装APACHE

```
cp  -r  /lamp/apr-1.4.6  /lamp/httpd-2.4.7/srclib/apr
cp  -r  /lamp/apr-util-1.4.1  /lamp/httpd-2.4.7/srclib/apr-util

cd /lamp/pcre-8.34  
./configure && make && make install

 cd /lamp/httpd-2.4.7
 ./configure --prefix=/usr/local/apache2/ --sysconfdir=/usr/local/apache2/etc/ --with-included-apr --enable-so --enable-deflate=shared --enable-expires=shared --enable-rewrite=shared
 make
 make install
 
 启动服务
 /usr/local/apache2/bin/apachectl start
ps  aux | grep httpd
netstat –tlun | grep :80

测试  打开浏览器   192.168.2.251   有 IT works

设置开机自启动
vim  /etc/rc.local
/usr/local/apache2/bin/apachectl start
```

```
安装ncurses
yum -y install ncurses-devel
cd /lamp/ncurses-5.9
./configure --with-shared --without-debug --without-ada --enable-overwrite
make 
make install
```

```
#安装cmake和bison
yum -y install cmake
yum -y install bison
```

### MySQL服务

```
安装服务
yum -y install ncurses-devel
yum -y install cmake
yum -y install bison

 groupadd mysql
 useradd -g mysql mysql
 
 cd /lamp/mysql-5.5.48
cmake  -DCMAKE_INSTALL_PREFIX=/usr/local/mysql    -DMYSQL_UNIX_ADDR=/tmp/mysql.sock  -DEXTRA_CHARSETS=all   -DDEFAULT_CHARSET=utf8    -DDEFAULT_COLLATION=utf8_general_ci    -DWITH_MYISAM_STORAGE_ENGINE=1   -DWITH_INNOBASE_STORAGE_ENGINE=1    -DWITH_MEMORY_STORAGE_ENGINE=1  -DWITH_READLINE=1    -DENABLED_LOCAL_INFILE=1   -DMYSQL_USER=mysql  -DMYSQL_TCP_PORT=3306
make  &&  make  install

----------------------------------------------------------

配置服务
cd /usr/local/mysql/
chown -R mysql .
chgrp -R mysql .
#修改mysql目录权限
/usr/local/mysql/scripts/mysql_install_db --user=mysql
#创建数据库授权表，初始化数据库
chown -R root .
chown -R mysql data
#修改mysql目录权限

cp support-files/my-medium.cnf /etc/my.cnf
#复制mysql配置文件

二次授权
/usr/local/mysql/scripts/mysql_install_db --user=mysql

-------------------------------------------------

启动MySQL服务：
1.用原本源代码的方式去使用和启动mysql
/usr/local/mysql/bin/mysqld_safe --user=mysql &
2.重启以后还要生效:
vim /etc/rc.local
/usr/local/mysql/bin/mysqld_safe --user=mysql &
3.设定mysql密码
/usr/local/mysql/bin/mysqladmin -uroot password 123456
	清空历史命令 	history  -c

 /usr/local/mysql/bin/mysql -u root -p 
 mysql> \s    查看配置
 mysql> quit  退出
```

### 安装PHP

```
yum -y install "libtool*"

cd /lamp/php-7.0.7
./configure --prefix=/usr/local/php/ --with-config-file-path=/usr/local/php/etc/ --with-apxs2=/usr/local/apache2/bin/apxs  --with-libxml-dir=/usr/local/libxml2/ --with-jpeg-dir=/usr/local/jpeg6/ --with-png-dir=/usr/local/libpng/ --with-freetype-dir=/usr/local/freetype/ --with-mcrypt=/usr/local/libmcrypt/   --with-mysqli=/usr/local/mysql/bin/mysql_config --enable-soap --enable-mbstring=all --enable-sockets  --with-pdo-mysql=/usr/local/mysql --with-gd   --without-pear

make   &&  make  install

-------------------------------------------------------
生成php.ini
mkdir /usr/local/php/etc/
cp /lamp/php-7.0.7/php.ini-production /usr/local/php/etc/php.ini  

vim /usr/local/apache2/etc/httpd.conf
 AddType application/x-httpd-php .php .phtml 
 AddType application/x-httpd-php-source .phps
 
  重启Apache服务：/usr/local/apache2/bin/apachectl stop
				  /usr/local/apache2/bin/apachectl start
				  
vim /usr/local/apache2/htdocs/test.php    
 	<?php
		phpinfo();
 ?>
 
 测试  浏览器   192.168.2.43/test.php
```

```
添加环境变量
vim  /etc/profile

export PATH="/usr/local/php/bin:$PATH"
export PATH="/usr/local/mysql/bin:$PATH"
export PATH="/usr/local/apache2/bin:$PATH"

source  /etc/profile

php -v
mysql -u root -p
apachectl  -v
```

### 收尾

```
安装openssl

yum -y install openssl-devel   必须安装
cd /lamp/php-7.0.7/ext/openssl
mv config0.m4 config.m4                否则报错：找不到config.m4
/usr/local/php/bin/phpize 
./configure --with-openssl --with-php-config=/usr/local/php/bin/php-config 
make
make install

vim  /usr/local/php/etc/php.ini
722  extension_dir = "/usr/local/php/lib/php/extensions/no-debug-zts-20151012/"
#打开注释，并修改
extension="openssl.so";
apachectl  stop
apachectl  start
```

```
安装phpMyAdmin
cp -r /lamp/phpMyAdmin-4.1.4-all-languages /usr/local/apache2/htdocs/phpmyadmin
cd /usr/local/apache2/htdocs/phpmyadmin
cp config.sample.inc.php config.inc.php
vim config.inc.php
//$cfg['Servers'][$i]['auth_type'] = 'cookie';
$cfg['Servers'][$i]['auth_type'] = 'http';

测试  浏览器 192.168.2.43/phpmyadmin/index.php
root
123456
```

### 安装memcache服务

```
1. Linux下安装操作：
	1.1 #安装memcache扩展模块
		
	unzip  pecl-memcache-php7.zip
        cd  pecl-memcache-php7
        /usr/local/php/bin/phpize
       ./configure --with-php-config=/usr/local/php/bin/php-config
        make && make install

       修改/usr/local/php/etc/php.ini
       extension_dir = "/usr/local/php/lib/php/extensions/no-debug-zts-20151012/"
       extension="memcache.so";
       #重启apache，通过浏览器 在phpinfo中可以找到这个模块
 
       1.2 #安装缓存服务 memcached-1.4.4-3.el6.i686.rpm

       mount /dev/sr0 /mnt/cdrom/     挂载ISO镜像文件
       yum -y install memcached 
       useradd memcache    添加memcache用户
       memcached -d -m 128 -l 127.0.0.1 -p 11211 -u memcache  启动服务
       chkconfig memcached on  设置开机自启动
```
## Apache服务器配置

```
一	简介
		1	www：world  wide  web	
			http	协议：	超文本传输协议
			HTML语言：	超文本标识语言
		2	URL：统一资源定位		协议+域名：端口+网页文件名
				http://www.sina.com.cn:80/admin/index.html
二	安装
	1、lamp源码安装	               
	2、二进制包安装    yum安装
			httpd
			mysql
			mysql-server		
			php
			php-devel
			php-mysql

三	相关文件
	apache配置文件
		源码包安装：/usr/lcoal/apache2/etc/httpd.conf
				   /usr/local/apache2/etc/extra/*.conf	    
		二进制包安装：/etc/httpd/conf/httpd.conf
	默认网页保存位置：
		源码包：/usr/local/apache2/htdocs/
		二进制包安装：/var/www/html/
	日志保存位置
		源码包：/usr/local/apache2/logs/
		二进制包： /var/log/httpd/
         二进制包默认使用日志处理程序   /var下都会轮替   源码包才				   需要设置
日志处理：
  1日志切割  apache自带日志里面自带日志切割
  2日志轮替  linux自带日志管理logrorate.conf	
          加入/usr/local/apache2/logs/access_log{
                                daily
                                rotate  30
						}
          logrotate -f /etc/logrotate.conf

             所有日志都要进行日i www! he htdocs bu yiyang! 
志轮替
 
	四	配置文件
vim /root/.bashrc
   alias sta=’/usr/local/apache2/bin/apachectl start’
   alias sto=’/usr/local/apache2/bin/apachectl stop’

source /root/.bashrc
		注意：apache配置文件严格区分大小写
		1	针对主机环境的基本配置

	31	ServerRoot		apache主目录          
	52	Listen			监听端口              
		LoadModule		加载的相关模块

		User
		Group			用户和组
		ServerAdmin		管理员邮箱
		ServerName		服务器名（没有域名解析时，使用临时解析）
		ErrorLog "logs/error_log	错误日志
		CustomLog "logs/access_log" common		正确访问日志
		DirectoryIndex index.html index.php		默认网页文件名,优先级顺序
		Include  etc/extra/httpd-vhosts.conf		子配置文件中内容也会加载生效
		
		2	主页目录及权限  

			DocumentRoot "/usr/local/apache2//htdocs"          
				主页目录

			<Directory "/usr/local/apache2//htdocs">                 
				#Directory关键字定义目录权限

				Options Indexes FollowSymLinks                    
					#options 
						None：没有任何额外权限
						All： 所有权限
						Indexes：浏览权限（当此目录下没有默认网页文件时，显示目录内容）
						FollowSymLinks：准许软连接到其他目录
				AllowOverride None
					#定义是否允许目录下.htaccess文件中的权限生效
						None：.htaccess中权限不生效
						All：文件中所有权限都生效
						AuthConfig：文件中，只有网页认证的权限生效。

				Require all granted	访问控制列表
403错误   				404错误  网页找不见

		3	目录别名  扩展网站目录，增加服务器   
子配置文件名	etc/extra/httpd-autoindex.conf

Alias /www/ "/usr/local/apache2//www/"
       
<Directory "/usr/local/apache2//www">
    			Options Indexes MultiViews			
    			AllowOverride None
    			Require all granted                   	
</Directory>
 
mkdir /usr/local/apache2/www/
浏览器测试 http://192.168.1.253/www/
4	虚拟主机		
		1）分类
	      基于IP的虚拟主机: 一台服务器，多个IP，搭建多个网站
	  	 基于端口的虚拟主机：一台服务器，一个ip，搭建多个网站，每个网络使用不同端口访问
	     基于名字的虚拟主机：	一台服务器，一个ip，搭建多个网站，每个网站使用不同域名访问
		2）步骤：
			①	解析试验域名
				www.sina.com
				www.sohu.com
C:\WINDOWS\system32\drivers\etc\hosts		
	②	规划网站主目录
		/share/sina--------------www.sina.com
		/share/sohu ------------ www.sohu.com
	③ 	修改配置文件
		vim  /usr/local/apache2/etc/httpd.conf
			Include etc//extra/httpd-vhosts.conf
				#打开虚拟主机配置文件
vim /usr/local/apache2/etc/extra/httpd-vhosts.conf
<Directory "/share/sina">
 		   Options Indexes
 		   AllowOverride None
Require all granted 
</Directory>

<Directory "/share/sohu">
 		   Options Indexes
 	 		   AllowOverride None
  		  Require all granted 
</Directory>

<VirtualHost 192.168.150.253>
#注意，只能写ip
 		   ServerAdmin webmaster@sina.com
				#管理员邮箱
 		   DocumentRoot "/share/sina"
				#网站主目录
   	  	   ServerName www.sina.com
				#完整域名
    		   ErrorLog "logs/sina-error_log"
				#错误日志
    		   CustomLog "logs/sina-access_log" common
				#访问日志
</VirtualHost>

<VirtualHost 192.168.150.253>
 		   ServerAdmin webmaster@sohu.com
 		   DocumentRoot "/share/sohu"
 		   ServerName www.sohu.com
  		  ErrorLog "logs/sohu.com-error_log"
  		  CustomLog "logs/sohu.com-access_log" common
</VirtualHost>

5	rewrite	重写功能    		
在URL中输入一个地址，会自动跳转为另一个
		1）域名跳转	www.sina.com  ------>  www.sohu.com
			开启虚拟主机，并正常访问 

[root@localhost ~]# vim /usr/local/apache2/etc/httpd.conf
LoadModule rewrite_module modules/mod_rewrite.so
#打开重写模块，记得重启apache
		修改配置文件，使sina目录的.htaccess文件生效
[root@localhost etc]# vim /usr/local/apache2/etc/extra/httpd-vhosts.conf

<Directory "/share/sina">
 		   Options Indexes FollowSymLinks
  		   AllowOverride All
  		   Require all granted 
 		</Directory>

vim  /share/sina/.htaccess
RewriteEngine on
	#开启rewrite功能
RewriteCond %{HTTP_HOST} www.sina.com
			把以www.sina.com	开头的内容赋值给HTTP_HOST变量
RewriteRule  .*   http://www.sohu.com
	.*  输入任何地址，都跳转到http://www.sohu.com

2)网页文件跳转 
vim  /share/sina/.htaccess
RewriteEngine on
RewriteRule index(\d+).html index.php?id=$1
	#输入index(数值).html时，跳转到index.php文件，同时把数值当成变量传入index.php
```

### Apache执行停止改名

```
命令别名  alias

vim /root/.bashrc

alias sto='/usr/local/apache2/bin/apachectl stop'

alias sta='/usr/local/apache2/bin/apachectl start'

source  /root/.bashrc

sto

sta
```

### 目录别名 扩容   增加服务目录

```
1）建立扩容目录

mkdir  /usr/local/apache2/www/

2）修改主配置文件 

vim  /usr/local/apache2/etc/httpd.conf

453 Include etc//extra/httpd-autoindex.conf

3）修改子配置文件

vim  /usr/local/apache2/etc/extra/httpd-autoindex.conf

     29 Alias /www/ "/usr/local/apache2/www/"
     30 
     31 <Directory "/usr/local/apache2/www/">
     32     Options Indexes
     33     AllowOverride None
     34     Require all granted
     35 </Directory>

4）重启服务  测试
sto
sta
测试  192.168.2.251/www/
```

### 虚拟主机

```
步骤：1）域名解析       文件解析
C:\Windows\System32\drivers\etc\hosts   添加下面两个网址
192.168.2.251  www.sina.com
192.168.2.251  www.sohu.com

2）网站目录规划  (想显示内容要在里面创建index.html ，里面写入中文会乱码，英文正常显示)
mkdir  -p  /share/sina/
mkdir   /share/sohu/

3）修改主配置文件
vim  /usr/local/apache2/etc/httpd.conf
465 Include etc//extra/httpd-vhosts.conf

4）修改子配置文件
vim  /usr/local/apache2/etc/extra/httpd-vhosts.conf
     23 <Directory "/share/sina/">
     24     Options Indexes
     25     AllowOverride None
     26     Require all granted
     27 </Directory>
     28     
     29 <Directory "/share/sohu/">
     30    Options Indexes 
     31    AllowOverride None
     32    Require all granted
     33 </Directory>
     35 <VirtualHost 192.168.2.251>
     36     ServerAdmin webmaster@sina.com
     37     DocumentRoot "/share/sina/"
     38     ServerName www.sina.com
     39     ErrorLog "logs/sina-error_log"
     40     CustomLog "logs/sina-access_log" common
     41 </VirtualHost>
     42 
     43 <VirtualHost 192.168.2.251>
     44     ServerAdmin webmaster@sohu.com
     45     DocumentRoot "/share/sohu/"
     46     ServerName www.sohu.com
     47     ErrorLog "logs/sohu-error_log"
     48     CustomLog "logs/sohu-access_log" common
     49 </VirtualHost>

5）重启服务  测试

sto
sta
测试    www.sina.com    www.sohu.com


```

### 重定向

```
rewrite  重写/重定向
www.sina.com  ->  www.sohu.com  

1）修改主配置文件
vim  /usr/local/apache2/etc/httpd.conf
147 LoadModule rewrite_module modules/mod_rewrite.so

2）修改子配置文件
vim /usr/local/apache2/etc/extra/httpd-vhosts.conf
     23 <Directory "/share/sina/">
     24     Options Indexes FollowSymLinks
     25     AllowOverride All
     26     Require all granted
     27 </Directory>

3）建立权限文件.htaccess
vim  /share/sina/.htaccess
      1 RewriteEngine on
      2 RewriteCond %{HTTP_HOST} www.sina.com
      3 RewriteRule .*  http://www.sohu.com
   .* 代表任意所有，要从上往下看，这里.*代表sina.com
4） 重启服务  测试
    sto 
    sta 
测试  www.sina.com   -> www.sohu.com
```

### 网页跳转

```
1）修改权限文件
vim /share/sina/.htaccess
      1 RewriteEngine on
      2 RewriteRule index(\d+).html  index.php?id=$1

2）建立index.php文件

vim /share/sina/index.php
      1 <?php
      2         echo "hello rewrite!";
      3 ?>

3）重启服务测试
sto
sta
测试  www.sina.com/index5.html
```
## LNMP环境搭建-Nginx服务

### LNMP环境搭建

```
准备工作： 恢复初始化安装      设置IP      关闭防火墙   
                   配置光盘yum源
安装步骤：1.解压缩  
     tar   -zxvf   lnmp1.2-full.tar.gz
     		ls
2.进入解压目录
 	cd    lnmp1.2-full
3.安装
	./install.sh  lnmp

环境目录和文件：

    Nginx 目录: /usr/local/nginx/
    MySQL 目录 : /usr/local/mysql/
    MySQL数据库所在目录：/usr/local/mysql/var/
    PHP目录 : /usr/local/php/
    PHPMyAdmin目录 : /home/wwwroot/default/phpmyadmin/ 
    默认网站目录 : /home/wwwroot/default/
    Nginx日志目录：/home/wwwlogs/
    
    Nginx主配置文件：/usr/local/nginx/conf/nginx.conf
    MySQL配置文件：/etc/my.cnf
    PHP配置文件：/usr/local/php/etc/php.ini

管理命令
lnmp   start  |  restart  | stop   | status
lnmp  nginx  start  |  stop  |  restart   |  status

配置文件  
ulimit  -a 
ulimit   -n   51200
    检查nginx配置文件语句错误
    /usr/local/nginx/sbin/nginx -t
    
    平滑重启nginx进程
    pkill -HUP nginx
```

### 虚拟主机

```
1）域名解析  文件解析

C:\Windows\System32\drivers\etc\hosts

    192.168.2.251    www.sina.com
    192.168.2.251    www.sohu.com

2）网站目录规划
mkdir   /home/wwwroot/sina/
mkdir   /home/wwwroot/sohu/
vim  /home/wwwroot/sina/index.html
vim  /home/wwwroot/sohu/index.html

3）修改配置文件
vim  /usr/local/nginx/conf/nginx.conf

 66         listen 80; 

4）建立虚拟主机文件
vim  /usr/local/nginx/conf/vhost/v.conf

      1 server {
      2         listen 80;
      3         server_name www.sina.com;
      4         index index.html  index.htm  index.php;
      5         root /home/wwwroot/sina/;
      6 
      7         include enable-php.conf;
      8 }
      9 server {
     10         listen 80;
     11         server_name www.sohu.com;
     12         index index.html  index.htm  index.php;
     13         root /home/wwwroot/sohu/;
     14 
     15         include enable-php.conf;
     16 }

5） 重启服务  测试
pkill -HUP nginx  
测试  www.sina.com   www.sohu.com
```

### 列表页显示

```
vim /usr/local/nginx/conf/vhost/v.conf

 加入  autoindex   on;      开启列表页显示功能 (两个里面都加)

cd /home/wwwroot/sina      mv index.html a.html（需要改名）
```

### 状态监控模块添加

```
vim  /usr/local/nginx/conf/vhost/v.conf

      9 server {
     10         listen 80;
     11         server_name www.sohu.com;
     12         index index.html  index.htm  index.php;
     13         root /home/wwwroot/sohu/;
     14         location /nginx_status{
            	stub_status on;
            	access_log  off;
           		}
     15         include enable-php.conf;
     16 }

测试   www.sohu.com/nginx_status
```

### rewrite重写、重定向

```
域名跳转   www.sina.com  ->  www.sohu.com

vim  /usr/loca/nginx/conf/vhost/v.conf
    server
            {
                    listen       80;
                    server_name www.sina.com;
                    index index.html index.htm index.php;
                    root  /home/wwwroot/sina;
    
                    if ($http_host = www.sina.com) {
                            rewrite  (.*)  http://www.sohu.com  permanent;
                    }
    		}
重启服务  测试
pkill -HUP nginx
测试   www.sina.com  -> www.sohu.com
```

### 网页文件跳转

```
1）修改配置文件
vim  /usr/local/nginx/conf/vhost/v.conf
      1 server {
      2         listen 80;
      3         server_name www.sina.com;
      4         index index.html  index.htm  index.php;
      5         root /home/wwwroot/sina/;
      6         rewrite  index(\d+).html  /index.php?id=$1 last;
      7         include enable-php.conf;
      8 }       

2）建立 php文件
vim /home/wwwroot/sina/index.php
      1 <?php
      2         echo "hi Nginx rewrite";
      3 ?>

3）重启服务 测试
pkill -HUP nginx
测试  www.sina.com/index5.html
```

### 代理负载均衡（反向代理）

```
准备工作：   S   192.168.2.251      Nginx       负载均衡               S1   192.168.2.102    Nginx       网站解析
            S2    192.168.2.191   Nginx       网站解析

实验步骤：
1）修改S 192.168.2.251  配置文件
vim /usr/local/nginx/conf/nginx.conf
     63 upstream myweb1 {
     64         server 192.168.2.102:80;
     65         server 192.168.2.191:80;
     66 }       
     67 server {
     68         listen 80;
     69         server_name www.sohu.com;
     70         location / {
     71         proxy_pass http://myweb1;
     72         proxy_next_upstream http_500 http_502 http_503 error timeout invalid_header;
     73         proxy_set_header Host $host; 
     74         proxy_set_header X-Forwarded-For $remote_addr; 
     75 }                
     76 } 
     77 }

2）修改S1 192.168.2.102        关闭虚拟主机
关闭虚拟主机： cd /usr/local/nginx/conf/    vim nginx.conf            
 # include vhost/*.conf;   检测这个有没有注释或者删了就行
 
cd   /home/wwwroot/default/ 
vim index.html
S111111111111

3）修改S1 192.168.2.191        关闭虚拟主机
cd   /home/wwwroot/default/ 
vim index.html
S2222222222

4） 重启S 服务   测试
pkill -HUP nginx  
测试   www.sohu.com      刷新   S1    S2
```
## Shell 编程

### shell的作用和历史

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml\wps1EA7.tmp.jpg)

```
Shell的作用 -- 命令解释器，“翻译官”
vim  /etc/shells      shell文件(里面有好多不同的shell)
```

### shell 常用功能

```
自动补全    Tab
命令历史     history 
  history  -w   同步历史命令/写入隐藏文件 
  history  -c    清除历史记录 
  
!n：执行历史记录中的第n条命令
!str：执行历史记录中以“str”开头的命令
vim   /etc/profile  
 48 HISTSIZE=1000
 为使用频率较高的复杂命令行设置简短的调用名称
存放位置：~/.bashrc
vim   /root/.bashrc

查看命令别名
格式：alias  [别名]

设置命令别名
执行：alias  别名='实际执行的命令'
alias   ls='ls  -lha'    设置之后需要执行此文件，否则不生效
ls  

取消已设置的命令别名 
格式：unalias  别名
unalias   ls

输入重定向
man  wc
wc   <   install.log

输出重定向
ls  >   bak.list
ls  -l  >>  bak.list

标准错误输出
lss  2>  bak.list
lss  2>>  bak.list

重定向标准输出和标准错误
ls   &>   /dev/null          黑洞设备文件（空设备文件）
lss  >>  a.txt   2>&1         重定向标准错误
2>&1  算是一个判断条件，如果前面正确，则无用，如果错误，就会把错误信息也输入到文件里
```

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml\wps728F.tmp.jpg)

```
管道符    |
    netstat -an | grep ESTABLISHED | wc -l     统计与服务器的连接数量
```

### Shell变量的应用

```
Shell变量的种类

用户自定义变量：由用户自己定义、修改和使用

环境变量：由系统维护，用于设置用户的Shell工作环境，只有极少数的变量用户可以修改

预定义变量：Bash预定义的特殊变量，不能直接修改

位置变量：通过命令行给程序传递执行参数

变量的赋值与引用

定义新的变量
变量名要以英文字母或下划线开头，区分大小写
格式：变量名=变量值

查看变量的值
格式：echo  $变量名

查看所有变量：set

清除变量
unset 变量名

定义变量                                                
Var=lamp
echo  ${var}3.0

""    ''   ``      单引号 双引号 反引号 对比
    DAY=xingqier
    echo $DAY         显示xingqier
    echo  "$DAY"	  显示xingqier
    echo '$DAY'		  显示$DAY
    echo `$DAY`		  执行 xingqier  （必须是命令。否则报错）
    
    unset DAY
    DAY=ls
    echo `$DAY`  执行ls

环境变量赋值
设置变量的作用范围
格式：export   变量名...
      export  变量名=变量值  [...变量名n=变量值n]

查看环境变量
	 env 	或	export

清除用户定义的变量
格式：unset   变量名
    命令执行时查找顺序
    1、以相对/绝对路径执行
    2、由alias找到的执行
    3、bash内部命令执行
    4、按$PATH路径执行
    
 环境变量PS1
    echo $PS1
    		\d  日期	\t  时间（24）	\T时间（12）
    		\H  完整主机名		\h  简写主机名
    		\u  用户名			\v  bash版本
    		\w  完整目录		\W  最后一个目录
    		\#   执行了第几个命令	\$  提示符
    PS1=‘[\u@\h  \W  \t  #\#]\$’
    
  常见的环境变量：
   $USER 、$LOGNAME
   $UID 、 $SHELL 、$HOME
   $PWD、 $PATH 
   $PS1、$PS2
   
查看环境变量
[root@localhost ~]# echo $PATH
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
    
    预定义变量
  表示形式如下
    $#：命令行中位置参数的个数
    $*：所有位置参数的内容
    $?：上一条命令执行后返回的状态，当返回状态值为0时表示执行正常，非0值表示执行异常或出错
    $$：当前所在进程的进程号
    $!：后台运行的最后一个进程号
    $0：当前执行的进程/程序名
 命令执行时查找顺序
    1、以相对/绝对路径执行
    2、由alias找到的执行
    3、bash内部命令执行
    4、按$PATH路径执行

    [root@localhost ~]# bash 
    [root@localhost ~]# echo  $0  $$
    bash 5887
    [root@localhost ~]# exxit
    bash: exxit: command not found
    [root@localhost ~]# echo $?
    127
    [root@localhost ~]# exit
    exit
    [root@localhost ~]# echo $? 
    0
    ；  命令顺序执行。
    && 前后命令的执行存在逻辑与关系，只有&&前面的命令执行成功后，它后面的命令才被执行。
    ||   前后命令的执行存在逻辑或关系，只有||前面的命令执行失败后，它后面的命令才被执行。

    通配符与特殊符号
    通配符
    		*	任意多个
    		？	任意一个
    		[]	括号内任一个	[^0-9]非数字
    		
    rm   -rf  *
    rm   -rf  ?.??
    touch   1.txt  2.txt  3.txt
    rm -rf  [1-9].* 
    
    特殊符号
    		\	转义符
    		&	后台
    		！	非
```

```
4.数值变量的运算
计算整数表达式的运算结果
格式：expr  变量1   运算符  变量2  ...[运算符 变量n]
expr的常用运算符
加法运算：+
减法运算： -
乘法运算： \*
除法运算： /
求模（取余）运算： % 

Bash程序并不适合进行强大的数学运算，例如小数或指数运算的，一般只能进行简单的整数运算
对Shell变量进行数值运算时，更多的时候是用于脚本程序的过程控制，如控制程序的循环次数
在expr命令的使用格式中，变量与运算符间是有空格的，可以同时使用多个运算符、多个变量
由于星号“*”作为Bash环境中的通配符使用，因此乘法运算符需要使用“\*”的特殊形式（转义字符）

#!/bin/bash
read -p "please input num1:" -t 30  test1
read -p "input num2:" -t 30  test2
declare -i sum=”$test1+$test2”
echo “num1 +  num2 = $sum”
```

### shell脚本的概念

```
    Shell脚本
    1.用途：完成特定的、较复杂的系统管理任务
    2.格式：集中保存多条Linux命令，普通文本文件
    3.执行方式：按照预设的顺序依次解释执行

[root@localhost ~]# vi repboot.sh
    #!/bin/bash
    # To show usage of /boot directory and mode of kernel file.
    echo "Useage of /boot: "
    du -sh /boot
    echo "The mode of kernel file:"
    ls -lh /boot/vmlinuz-*
    [root@localhost ~]# chmod a+x repboot.sh 

    运行Shell脚本程序
    
    1.直接执行具有“x”权限的脚本文件
     例如：./repboot.sh 
    2.使用指定的解释器程序执行脚本内容
     例如：bash  repboot.sh
    3.通过source命令（或 . ）读取脚本内容执行
     例如：souce  repboot.sh  或  .  hello.sh 
```

### shell脚本应用实例

```
    示例1：
    每周五17:30清理FTP服务器的公共共享目录
     检查 /var/ftp/pub/ 目录，将其中所有子目录及文件的详细列表、当时的时间信息追加保存到 /var/log/pubdir.log 日志文件中，然后清空该目录

    [root@localhost ~]# vi /opt/ftpclean.sh
    #!/bin/bash
    date  >>  /var/log/pubdir.log
    ls  -lhR  /var/ftp/pub  >>  /var/log/pubdir.log
    rm  -rf  /var/ftp/pub/*
    
    [root@localhost ~]# crontab -e
    30 17 * * 5  /opt/ftpclean.sh
    
    chmod  +x   /opt/ftpclean.sh

```

```
    示例2:
    每隔3天时间3：30对数据库目录做一次完整备份
     统计 /usr/local/mysql/var 目录占用的空间大小、查看当前的日期，并记录到临时文件 /tmp/dbinfo.txt 中， 将 /tmp/dbinfo.txt 文件、/usr/local/mysql/var 目录进行压缩归档，备份到/opt/dbbak/目录中， 备份后的包文件名中要包含当天的日期信息， 最后删除临时文件/tmp/dbinfo.txt

    [root@localhost ~]# vi /opt/dbbak.sh
    #!/bin/bash
    DAY=`date +%Y%m%d`
    SIZE=`du -sh /usr/local/mysql/var`
    echo "Date: $DAY" >> /tmp/dbinfo.txt
    echo "Data Size: $SIZE" >> /tmp/dbinfo.txt
    mkdir  /opt/dbbak
    cd /opt/dbbak
    tar -zcPf mysqlbak-${DAY}.tar.gz /usr/local/mysql/var /tmp/dbinfo.txt
    rm -f /tmp/dbinfo.txt
    
    [root@localhost ~]# crontab -e
    30 3 */3 * *  /opt/dbbak.sh
    
    chmod  +x  /opt/dbbak.sh
```

### shell 显示写法

```
从键盘输入内容为变量赋值
格式： read  [-p  "信息"]  变量名
结合不同的引号为变量赋值
双引号 “ ” ：允许通过$符号引用其他变量值
单引号 ‘ ’ ：禁止引用其他变量值，$视为普通字符
反撇号 ` ` ：将命令执行的结果输出给变量
下面就是一个简单计算器的运用写法：
  read -p "input first num: " var1
  read -p "input +-*/ : " var
  read -p "input second num: " var2

  v=`echo " $var1 $var $var2 "|bc`
  echo "$var1 $var $var2 = $v"
```
## Shell 正式编程

### 正则表达式

```
1  ^
#只匹配行首
2  $
#只匹配行尾
3  *
#匹配0个或者多个单字符
4  []
#只匹配[]内字符，可以是一个单字符，也可以是字符序列，可以使用*表示[]内字符序列范围，如用[1-5]代替[12345]
5  \
#只用来屏蔽一个元字符的特殊含义
6  .
#只匹配任意单字符
7  pattern\{n\}
#匹配n次pattern
8  pattern\{n,\}
#匹配n次以上pattern
9  pattern\{n,m\}
#匹配n到m次pattern
11  ^只允许在一行的开始匹配字符或单词
^d   筛选出以d开头的文件属性
12  ^ $
#匹配空行
13  ^.$
#匹配包含一个字符的行
14  kkk$
#匹配以kkk结尾的所有字符
15  \*\.pas
#匹配以*.pas结尾的所有字符或文件
16  a\{2\}b
#a出现两次，aab     
17  a\{4,\}b
#a至少出现4次，aaaab,aaaaab ..
18  a\{2,4\}
#a出现次数范围2-4次
19  [0-9]\{3\}\.[0-9]\{3\}\.[0-9]\{3\}\.[0-9]\{3\}
#匹配所有ip地址
20   cal 显示日历
```

### shell编程中常用的命令

```
行提取命令

grep	选项：		-v     -n 	-i
	
	grep  "[^a-z]oo"  aa  (文件名)
	oo前不是小写字母的行匹配。	注意：和开头没有关系
	grep  “\.$”	aa
	匹配以.结尾的行
	grep  "^[^A-Za-z]"  aa
	匹配不以字母开头的行		注意：所有字母不能这样写   A-z
	grep  “^$”  aa
	匹配空白行
	grep  "oo*" aa
	匹配最少一个o
	grep  “g.*d” aa
	匹配g开头，d结尾，中间任意字符	gd
```

```
列提取命令

awk  '条件 ｛动作｝'
	last | awk '{printf $1 "\t" $3 "\n"}'
	提取last显示结果的第一和第三列

last | grep "[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}"|awk '{printf $1 "\t" $3 "\n"}'
在last中提取包含ip的行，在行中提取第一和第三列

awk内置变量		FS  指定分隔符
more /etc/passwd | awk 'BEGIN {FS=":"} {printf $1 "\t" $3 "\n"}'
读取passwd文件，以":"为分隔符，截取第一和第三列
BEGIN	在截取前使分隔符生效。如果没有BEGIN，那么第一行自定义的分隔符不生效

1  last  > file
#把last命令结果保存在file文件中
2  awk ‘{print $0 “\n”}' file 
#查找出file文件中的每1列
3  awk '{print $1"\t"$7 “\n”}' file
#查找出file文件中的第1列和第7列

cut	

cut  -d  “分隔符”  -f  提取列   文件名

more /etc/passwd | grep "/bin/bash" | cut -d ":" -f 1,3
提取passwd文件中可以登录的用户的用户名和UID
```

```
输出命令

echo  -e  “输出内容”

	-e  识别格式化打印内容

	echo  -e  “1\t2\t3”	打印tab键

	echo  -e   "\e[1;31m  this is red text \e[0m"	输出红色字体
					\e[  格式
					1;31m  指定颜色
					0m	恢复颜色（重置）
30m=黑色，31m=红色，32m=绿色，33m=黄色，34m=蓝色，35m=洋红，36m=青色，37=白色
```

### shell条件测试操作

```
条件测试操作

test命令
用途：测试特定的表达式是否成立，当条件成立时，命令执行后的返回值为0，否则为其他数值

格式：test  条件表达式   [   条件表达式   ]

常见的测试类型
测试文件状态
字符串比较
整数值比较
逻辑测试

测试文件状态
格式：[  操作符  文件或目录  ]

常用的测试操作符
-d：测试是否为目录（Directory）
-e：测试目录或文件是否存在（Exist）
-f：测试是否为文件（File）
-r：测试当前用户是否有权限读取（Read）
-w：测试当前用户是否有权限写入（Write）
-x：测试当前用户是否可执行（Excute）该文件
-L：测试是否为符号连接（Link）文件

[root@localhost ~]# [  -d /etc/vsftpd  ]
[root@localhost ~]# echo $?
0
[root@localhost ~]# [  -d /etc/hosts  ]
[root@localhost ~]# echo $?
1

[root@localhost ~]# [ -e /media/cdrom ] && echo "YES"
YES 
[root@localhost ~]# [ -e /media/cdrom/Server ] && echo "YES”
[root@localhost ~]#

整数值比较

格式：[  整数1  操作符  整数2  ]

常用的测试操作符
-eq：等于（Equal）
-ne：不等于（Not Equal）
-gt：大于（Greater Than）
-lt：小于（Lesser Than）
-le：小于或等于（Lesser or Equal）
-ge：大于或等于（Greater or Equal）


[root@localhost ~]# who | wc -l
5
[root@localhost ~]# [ `who | wc -l` -le 10 ] && echo "YES"
YES 

[root@localhost ~]# df -hT | grep "/boot" | awk '{print $6}'
18% 
[root@localhost ~]# BootUsage=`df -hT | grep "/boot" | awk '{print $6}' | cut -d "%" -f 1`
[root@localhost ~]# echo $BootUsage
18
[root@localhost ~]# [ $BootUsage -gt 95 ] && echo "YES" 


字符串比较

格式：[  字符串1  ==  字符串2 ]  
	  [  字符串1  !=  字符串2 ]
      [  -z  字符串 ]

常用的测试操作符
==：字符串内容相同  
  !!  ==两边不能有空格！！！【】两边必须有空格！！！
!=：字符串内容不同，! 号表示相反的意思
-z：字符串内容为空

[root@localhost ~]# read -p "Location：" FilePath
Location：/etc/inittab
[root@localhost ~]# [ $FilePath == "/etc/inittab" ] && echo "YES"
YES 

[root@localhost ~]# [ $LANG != "en.US" ] && echo $LANG
zh_CN.UTF-8 
```

```
逻辑测试

格式：[  表达式1  ]  操作符  [  表达式2  ]  ... 

常用的测试操作符
-a或&&：逻辑与，“而且”的意思
#前后两个表达式都成立时整个测试结果才为真，否则为假 
-o或||：逻辑或，“或者”的意思
#操作符两边至少一个为真时，结果为真，否则结果为假
!：逻辑否
#当指定的条件不成立时，返回结果为真

[root@localhost ~]# echo $USER
root
[root@localhost ~]# [ $USER != "teacher" ]  &&  echo "Not teacher"
Not teacher
[root@localhost ~]# [ $USER = "teacher" ]  ||  echo "Not teacher"
Not teacher
```

### if 条件语句(流程控制) 

```
if条件语句 -- 单分支
应用示例：
如果/boot分区的空间使用超过80%，输出报警信息
如果测试 / 目录的话  将 /boot 换成 /$  就可以了 

#!/bin/bash
RATE=`df -hT | grep "/boot" | awk '{print $6}' | cut -d "%" -f1 `
if  [  $RATE  -gt  80  ]
then
    echo "Warning,DISK is full!"
fi
```

```
if条件语句 -- 双分支
应用示例：
判断mysqld是否在运行，若已运行则输出提示信息，否则重新启动mysqld服务

#!/bin/bash
TEST=`/usr/bin/pgrep mysqld `
if  [  “$TEST”  != “”  ]
    then
        echo  "mysqld service is running."
    else
        /etc/init.d/mysqld  restart
fi
```

```
if条件语句 -- 多分支

相当于if语句嵌套，针对多个条件执行不同操作
if  条件测试命令1  ;  then
    命令序列1
elif  条件测试命令2  ;  then
    命令序列2
elif  ...
else
    命令序列n
fi
```

### for 循环语句

```
应用示例1：
依次输出3条文字信息，包括一天中的“Morning”、“Noon”、“Evening”字串

[root@localhost ~]# vi showday.sh
#!/bin/bash
for TM in "Morning" "Noon" "Evening"
do
    echo "The $TM of the day."
done 

[root@localhost ~]# sh showday.sh
The Morning of the day.
The Noon of the day.
The Evening of the day 
```

```
应用示例2：
对于使用“/bin/bash”作为登录Shell的系统用户，检查他们在“/opt”目录中拥有的子目录或文件数量，如果超过100个，则列出具体个数及对应的用户帐号

 #!/bin/bash
DIR="/opt"
LMT=100
ValidUsers=`grep "/bin/bash" /etc/passwd | cut -d ":" -f 1`
for UserName  in  $ValidUsers
do
    Num=`find $DIR -user $UserName | wc -l`
    if  [  $Num  -gt  $LMT  ]  ;  then
         echo "$UserName have $Num files."
    fi
done 
```

### while 循环语句

```
重复测试指定的条件，只要条件成立则反复执行对应的命令操作

应用示例1：
批量添加20个系统用户帐号， 用户名依次为“stu1”、“stu2”、……、“stu20”
这些用户的初始密码均设置为“123456” 
--stdin  表示转换成键盘输入
expr  是shell计算器（bc）里的加法

#!/bin/bash
i=1
while  [  $i  -le  20  ]
do
    useradd stu$i
    echo "123456" | passwd --stdin stu$i &> /dev/null
    i=`expr $i + 1`
done 

应用示例2：
批量删除上例中添加的20个系统用户帐号

#!/bin/bash
i=1
while  [  $i  -le  20  ]
do
    userdel -r stu$i
    i=`expr $i + 1`
done 
```

### case 多重分支语句

```
根据变量的不同取值，分别执行不同的命令操作

应用示例1：
编写脚本文件 mydb.sh，用于控制系统服务mysqld
当执行 ./mydb.sh  start 时，启动mysqld服务
当执行 ./mydb.sh  stop 时，关闭mysqld服务
如果输入其他脚本参数，则显示帮助信息

#!/bin/bash 
case   $1   in
    start)
        echo  "Start MySQL service."
        ;;
    stop)
        echo  "Stop MySQL service."
        ;;
    *)
        echo  "Usage：$0  start|stop"
        ;;
esac


应用示例2：
提示用户从键盘输入一个字符，判断该字符是否为字母、数字或者其它字符，并输出相应的提示信息 

#!/bin/bash
read  -p  "Press some key, then press Return:“  KEY
case  "$KEY“  in
  [a-z]|[A-Z])
      echo "It's a letter."
      ;;
  [0-9])
      echo "It's a digit."
      ;;
  *)
      echo "It's function keys、Spacebar or other keys. "
esac
```

### shell 函数应用

```
Shell函数概述
在编写Shell脚本程序时，将一些需要重复使用的命令操作，定义为公共使用的语句块，即可称为函数
合理使用Shell函数，可以使脚本内容更加简洁，增强程序的易读性，提高执行效率

定义新的函数
function 函数名 {
　　命令序列
} 

函数名() {
　　命令序列
}


调用已定义的函数
函数名

向函数内传递参数
函数名  参数1  参数2  ...


应用示例：
在脚本中定义一个加法函数，用于计算2个整数的和
调用该函数计算（12+34）、（56+789）的和

#!/bin/bash
adder() {
    echo `expr $1 + $2`
}
adder 12 34
adder 56 789

[root@localhost ~]# bash adderfun.sh
46
845 
```
## 额外

	#传输文件的方法
	yum -y install lrzsz
	rz

	#下载东西
	wget 网址
##监控工具 dstat和vmstat
	编译安装：

		工具下载地址：wget http://dstat.sourcearchive.com/downloads/0.7.2-2/dstat_0.7.2.orig.tar.gz

		yum安装：
	yum -y install dstat 
写的比较详细的博客
	http://blog.csdn.net/smooth00/article/details/78623728
    
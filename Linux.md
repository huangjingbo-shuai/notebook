## linux的目录结构
![目录结构示意图](./.assets_IMG/Linux/image-1.png)
![一切皆文件](./.assets_IMG/Linux/image-2.png)
## linux常见的帮助命令
1. man获取帮助信息（简单记为有问题找那个男人）
   ![alt text](./.assets_IMG/Linux/image-3.png)
+ ls：查询当前目录表
![ls](./.assets_IMG/Linux/image-4.png)
+ man ls：![man ls](./.assets_IMG/Linux/image-5.png)
2. help
+ 只能显示shell内置的命令
## 开关机命令
1. 基本语法：![alt text](./.assets_IMG/Linux/image-6.png)
2. 选项：![alt text](./.assets_IMG/Linux/image-7.png)
## 文件目录类命令
1. pwd：显示当前工作目录的局对路径（从根目录开始写起）
2. ls -a:显示当前目录的隐藏文件
3. cd：进入某一文件夹
4. ls -l：显示完整信息（long）![alt text](./.assets_IMG/Linux/image-8.png)前面是文件类型及权限  第二列是连接数  第三为作者  第四列为大小（bate）  时间   文件（夹）名字
5. 最最常用的切换命令：cd
   + ![cd常用语法](./.assets_IMG/Linux/image-9.png)
   + 注意使用cd使用的绝对路径和相对路径，熟练使用相对路径会节省大量时间
   + cd..：退回上一路径
   + cd（直接回车）或者cd ~：回到家目录
   + cd -:切换到上一次使用的目录
## 创建目录和删除目录
1. mkdir：创建目录（/继续创建文件夹）注意，要一级一级创建，要一次性创建则需要使用递归创建目录命令：mkdir -p。
2. rmdir：删除空目录
## 创建空文件命令
1. touch：`touch 1.txt`
## 复制文件
1. cp：`cp 1.txt /1/2/3`
2. cp -r：递归复制文件夹
3. 复制文件中所有的内容需要加*
4. \cp：不询问，直接覆盖
## 删除文件（夹）命令
1. rm：询问删除
2. rm -f：不询问直接删除
3. rm -r：递归删除文件夹中的所有内容（询问）
4. rm -rf：直接干掉文件夹，不询问
5. rm -rv：显示指令的详细执行过程
6. mv `文件名` `地址` `重命名文件名`
## 查看文件内容命令
1. cat `文件名`：查看文件内容
2. cat -n `文件名`：带上行号（有回车则是换行）![查看文件示意图](./.assets_IMG/Linux/image-10.png)
3. more `文件名`：全屏按页显示，操作之后可通过若干快捷键查看内容
4. less `要查看的文件`：效率高，可以根据文件的大小来显示内容，推荐使用，功能比more强大
5. q：离开这个程序
## 查看文件头
1. head -`n` `文件名`：显示文件的n行内容
## 查看文件尾
1. tail -`n` `文件名`：查看尾部，通常用来查看文件后面的错误信息
2. tail -f `文件名`：挂起，持续观察文件，实时监控
3. tail `文件`：查看后10行内容
## 打印信息，输出命令（同c++）
1. echo
![alt text](./.assets_IMG/Linux/image-11.png)
![alt text](./.assets_IMG/Linux/image-12.png)
![alt text](./.assets_IMG/Linux/image-13.png)
## 覆盖与追加
1. `ll > 1.txt`：覆盖`1.txt`中的内容
2. `ll >> 1.txt`：在`1.txt`后追加内容
## 硬链接、软链接不常用
## history
1. history：查看所有历史命令
2. ![alt text](./.assets_IMG/Linux/image-14.png)
3. 或者按上下查看，且方便使用
# 使用VI和VIM编辑器
## 什么是VI和VIM编辑器
![alt text](./.assets_IMG/Linux/image-15.png)
在linux没有交互界面的环境中，可以利用VI或者VIM对一些文本来进行编辑和修改。
## 一般模式
+ 进入编辑界面无法使用鼠标，也叫一般模式
1. 输入两下gg：移动到页面开头
2. `shift+g`：到末尾（实际上是大写的G）
3. 如果想到某一行，则键盘输入`100+shift+g`，（不会显示，只需要操作就行）
4. 两次大写的ZZ：`ZZ`退出编辑器模式
5. yy：复制
6. p：粘贴
7. dd：删除全部内容
## 编辑模式
1. 在一般模式中按下`ℹ或者a或o`可以进入编辑模式（光标为a前，i后，o为下一行）。其他命令不推荐使用，不符合我们的编辑习惯故舍弃
`注意：在linux终端系统中，按下鼠标滚轮中键可以快速粘贴`
## 命令模式
1. 先按下键盘`esc`键，进入命令模式，在编辑模式中输入`：`通常我们用`wq`命令来保存并推出。
需要注意的是，`q`一般表示退出，而`wq`一般表示写入并退出。
1. 查找：`：/+内容`
2. 替换，`%s/内容/后内容/`。一般用的比较少。
3. 查找过后会高亮，通过`：noh`回车取消高亮。
4. 取消行号：`set nonu`
5. 有的时候修改文档的权限会不够，故通常在命令后面加一个`！`。
# VIM的三种模式的切换
![alt text](./.assets_IMG/Linux/image-16.png)
# 文件查找
1. 文件名查找
## 语法
	find 搜索路径 -name "文件名关键词"
***例子***
	find / -name "passwd"
	find / -name "ifcfg-*"
2. 文件内容查找
## 语法
	grep -参数 要查找的目录范围
	# 参数
	-n 显示查找结果所在行号
	-R 递归查找目录下的所有文件
***例子***
	grep aries /etc
	grep aries /etc/passwd
# 系统管理
1. 静态查看系统进程 
    + 使用命令`ps -aux`   ![alt text](./.assets_IMG/Linux/image-18.png)
2. 时时查看系统进程
    + 使用`top`命令，上下反动，q退出
3. 关闭进程
    + `kill 进程id`
4. 强制关闭进程（谨慎使用）
    + `kill -9 进程id`
# 系统软件管理
## 压缩解压缩
1. 压缩语法：`tar -zcvf 压缩后文件名 被压缩文件`
2. 解压语法：`tar -zxvf 解压缩文件名 -C 解压后文件所在目录`。实际上`-C`指的是解压后的文件存放的位置
## rpm软件（类似windows中的.exe程序）
1. 安装rpm软件
    语法：`rpm -ivh xxx.rpm`
2. 查看系统中是否一安装过该rpm软件
    语法：`rpm -qa 软件名`
3. 卸载rpm软件
    语法：`rpm -e 软件名`
## yum
+ 说明：（yum基于rpm实现的，提供了除了rpm的安装软件、卸载软件等功能以外还有，自动查找、下载软件并自动处理软件的彼此之间的依赖关系，下载并安装依赖包。）
1. 列出所有可以安装的软件包。语法：`yum list`
2. 安装软件。语法：`yum install -y 软件名`
3. 卸载软件。语法：`yum remove 软件名`
4. 查找软件包。语法：`yum search all 软件名`
# dpkg命令的使用
+ 说明：管理系统的里deb包,可以对其安装、卸载、deb打包、deb解压等操作，与之相关apt-get工具可以在线下载 deb包 安装。
## 参数：
1. `-i：安装软件包； `
2. `-r：删除软件包； `
3. `-P：删除软件包的同时删除其配置文件； `
4. `-L：显示于软件包关联的文件； `
5. `-l：显示已安装软件包列表； `
6. `--unpack：解开软件包； `
7. `-c：显示软件包内文件列表； `
8. `--confiugre：配置软件包。`
***
***
1. 安装软件。命令：`dpkg -i deb文件名`
2. 列出与该包相关联的文件。命令：`dpkg -L 包名`
3. 显示包的版本。命令`dpkg -l 包名`
4. 移除软件（保留配置）。命令:`dpkg -r 包名`
实例:dpkg -r zabbix-release
5. 移除软件（不保留配置）命令:`dpkg -P 包名`
实例:dpkg -P zabbix-release
6. 查找包的详细信息。命令:`dpkg -s 包名`
实例:dpkg -s zabbix-release
7. 列出deb包的内容。命令:`dpkg -c 包名.deb 列出 deb 包的内`
实例:dpkg -c zabbix-release
8. 解开deb包的内容
命令：`dpkg –unpack 包名.deb 解开 deb 包的内容`
9. 搜索所属的包内容
命令：`dpkg -S keyword 搜索所属的包内容`
10. 配置包
`dpkg –configure package 配置包`
注意：详细教程可以打开[https://blog.csdn.net/qq_35078688/article/details/119382985?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522172092295616800215080288%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=172092295616800215080288&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-119382985-null-null.142^v100^pc_search_result_base8&utm_term=dpkg&spm=1018.2226.3001.4187](./.assets_IMG/Linux/)
# 重点！！！！！！！！！！！
***
***
***
# 基于SSH的远程登陆方法的说明
说明：Secure Shell(./.assets_IMG/Linux/SSH) 是由 IETF(./.assets_IMG/Linux/The Internet Engineering Task Force) 制定的建立在应用层基础上的安全网络协议。
## 安全机制
1. 口令级别：只要你知道自己帐号和口令，就可以登录到远程主机。但安全度不高，容易受到攻击或者连接到错误的主机。
2. 密钥级别：你必须为自己创建一对密钥，并把公钥放在需要访问的服务器上。
## SSH的安装
+ SSH分为客户端和服务器两个部分
+ 可以输入`dpkg -l | grep ssh`确认或者检查电脑上是否安装了客户端和服务器。
+ 如果只是想远程登陆别的机器只需要安装客户端（Ubuntu默认安装了客户端），如果要开放本机的SSH服务就需要安装服务器。
+ 安装：
    1. `sudo apt-get install openssh-client`(./.assets_IMG/Linux/客户端)
    2. `sudo apt-get install openssh-server`(./.assets_IMG/Linux/服务器)
## 启动服务器的SSH服务
1. 首先要确认ssh-server是否已经启动。在终端输入命令：`ps -e | grep ssh`![alt text](./.assets_IMG/Linux/image-19.png)出现sshd，代表ssh-server已经启动了。
    + 如果没有启动，可以使用以下命令启动。`sudo /etc/init.d/ssh start `
2. 停止和重启ssh服务的命令分别为：
    + `sudo /etc/init.d/ssh stop `#server停止ssh服务 
    + `sudo /etc/init.d/ssh restart  `#server重启ssh服务
## 一、口令登陆
1. 口令登录非常简单，只需要一条命令，命令格式为： ssh 客户端用户名@服务器ip地址  
eg:`ssh ldz@192.168.0.1`
2. 如果需要调用图形界面程序可以使用 -X 选项
eg:`ssh -X ldz@192.168.0.1`
3. 如果客户机的用户名和服务器的用户名相同，登录时可以省略用户名。eg:`ssh 192.168.0.1`
4. 还要说明的是，SSH服务的默认端口是22，也就是说，如果你不设置端口的话登录请求会自动送到远程主机的22端口。我们可以使用 -p 选项来修改端口号，比如连接到服务器的1234端口：`ssh -p 1234 ldz@192.168.0.1`。
5. 客户机必须要知道服务器的ip地址。可以在服务器端电脑上利用 `ifconfig`命令查看该机的ip地址。
6. 如果是第一次登录远程主机，系统会给出下面提示：
   ![alt text](./.assets_IMG/Linux/image-55.png)
7. 意思是，该远程主机的真实性无法确定，其公钥指纹为 SHA256:FFobshqrGOachj7Xp4LsJ9+xkNBlyyOe8ZIPl7K+qQI，确定想要继续连接吗？
输入yes即可。这时系统会提示远程主机被添加到已知主机列表。
8. 然后会要求我们输入远程主机的密码，输入的密码正确就可以成功登录了。命令提示符会修改为远程主机的提示符，现在开始，终端中输入的命令都将在服务器中执行。
## 二、公钥登陆
1. 每次登录远程主机都需要输入密码是很不方便的，如果想要省去这一步骤，可以利用密钥对进行连接，还可以提高安全性。
2. 在本机生成密钥对。使用`ssh-keygen -t rsa`。然后根据提示一步步的按enter键即可（其中有一个提示是要求设置私钥口令passphrase，不设置则为空，这里看心情吧，如果不放心私钥的安全可以设置一下），执行结束以后会在 /home/当前用户 目录下生成一个 .ssh 文件夹,其中包含私钥文件 id_rsa 和公钥文件 id_rsa.pub。
3. 将公钥复制到远程主机中。使用`ssh-copy-id`命令将公钥复制到远程主机。`ssh-copy-id`会将公钥写到远程主机的` ~/ .ssh/authorized_key `文件中.
4. `ssh-copy-id ldz@192.168.0.1`
5. 经过以上两个步骤，以后再登录这个远程主机就不用再输入密码了。
## 三、SSH的高级应用
***使用远程主机不中断的跑程序***
+ 当我们利用ssh在远程主机上跑程序的时候，只要关闭了终端就会中断ssh连接，然后远程主机上正在跑的程序或者服务就会自动停止运行。我们可以利用`nohup + 需要运行的程序` 使运行的程序在切断ssh连接的时候仍然能够继续在远程主机中运行。`nohup`即`no hang up`(./.assets_IMG/Linux/不挂起)。
+ 除此之外还有很多远程操作应用，包括 数据传输、端口操作(./.assets_IMG/Linux/将不加密的网络连接绑定到ssh端口实现间接加密) 等等，可以参考柚子皮大神的博客：[https://blog.csdn.net/pipisorry/article/details/52269785](./.assets_IMG/Linux/)

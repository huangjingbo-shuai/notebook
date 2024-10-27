### 碰到一打开项目文件终端就自动进入最初的虚拟环境的解决办法
如果碰到一打开项目文件终端就自动进入最初的虚拟环境，且这个虚拟环境不是自己想要的虚拟环境的时候，解决办法很简单：
1. json里加一句就不会一打开就进去上一次的虚拟环境了，语句如下：
2. "python.terminal.activateEnvironment": false
3. 注意，加JSON语句的时候，这里要小心上一句是否添加了 `,`
### windows系统上配置视觉环境
1. 安装显卡驱动，最好安装高版本，支持的固件版本更多，不容易出现问题
2. 安装Anaconda，注意，安装的时候这里要选择all user，其实不选也没事，这是要所有的电脑用户都可以使用。![alt text](.assets_IMG/yolov11/image.png)
3. 安装cuda。`https://developer.nvidia.com/cuda-toolkit-archive`进入这个网址，下载11.1.1 Octorbor 2020 版本的cuda。
4. 打开Anaconda的prompt命令行窗口，创建一个新的conda环境`conda create -n yolov11 python=3.8`,这里一般只指定python版本，如果用它默认的版本的话会存在一些问题，虽然Anaconda会一次性安装完所有的依赖，但是有些历史版本不完整，导致后期要使用的一些历史版本会非常混乱。
5. 安装pytorch。注意，一定要进入环境后安装`https://pytorch.org/get-started/previous-versions/`进入网站下载对应cuda版本的pytorch，这里下载的cuda版本是1.11.1，所以对应的pytorch版本应该为![alt text](.assets_IMG/yolov11/image-1.png)
6. 安装cudNN。这里的cudnn可以随意下载版本，最新版本的也可以，下载好了以后，把这三个文件夹移动到cuda安装的Computing\Toolkit\CUDA\11.1下面，替换掉之前的。
![alt text](.assets_IMG/yolov11/image-2.png)
![alt text](.assets_IMG/yolov11/image-3.png)
7. 安装完成。
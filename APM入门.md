## Ubuntu搭建APM固件编译环境
### 下载源码
1. `git clone https://github.com/ArduPilot/ardupilot.git`，这句命令可以下载APM的源码，但是我发现这句命令有的时候不管用，硬是得从github官网上复制HTTP链接再 `git clone`才行，具体为什么还不知道，但最好手动复制一下，这样不会出错。
2. 下载完之后

        + cd ardupilot
        + git submodule init
        + git submodule update
    + 在执行git submodule update时若出现报错没有更新完毕子模块，则继续执行该命令，直至更新完毕。如果一次不成功就多次，如果下载慢的话就反复切换`proxy`和`unproxy`
### 配置编译环境
1. 在ardupilot目录下执行下面的命令安装环境：`Tools/environment_install/install-prereqs-ubuntu.sh -y`,如果一次不成功就多次尝试，知道最后底下出现`OK`字样。
2. 配置成功后执行：`. ~/.profile`
### 编译固件
1. 编译固件前，要配置编译的固件的目标硬件
我这里使用的是pix2.4.8飞控，所以使用fmuv3的固件，配置如下：`./waf configure --board fmuv3`
2. 如果出现报错`缺少waf子模块`，用命令`git submodule update --init --recursive --force`后解决。
3. 如果出现报错`ChibiOS build requires g++ version 10.2.1 or later, found 5.4.1`,![alt text](.assets_IMG/APM入门/image.png)原因是我们用源码下载依赖的时候下的版本就没有达到`10.2.1`以上，这地方很坑，我一直以为是`gcc`的版本问题，导致我不断地找gcc的问题，但其实不是，这里是用的ARM专用的工具链。而一开始我们下载的这个工具链的版本就是不对的，需要手动下载，链接是`https://developer.arm.com/downloads/-/gnu-rm`,这是ARM已经弃用的一个网站，但是可以从上面下载大于10.2.1的
`gcc-arm-none-eabi`版本。最好用命令`sudo tar -xvf gcc-arm-none-eabi-10.x-linux.tar.bz2 -C /opt`解压到opt路径下,然后最关键的一步设置环境变量。进入`~/.bashrc`中，最后一行加上`export PATH=/opt/gcc-arm-none-eabi-10.x/bin:$PATH`,这里注意路径一定要找正确，应该是有这些文件的文件夹目录下：![alt text](.assets_IMG/APM入门/image-1.png)。
4. 完成操作以后再运行`arm-none-eabi-gcc --version`，此时arm-none-eabi-gcc的版本已经成功换成高版本的了。![alt text](.assets_IMG/APM入门/image-2.png)
5. 最后正常编译车/船部分，`./waf rover`，成功
        ![alt text](.assets_IMG/APM入门/image-3.png)
### 仿真
1. 以无人车/船为例，在ardupilot/Rover目录下执行：`../Tools/autotest/sim_vehicle.py -f rover`，执行完毕后会弹出下面的页面，然后打开地面站就可以链接到仿真的无人车了。
![alt text](.assets_IMG/APM入门/image-4.png)
2. 仿真水下机器人的话，就在ardupilot/ArduSub目录下执行：`sim_vehicle.py -L RATBeach --out=udp:0.0.0.0:14550 --map --console`。执行成功后：![alt text](.assets_IMG/APM入门/image-5.png)
3. gazebo安装：参考连接：`https://blog.csdn.net/qq_38768959/article/details/131133686`
        + ```sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'```
        + `wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -`
        + `sudo apt update`
        + `sudo apt install gazebo9 libgazebo9-dev`
        + 安装成功后执行：`gazebo --verbose`
        + 如果能弹出空的gazebo界面，说明安装成功
4. 装gazebo插件：
        + `git clone https://github.com/khancyr/ardupilot_gazebo`
        + `cd ardupilot_gazebo`
        + `mkdir build`
        + `cd build`
        + `cmake ..`
        + `make -j4`
        + `sudo make install`
        + 成功后如下：![alt text](.assets_IMG/APM入门/image-6.png)
5. 修改环境变量：
        + `source /usr/share/gazebo/setup.sh`
        + `export GAZEBO_MODEL_PATH=~/ardupilot_gazebo/models:${GAZEBO_MODEL_PATH}`
        + `export GAZEBO_MODEL_PATH=~/ardupilot_gazebo/models_gazebo:${GAZEBO_MODEL_PATH}`
        + `export GAZEBO_RESOURCE_PATH=~/ardupilot_gazebo/worlds:${GAZEBO_RESOURCE_PATH}`
        + `export GAZEBO_PLUGIN_PATH=~/ardupilot_gazebo/build:${GAZEBO_PLUGIN_PATH}`
        + 然后启动仿真：`gazebo --verbose worlds/iris_arducopter_runway.world`,可以看到弹出一个gazebo页面，里面有一架无人机（如果没有无人机，检查环境变量设置），但此时的无人机无法连接地面站![alt text](.assets_IMG/APM入门/image-7.png)
### 仿真连接mavros
+ 参考博客`https://blog.csdn.net/qq_38768959/article/details/131133686`
### 多机仿真
1. 参考博客`https://blog.csdn.net/qq_38768959/article/details/131133686`


## APM实物上手
+ 想顺利的用APM固件控制电机有以下需要注意的点
1. APM的电机通道是通道1和通道3，而PX4的电机通道是通道1和通道2
2. 校准APM的时候涉及到遥控器的校准，但是在QGC地面站上校准APM的遥控器似乎有bug，只要碰到右下角或者左下角的校准就没反应了，根本无法校准。解决办法是用`Mission Planner`地面站校准遥控器，而其他的不变可以继续用QGC地面站，因为MP地面站太丑了，不想用。MP地面站的安装见下面的教程。
3. 进入地面站以后，要先点击右上角的连接，和飞控建立连接。
4. 连接好飞控以后点击初始设置，找到必选硬件，找到遥控器校准，即可进行遥控器的校准。
5. 校准好遥控器以后还是打开QGC地面站观察，尝试解锁，发现报错`Hardware safety switch`，这是因为APM固件在解锁之前需要按下飞控上的物理按钮，在飞控的右边有一个小按钮。为了以后的使用方便，我们把这个选项禁用掉。在QGC地面站的参数搜索`BRD_SAFETYDEFLT`，将这个参数改成0即可。![alt text](.assets_IMG/APM入门/image-9.png)，![alt text](.assets_IMG/APM入门/image-10.png)
6. 禁用完以后发现还是解锁不了，报错`Arm: Throttle (RC3) is not neutral`，这是因为还要配置遥控器油门通道（RC3）的中立值参数，将参数`RC3_TRIM`改成1500。在某些需要偏中立油门的模式（如中性点在中间）中，RC3_TRIM会设置为1500（通常是中间位置）。
7. 再解锁，成功启动电机。
8. 注意，此时要注意观察电机的正反转，以及遥控器的通道设置，检查修改即可，这个很简单。

## MP地面站的安装
1. `Mission Planner`可以在官网免费下载，`https://firmware.ardupilot.org/Tools/MissionPlanner/MissionPlanner-latest.msi`
2. 下载好以后解压，注意要提取到一个文件夹里，不然根目录下就会多出几百个文件和文件夹，非常乱。
3. 解压好以后需要安装Mono包。`sudo apt update`，`sudo apt install mono-complete`，运行以下命令查看是否安装成功`mono --version` ，![alt text](.assets_IMG/APM入门/image-8.png)
4. 进入`/MissionPlanner-latest`文件夹，运行指令`mono MissionPlanner.exe`,即可打开MP地面站
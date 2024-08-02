## ros通讯进阶
1. 初始化  
    + 作用：ROS初始化函数
    + 参数：
    1. argc：（命令行参数的数量）封装实参个数（n+1），因为第一个传入的是文件自身
    2. argv：封装参数的数组
    3. name：为节点命名（需要保证唯一性）
    4. options：节点启动选项
    5. 返回值：void。该函数的返回值为空
    + 使用：
            
        1. argc与argv的使用
            + 如果按照ros中的特定格式传入实参，那么ros可以加以使用，比如用来设置全局参数，给节点重命名....
        2. options的使用
            + 节点名称需要保证唯一，会导致一个问题：同一个节点不能重复启动。  ros中当有重名的节点启动时，之前的节点会被关闭。
            + 需求：特定场景下名需要一个节点多次启动且能正常运行，怎么办？!
            + 解决：设置启动项    
            ros::init_options::AnonymousName
            创建ros节点时，会在用户自定义的节点名称后缀随机数，从而避免重名问题。
2. 话题与服务相关对象：在话题和服务的相关对象一般由Nodeandle（节点句柄）创建。  
    + 作用：创建发布者对象
    + 模板：被发布的消息的类型
    + 参数：
        1. 话题名称
        2. 队列长度
        3. latch（可选）  如果设置为true，会保存发布方的最后一条消息，并且新的对象连接到发布方时，发布方会将这条消息发送给订阅者。
    + 使用：
        + latch设置为true的作用？
        + 以静态地图发布为例
          
          方案一：可以使用固定频率发送地图数据，但是效率低；
          
          方案2：可以将地图对象的 latch 设置为true，并且发布方值发送一次数据，每当订阅者连接时，就可以将地图数据发送给订阅者（只发送一次），这样提高了数据的发送效率。
          ![alt text](.assets_IMG/ros/image-19.png)
3. 回旋函数（回头函数）  
在ROS程序中，频繁使用了ros::spin()和ros::spinOnce（）两个回旋函数，可以用于处理回调函数。
    + spinOnce（）  
    brief 处理一轮回调
    一般应用场景:
    在循环体内，处理所有可用的回调函数

        ROSCPP_DECL void spinOnce();
        ![alt text](.assets_IMG/ros/image-20.png)
        执行一次后向后运行
    + spin（）
    brief 进入循环处理回调 

        ROSCPP_DECL void spin();
        ![alt text](.assets_IMG/ros/image-21.png)
        进入循环体内就不会退出的，spin（）后的代码就不会运行到了。
    + 相同点：二者都用于处理回调函数
    + 不同点：ros::spin()是进入了循环执行回调函数，而ros::spinOnce()只会执行一次回调函数（没有循环），在ros::spin()后的语句不会执行到，而ros::spinOnce()后的语句可以执行。
4. 时间
    + 时刻：获取时刻，或者设置指定时刻。
    + 需求：演示时间相关操作（获取当前时刻 + 设置指定时刻）
    + 实现：
        1. 准备（头文件、节点初始化、NodeHandle创建）

                setlocale(LC_all,"");
                ros::init(argc,argv,"hello_time");
                ros::NodeHandle nh;//注意，这一步必须要实现，否则会导致时间API调用失败（在NodeHandle中会初始化时间操作）
        2. 获取当前时刻
        now函数会将当前时刻封装并返回
        当前时刻：now被调用执行的那一刻
        参考系：1970年1月1日 00：00：00
        ros::Time right_now=ros::Time::now();
        ROS——INFO("当前时刻:%.2f",right_now.toSec());
        toSec函数可以把逝去的时间转换成以秒为单位的数值（以1970年为参考）
        toSec函数可以把逝去的时
        ROS——INFO("当前时刻:%.d",right_now.sec());
        sec函数返回的是整数类型
        3. 设置指定时刻
        + ros::Time t1(20,312345678);
        ![alt text](.assets_IMG/ros/image-22.png)
    + 持续时间
    1. 实现
        + 创建持续时间对象
            1. ros::Duration du(4.5);
                du.sleep();
        + 休眠
        ![alt text](.assets_IMG/ros/image-23.png)
    + 持续时间与时刻运算
    1. 需求：一直程序开始运行的时刻和程序运行的时间，求运行结束时的时刻
    2. 实现：
        + 获取开始执行的时刻
        + 模拟运行的时间（N秒）
        + 计算结束时刻 = 开始 + 持续时间
        ![alt text](.assets_IMG/ros/image-24.png)
        + 时刻与时刻的运算
        ![alt text](.assets_IMG/ros/image-25.png)
        + 持续时间和持续时间的运算
        ![alt text](.assets_IMG/ros/image-26.png)
        + 注意：
        1. 时刻与持续时间可以执行加减
        2. 持续时间之间也可以执行加减
        3. 时刻之间值可以相减，不可以相加
    + 设置运行频率
    ![alt text](.assets_IMG/ros/image-27.png)
    + 定时器的使用
    1. 需求：每隔1秒钟，在控制台输出一段文本
    2. 实现：
    + 策略1：ros::Rate()
    + 策略2:定时器
    ![alt text](.assets_IMG/ros/image-31.png)
    说明：
          1. 创建定时器需要调用句柄中的createimer函数来创建，返回值是一个ros::Timer对象
    + 回调函数
    ![alt text](.assets_IMG/ros/image-29.png)
    + 注意：
        1. 创建：nh.createTimer()
        2. 参数1：时间间隔
        3. 参数2：回调函数（时间事件 TimerEvent）
        4. 参数3：是否执行一次
        5. 参数4：是否自动启动（当设置为 false，需要手动调用 timer.start()）
        6. 切记，定时器启动后：使用ros:spin()
    + 节点
    ![alt text](.assets_IMG/ros/image-32.png)
    + 日志
    1. ![alt text](.assets_IMG/ros/image-33.png)
    2. ![alt text](.assets_IMG/ros/image-34.png)
    ### python的通讯进阶
    1. 节点初始化  ![alt text](.assets_IMG/ros/image-35.png)
    2. 创建发布者对象  ![alt text](.assets_IMG/ros/image-36.png)
    3. 回旋函数：python中没有spinOnce，只有spin()
    4. 时间
    + 获取当前时刻： ![alt text](.assets_IMG/ros/image-37.png)
    + 从某个时间值获取时间对象    ![alt text](.assets_IMG/ros/image-38.png)
    + 持续时间：  ![alt text](.assets_IMG/ros/image-39.png)
    + 时间运算：  ![alt text](.assets_IMG/ros/image-40.png)
    + 设置运行频率：![alt text](.assets_IMG/ros/image-41.png)
    + 定时器：  ![alt text](.assets_IMG/ros/image-42.png)
    + 节点的关闭：  ![alt text](.assets_IMG/ros/image-43.png)
      ![alt text](.assets_IMG/ros/image-44.png)
    5. 日志  ![alt text](.assets_IMG/ros/image-45.png)
## ros中的头文件与源文件
本节主要介绍ROS的C++实现中，如何使用头文件与源文件的方式封装代码，具体内容如下:  

设置头文件，可执行文件作为源文件；
分别设置头文件，源文件与可执行文件。
在ROS中关于头文件的使用，核心内容在于CMakeLists.txt文件的配置，不同的封装方式，配置上也有差异。
###  自定义头文件调用
+ 需求:设计头文件，可执行文件本身作为源文件。

流程:

编写头文件；
编写可执行文件(同时也是源文件)；
编辑配置文件并执行。
1. ![alt text](.assets_IMG/ros/image-46.png)  
注意：在 VScode 中，为了后续包含头文件时不抛出异常，请配置 .vscode 下 c_cpp_properties.json 的 includepath属性。`/home/用户/工作空间/src/功能包/include/**`
2. 可执行文件  ![alt text](.assets_IMG/ros/image-47.png)
3. 配置文件  ![alt text](.assets_IMG/ros/image-48.png)
### 自定义源文件调用
+ 需求:设计头文件与源文件，在可执行文件中包含头文件。

流程:

编写头文件；
编写源文件；
编写可执行文件；
编辑配置文件并执行。
1. 头文件  ![alt text](.assets_IMG/ros/image-49.png)/
注意：在 VScode 中，为了后续包含头文件时不抛出异常，请配置 .vscode 下 c_cpp_properties.json 的 includepath属性。`/home/用户/工作空
2. 源文件  ![alt text](.assets_IMG/ros/image-50.png)
3. 可执行文件  ![alt text](.assets_IMG/ros/image-51.png)
4. 配置文件  ![alt text](.assets_IMG/ros/image-52.png)
### python模块导入
1. ![alt text](.assets_IMG/ros/image-53.png)
2. ![alt text](.assets_IMG/ros/image-54.png)
## ros运行管理
### ROS元功能包
![alt text](.assets_IMG/ros/image-55.png)
### ROS节点 运行管理launch文件
1. ![alt text](.assets_IMG/ros/image-56.png)
#### 文件标签launch
![alt text](.assets_IMG/ros/image-57.png)
#### 文件标签node
1.  必选：  ![alt text](.assets_IMG/ros/image-58.png)
2.  可选：  ![alt text](.assets_IMG/ros/image-59.png)
#### 文件标签include
![alt text](.assets_IMG/ros/image-60.png)
#### 文件标签remap
![alt text](.assets_IMG/ros/image-61.png)

![alt text](.assets_IMG/ros/image-62.png)
#### 文件标签param
![alt text](.assets_IMG/ros/image-63.png)

![alt text](.assets_IMG/ros/image-64.png)
#### 文件标签rosparam
![alt text](.assets_IMG/ros/image-65.png)
#### 文件标签group
![alt text](.assets_IMG/ros/image-66.png)
#### 文件标签arg

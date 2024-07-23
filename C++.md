# 函数
## 函数的定义
    + 返回值类型
    + 函数名
    + 参数列表
    + 函数体语句
    + return表达式
1. 语法：![alt text](./.assets_IMG/C++/image.png)
2. ``int add（int num1,int num2）{
    int sum = num1 + num2;
    return sum;
}``
## 函数的调用
+ 函数调用语法：函数名称（参数）
![alt text](./.assets_IMG/C++/image-20.png)
+ 在函数定义的时候，num1和num2并没有真实的数据，只是一个形式上的参数，简称形参。
+ a和b称为 实际参数，简称实参。
+ 当调用函数的是时候，实参的值会传递给形参。
## 值传递
+ 所谓值传递，就是函数调用时实参将数值传入给形参
+ 值传递时，如果形参发生变化，并不会影响实参。
![实例](./.assets_IMG/C++/image-21.png)
![alt text](./.assets_IMG/C++/image-22.png)
## 常见的样式
1. 无参数，无返回
2. 有参数，无返回
3. 无参数，有返回
4. 有参数，有返回
![样式](./.assets_IMG/C++/image-23.png)
## 函数的声明
+ 作用：告诉编译器函数名称及如何调用函数。函数的实际主体可以单独定义。
+ 声明可以写多次，但是定义只能有一次。
+ 声明是为了告诉编译器这个函数存在，不会报错，保证函数的顺利运行。
![声明](./.assets_IMG/C++/image-24.png)
## 函数的分文件编写
+ 作用：让代码结构更加清晰。函数分文件编写一般有4个步骤。
1. 创建后缀名为`.h`的头文件。
2. 创建后缀名为`.cpp`的源文件。
3. 在头文件中写函数的声明。
4. 在源文件中写函数的定义。
![头文件](./.assets_IMG/C++/image-25.png)
![源文件](./.assets_IMG/C++/image-26.png)
5. 在其他源文件中只需要把函数的头文件名称包含进去，就可以调用该函数了。一般在头部写`#include “头文件名称.h”`即可。
# 重要！！！！！！！！！！！！！
***
***
# 指针
## 指针的基本概念
1. 指针的作用：可以通过指针间接访问内存。
    + 内存编号是从0开始记录的，一般用十六进制数字表示
    + 可以利用指针变量保存地址
2. 定义指针
    + 指针定义的语法：数据类型*指针变量。
    + 让指针记录变量a的地址用`&`来实现。
  3. 使用指针
    + 可以通过解引用的方式来找到指针指向的内存。即，指针前加一个 * 代表解引用，找到指针指向的内存中的数据。
4. eg.![示例](./.assets_IMG/C++/image-27.png)
## 指针所占内存空间
1. 提问：指针也是一种数据类型，那么这种数据类型占多少内存空间？
+ 在32位系统下，占4个字节，64位下占8个字节。
## 空指针和野指针
1. 空指针：指针变量指向内存中编号为0的空间。
    + 用途：初始化指针变量。![alt text](./.assets_IMG/C++/image-28.png)
    + 注意：空指针的内存是不可以访问的。原因是，0～255之间的内存是系统占用的，因此不可以访问。
2. 野指针：指针变量指向非法的内存空间。
    +  在程序中，尽量避免出现野指针。
![野指针](./.assets_IMG/C++/image-29.png)
## const修饰指针
1. 常量指针![alt text](./.assets_IMG/C++/image-36.png)
    + 特点是：指针的指向可以修改，但是指针指向的值不可以改。
    + eg：![常量指针](./.assets_IMG/C++/image-31.png)
2. 指针常量![alt text](./.assets_IMG/C++/image-38.png)
    + 特点：指针的指向不可以改，指针指向的值可以改。
    + ![指针常量](./.assets_IMG/C++/image-32.png)
3. 修饰常量![alt text](./.assets_IMG/C++/image-39.png)
    + 特点：指针的指向和指针指向的值都不可以改
    + ![修饰常量](./.assets_IMG/C++/image-35.png)
### 辨别是哪种修饰指针的技巧：看const右侧紧跟着的是指针还是常量，是指针就是常量指针，是常量就是指针常量。
### 指针和数组
+ 作用：利用指针访问数组中的元素
## 指针和函数。作用：利用指针作函数参数，可以修改实参的值。
1. 值传递
2. 地址传递
![alt text](./.assets_IMG/C++/image-40.png)
![alt text](./.assets_IMG/C++/image-41.png)
# 结构体
1. 定义：自定义数据类型，一些类型集合组成的一个类型
2. 语法：`struct 类型名称{ 成员列表 }`注意：定义结构体时`struct`关键字不能省略。
3. 创建结构体变量的方法有三种(创建结构体变量时关键字`struct`可以省略)
    + ![alt text](./.assets_IMG/C++/image-42.png)
    + ![alt text](./.assets_IMG/C++/image-43.png)
    + ![alt text](./.assets_IMG/C++/image-44.png)
4. 结构体变量利用操作符`.`来访问成员
### 结构体数组
+ ![alt text](./.assets_IMG/C++/image-45.png)
## 结构体指针
1. 作用：通过指针访问结构体中的成员
  + ***利用操作符->可以通过结构体指针访问结构体中的成员属性***
2. 操作：
   + 创建学生结构体变量
    ![alt text](./.assets_IMG/C++/image-46.png)
   + 通过指针指向结构体变量
    ![alt text](./.assets_IMG/C++/image-47.png)
   + 通过指针访问结构体变量中的数据
    ![alt text](./.assets_IMG/C++/image-48.png)
    ![alt text](./.assets_IMG/C++/image-49.png)
## 结构体嵌套结构体
1. 定义学生的结构体

![alt text](./.assets_IMG/C++/image-50.png)

2. 定义老师的结构体

![alt text](./.assets_IMG/C++/image-51.png)

3. 创建老师

![alt text](./.assets_IMG/C++/image-52.png)
# 结构体作函数参数
+ ***作用：将结构体作为参数向函数中传递***
+ 传递的方式有两种：
    1. 值传递
    2. 地址传递
## 结构体中const使用场景
![alt text](./.assets_IMG/C++/image-54.png)
### 全局区
+ C++中在程序运行前分为全局区和代码区
+ 代码区特点是共享和只读
+ 全局区中存放全局变变量、静态变量、常量
+ 常量区中存放const修饰的全局常量和字符串常量
## 栈区
+ 注意事项：
1. 不要返回局部变量的地址

2. 栈区的数据由编译器管理开辟和释放
## 引用
### 引用的基本使用
1. 作用：给变量起别名
2. 语法：数据类型 &别名 = 原名
3. 优点：可以简化指针修改实参
## 菱形继承
菱形继承概念：  
1. 两个派生类继承同一个基类
2. 又有某个类同时继承这两个派生类
3. 这种继承被称为菱形继承，或者钻石继承  
![alt text](.assets_IMG/C++/image-96.png)
![alt text](.assets_IMG/C++/image-97.png)
4. 菱形继承问题：

        1. 羊继承了动物的数据，驼同样继承了动物的数据，当草泥马使用数据时，就会产生二义性。
        2. 草泥马继承自动物的数据继承了两份，其实我们应该清楚，这份数据我们只需要一份就可以，当菱形继承时，两个父类拥有相同的数据，需要加以作用域区分
5. 利用虚继承  解决菱形继承的问题
6. 继承之前  加上关键字  virtual  把父类变为虚继承   我们把Animal类称为虚基类
![alt text](.assets_IMG/C++/image-98.png)
# 多态
+ 多态是C++面向对象三大特性之一
+ 多态分为两类：  
    1. 静态多态：函数重载和运算符重载属于静态多态，复用函数名
    2. 动态多态：派生类和虚函数实现运行时多态
+ 静态多态和动态多态区别：  
    1. 静态多态的函数地址早绑定 - 编译阶段确定函数地址
    2. 动态多态的函数地址晚绑定 - 运行阶段确定函数地址
# 多态的原理
![alt text](.assets_IMG/C++/image-99.png)
当在父类中声明了虚函数之后，构成动态，会生成一个指针，指向该父类虚函数表，这个表记录的是父类虚函数的地址，当子类重写父类的虚函数时，子类中的虚函数表内部会替换成子类的虚函数表，从而输出子类的虚函数结果。这也是地址的晚绑定
## 多态案例————计算器类
![ ](.assets_IMG/C++/image-100.png)

案例：  
![alt text](.assets_IMG/C++/image-101.png)
![alt text](.assets_IMG/C++/image-102.png)
## 纯虚函数和抽象类
![alt text](.assets_IMG/C++/image-103.png)
实际代码
![alt text](.assets_IMG/C++/image-104.png)
注意：纯虚函数和虚函数的区别在于，凡是有纯虚函数的类则不能定义出实例对象 ，而没有纯虚函数有虚函数的类可以定义出实例对象。
## 多态案例二-制作饮品
案例描述：  ![alt text](.assets_IMG/C++/image-105.png)
![alt text](.assets_IMG/C++/image-106.png)
![alt text](.assets_IMG/C++/image-107.png)
+ 需要注意的是，父类一定要设定为纯虚函数，子类一定要重写父类函数，并且一定要用指针调用才会从父类中访问子类的函数。
## 虚析构和纯虚析构
1. ![alt text](.assets_IMG/C++/image-108.png)
2. ![alt text](.assets_IMG/C++/image-109.png)
3. 总结： ![alt text](.assets_IMG/C++/image-110.png)
4. 代码实现：  ![alt text](.assets_IMG/C++/image-111.png)  
5. ![alt text](.assets_IMG/C++/image-112.png)
## 电脑组装案例
1. ![alt text](.assets_IMG/C++/image-113.png)
2. 电脑在组装案例的思路整理：

        + 首先需要抽象出零件的父类，写入对应的纯虚函数，以便子类重写纯虚函数。
        + 再抽象出电脑类，定义出三个零件的指针，并建立工作函数，让指针调用子类中重写后的函数。
        + 构建出Intel的子类，因特尔分别有这三种零件，继承上述的三种父类，并定义输出函数。Lenovo也是如此。
        + 编写测试函数，给第一台电脑的零件在堆区创建三个新的指针，再创建第一台电脑，定义第一台电脑的指针指向第一台电脑的对象，将new出来的三种零件传入第一台电脑中。
        + 最后用电脑的指针调用工作函数即可。
+ ![alt text](.assets_IMG/C++/image-114.png)
+ ![alt text](.assets_IMG/C++/image-115.png)
+ ![alt text](.assets_IMG/C++/image-116.png)
+ ![alt text](.assets_IMG/C++/image-117.png)
## 文件操作：写文件
1. ![alt text](.assets_IMG/C++/image-119.png)
2. 5个步骤：![alt text](.assets_IMG/C++/image-120.png)
3. ![alt text](.assets_IMG/C++/image-121.png)
# 模板
1. 本阶段主要针对C++泛型编程和STL技术做详细讲解，探讨C++更深层次的使用
2. ![alt text](.assets_IMG/C++/image-122.png)
3. 特点：![alt text](.assets_IMG/C++/image-123.png)
## 函数模板
+ ![alt text](.assets_IMG/C++/image-124.png)
+ 语法：![alt text](.assets_IMG/C++/image-125.png)
+ 实例：

        创建两个函数，![alt text](.assets_IMG/C++/image-126.png)
        发现两个函数除了传入的数据类型不一样以外，几乎都是一样的，为了再调用时更方便，是语言具有一定的复用性，我们利用函数模板的概念和方法，为这两个函数创建一个模板!![alt text](.assets_IMG/C++/image-128.png)
        这样一来，函数的调用就非常简介明了了，甚至使用自动识别的方式来引用。
## 模板的注意事项
1. template<typename>//typename 可以替换成class，但人们通常用class来区分类模板，其他情况也可以使用，但始终要养成使得代码具有一点可读性的好习惯
2. 自动类型推导，必须要推导出一致的数据类型T才可以使用
3. 模板必须要确定出T的数据类型，才可以使用
## 函数模板案例
1. ![alt text](.assets_IMG/C++/image-129.png)
2. ![alt text](.assets_IMG/C++/image-130.png)
3. ![alt text](.assets_IMG/C++/image-131.png)
## 普通函数和函数模板的区别
1. ![alt text](.assets_IMG/C++/image-132.png)
2. ![alt text](.assets_IMG/C++/image-133.png)
## 普通函数与函数模板的调用规则
1. 如果函数模板和普通函数都可以实现，优先调用普通函数
2. 可以铜通过空模板参数列表来强制调用函数模板
3. 函数模板也可以发生重载
4. 如果函数模板可以产生更好的匹配，优先调用函数模板
5. 实例：

        ![alt text](.assets_IMG/C++/image-134.png)
        ![alt text](.assets_IMG/C++/image-135.png)
        注意：既然提供了函数模板，最好就不要提供普通函数，否则容易出现二义性
## 模板的局限性
1. 局限性：模板的通用性并不是万能的  例如：![alt text](.assets_IMG/C++/image-136.png)  再例如：![alt text](.assets_IMG/C++/image-137.png)
2. ![alt text](.assets_IMG/C++/image-138.png)
3. ![alt text](.assets_IMG/C++/image-139.png)
4. ![alt text](.assets_IMG/C++/image-140.png)
5. 总结

        + 利用具体化模板，可以解决自定义类型的通用化
        + 学习模板并不是为了写模板，而是在STL能够运用系统提供的模板
6. 其实这段代码中对Person这个类的模板的编写与规定，就相当于是重载了”=“号，当然也可以直接用运算符重载的方式，重载”=“号，以达到目的，但是直接重载相对较为麻烦，所以这里用模板的方式。
## 类模板
1. ![alt text](.assets_IMG/C++/image-141.png)
2. ![alt text](.assets_IMG/C++/image-142.png)
3. 这段代码中主要是要记住创建类模板的方式以及怎么规范的调用

        类似函数模板，在类上面写入模板声明，这个类就称为类模板了，  template <class NameType,class AgeType>，对象中有几种数据类型就规定几种
        在测试函数中，使用Person<string，int>p1（”孙悟空“，999）来调用
## 类模板与函数模板的区别
+ 类模板与函数模板的区别主要有两点：  
    1. 类模板没有自动类型推导的使用方式
![alt text](.assets_IMG/C++/image-143.png)
    2. 类模板在模板参数列表中可以有默认参数
![alt text](.assets_IMG/C++/image-144.png)
如果传了，就用你的，如果没传就用默认类型
## 类模板中的成员函数创建时机
+ 类模板中成员函数和普通类中成员函数创建时机是有区别的：  
    
    1. 普通类中的成员函数一开始就可以创建
    2. 类模板中的成员函数在调用时才创建
+ ![alt text](.assets_IMG/C++/image-145.png)
+ 总结：类模板中的成员函数并不是一开始就创建的，在调用时才去创建的。
## 类模板对象做函数参数
1. ![alt text](.assets_IMG/C++/image-146.png)
2. 代码实现：  
![alt text](.assets_IMG/C++/image-147.png)
![alt text](.assets_IMG/C++/image-148.png)
3. 总结：

        + 通过类模板创建的对象，可以有三种方式像函数中进行传参
        + 使用比较广泛的是第一种：指定传入类型
## 类模板与继承
当类模板碰到继承时，需要注意以下几点：
  + 当子类继承的父类是一个类模板时，子类在声明的时候，要指定出父类中T的类型
  + 如果不指定，编译器无法给子类分配内存
  + 如果想灵活指定出父类中T类型，子类也需变为类模板
总结：正常来讲一般不会这么用，除非是碰到及其复杂的情况，我们一般会将代码写的尽量具有可读性，过于简单或者过于抽象，反而不利于读懂代码。只需要知道，如果父类时类模板，子类需要指定出父类中T的数据类型。 
## 类模板中成员函数的类外实现
1. ![alt text](.assets_IMG/C++/image-149.png)
2. 总结：  类模板中成员函数类外实现时，需要加上模板参数列表。
## 类模板分文件编写
![alt text](.assets_IMG/C++/image-151.png)
![alt text](.assets_IMG/C++/image-150.png)
## 类模板与友元
![alt text](.assets_IMG/C++/image-152.png)
实例： 
![alt text](.assets_IMG/C++/image-153.png)
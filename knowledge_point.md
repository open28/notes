***虚调用***

​	虚调用是相对于实调用而言的，他的本质是动态联编。在发生函数调用的时候，如果函数的入口地址是在编译阶段静态确定的，就是实调用。反之，如果函数的入口地址要在运行时通过查询虚函数表的方式获得，就是虚调用。







**NAS**(network attached sstorage)(DAS)

smb





## C++面向对象编程的基本概念及四种2机制及类和对象

### 面向对象编程的基本概念

1.对象——实体

组成部分：{属性，行为}

eg.一个可以是一个对象，那么这个学生的属性有学号，年纪，班级等；

​	行为有选课，考试，体测等。

2.类——抽象

组成部分是{属性，行为}。

类是将所有对象的公有属性和行为抽象出来的。

eg.学校的学生类，这个类的属性有学号，年纪，班级等：行为有选课，考试，体测等。（这是每一个对象公有的行为属性中抽象出来的）

3.方法

类的行为的实现过程叫做类的方法。其实也就是类中成员函数的定义。即一个方法包含方法名（函数名），返回值类型，参数表，方法体（函数体）

4.消息

对象之间需要沟通，沟通的途径就是向对象之间发送消息。其实也就是说对象调用类的成员函数的语句。即一条消息包含接收消息的对象名，对象需要执行的行为名称（方法名），调用发放需要的参数。

### 调用对象的四种机制

抽象——封装（封装的程度通过访问控制符：public、protected、private）——继承——多态（多态的两种方式：虚函数和函数重载）

》友元函数出现的原因是访问某个类的私有成员，同时也破坏了封装性。

### C++对象之间通信的三中种常见方式

* 使用一个全局单例对象作为交互对像的中介

* 为交互对象创建一个虚接口代理类

  适合常常要给第三方发送回调消息的对象，因为自己包含于目标对象，所以比较方便设置代理，也可以使用目标对象对控件对象对外组合封装起来。

  这种交互方式，有两个对象参与进来，创建类时，需要创建发送消息的虚代理类。而目标对象需要要继承这个虚代理类，并实现这个虚代理类的虚方法。

* 创建交互对象的基类方法函数指针

在A类对象成员变量中注册B、C、D等类的回调函数，通过类内部的指针调用其他类的成员。
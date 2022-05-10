# 设计模式
设计模式的目标
* 理解松耦合设计思想
* 掌握面向对象设计原则
* 掌握重构技法改善设计
* 掌握GOF核心设计模式
## 什么是设计模式
每一个模式描述了一个在我们周围不断重复发送的问题，以及该问题的解决方案的核心。这样你就能一次又一次的使用该方案而不必重复劳动。
### 深入理解面向对象
向下需要深入理解三大面向对象机制
封装：隐藏内部实现
继承：复用现有代码
多态：改写对象行为
向上需要深刻把握面向对象机制所带来的抽象意义，理解如何使用这些机制来表达现实世界，掌握什么是好的面向对象设计。
###	重新认识面向对象
	~理解隔离变化：从宏观层面来看，面向对象的构建方式能适应软件的变化，能将变化所带来的影响减为最小。
	~各司其职：从微观层面看，面向对象的方式更强调个个类的责任。
	由于需求变化导致的新增类型不会影响之前类型的实现。是所谓各司其职
	~对象是什么：从语言层面看，对象封装了代码和数据，从规格层面看，对象是一系列可被使用的公共接口。从概念方面讲：对象是某种拥有责任的抽象。

### 如何解决复杂性
	~分解
	~抽象
## 面向对象设置原则
### 依赖倒置原则
* 高层模块（**稳定**）不应该依赖于底层模块（**变化**），二者都应该依赖于抽象（**稳定**）。
* 抽象（**稳定**）不应该依赖于实现细节（**变化**），实现细节应该依赖于抽象（**稳定**）；
### 开放闭合原则
* 对扩展开发，对更改关闭
* 类模块应该是可扩展的，但是不可修改
### 单一职责原则
* 一个类应该只有一个引起他变化的原因
* 变化的方向隐含在类的责任

### 替换原则

* 子类必须能够替换他们的基类（IS-A）
* 继承表达类型抽象

### 接口隔离原则

* 不应该强迫客户依赖他们不用的方法

* 接口应该小而完备

### 优先使用组合而非继承

* 类继承通常为白箱复用，组合为黑箱复用

* 继承某种程度上破坏了封装性，父类与子类的耦合程度高

* 对象组合只要求被组合的对象具有良好定义的接口，耦合度低。

### 封装变化点

* 使用封装来创建对象之间的分界层，让设计者可以在分界层的一侧进行修改，而不会对另一侧产生不良影响。从而实现层次间的松耦合。

### 针对接口编程，而不是针对实现编程（接口标准化是产业强盛的标准）

* 不将变量类型声明为某个具体类，而是声明为某个接口（**主要指业务问题**）。
* 客户程序无需获知对象的具体类型，只需要知道对象锁具有的接口。
* 减少系统间各部分的依赖关系，实现**高内聚，松耦合**的类型设计方案

### 将设计原则提升为设计经验

* 设计习语(Design Idioms)	

  * 描述与特定编程语言相关的底层模式，技巧，惯用法

* 设计模式(Design Patterns)

  * 类与相互通信的对象之间的组织关系，包括他们的角色，职责，协作方式等方面

* 架构模式

  * 系统中与基本结构组织关系密切的高层模式，包括子系统划分，职责，以及如何组织他们之间关系的规则。

## 设计模式的划分

* 从目的来看
  * 创建型	将对象的部分创建工作延迟到子类或者其他类对象，从而应对需求变化为对象创建时具体实现带来的冲击。
  * 结构型
  * 行为型

* 从范围来看
  * 类模式处理类与子类的静态关系（偏重继承方案）
  * 对象模式处理对象之间的动态关系（偏重组合方案）

* 从封装变化角度
  * 组建协作	现代软件专业分工之后的第一个结果是**框架与应用程序的**划分，组建协作模式通过晚期绑定来实现框架与应用程序之间的松耦合，是二者之间协作时常用的模式。
    * Template Method
    * Strategy 
    * Observer / Event
  * 单一职责    在软件组件的设计中，如果责任划分的不清晰，使用继承得到的结果往往是随着需求的变化子类急剧的膨胀，同时充斥着重复代码，这时候的关键是划清责任。
    * Decorator
    * Bridge
  * 对象创建    通过对象创建模式绕开new，来避免创建过程中所导致的紧耦合（依赖具体类），从而支持对象创建的稳定。他是接口抽象之后的第一步工作。
    * factory Method
    * Abstract Factory
    * Prototype
    * Builder
  * 对象性能    面向对象很好的解决了**抽象**问题，但是不可避免的付出了一定的代价。对于通常情况来说，面向对象的成本大都可以忽略不计。但是某些情况下 ，面向对象带来的成本必须谨慎处理。
    * Singleton
    * Flyweight
  * 接口隔离    在组件构建过程中，某些接口之间直接的依赖常常会带来很多问题，甚至会根本无法实现。采用添加一层间接（**稳定**）接口，来隔离本来互相紧密关联的接口是一种常见的解决方案。
    * Facade
    * Proxy
    * Mediator
    * Adapter
  * 状态变化    在组件构建过程中，某些对象的变化经常面临变化，如何对这些变化进行有效的管理？同时维持高层模块的稳定？**状态变化模式**为这一问题提供了一种解决方案。
    * Memento
    * State
  * 数据结构    常常有一些组件在内部具有特定的数据结构，如果如果让客户程序依赖这些特定的数据结构，将极大的破坏组件的复用，这时候将这些特定的数据结构封装在内部，在外部提供同意的接口，来实现与特定数据结构无关的访问，是一种行之有效的解决方案。
    * Composite
    * Iterator
    * Chain of  Resposibility
  * 行为变化
    * Command
    * Visitor
  * 领域问题
    * Interpreter

## 重构的关键技法

* 静态	——	动态
* 早绑定 ——晚绑定
* 继承——组合
* 编译时依赖——运行时依赖
* 紧耦合——松耦合

## Template Method

模式定义：定义到一个操作中的算法的骨架（**稳定**），而将一些步骤（**变化**）延迟到子类中。Template Method设计模式使得子类可以不改变（**复用**）一个算法的结构即可重定义（**override 重写**）该算法的某些步骤。

* Template Method是一种非常基础性的设计模式，在面向对象系统中有大量的应用。他用最简洁的机制（**虚函数的多态**）为很多应用程序框架提供了灵活的扩展点（**继承加多态，子类对父类的虚函数进行override**）是代码复用方面最基本的实现结构。
* 除了可以灵活应对子步骤的变化外，**不要调用我，让我来调用你**的反向控制结构是Template Method的典型应用。
* 在具体的实现方面，被Template Method 调用的虚方法可以具有实现，也可以不具有任何实现（抽象方法，纯虚函数），但一般推荐将其设置为protected（**一般在固定流程中使用，不供外界调用**）方法。

##  策略模式（strategy）

### 动机（Motivation）

* 在软件构建过程中，某些对象使用的算法可能多种多样，经常改变，如果将这些算法都编码到对象中，将会使对象变得异常复杂，而且有时候支持不使用的算法也是一种性能负担。
* 如何在运行时根据需要透明的更改对象的算法？将算法与对象本身解耦，从而避免上述问题。

### 定义

定义一系列算法，把他们一个个封装起来，并且使他们可以互相替换（**变化**），该模式使得算法可独立于使用他的客户程序（**稳定**）而变化（**扩展，子类化**）。

各国税收变化（if -else 与 抽象出cala方法）

### 要点总结

* Strategy及其子类为组建提供了一系列可重用的算法，从而可以使得类型在运行时，方便的根据需要在各个算法之间进行切换。
* Strategy模式提供了用条件判断语句以外的另一种选择，消除条件判断语句就是在解耦合。含有许多条件判断语句的代码通常需要策略模式。
* 如果Strategy对象没有实例对象，那么各个上下文可以共享同一个Strategy对象，从而节省对象开销。

##  观察者模式（Observer）

### 动机（Motivation）

* 在软件构建过程中，我们需要为某些对象建立一种“通知依赖关系”，一个对象（目标对象）的状态发送改变，所有的依赖对象（观察者对象）都将得到通知。如果这样的依赖过于紧密，将使软件不能很好的抵御变化。
* 使用面向对象技术，可以将这种依赖关系弱化，并形成一种稳定的依赖关系，从而实现软件体系结构的松耦合。

### 定义

定义对象间一种一对多（**变化**）的依赖关系，以便当一个对象（Subject）的状态发生改变时，所有依赖于他的对象都得到通知并自动更新。

### 要点总结

* 使用面向对象的抽象，Observer模式使得我们可以独立的改变目标与观察者，从而使二者之间的依赖关系达到松耦合。
* 目标发送消息时，无需指定观察者，通知（可以携带通知信息作为参数）会自动传播。
* 观察者自己决定是否需要订阅通知，目标对此一无所知。
* Observer模式是基于事件的UI框架中常用的设计模式。也是MVC模式的一个重要组成部分。dan

## 装饰模式（Decorator）

### 动机（Motivation）

* 在某些情况下我们可能会”过度的使用继承来扩展对象的功能“，由于继承为类型引入的静态特质，使得这种扩展方式缺乏灵活性；并且随着子类的增多（扩展功能的增多），各种子类的组合（扩展功能的组合）会导致更多子类的膨胀。
* 如何使”对象功能的扩展“能够根据需要来动态的实现？同时避免扩展功能的增多带来的子类膨胀问题？从而使得任何”功能扩展变化“所导致的影响为最低。

### 定义

动态（**组合**）的给一个对象增加一些额外的职责，就增加功能而言，Decorator模式比生成子类（**继承**）更加灵活。（**消除重复代码，减少子类个数**）。

### 要点总结

* 通过采用组合而非继承的手法，Decorator模式实现了在运行时动态扩展对象功能的能力，而且可以根据需要扩展多个功能。避免了使用继承带来的**灵活性差**和**多子类衍生**问题。
* Decorator类在接口上表现为is-a Component的继承关系，即Decorator继承了Component的所有接口。但在实现上又表现为has-a Component的组合关系，即Decorator类又使用了另外一个Component类。
* Decorator模式的目的并非解决”多子类衍生的多继承问题“，Decorator模式应用的要点在于解决”主体类在多个方向上的扩展功能“ ——是为装饰的含义。

## 桥接模式（Bridge）

### 动机（Motivation）

* 由于某些类型的固有的实现逻辑，使得他们有两个变化的维度，乃至多个维度的变化。

* 如何应对这种多维度的变化？如何利用面向对象技术使得类型可以轻松的沿着两个乃至多个方向变化，而不引入多个复杂度？

### 定义

将抽象部分（业务功能）与实现部分（平台实现）分离，使他们都可以独立变化。

### 要点总结

* Bridge模式使用“对象间的组合关系”解耦了抽象和实现之间固有的绑定关系，使得抽象和实现可以沿着各自的维度来变化。所谓抽象和实现沿着各自的维度变化，即子类化他们。
* Bridge模式有时候类似与多继承方案，但是多继承方案往往违背单一职责原则（**一个类只有一个变化的原因**），复用性较差。Bridge模式是比多继承方案更好的解决方法。
* Bridge模式一般在两个非常强的变化维度，有时一个类也有多余两个的变化维度，这时候可以使用Bridge的扩展模式。

## 工厂方法模式（Factory Method）

### 动机（Motivation）

* 在软件系统中，经常面临着创建对象的工作；由于需求的变化，需要创建的对象的具体类型经常变化。
* 如何绕过这种变化？如何如何绕过常规的对象创建方法（**new会带来细节依赖**），提供一种封装机制来避免客户程序和”具体对象创建”，这种工作的紧耦合？

### 定义

定义一个用于创建对象的接口，让子类决定实例化哪一个类。Factory Method使得一个类的实例化延迟（**目的：解耦 手段：虚函数**）

### 要点总结

* Factory Method模式用于隔离类对象的使用者和具体类型之间的耦合关系。面对一个经常变化的具体类型，紧耦合关系（new）会导致软件的脆弱。
* Factory Method模式通过面向对象的手法，将所要创建的具体对象工作延迟到子类，从而实现一种扩展（**而非更改**）的策略，较好的解决了这种紧耦合关系。
* Factory Method解决了单个对象的需求变化，缺点在于要求创建**方法参数**相同。

## 抽象工厂模式（Abstract Factory）

### 动机（Motivation）

* 在软件系统中，经常面临着“一系列相互依赖的对象”的创建工作；同时，由于需求变化，往往存在更多系列对象的创建工作。
* 如何应对这种变化？如何绕过常规的对象创建方法（new），提供一种封装机制来避免客户程序和这种“多系列具体对象创建工作”的紧耦合？

### 模式定义

提供一个接口让该接口创建一系列“相关或者相互依赖的对象”，无需指定他们具体的类。

* 如果没有应对“多系列对象构建”的需求变化，则没有必要使用Abstract Factory模式	，这个时候使用简单工厂完全可以。
* “系列对象”是指某一特定系列下的对象之间有相互依赖或者作用的关系。不同系列的对象之间不能相互依赖。
* Abstract Factory模式主要在于应对新系列的需求变动。其缺点在于难以应对新对象的需求变动。

## 原型模式（Prototype）

### 动机（Motivation）

* 在软件系统中，经常面临着“某些结构复杂的对象”的创建工作；由于需求的变化，这些对象经常面料着剧烈的变化，但是他们却拥有比较稳定一致的接口。
* 如何应对这种变化？如何向“客户程序（使用这些对象的程序）”隔离出这些“易变的对象”，从而使得“依赖这些易变对象的客户程序”不随着需求改变而改变？

### 定义

使用原型实例指定创建对象的种类，然后通过拷贝这些原型来创建新的对象。

### 要点总结

* Prototype模式同样用于隔离类对象的使用者和具体类型（易变类）之间的耦合关系，他同样要求这些“易变类”拥有“稳定的接口”。
* Prototype模式对于“如何创建易变类的实体对象”采用**原型克隆**的方法来做。它使得我们可以非常灵活的动态创建“拥有某些稳定接口的新对象”——所需的工作仅仅是注册一个新类的对象（即原型），然后在任何需要的地方**Clone**。
* prototype模式中的**Clone**方法可以利用某些框架中的序列化来实现深拷贝。

## 构建器模式（Builder）

### 动机（Motivation）

* 在软件系统中有时候面临一个复杂对象的创建工作，其通常由各个部分的子对象用一定的算法构成；由于需求的变化这个复杂对象的各个部分经常面临剧烈的变化，但是将他们组合在一起的算法却相对稳定。
* 如何应对这种变化？如何提供一种封装机制“来隔离出”复杂对象的各个部分的变化，从而保证系统中的**稳定构建算法**不随需求的改变而改变。

### 定义

将一个复杂对象的构建与其表示相分离，使得同样的构建过程（**稳定**）可以创建不同的表示（**变化**）。

### 要点总结

* Builder模式主要用于**分步骤构建一个复杂的对象**。这其中分步骤是一个稳定的算法，而复杂对象的各个部分则经常变化。
* 变化点在哪里封装哪里——Builder模式在于应对“复杂对象的各个部分”的频繁需求变动。其缺点在于**分步骤构建算法的需求变动**。
* 在Builder模式中，要注意**不同语言中构造器内调用虚函数的差别**（c++ VS c#，Java）

## 单件模式（Singleton）

### 动机（Motivation）

* 在软件系统中，经常有这样一些特殊的类，必须保证他们在系统中只存在一个实例，才能保证他们的逻辑正确性，以及良好的效率。
* 如何绕过常规的构造器，提供一种机制来保证一个类只有一个实例？
* 这应该是类设计者的责任，而不是使用者的责任。

### 代码实现

```c++
class Singleton{
private:
    Singleton();
    Singleton(const Singleton& other);
public:
    static Singleton* m_instance;
    static Singleton* get_instance();  
};
Singleton::m_instance = nullptr;
//线程非安全版本
Singleton* get_instance()
{
    if(m_isntance == nullptr)
        m_instance = new Singleton();
    return m_instance;
}
//线程安全版本，锁的代价过大
Singleton* get_instance()
{
    Lock lock;
    if(m_instance == nullptr)
        m_instance = new Singleton();
    return m_instance;
}
//线程安全版本，双检查锁，但由于内存读写reorder不安全
Singleton* get_insstance()
{
    if(m_instance == nullptr)
    {
        Lock lock;
        if(m_instance == nullptr)
            m_instance = new Singleton();//正常情况，分配内存，调用构造器，赋值
        								//（可能情况，分配内存,赋值，调用构造器）
        								//thread A在调用构造器前，thread B以为已经构造完成，开始使用
    }
    return m_instance;
}
//c++11之后的版本(volatile)
std::atomic<Singleton*> Singleton::m_instance;
std::mutex Singleton::mutex;
Singleton* Singleton::Singleton()
{
    Singleton* tmp = m_instance.load(std::memory_order_relaxed);
    std::atomic_thread_fence(std::memory_order_acquire);//获取内存fence
    if(tmp == nullptr)
    {
        std::lock_guard<std::mutex> lock(mutex);
    	tmp = m_instance.load(std::memory_order_relaxed);
        if(tmp == nullptr)
        {
            tmp = new Singleton;
            std::atomic_thread_fence(std::memory_order_relaxed);//释放内存fence
            m_instance.store(tmp,std::memory_order_relaxed);
        }
    }
     return tmp;
}
```

### 定义

保证一个类只有一个实例，并提供一个该实例的全局访问点。

### 要点总结

* Singleton模式中的实例构造器可以设置为protected以允许子类派生
* Singleton模式一般不支持拷贝构造函数和Clone接口。因为这有可能导致多个对象实例。
* 如何实现多线程环境下安全的Singleton？注意对双检查锁的正确实现。

## 享元模式（Flyweight）

### 动机（Motivation）

* 在软件系统采用纯对象方案的问题在于大量细粒度的对象会很快充斥在系统中，从而带来很高的运行时代价——主要指内存需求方面的代价。
* 如何在避免大量细粒度对象的同时，让外部客户程序仍能够透明的使用面向对象的方式来进行操作？

### 代码片段

```c++
class Font{
private:
    //unique object key
    string key;
    
    //object state
    //...
public:
    Font(const string& key){
        //...
    }
};
class FontFactory{
private:
    map<string,Font*> fontPool;
public:
    Font* GetFont(const string& key)
    {
        map<string,Font*>::iterator item = fontPool.find(key);
        if(item != fontPool.end())
        {
            //return item;
            return fontPool[key];
        }
        else
        {
            Font* font = new Font(key);
            fontPool[key] = font;
            return font;
        }
    }
};
```



### 模式定义

运用共享技术有效的支持大量的细粒度的对象

### 要点总结

* 面向对象很好地解决了抽象性的问题，单作为一个运行在机器中的运行实体，我们需要考虑对象的代价问题。Flyweight主要解决面向对象的代价问题。一般不触及面向对象的抽象性问题。
* Flyweight采用对象共享的方法来降低系统中对象的个数，从而降低细粒度对象给系统带来的内存压力。在具体实现方面，要注意**对象状态的处理**。
* 对象的数量太大从而导致对象内存开销增大，——什么样的数量才算大？这需要我们仔细的根据具体应用情况进行评估，而不能凭空臆断。

## 门面模式（facade）

![image-20220503100539479](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20220503100539479.png)

### 动机（Motivation）

* 上述A方案的问题在于组件的客户和组件中个复杂的子系统有了过多的耦合，随着外部程序和各系统的演化，这种过多的耦合面临很多变化的挑战。
* 如何简化外部客户程序和系统间的交互接口？如何将外部客户程序的演化和内部子系统的变化之间的依赖相互解耦？

### 模式定义

为子系统中的一组接口提供一个一致（**稳定**）的界面，facade模式定义了一个高层的接口，这个接口使得使得这一子系统更加容易使用（复用）。

### 要点总结

* 从客户程序的角度看，facade模式简化了整个组件系统的接口，对于组建内部与外部的客户程序来说，达到了一种解耦的效果——内部子系统的任何变化不会影响到facade接口的变化。
* facade设计模式更注重从架构的层次去看整个系统，而不是单个类的层次。facade很多时候更是一种架构设计模式。
* facade模式并非一个集装箱，可以任意的放进任何多个对象。facade模式中组件的内部应该是**相互耦合关系比较大的一系列组件**，而不是一个简单的功能集合。

## 代理模式（proxy）

### 动机（Motivation）

* 在面向对象系统中，有些对象由于某种原因（**创建对象的开销很大，某些操作需要安全控制，或者需要进程外的访问**）直接访问会给使用者、或者系统结构带来很多麻烦。
* 如何在不失透明操作对象的同时来管理/控制这些对象特有的复杂性？增加一层间接层是软件开发中常见的解决方式。

### 代码片段

```c++
//-------------------------普通模式--------------------------------
class ISubject{
public:
    virtual void process();
    virtual ~ISubject();
};
class RealSubject : public ISubject
{
public:
    virtual void process(){
        
    }
};
class ClientApp{
    ISubject* subject;
public:
    ClientApp(){
        subject = new RealSubject();
    }
    void tasd(){
        //...
        subject->process();
        //...
    }
};
//-------------------------代理模式--------------------------------
class ISubject{
public:
    virtual void process();
    virtual ~ISubject();
};
//proxy的设计
class Subjectproxy : public ISubject
{
public:
    virtual void process(){
        //对RealSubject的一种间接访问
        //...
    }
};
class ClientApp{
    ISubject* subject;
public:
    ClientApp(){
        subject = new Subjectproxy();
    }
    void tasd(){
        //...
        subject->process();
        //...
    }
};
```



### 模式定义

为其他对象提供一种代理以控制（**隔离**，**使用接口**）对这个对象的访问。

### 要点总结

* **增加一层间接层**是软件系统中对徐对复杂问题的一种常见解决方法，在面向对象系统中，直接使用某些对象会带来很多问题，作为间接层的proxy对象便是解决这些问题的常用手段。
* 具体proxy设计模式的实现方法，实现粒度都相差很大，有些可能对单个对象作细粒度的控制，如copy-on-write技术，有些可能对组件模块提供抽象代理层，在架构层次对对象做proxy。
* Proxy并不一定要求保持接口完整的一致性，只要能够实现一些间接控制，有时候损及一些透明性是可以接受的。

## 适配器（Adapter）

### 动机（Motivation）

* 在软件系统中由于应用环境的变化，常常需要将一些现存的对象放在新的环境中应用，但是新环境要求的接口是这些现存对象锁不满足的。
* 如何应对这种迁移的变化？如何能既利用现有对象的良好实现，同时又能满足新的应用环境所要求的接口？

### 模式定义

将一个类的接口转换成客户希望的另一个接口。Adapter模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。



![image-20220503145232874](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20220503145232874.png)

### 代码片段

```c++
//目标接口（新接口）
class ITarget{
public:
    virtual void process()=0;
    
};
//遗留类型
class Oldclass : public IAdaptee{
    //...
};
//遗留接口（老接口）
class IAdaptee{
    virtual void  foo(int ,int) = 0;
    virtual int abr()=0;
};
//对象适配器
class Adapter : public ITarget{
protected:
    IAdaptee* pAdaptee;
public:
    Adapter(IAdaptee* pAdaptee){
        this->pAdaptee = pAdaptee;
    }
    virtual void process(){
        int data = pAdaptee->bar();
        pAdaptee->foo(data);
    }
};
//类适配器(基本不用)
class Adapter : public ITarget,
			protected Oldclass(IAdaptee){//多继承
    
};
int main()
{
    IAdaptee* pAdaptee = new OldClass();
    
    ITarget* pTarget=new Adapter(pAdaptee);
    pTarget->process();
}
```

### 要点总结

* Adapter模式主要主要应用于**希望复用一些现存的类但是接口又与复用环境要求不一致的情况**，在遗留代码复用，类库迁移等方面十分有用。
* GOF23定义了两种Adapter模式的实现结构；对象适配器和类适配器。但类适配器采用多继承的方式实现，一般不推荐使用。对象适配器采用**对象组合方式**，更符合松耦合精神。
* Adapter模式可以实现的非常灵活，不必拘泥于GOF23中定义的两种结构。例如，完全可以将Adapter中的**现存对象**，作为新的接口方法参数，来达到适配的目的。

## 中介者（Mediator）

### 动机（Motivation）

* 在软件构建过程中，经常会出现多个对象互相关联交互的情况，对象之间常常会维持一种复杂的引用关系，如果遇到一些需求的更改，这种直接的引用关系将面临不断的变化。
* 在这种情况下，我们可以使用一个中介者来管理对象间的关联，避免相互交互对象间的紧耦合引用关系，从而更好的抵御变化。



![image-20220503163529621](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20220503163529621.png)

### 模式定义

用一个中介对象来封装（**封装变化**）一系列的对象交互。中介者使各对象不需要显示的相互引用（**从编译时依赖到运行时依赖**）。从而使其耦合松散（**管理变化**），而且可以独立的改变他们之间的交互。

### 要点总结

* 将多个对象间复杂的关联关系解耦，Mediator模式将对个对象间的控制逻辑进行集中管理，变**多个对象互相关联**为**多个对象和一个中介者关联**，简化了系统的维护，抵御了可能的变化。
* 随着控制逻辑的复杂化，Mediator具体对象的实现可能相当复杂。这时候可以对Mediator对象进行分解处理。
* Facade模式是解耦系统间（**单向**）的对象关联关系；Mediator是解耦系统内各个对像之间（**双向**）的关联关系。

### 状态模式 （state）

### 动机（Motivation）

* 在软件构建过程中，某些对象的状态如果改变，其行为也会随之发生变化，比如文档处于只读状态，其支持的行为和读写状态支持的行为就可能完全不同。
* 如何在运行时根据对象的状态来透明的更改对象的行为？而不会为状态操作和对象转化之间引入紧耦合？



### 代码片段

```cpp
enum class NetworkState{
    Network_Open,
    Network_Close,
    Network_Connect//如果需要新增一个状态
};
class NetworkProcessor{
	NetworkState state;
public:
    void Operation1(){
        if(state == NetworkState::Network_Open)
        {
            //...
        }
        else if(state == NetworkState::Network_Close)
        {
            //...
        }
        else if(state == NetworkState::Network_Connect)
        {
            //...
        }
    }
    void Operation2(){
        if(state == NetworkState::Network_Open)
        {
            //...
        }
        else if(state == NetworkState::Network_Close)
        {
            //...
        }
        else if(state == NetworkState::Network_Connect)
        {
            //...
        }
    }
};
//---------------------状态模式------------------------------
class NetworkState{
public:
    NetworkState* pNext;
    virtual void Operation1() = 0;
    virtual void Operation2() = 0;
    virtual void Operation3() = 0;
    virtual ~NetworkState();
};
class OpenState : public NetworkState{
	static NetworkState* m_instance;
public:
    static NetworkState* getInstance(){
        if(m_instance == nullptr){
            m_instance = new OpenState();
        }
        return m_instance;
    }
   
};
class NetworkProcessor{
	NetworkState* pState;
public:
   void Operation1(){
        //...
        pState->operator1();
       pState = pState->pNext;
    }
    void Operation2){
        //...
         pState->operator1();
       pState = pState->pNext;
    }
    void Operation3){
        //...
         pState->operator1();
       pState = pState->pNext;
    }
};
```



### 模式定义

允许一个对象在他的状态改变时改变他的行为。从而使对象看起来似乎修改了他的行为。

### 要点总结

* State模式将所有与一个状态相关的行为都放入一个State的子类对象中，在对象状态切换时，切换相应的对象，但同时维持State的接口，这样实现了具体操作与状态转换之间的解耦。
* 为不同状态引入不同的对象使得状态转换变得更加明确，而且可以保证不会出现状态不一致的情况。因为转换是原子性的——即要么彻底转换要么不转换。
* 如果State对象没有实例变量，那么各上下文可以共享同一个State对象，从而节省对象开销。

## 备忘录模式（Memento)

### 动机（Motivation）

* 在软件构建过程中，某些对象在状态转换过程中，可能由于某种需要，要求程序能够回溯到对象之前处于某个点时的状态。如果使用一些公有接口来来让其他对象得到对象的状态，便会暴露对象的实现细节。
* 如何实现对象状态的良好保存与恢复？但是同时又不会因此破坏对象本省的封装性。

### 模式定义

在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。这样就可以将该对象回复到原先保存的状态。

### 代码片段

```cpp
class Memento{
	string state;
    //.....
public:
    Memento(const string & s):state(s){}
    string getState() const {return state;}
    void setState(const string &s){state = s};
};
class Orginator{
    string state;
    //.....
public:
    Orginator(){}
    Momento createMomento(){
        Momento m(state);
        return m;
    }
    void setMomento(const Memento & m){state = m.getState();}
};

int main()
{
    Orginator orginator;
    //存储到备忘录
    Momento mom = orginator.createMomento();
    //... 改变orginator状态
    
    //从备忘录中回复
    orginator.setMomento();
}
```



![image-20220503220355316](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20220503220355316.png)

### 要点总结

* 备忘录（Memento）存储源发器（Originator）对象的内部状态，在需要时回复源发器状态。
* Memento模式的核心是信息隐藏，即Originator需要向外接隐藏信息，保持其封装性，但同时又需要将状态保持到外界（Memento）。
* 由于现代语言运行时（如c#，java）都有相当的对象序列化支持，因此往往采用效率较高，又较容易正确实现的序列化方案来实现Memento模式。

## 组合模式（composite）

### 动机（motivation)


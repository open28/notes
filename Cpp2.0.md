》获取cpp的版本 ，输出宏__cplusplus,

》语言

* Variadic Templates
* move Smantics
* auto
* Range-base for loop
* Initializer list
* Lambdas
* ......

》标准库

* type_traits
* Unordered 容器
* Forward_list
* array
* tuple
* Con-currency
* Regex
* .....

**Variadic Templates**

版本1；

```cc

void print(){}
template <typename T,typename... Types>
void print(const T& Args1,const Types...& args)
{
    cout<<Args1<<endl;
    print(args...);
}

版本2；
template <typename... Types>
    void print(const Types&... args){
    
}
```

**可以很方便的完成recursive function call。**

```cc
#include <functional>

class CustomerHash{
  public;
    std::size_t operator()(const Customer& c) const{
        return hash_val(c.fname,c.lname,c.no);
    }
};
template <typename... Types>
inline size_t hash_val(const Types&... args){
    size_t seed=0;
    hash_val(seed,args...);
    return seed;
}
template <typename T,typename... Types>
inline void hash_val(size_t& seed,const T& val.const Types&... args){
    hash_combine(seed,val);
    hash_val(seed,args...);
}
template <typename T>
inline void hash_val(size_t& seed,const T& val){
    hash_combine(seed,val);
}

#include <functional
typeplate <typename T>
    inline void hash_combine(size_t& seed,const T& val){
    seed^=std::hash<T>()(val)+0x9e3779b9
        +(seed<<6)+(seed>>2);
}
```

**通过继承实现recursive inheritance**

```cc
template <typename... Values> class tuple;
template<> class tupe<>{};
```

```cc
template <typename Head,typename... Tail>
class tupe<Head,Tail...>
    :private tupe<tail...>
    {
        typedef tupe<Tail...> inherited;
        public:
        tuple(){}
        tupe(Head v,Tail... vtail)
            :m_head(v),inherited(vtail...){}
        
        typename Head::type head(){return m_head;}
        inherited& tail(){return *this}
        protect:
        Head m_head;
    }
```

**space in Template Expressions** 

```cc
#include <vector>
using std::vector;
vector<list<int> >;
vector<list<int>>;
```

**Uniform Initialization**

其实是利用这样一个事实；编译器看到{t1,t2,t3...}的时候便会作出一个initializer_list<T>,他关联一个array<T,n>.调用函数时该array内的元素可以被编译器分解逐一传给函数。但若函数参数是个initializer_list<T>,调用者





**initializer_list<>**

```cc
void print(std::initializer_list<int> valus)
{//打印不定数量的整形值；
    for(auto p=valus.begin();p!=valus.end();++p){//a list of value
        std::cout<<*p<<"\n";
    }
}
print({12,32,43,54,654,65}))//pass a list of value to print();
```

**The source code of initializer **

```cc
template<class _E>
    class initializer_list{
      public:
        typedef _E value_type;
        typedef const _E& reference;
        typedef const _E& const_reference;
        typedef size_t    size_type;
        typedef const _E* iterator;
        typedef const _E* const_iterator;
      Private:
        iterator _M_array;
        size_type _M_len;
        
        //the compiler can call a private constructor.
        constexpr initializer_list(const_iterator __a,size_type __l):_M_arrray(__a),_M_len(__l){}
        public:
        constexpr initalizer_list() noexcept
            :_M_array(0),_M_len(0){}
        //Number of elements.
        constexpr size_type size() const noexcept
        {
            return _M_len;
        }
        //first enements.
        constexpr const_iterator
            begin() const noexcept {return _M_array;}
        //one post the last element.
        constexpr const_iterator
            end() const noexcept
        {return begin()+size()}
        
    };
```

**the source code of array**

```cc
template<typename _Tp,std::size_t _Nm>
struct array
{
    typedef _Tp 		value_type;
    typedef _Tp*		pointer;
    typedef value_type* iterator;
    
    //support for zero-sized arrays mandatory.
    value_type _M_instance[_Nm ? _Nm:1];
    
    iterator begin()
    {return iterator(&_M_instance[0]);}
    iterator end()
    {return iterator(&_M_instance[_Nm]);}
}
....
```

**initializer_list<>**

```cc
#include <initializer_list>
vector(initializer_list<value_type> _l
      ,const allocator_type __a=allocator_type())
    :_Base(__a)
    {_M_range_initialize(__l.begin(),__l.end()                         ,random_access_iterator_tag();)}
vector& operator=(initalizer_list<value_type> __l)
{this->assign(__l.begin(),__l.end());}

void insert(iserator __position,
            initializer_list<value_type> __l)
{this->insert(__position,__l.begin(),__l.end());}
void assign(initializer_list<value_type> __l)
{this->assign(__l.begin(),__l.end());}
```

**range -base for statement**

```cc
for(decl:coll){
    statement;
}
//
for(auto _pos=coll.begin(),_end()=coll.end()
   ;_pos!=_end;++_pos){
    decl=*_pas;//
    statement;
}
//both begin() ang end() are global;
for(auto -pos=begin(coll),_end=end(coll)
   ;_pos!=_end;++_pos){
    decl=*_pos;
    statement;
}
```

**=default,=delete**

```cc
class Zoo{
  public:
    Zoo(int i1,int i2):d1(i1),d2(i2){}
    Zoo(const Zoo&)=delete;
    Zoo(Zoo&&)=default;
    Zoo& operator=(const Zoo&)=default;
    Zoo& operator=(const Zoo&&)=delete;
    virtual ~Zoo(){}
    private:
    int d1,d2;
};
```

**Know what function C++ silently writes and calls**

**Big three**

》如果类中有指针一般就需要自己写三大函数；如果是没有指针，一般只需要用默认的构造函数，拷贝构造函数，析构函数，（移动构造函数，移动赋值函数，拷贝赋值函数）

**NO-Copy and Private_Copy**

```cc
struct NoCopy{
    NoCopy()=default;
	NoCopy(const NoCopy&)=delete;
	NoCopy &operator=(const NoCopy&)=delete;
	~NoCopy()=default;
};
```

```cc
struct NoDtor{
    NoDtor()=default;
    ~NoDtor()=delete;
};

```

```cc
class PrivateCopy{
  private:
    PrivateCopy(const PrivateCopy&);
    PrivateCopy &operator=(const PrivateCopy&);
  public:
  	PrivateCopy()  =default;//use the synthesized default constructor
    ~PrivateCopy();//user can define objects of this //type but not copy them;
};
```

**Alias Template(template typedef)**

```cc
template <typename T>
using Vec = std::vector<T,MyAlloc<T>>;
//it it not possible to partially or explicitly specialize an alias template.
```

```cc
template<typename Container>
void test_moveable(Container c)
{
    typedef typename iterator_traits
        <typename Container::iterator>::value_type  
            Valtype;
    for(long i=0;i<SIZE;++i){
        c.insert(c.end(),Valtype());
        
        output_static_data(*(c.begin()));
        Container c1(c);
        container c2(std::move(c));
        c1.swap(c2);
    }
}
```

***type Alias***

```cc
//type alias,identical to
//typedef void (*func(int,int));
using func=void(*)(int,int);
//the name 'func' now denotes apointer to function;
void example(int,int){}
func fc=exanple;
```

```cc
//Alias template
//type alias used to hide a template parameter
template<class CharT> using mystring=
    std::basic_string<charT,std::char_traits<CharT>>;
mystring<char> str;
//<string>和<string_fwd.h>都有一下typedef：
typedef basic_string<char> string;
```

there is no efference between a type alias declaration and typedef declaration.this declaration may appear in block scope,class scope,or namespace scope.

```cc
//type alias can introduce a member typedef name
template<typename T>
struct Container{
    using value_type = T;
};
//which can be used in generic programming
template<typenae Cntr>
void fn2(const Cntr& c)
{
    typename Cntr::value_type n;
}
```

**noexcept**

```cc
void foo() noexcept; void foo() noexcept(true);

```

**override**重载

**final**不允许被继承

**decltype**

By using the new decltype keyword,you can let the compiler find out the type of an expression.This is the realization of the often requested typeof feature.However,the exiting typeof implementations were inconsistemt and incomplete,so C++11 introduce a new keyword ,For example:

```cc
map<string,float> coll;
decltype(coll)::value_type elem;
```

```cc
template <typename T1,typename T2>
decltype(x+y) add(T1 x, T2 y);//error,use of undeclared identifier 'x';
```

```cc
template <typename T1,typename T2>
auto add(T1 x,T2 y)->decltype(x+y);//correct
```

By using the new decltype keyword,you can let the compiler find out the type of the often requested typeof feature.

One application of decltype is to declare return types.Another is to use it in metaprogramming or to pass the type of lambda.

```cc
typedef typename decltype(obj)::iterator iType;
```

**Lambdas**

C++ 11 introduce lambdas,allowing the definition of inline functionality,which,which can ba used as a parameter or local object.Lambdas change the way the C++ standard is used.

```cc
auto I=[]{
    std::cout<<"hello lambda"<<endl;
};
I();
```

A lambda is a definition of functionality that can be define inside statement and expression.thus,you can use a lambda as an inline function. the minimal lambda function has no paramenters and simply does something;

```cc
int id=0;
auto f=[id]() mutable{
    std::cout<<"id:"<<id<<std::endl;
    ++id;
};
//等价于下面的一个类
class Functor{
    private:
    int id;//copy of outside id
    public:
    void operator(){
        std::cout<<"id:"<<id<<std::endl;
        ++id;
    }
};
Functor
```

the type of lambda is an anonymous function object(or function) that in unique for each lambda expression.thus,to declare objects of that type,if you need the type,you can use decltype(),which is,for example,required to pass a lambda as hash function or ordering or sorting criterion to associative or unordered containers.

```cc
auto cmp=[](const Person& p1,const Person& p2){
    return p1.lastname()<p2.lastname()||
        (p1.lastname()==p2.lastname()&&
        p1.firstname()<p2.firstname());
};
std::set<Person,decltype(cmp)>coll(cmp);
```

Because you need the type of lambda for declaration of the set,decltype must be used,which yields the type of a lanbda object to constructor for the sorting criterion passed,and by rule lambdas have no dafault constructor and no assignment operator. So,for a sorting criterion,a class defining the function objects might still be more intuitive.

***Variadic Templates***

例一

```cc
void printX(){}
template <typename T,typename... Types>
void printX(const T& firstArg,const Types& ...args)
{
    cout<<firstArg<<endl;
    printX(args...);
}
//Inside variadic templates, sizeof...(args) yields the number of arguments;
```

例二

```cc
//使用variadic templates 重写printf()
template<typename T,typename ...Args>
void printf(const char* s,T value,Args... args)
{
    while(*s){
        if(*s=='%'&&*(++s)!='%'){
            std::cout<<value;
            printf(++s,args...);//call even when *s==0to detect extra argument
            return;
        }
        std::cout<<*s++;
    }
    throw std::logic_error(" arguments provided to printf");
}

void printf(const char*)
{
    while(*s)
    {
        if(*s=='%'&&*(++s)!='%')
            throw std::runtime_error("invalid format string:missing argument");
        std::cout<<*s++;
    }
}
```

例三

```cc
//若参数type都相同，无需动用variadic template，使用initializer_list<T> 足以；
cout<<max{57,48,60,100,20,18}<<endl;

template(<typename _Tp> __I)
    inline _Tp
       max(initializer_list<_Tp> __I){
        return *max_enement(__I.begin(),__I.end);
    };


```

```cc
template<typename _ForwardIterator,typename _Compare>
    _ForwardIterator
	__max_element(_ForeardIterator __first,
                  _ForwardIterator __last,
                  _Complare __comp)
{
    if(__first==__last) return __first;
    _ForwardIterator __result=_first;
    
    while(++__first!=__last)
    	if(__comp(__result,__first))
            __result=__first;
    return __result;
};
template<typename __ForwardIterator>
	inline _ForwardIterator
max_element(_ForwardIterator __first,
            _ForwardIterator __last)
{
    return __max_element(__first,__last,
                        __iter_less_iter());
};
```

```cc
inline _Iter_less_iter
    __iter_less_iter()
{return _Iter_less_iter();}
```

```cc
struct _Iter_less_iter
{
    template<typename _Iterator1,
    		 typename _Iterator2>
    bool 
                 operator()(_Iterator __it1,
                            _Iterator __it2) const
             {
                 return __*it1<*__it2;
             };
};
```

```cc
//cout<<maximum(57,48,60,100,20,18)<<endl;
int maximum(int n)
{
    return n;
}
template<typename... Args>
int maximum(int n,Args ...args){
    return std::max(n,maximum(args...));
};
//利用标准库的只能比两个的特点用递归来做；
```

例5

```cc
//以异于一般的情况处理first和last元素
//output operator for tupes
template <typename... Args>
ostream& operator<<(ostream& os, const tuple<Args...>& t){
    os<<"[";
    PRINT_TUPLE<0<sizeof...(Args),Args...>::print(os,t);
    return os<<"]";
}

//helper:print element with index IDX of tuple
//with MAX elementl
template<int IDX,int MAX,typename... Args>
struct PRINT_TUPLE{
    static void print (ostream &os,const tuple<Args...> & t){
        os<<get<IDX>(t)<<(IDX+1==MAX?"":",");
    PRINT_TUPLE<IDX+1,MAX,Args...>::print(ost);
    }
};
```

```cc
//partial specialization to end the recursion
template <int MAX,MAX,Args...>{
    static void print(std::ostream& os,const tuple<Args...>& t)
};
```

```cc
//例6
//用于递归继承，recursive inheritance
template<typename... Values> calss tuple;
template<> class tuple<>{};
```

```cc
template<typename Head,typename... Tail>
calss tuple<Head,Tail...>
:private tupel<Tial...>
{
    typedef tuple<Tail...> inherited;
    public:
    tuple(){}
    tuple(Head V,Tail... vtail)
        :m_hrad(v),inherited(vtail...){}
    typename Head::type head() {return m_head;}
    inheried& tail{return *this;}
    protected:
    Head m_head;
};
```


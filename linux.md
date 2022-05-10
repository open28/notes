# linux

## 线程的同步和互斥

### 锁的创建和销毁

* 静态方式

  pthread_mutex_t mutex=PTHREAD_MUTEX_INITIALIZER;

* 动态方式

  #include<pthread>

  ```c
  int pthraed_mutex_init(pthread_mutex_t *mutex,const pthread_mutexattr_t* mutexattr);
  pthread_mutex_destory();
  int pthread_mutex_destory(pthread_mutex_t *mutex);
  
  ```

  互斥锁的属性：

  有三种属性：

》PTHREAD_MUTEX_TIMED_NP，（这是缺省值可以用ＮＵＬＬ表示）

这是一个普通锁（快速锁），当一个线程加锁后，其余请求锁的线程将形成一个等待队列并在解锁后按优先级获得锁，这种锁策略保证了资源分配的公平性。

示例：

```cc
pthread_mutex_t lock;
pthread_mutex_init(&lock,NULL);
```

》PTHREAD_MUTEX_RECUURSIVE,嵌套锁，允许同一个线程对同一个锁获取多次，并通过unlock解锁，如果是不同线程请求，则在加锁线程解锁时重新竞争。

示例：初始化一个嵌套锁

```cc
pthread_mutex_t lock;
pthread_mutexattr_t mutexattr;
pthread_mutexattr_init(&mutexattr)
pthrad_mutexattr_settype(&mutexattr,PTHREAD_MUTEX_RECURSIVE);
pthread_mutex_init(&lock,&mutexattr);
```

》PTHREAD_MUTEX_ERRORCHECK,检错锁，如果一个锁已经被使用，同一个线程再次请求这把锁，则返回EDEADLK,否则与PTHREAD_MUTEX_NP类型的动作一样。这样就不允许在多次加锁时发生死锁。

示例：初始化一个检错锁。



```cc
pthread_mutex_t lock;
pthread_mutexattr_t mutexattr;
pthared_mutexattr_init (&mutexattr);
pthread_mutexattr_settype(&mutexattr,PTHREAD_MUTEX_ERRORCHECK);
pthread_mutex_init(&lock,&mutexattr);
```

### 锁操作

```cc
加锁：int pthread_mutex_lock(pthread_mutex_t *mutex)
解锁：int pthread_mutex_unlock(pthread_mutex_t* mutex)
测试加锁：int pthread_mutex_trylock(pthread_mutex_t* mutex)
```

》pthread_mutex_lock:加锁，不论哪种类型的锁，都不可能被两个不同的线程同时得到，而必须等待解锁。

普通锁：解锁者可以是同线程内任何线程；

检错锁：必须由加锁者解锁；

嵌套锁：文档和实现要求加锁者解锁，实际并没有这个要求，

注意事项

* 如果线程在加锁后解锁前被取消，所讲永远保持锁定状态，所以要设置取消点。pthread_cleanup_push/pthread_cleanup_pop;同时不应该在信号处理函数中使用互斥锁，否则容易造成死锁。
* 死锁是指多个进程因竞争资源而进入了一种互相等待的状态，若无外力作用，这些进程都无法推进。
* 死锁产生的四个必要条件
* * 互斥条件
  * 请求与保持条件
  * 不可剥夺条件
  * 循环等待条件

## 条件变量

条件变量时利用线程间进共享的全局变量进行同步的一种机制，主要包括两个动作：

* 线程等待条件变量的条件成立而挂起；
* 线程使条件成立（给出条件成立信号）

创建和注销

》静态创建

* pthraed_cond_t cond=PTHREAD_COND_INITIALIZER;

》动态创建

* int pthread_cond_init(pthread_cond_t* cond,pthread_cond_t *cond_attr);第二个参数通常为NLLU,

》注销一个条件变量需要调用pthreadz_cond_destory(),只有在没有线程在改变量上等待的时候能注销这个条件变量，否则返回EBUSY。

* int pthread_cond_destory(pthread_cond_t * cond);

》等待和激发

* 无条件等待:pthread_cond_wait()
* 计时等待:pthread_cond_timewait()

```cc
int pthread_cond_wait(pthread_cond_t *cond,pthread_mutex_t *mutex);
int pthread_cond_timewait(pthread_cond_t *cond,pthread_mutex_t * mutex,const struct timespec* abstime);
//配合锁是为了防止多个线程同时请求pthread_cond_wait()
```

》激发条件有两种

```cc
int pthread_cond_single(pthread_cond_t* cond);
//激活一个等待该条件的线程，存在多个线程时按照入队顺序激活其中一个
int	pthread_cond_broadcast(pthread_cond_t* cond);
```

**回调函数保护**等待条件亲爱锁定，pthread_cond_wait()返回后解锁。

》条件变量机制和互斥锁一样，不能用于信号处理函数调用中，

## 线程安全和线程属性

线程安全：如果一个函数能够安全的同时被多个线程调用而得到正确的结果，那么我们说线程是安全的。

可重入函数：函数被中断后在执行，仍能得到正确的结果。
# 1 函数

## 1.1 字符操作

### sizeof：运算符

sizeof 是 C/C++ 中的运算符，不是函数。

**不需要包含头文件。**

作用：获取一个数据类型或对象所占的内存字节数。

基本形式：

```c
sizeof(数据类型);
sizeof(变量);
```

返回值类型为 size_t。

例如：

```c
int a;

sizeof(int);    // 获取 int 类型占用的字节数
sizeof(a);      // 获取变量 a 占用的字节数
```

对于数组，sizeof 可以得到整个数组占用的字节数：

```c
int arr[10];

sizeof(arr);    // 整个数组占用的字节数
```

因此可以使用 sizeof 计算数组元素个数：

```c
sizeof(arr) / sizeof(arr[0]);
```

当操作数不是变长数组（VLA）时，sizeof 通常不会对表达式进行求值。

```c
int a = 10;

sizeof(a++);

// a 不会因为 sizeof 而自增
```

sizeof 得到的是对象本身占用的空间，而不是指针所指向对象的大小：

```c
int *p;

sizeof(p);      // 获取指针变量本身的大小
```
### strtoul：字符串转整型函数

```c
/**
 * @brief  将字符串转换成 unsigned long 类型的无符号整数。
 *
 * @param  str: 要转换的字符串。
 *
 * @param  endptr: 用于保存转换结束位置的指针。
 *                 不需要时可以传入 NULL。
 *
 * @param  base: 转换时使用的进制。
 *               0 表示根据字符串前缀自动判断进制。
 *               10 表示十进制。
 *               16 表示十六进制。
 *
 * @retval 转换得到的 unsigned long 类型数值。
 */
unsigned long strtoul(const char *str,
                      char **endptr,
                      int base);
```

代码示例：

```
unsigned long num;

num = strtoul("30", NULL, 10);

/*
 * 将字符串 "30" 按照十进制转换。
 *
 * 转换结果：
 * num = 30
 */
```

### strcmp：比较字符串大小

```c
/**
 * @brief  按字符逐个比较两个字符串的大小。
 *
 * @param  s1: 指向第一个以 '\0' 结尾的字符串。
 *
 * @param  s2: 指向第二个以 '\0' 结尾的字符串。
 *
 * @retval 0: 两个字符串内容相同。
 *
 * @retval 负数: s1 小于 s2。
 *
 * @retval 正数: s1 大于 s2。
 */
#include <string.h>

int strcmp(const char *s1, const char *s2);
```

代码示例：

```c
int result;

result = strcmp("apple", "banana");

/*
 * 比较字符串 "apple" 和 "banana"。
 *
 * 结果：
 * result < 0；
 * 表示 "apple" 小于 "banana"。
 *
 * strcmp() 的正数或负数具体是多少没有固定要求，
 * 判断时应与 0 比较。
 */
```

### strlen：计算字符串的长度

```c
/**
 * @brief  计算字符串的长度，即字符串结束符 '\0' 之前的字符数量。
 *
 * @param  s: 指向要计算长度的字符串。
 *
 * @retval 字符串中 '\0' 之前的字符数量，不包括 '\0'。
 */
#include <string.h>

size_t strlen(const char *s);
```

例如：

```c
char str[] = "hello";

size_t len = strlen(str);
```

此时：

```c
len == 5
```

字符串实际存储为：

```text
'h' 'e' 'l' 'l' 'o' '\0'
```

strlen 只统计 '\0' 前面的字符，所以结果为 5，不包含字符串结束符 '\0'。

返回值类型为 size_t。
### str_delete：字符删除

```c
/**
 * @brief  从字符串的指定下标开始删除指定数量的字符。
 *
 * @param  str: 需要修改的字符串。
 *
 * @param  pos: 开始删除的位置，下标从 0 开始。
 *
 * @param  count: 需要删除的字符数量。
 *
 * @retval 无返回值。
 *
 * @note   str_delete() 不是 C 标准库函数，需要自行定义。
 */
#include <string.h>

void str_delete(char *str, size_t pos, size_t count)
{
    size_t len = strlen(str);

    if (pos >= len)
        return;

    if (count > len - pos)
        count = len - pos;

    memmove(str + pos,
            str + pos + count,
            len - pos - count + 1);
}
```

代码示例：

```c
char str[] = "abcdefg";

str_delete(str, 2, 3);

/*
 * 从下标 2 开始删除 3 个字符。
 *
 * 删除前：
 * "abcdefg"
 *
 * 删除的字符：
 * c、d、e
 *
 * 删除后：
 * "abfg"
 *
 * memmove() 会把后面的字符和结尾的 '\0'
 * 一起向前移动，覆盖需要删除的内容。
 */
```

### fgets：从指定文件流中读取字符串

```c
/**
 * @brief  从指定文件流中读取字符串，最多读取 n - 1 个字符。
 *         遇到换行符或文件结束符时停止读取。
 *         如果读取到换行符，换行符也会被保存到字符串中，
 *         最后会自动添加字符串结束符 '\0'。
 *
 * @param  str: 用于保存读取内容的字符数组。
 *
 * @param  n: 最多允许写入 str 的字符数，包括结尾的 '\0'。
 *
 * @param  stream: 要读取的文件流。
		example:
			 stdin // 标准输入流，通常对应键盘 
			 stdout // 标准输出流，通常对应屏幕 
			 stderr // 标准错误流，通常对应屏幕
 *
 * @retval str: 读取成功。
 *         返回参数 str 本身，也就是保存读取结果的字符数组的首地址。
 *
 * @retval NULL: 到达文件末尾且没有读取到字符，或发生读取错误。
 */
#include <stdio.h>

char *fgets(char *str, int n, FILE *stream);
```

常见用法：

```c
char buf[100];

fgets(buf, sizeof(buf), stdin);
```

从标准输入读取字符串时，fgets 可以限制最大读取长度，因此可以避免输入内容超过字符数组的容量。

如果用户输入：

```text
hello
```

buf 中保存的实际内容通常为：

```text
"hello\n\0"
```

因为 fgets 会保留读取到的换行符。
## 1.2 动态内存管理

### calloc

```c
/**
 * @brief  在堆内存中申请一块连续空间，并将申请到的内存全部初始化为 0。
 *
 * @param  nmemb: 要申请的元素个数。
 *
 * @param  size: 每个元素占用的字节数。
 *
 * @retval 非 NULL: 内存申请成功，返回所申请内存的首地址。
 *
 * @retval NULL: 内存申请失败。
 */
#include <stdlib.h>
void *calloc(size_t nmemb, size_t size);
```

代码示例：

```c
int *array;

array = calloc(10, sizeof(int));

/*
 * 申请可以存放 10 个 int 类型数据的连续内存空间。
 *
 * 申请的总大小：
 * 10 × sizeof(int)
 *
 * calloc() 会将这块内存中的所有字节初始化为 0。
 *
 * array：
 * 申请成功时，保存内存空间的首地址；
 * 申请失败时，值为 NULL。
 */
```

### malloc

```c
/**
 * @brief  在堆内存中申请一块指定字节数的连续内存空间。
 *
 * @param  size: 要申请的内存字节数。
 *
 * @retval 非 NULL: 内存申请成功，返回所申请内存的首地址。
 *
 * @retval NULL: 内存申请失败。
 */
#include <stdlib.h>
void *malloc(size_t size);
```

代码示例：

```c
int *array;

array = malloc(10 * sizeof(int));

/*
 * 申请可以存放 10 个 int 类型数据的连续内存空间。
 *
 * 申请的总大小：
 * 10 × sizeof(int)
 *
 * malloc() 不会初始化申请到的内存，
 * 内存中原来的数据是不确定的。
 *
 * array：
 * 申请成功时，保存内存空间的首地址；
 * 申请失败时，值为 NULL。
 */
```

### free

```c
#include <stdlib.h>

/**
 * @brief  释放之前由 malloc()、calloc() 或 realloc() 分配的动态内存。
 *
 * @param  ptr: 指向需要释放的动态内存的指针。
 *              如果 ptr 为 NULL，则 free() 不执行任何操作。
 *
 * @retval 无返回值。
 */
void free(void *ptr);
```

代码示例：

```c
int *p = malloc(sizeof(int) * 5);

if (p != NULL)
{
    /*
     * 使用完动态内存后将其释放。
     */
    free(p);

    /*
     * free() 之后，p 中保存的地址已经失效。
     * 将其设为 NULL，可以避免继续误用已经释放的内存。
     */
    p = NULL;
}
```

## 1.3 内存操作
### memcpy

```c
#include <string.h>

/**
 * @brief  将源内存中的指定字节复制到目标内存中。
 *         源内存和目标内存不能重叠。
 *
 * @param  dest: 目标内存的起始地址。
 *
 * @param  src: 源内存的起始地址。
 *
 * @param  n: 要复制的字节数。
 *
 * @retval 返回目标内存的起始地址 dest。
 */
void *memcpy(void *dest, const void *src, size_t n);
```

代码示例：

```c
int src[3]  = {1, 2, 3};
int dest[3] = {0};

memcpy(dest, src, sizeof(src));

/*
 * 将 src 中的所有数据复制到 dest 中。
 *
 * 复制结果：
 * dest[0] = 1
 * dest[1] = 2
 * dest[2] = 3
 */
```

## 1.4 进程
### fork：创建子进程

```c
/**
 * @brief  创建一个新的子进程。
 *
 * @retval 0: 当前进程为子进程。
 *
 * @retval >0: 当前进程为父进程，返回值为新创建子进程的 PID。
 *
 * @retval -1: 创建子进程失败。
 */
#include <sys/types.h>
#include <unistd.h>

pid_t fork(void);
```

fork 调用成功后，会产生一个新的子进程。

父进程和子进程都会从 fork 返回的位置继续向下执行，可以通过 fork 的返回值区分父进程和子进程。

```c
pid_t pid = fork();

if (pid == -1)
{
    // 创建子进程失败
}
else if (pid == 0)
{
    // 子进程
}
else
{
    // 父进程
    // pid 为子进程的 PID
}
```

父进程和子进程拥有各自独立的地址空间。

子进程创建时会继承父进程的大部分运行环境，例如打开的文件描述符等。

## 1.5 C线程
### pthread_create

```c
/**
 * @brief  创建一个新的线程。
 *
 * @param  thread: 用于保存新线程的线程 ID。
 *
 * @param  attr: 线程属性，传入 NULL 表示使用默认属性。
 *
 * @param  start_routine: 新线程开始执行的函数。
 *
 * @param  arg: 传递给线程函数的参数。
 *
 * @retval 0: 创建线程成功。
 *
 * @retval 非0: 创建线程失败，返回错误码。
 */
#include <pthread.h>

int pthread_create(pthread_t *restrict thread,
                   const pthread_attr_t *restrict attr,
                   void *(*start_routine)(void *),
                   void *restrict arg);
```

线程函数通常写成：

```c
/*****************不带参数***********************/
void *thread_func(void *arg)
{
    // 线程执行的代码

    return NULL;
}

pthread_t tid;

pthread_create(&tid, NULL, thread_func, NULL);


/*****************带参数***********************/
void *thread_func(void *arg)
{
    int num = *(int *)arg;

    printf("num = %d\n", num);

    return NULL;
}

int main(void)
{
    pthread_t tid;
    int num = 100;

    pthread_create(&tid, NULL, thread_func, &num);

    pthread_join(tid, NULL);

    return 0;
}
```

pthread_create 创建成功后，新线程会从 start_routine 指定的函数开始执行。

arg 可以用于向线程函数传递数据。

### pthread_join

```c
/**
 * @brief  等待指定线程结束，并回收该线程的资源。
 *
 * @param  thread: 要等待的线程 ID。
 *
 * @param  retval: 用于接收目标线程的返回值；
 *                 不需要返回值时可以传入 NULL。
 *
 * @retval 0: 调用成功。
 *
 * @retval 非0: 调用失败，返回错误码。
 */
#include <pthread.h>

int pthread_join(pthread_t thread, void **retval);
```

基本用法：

```c
pthread_t tid;

pthread_create(&tid, NULL, thread_func, NULL);

pthread_join(tid, NULL);
```

pthread_join 通常会阻塞当前线程，直到指定线程结束。

如果需要获得线程函数的返回值：

```c
void *ret;

pthread_join(tid, &ret);
```

此时 ret 用于接收目标线程结束时返回的指针。

### pthread_exit

```c
/**
 * @brief  结束当前线程。
 *
 * @param  retval: 当前线程的返回值，可以被其他线程通过
 *                 pthread_join 获取。
 *
 * @retval 不返回。
 */
#include <pthread.h>

void pthread_exit(void *retval);
```

基本用法：

```c
pthread_exit(NULL);
```

也可以返回一个指针：

```c
pthread_exit(ptr);
```

其他线程可以通过 pthread_join 获取该返回值：

```c
void *ret;

pthread_join(tid, &ret);
```

在线程函数中执行：

```c
return value;
```

通常与：

```c
pthread_exit(value);
```

具有结束当前线程并返回线程结果的作用。

### pthread_mutex_lock

```c
/**
 * @brief  对互斥锁进行加锁。
 *
 * @param  mutex: 指向要加锁的互斥锁。
 *
 * @retval 0: 加锁成功。
 *
 * @retval 非0: 加锁失败，返回错误码。
 */
#include <pthread.h>

int pthread_mutex_lock(pthread_mutex_t *mutex);
```

如果互斥锁当前没有被其他线程持有，则当前线程获得互斥锁并继续执行。

如果互斥锁已经被其他线程持有，则当前线程通常会阻塞等待，直到能够获得该互斥锁。

常用于保护多个线程共享的临界资源：

```c
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

pthread_mutex_lock(&mutex);

/* 操作临界资源 */

pthread_mutex_unlock(&mutex);
```

### pthread_mutex_unlock

```c
/**
 * @brief  释放当前线程持有的互斥锁。
 *
 * @param  mutex: 指向要解锁的互斥锁。
 *
 * @retval 0: 解锁成功。
 *
 * @retval 非0: 解锁失败，返回错误码。
 */
#include <pthread.h>

int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

pthread_mutex_unlock 通常与 pthread_mutex_lock 配合使用：

```c
pthread_mutex_lock(&mutex);

/* 操作临界资源 */

pthread_mutex_unlock(&mutex);
```

线程完成对共享资源的操作后，应释放互斥锁，使其他线程能够获得该锁。

### pthread_cond_wait

```c
/**
 * @brief  等待条件变量，并在等待过程中释放互斥锁。
 *
 * @param  cond: 指向要等待的条件变量。
 *
 * @param  mutex: 指向与条件变量配合使用的互斥锁。
 *
 * @retval 0: 等待成功并被唤醒。
 *
 * @retval 非0: 调用失败，返回错误码。
 */
#include <pthread.h>

int pthread_cond_wait(pthread_cond_t *restrict cond,
                      pthread_mutex_t *restrict mutex);
```

调用 pthread_cond_wait 前，当前线程必须先持有 mutex。

```c
pthread_mutex_lock(&mutex);

pthread_cond_wait(&cond, &mutex);

pthread_mutex_unlock(&mutex);
```

pthread_cond_wait 执行时会：

1. 原子地释放 mutex。
    
2. 阻塞当前线程，等待条件变量 cond。
    
3. 被唤醒后重新获得 mutex。
    
4. 获得 mutex 后 pthread_cond_wait 才返回。
    

条件变量通常应配合条件判断使用：

```c
pthread_mutex_lock(&mutex);

//使用 while 是因为线程被唤醒并不一定表示所等待的条件此时仍然成立。
while (!condition)
{
    pthread_cond_wait(&cond, &mutex);
}

/* 操作临界资源 */

pthread_mutex_unlock(&mutex);
```


### pthread_cond_signal

```c
/**
 * @brief  唤醒至少一个正在等待指定条件变量的线程。
 *
 * @param  cond: 指向要发送信号的条件变量。
 *
 * @retval 0: 调用成功。
 *
 * @retval 非0: 调用失败，返回错误码。
 */
#include <pthread.h>

int pthread_cond_signal(pthread_cond_t *cond);
```

如果有线程正在通过 pthread_cond_wait 等待该条件变量，pthread_cond_signal 会唤醒至少一个等待线程。

```c
pthread_cond_signal(&cond);
```

如果当前没有线程等待该条件变量，则此次通知不会被保存，之后才开始等待的线程不会收到这次通知。

通常在线程修改了与条件变量相关的共享状态之后调用：

```c
pthread_mutex_lock(&mutex);

condition = 1;

pthread_cond_signal(&cond);

pthread_mutex_unlock(&mutex);
```

被唤醒的线程从 pthread_cond_wait 返回之前，需要重新获得与条件变量配合使用的互斥锁。
### pthread 静态初始化宏
#### POSIX 标准宏

```c
#include <pthread.h>
//这些宏用于在定义 pthread 同步对象时直接进行静态初始化。

PTHREAD_MUTEX_INITIALIZER          // 初始化一个默认属性的互斥锁 pthread_mutex_t
PTHREAD_COND_INITIALIZER           // 初始化一个默认属性的条件变量 pthread_cond_t
PTHREAD_RWLOCK_INITIALIZER         // 初始化一个默认属性的读写锁 pthread_rwlock_t
PTHREAD_ONCE_INIT                  // 初始化 pthread_once_t 控制对象，配合pthread_once 使用
```

基本用法：

```c
static pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

static pthread_cond_t cond = PTHREAD_COND_INITIALIZER;

static pthread_rwlock_t rwlock = PTHREAD_RWLOCK_INITIALIZER;

static pthread_once_t once = PTHREAD_ONCE_INIT;


//使用这些宏进行静态初始化后，不需要再调用对应的初始化函数。
例如：
static pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

// 不需要再调用
// pthread_mutex_init(&mutex, NULL);
```

#### GNU/Linux glibc 扩展宏

```c
//下面这些宏属于 GNU 扩展，不属于 POSIX 标准，名称末尾的 NP 表示非可移植扩展
//使用时通常需要启用 GNU 扩展：
#define _GNU_SOURCE
#include <pthread.h>

PTHREAD_RECURSIVE_MUTEX_INITIALIZER_NP            // 初始化递归互斥锁
PTHREAD_ERRORCHECK_MUTEX_INITIALIZER_NP           // 初始化错误检查型互斥锁
PTHREAD_ADAPTIVE_MUTEX_INITIALIZER_NP             // 初始化自适应互斥锁
PTHREAD_RWLOCK_WRITER_NONRECURSIVE_INITIALIZER_NP // 初始化偏向写线程的非递归读写锁
```

## 1.6 C信号量

### 基本使用流程
```

#include <semaphore.h>

sem_t sem;

sem_init(&sem, 0, 1);

sem_wait(&sem);

/* 操作共享资源 */

sem_post(&sem);

sem_destroy(&sem);


基本流程：

sem_init()
    ↓
初始化信号量
    ↓
sem_wait()
    ↓
获取信号量
    ↓
操作共享资源
    ↓
sem_post()
    ↓
释放信号量
    ↓
sem_destroy()
    ↓
销毁信号量

当信号量初始值为 1 时，可以使同一时刻最多只有一个线程进入受保护区域，其作用类似于互斥锁。

当信号量初始值大于 1 时，可以限制同时访问某个资源的线程数量。
```

### sem_init

```
/**
 * @brief  初始化一个未命名信号量。
 *
 * @param  sem: 指向需要初始化的信号量。
 *
 * @param  pshared: 指定信号量的共享方式。
 *                  0 表示用于同一进程中的线程之间；
 *                  非 0 表示用于进程之间。
 *
 * @param  value: 信号量的初始值。
 *
 * @retval 0: 初始化成功。
 *
 * @retval -1: 初始化失败。
 */
#include <semaphore.h>

int sem_init(sem_t *sem, int pshared, unsigned int value);
```

线程之间使用时通常写成：

```
sem_t sem;

sem_init(&sem, 0, 1);
```

其中：

```
0    // 在线程之间共享
1    // 信号量初始值
```

---

### sem_wait

```
/**
 * @brief  获取信号量，使信号量值减 1。
 *
 * @param  sem: 指向要获取的信号量。
 *
 * @retval 0: 获取成功。
 *
 * @retval -1: 调用失败。
 */
#include <semaphore.h>

int sem_wait(sem_t *sem);
```

如果信号量值大于 0：

```
信号量值减 1
线程继续执行
```

如果信号量值为 0：

```
当前线程阻塞等待
```

直到信号量可以被获取。

基本用法：

```
sem_wait(&sem);

/* 操作共享资源 */

sem_post(&sem);
```

---

### sem_post

```
/**
 * @brief  释放信号量，使信号量值加 1。
 *
 * @param  sem: 指向要释放的信号量。
 *
 * @retval 0: 操作成功。
 *
 * @retval -1: 调用失败。
 */
#include <semaphore.h>

int sem_post(sem_t *sem);
```

sem_post 会使信号量值增加。

如果有线程正在 sem_wait 中等待该信号量，可以使等待线程获得继续运行的机会。

---

### sem_destroy

```
/**
 * @brief  销毁一个由 sem_init 初始化的未命名信号量。
 *
 * @param  sem: 指向需要销毁的信号量。
 *
 * @retval 0: 销毁成功。
 *
 * @retval -1: 销毁失败。
 */
#include <semaphore.h>

int sem_destroy(sem_t *sem);
```

信号量不再使用时，可以调用：

```
sem_destroy(&sem);
```

# 2 关键字
## restrict

restrict 是 C99 引入的指针限定符，用于告诉编译器：在特定作用域内，对某个对象的访问会遵守 restrict 所要求的指针访问规则。

它主要用于帮助编译器进行优化。

**不需要包含头文件。**

基本形式：

```c
int *restrict p;
```

也经常出现在函数参数中：

```c
void func(int *restrict p);
```

例如：

```c
int func(int *restrict p1, int *restrict p2);
```

restrict 表示程序员向编译器保证，这些受 restrict 限定的指针在使用过程中不会以违反 restrict 规则的方式访问同一对象。

因此编译器可以减少对指针可能指向同一内存区域的考虑，从而进行更多优化。

例如在函数声明中：

```c
int pthread_create(
    pthread_t *restrict thread,
    const pthread_attr_t *restrict attr,
    void *(*start_routine)(void *),
    void *restrict arg
);
```

调用时不需要对 restrict 进行特殊处理：

```c
pthread_t tid;

pthread_create(&tid, NULL, thread_func, NULL);
```

restrict 是 C 语言标准关键字。

在标准 C++ 中没有 restrict 关键字，一些编译器提供类似的扩展，例如：

```cpp
__restrict
```
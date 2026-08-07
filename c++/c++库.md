# 1 宏
## 1.1 宏定义

## 1.2 宏函数

# 2 数据类型


# 3 函数

## 3.1 字符相关函数

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

## 3.2 动态内存管理

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

## 3.3 内存操作
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


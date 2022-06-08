<!--yml
category: C/C++
date: 0001-01-01 00:00:00
-->

# C 语言面试题（山月）

# 一个守护进程的创建步骤是什么，如何用 C 语言创建

> 原文：[https://q.shanyue.tech/server/c/139.html](https://q.shanyue.tech/server/c/139.html)

更多描述

#50

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 139(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/139)

# 如何创建一个线程

> 原文：[https://q.shanyue.tech/server/c/164.html](https://q.shanyue.tech/server/c/164.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 164(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/164)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

创建一个最简单的线程

```
#include <pthread.h>
#include <stdio.h>
#include <unistd.h>

void *thread_function(void *arg) {
  printf("hello, world\n");
  sleep(10);
}

int main() {
  pthread_t thread;

  pthread_create(&thread, NULL, thread_function, NULL);
  pthread_join(thread, NULL);
} 
```

执行它

```
$ gcc thread.c -std=c99 -lpthread && ./a.out
hello, world 
```

# 在 C 语言中，void * 是什么意思

> 原文：[https://q.shanyue.tech/server/c/167.html](https://q.shanyue.tech/server/c/167.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 167(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/167)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

`void` 指无类型，常用在函数前，表示什么也不用返回。

`*` 代表一个指针，如 `int *p` 代表指针 p 指向一个整型，`char *s` 代表指针 s 指向一个字符串的首地址。

而 `void *` 代表一个可能指向任何类型的指针，如下代码所示：

```
#include <stdio.h>

int main() {
  void *p;

  // 使用它装一个整数
  int a = 3;
  p = &a;
  printf("%d", *(int *)p);

  // 使用它装一个字符串
  char s[] = "hello, world";
  p = s;
  printf("%s", p);
  return 0;
} 
```

## 相关问题

*   [【Q433】在 C 语言中，void 是什么意思(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/440)

# 每个指针所占的存储空间是多少

> 原文：[https://q.shanyue.tech/server/c/168.html](https://q.shanyue.tech/server/c/168.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 168(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/168)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

与字长有关。如果是 64 位系统，则占八个字节，32 位系统，则占四个字节。可以用 `sizeof` 测试

```
#include <stdio.h>

int main() {
  int *p;

  printf("size: %d", sizeof(p));
} 
```

# C 语言中 printf 与 puts 有什么区别

> 原文：[https://q.shanyue.tech/server/c/173.html](https://q.shanyue.tech/server/c/173.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 173(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/173)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
// 支持各种格式
int printf(const char *__restrict__ __format, ...);

// 只支持字符串输出到 stdout，适用于只有字符串时
int puts(const char *__s); 
```

# TCP 三次握手发生在 socket 建立的哪一步

> 原文：[https://q.shanyue.tech/server/c/175.html](https://q.shanyue.tech/server/c/175.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 175(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/175)

Author

回答者: [changshou83(opens new window)](https://github.com/changshou83)

TCP Client 调用 connec()请求建立连接时

# 如何创建一个进程

> 原文：[https://q.shanyue.tech/server/c/300.html](https://q.shanyue.tech/server/c/300.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 300(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/300)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

*   `exec`
*   `fork`

# 在 C 语言中，void 是什么意思

> 原文：[https://q.shanyue.tech/server/c/440.html](https://q.shanyue.tech/server/c/440.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 440(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/440)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

`void`，空的意思，意即无需返回。

```
#include <stdio.h>

void print() {
  puts("hello, world");
  return;
}

int main() {
  print();
  return 0;
} 
```

代码如上所示: `return` 没有返回任何东西，为其简便可以省略不写，以下两者是等价的

```
void print() {
  puts("hello, world");
  return;
}

void print() {
  puts("hello, world");
} 
```

# GraphQL

# 简述一下 graphql，它的引进有什么好处

> 原文：[https://q.shanyue.tech/server/graphql/52.html](https://q.shanyue.tech/server/graphql/52.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 52(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/52)
<!--yml
category: Linux
date: 0001-01-01 00:00:00
-->

# Linux 面试题（爪哇程序员）

# vim有几种工作模式？

> 原文：[https://zwmst.com/561.html](https://zwmst.com/561.html)

命令模式，行末模式，编辑模式

# find命令如何使用？

> 原文：[https://zwmst.com/563.html](https://zwmst.com/563.html)

查找指定文件名的文件(不区分大小写)：find -iname "MyProgram.c" 。
对找到的文件执行某个命令：find -iname "MyProgram.c" -exec md5sum {} \; 。
查找 home 目录下的所有空文件：find ~ -empty 。

# 如何在usr目录下找出大小超过10MB的文件?

> 原文：[https://zwmst.com/565.html](https://zwmst.com/565.html)

find /usr -type f -size +10240k

# 如何在var目录下找出90天之内未被访问过的文件？

> 原文：[https://zwmst.com/567.html](https://zwmst.com/567.html)

find /var ! -atime -90

# 如何在home目录下找出120天之前被修改过的文件？

> 原文：[https://zwmst.com/569.html](https://zwmst.com/569.html)

find /home -mtime +120

# 在整个目录树下查找文件“core”，如发现则无需提示直接删除它们？

> 原文：[https://zwmst.com/571.html](https://zwmst.com/571.html)

find / -name core -exec rm {} \;

# ls命令

> 原文：[https://zwmst.com/573.html](https://zwmst.com/573.html)

以易读的方式显示文件大小(显示为 MB,GB…)：ls -lh 。
以最后修改时间升序列出文件：ls -ltr 。
在文件名后面显示文件类型：ls -F 。

# df命令

> 原文：[https://zwmst.com/575.html](https://zwmst.com/575.html)

显示文件系统的磁盘使用情况，默认情况下 df -k 将以字节为单位输出磁盘的使用量。
使用 df -h 选项可以以更符合阅读习惯的方式显示磁盘使用量。
使用 df -T 选项显示文件系统类型。

# rm命令

> 原文：[https://zwmst.com/577.html](https://zwmst.com/577.html)

删除文件前先确认：rm -i filename.txt 。
在文件名中使用 shell 的元字符会非常有用。删除文件前先打印文件名并进行确认：rm -i file* 。
递归删除文件夹下所有文件，并删除该文件夹：rm -r example 。

# mv命令

> 原文：[https://zwmst.com/579.html](https://zwmst.com/579.html)

将 file1 重命名为 file2 ，如果 file2 存在则提示是否覆盖：mv -i file1 file2 。
-v 会输出重命名的过程，当文件名中包含通配符时，这个选项会非常方便：mv -v file1 file2 。

# cp命令

> 原文：[https://zwmst.com/581.html](https://zwmst.com/581.html)

拷贝 file1 到 file2 ，并保持文件的权限、属主和时间戳：cp -p file1 file2 。
拷贝 file1 到 file2 ，如果 file2 存在会提示是否覆盖：cp -i file1 file2 。

# tail命令

> 原文：[https://zwmst.com/583.html](https://zwmst.com/583.html)

tail 命令默认显示文件最后的 10 行文本：tail filename.txt 。
你可以使用 -n 选项指定要显示的行数：tail -n N filename.txt 。
你也可以使用 -f 选项进行实时查看，这个命令执行后会等待，如果有新行添加到文件尾部， 它会继续输出新的行，在查看日志时这个选项会非常有用。
你可以通过 CTRL-C 终止命令的执 行：tail -f log-file 。

# grep命令

> 原文：[https://zwmst.com/585.html](https://zwmst.com/585.html)

在文件中查找字符串(不区分大小写)：grep -i "the" demo_file 。
输出成功匹配的行，以及该行之后的三行：grep -A 3 -i "example" demo_text 。
在一个文件夹中递归查询包含指定字符串的文件：grep -r "ramesh" * 。

# sed命令

> 原文：[https://zwmst.com/587.html](https://zwmst.com/587.html)

当你将 Dos 系统中的文件复制到 Unix/Linux 后，这个文件每行都会以 \r\n 结尾，sed 可以 轻易将其转换为 Unix 格式的文件，使用\n 结尾的文件：sed ‘s/.$//’ filename 。
反转文件内容并输出：sed -n ‘1!G; h; p’ filename 。
为非空行添加行号：sed ‘/./=’ thegeekstuff.txt | sed ‘N; s/\n/ /’ 。

# 用sed命令将指定的路径/usr/local/http替换成为/usr/src/local/http？

> 原文：[https://zwmst.com/589.html](https://zwmst.com/589.html)

echo "/usr/local/http/" | sed ‘s#/usr/local/#/usr/src/local/#’

# 打印/etc/ssh/sshd_config的第一百行？

> 原文：[https://zwmst.com/591.html](https://zwmst.com/591.html)

sed -n ‘100p’ /etc/ssh/sshd_config

# awk命令

> 原文：[https://zwmst.com/596.html](https://zwmst.com/596.html)

删除重复行：$ awk ‘!($0 in array) { array[$0]; print}’ temp 。
打印 /etc/passwd 中所有包含同样的 uid 和 gid 的行：awk -F ‘:’ ‘$3=$4’ /etc/passwd 。
打印文件中的指定部分的字段：awk ‘{print $2,$5;}’ employee.txt 。

# 打印/etc/passwd的1到3行？

> 原文：[https://zwmst.com/598.html](https://zwmst.com/598.html)

使用 sed 命令：sed -n ‘1,3p’ /etc/passwd
使用 awk 命令：awk ‘NR>=1&&NR<=3{print $0}' /etc/passwd

# vim命令

> 原文：[https://zwmst.com/600.html](https://zwmst.com/600.html)

打开文件并跳到第 10 行：vim +10 filename.txt 。

打开文件跳到第一个匹配的行：vim +/search-term filename.txt 。

以只读模式打开文件：vim -R /etc/passwd 。

# diff命令

> 原文：[https://zwmst.com/602.html](https://zwmst.com/602.html)

比较的时候忽略空白符：diff -w name_list.txt name_list_new.txt 。

# sort命令

> 原文：[https://zwmst.com/604.html](https://zwmst.com/604.html)

以升序对文件内容排序：sort names.txt 。

以降序对文件内容排序：sort -r names.txt 。

以第三个字段对 /etc/passwd 的内容排序：sort -t: -k 3n /etc/passwd | more 。

# xargs命令

> 原文：[https://zwmst.com/606.html](https://zwmst.com/606.html)

将所有图片文件拷贝到外部驱动器：ls *.jpg | xargs -n1 -i cp {} /external-harddrive/directory 。

将系统中所有 jpg 文件压缩打包：find / -name *.jpg -type f -print | xargs tar -cvzf images.tar.gz 。

下载文件中列出的所有 url 对应的页面：cat url-list.txt | xargs wget –c 。

# 把当前目录下所有后缀名为.txt的文件的权限修改为777？

> 原文：[https://zwmst.com/608.html](https://zwmst.com/608.html)

方式一，使用 xargs 命令：find ./ -type f -name ".txt" |xargs chmod 777

方式二，使用exec命令：find ./ -type f -name ".txt" -exec chmod 777 {}

# tar命令

> 原文：[https://zwmst.com/610.html](https://zwmst.com/610.html)

创建一个新的 tar 文件： tar cvf archive_name.tar dirname/ 。

解压 tar 文件：tar xvf archive_name.tar 。

查看 tar 文件：tar tvf archive_name.tar 。

# gzip命令

> 原文：[https://zwmst.com/612.html](https://zwmst.com/612.html)

创建一个 *.gz 的压缩文件：gzip test.txt 。

解压 *.gz 文件：gzip -d test.txt.gz 。

显示压缩的比率：gzip -l *.gz 。

# bzip2命令

> 原文：[https://zwmst.com/614.html](https://zwmst.com/614.html)

创建 *.bz2 压缩文件：bzip2 test.txt 。

解压 *.bz2 文件：bzip2 -d test.txt.bz2 。

# unzip命令

> 原文：[https://zwmst.com/616.html](https://zwmst.com/616.html)

解压 *.zip 文件：unzip test.zip 。

查看 *.zip 文件的内容：unzip -l jasper.zip 。

# export命令

> 原文：[https://zwmst.com/618.html](https://zwmst.com/618.html)

输出跟字符串 oracle 匹配的环境变量：export | grep ORCALE 。

设置全局环境变量：export ORACLE_HOME=/u01/app/oracle/product/10.2.0 。

# yum命令

> 原文：[https://zwmst.com/620.html](https://zwmst.com/620.html)

使用 yum 安装 apache ：yum install httpd 。

更新 apache ：yum update httpd 。

卸载/删除 apache ：yum remove httpd 。

# rpm命令

> 原文：[https://zwmst.com/622.html](https://zwmst.com/622.html)

使用 rpm 安装 apache ：rpm -ivh httpd-2.2.3-22.0.1.el5.i386.rpm 。

更新 apache ：rpm -uvh httpd-2.2.3-22.0.1.el5.i386.rpm 。

卸载/删除 apache ：rpm -ev httpd 。

# shutdown命令

> 原文：[https://zwmst.com/624.html](https://zwmst.com/624.html)

关闭系统并立即关机：shutdown -h now 。

10 分钟后关机：shutdown -h +10 。

重启：shutdown -r now 。

重启期间强制进行系统检查：shutdown -Fr now 。

# service命令

> 原文：[https://zwmst.com/626.html](https://zwmst.com/626.html)

service 命令用于运行 System V init 脚本，这些脚本一般位于 /etc/init.d 文件下，这个命令 可以直接运行这个文件夹里面的脚本，而不用加上路径。

查看服务状态：service ssh status 。

查看所有服务状态：service –status-all 。

重启服务：service ssh restart 。

# whereis命令

> 原文：[https://zwmst.com/628.html](https://zwmst.com/628.html)

当你不知道某个命令的位置时可以使用 whereis 命令，下面使用 whereis 查找 ls 的位置： whereis ls 。

当你想查找某个可执行程序的位置，但这个程序又不在 whereis 的默认目录下，你可以使用 B 选项，并指定目录作为这个选项的参数。

下面的命令在 /tmp 目录下查找 lsmk 命令： whereis -u -B /tmp -f lsmk 。

# 用一条命令显示本机eth0网卡的IP地址，不显示其它字符？

> 原文：[https://zwmst.com/630.html](https://zwmst.com/630.html)

方法一

ifconfig eth0|grep inet|awk -F ‘:’ ‘{print $2}’|awk ‘{print $1}’

方法二

ifconfig eth0|grep "inet addr"|awk -F ‘[ :]+’ ‘{print $4}’

方法三

ifconfig eth0|awk -F ‘[ :]+’ ‘NR==2 {print $4}’

方法四

ifconfig eth0|sed -n ‘2p’|sed ‘s#^.addr:##g’|sed ‘s# Bc.$##g’

方法五

ifconfig eth0|sed -n ‘2p’|sed -r ‘s#^.addr:(.) Bc.*$#\1#g’

方法六

(CENTOS7 也适用)： ip addr|grep eth0|grep inet|awk ‘{print $2}’|awk -F ‘/’ ‘{print $1}’

# 如何禁止服务器被ping？

> 原文：[https://zwmst.com/632.html](https://zwmst.com/632.html)

echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all

# 设置DNS需要修改哪个配置文件？

> 原文：[https://zwmst.com/634.html](https://zwmst.com/634.html)

全局的配置，可以在 /etc/resolv.conf 文件中配置。

指定网卡的配置，可以在 /etc/sysconfig/network-scripts/ifcfg-eth0 文件中配置。

# 在Linux下如何指定dns服务器，来解析某个域名？

> 原文：[https://zwmst.com/636.html](https://zwmst.com/636.html)

使用谷歌 DNS 解析百度：dig @8.8.8.8 www.baidu.com

# 1010.Linux 中主要有哪几种内核锁?

> 原文：[https://zwmst.com/5307.html](https://zwmst.com/5307.html)

Linux 的同步机制从 2.0 到 2.6 以来不断发展完善。从最初的原子操作,到后来的信号量,从大内核锁到今天的自旋锁。这些同步机制的发展伴随 Linux 从单处理器到对称多处理器的过渡;
伴随着从非抢占内核到抢占内核的过度。Linux 的锁机制越来越有效,也越来越复杂。
Linux 的内核锁主要是自旋锁和信号量。
自旋锁最多只能被一个可执行线程持有,如果一个执行线程试图请求一个已被争用(已经被持有)的自旋锁,那么这个线程就会一直进行忙循环——旋转——等待锁重新可用。要是锁未被争用,请求它的执行线程便能立刻得到它并且继续进行。自旋锁可以在任何时刻防止多于一个的执行线程同时进入临界区。
Linux 中的信号量是一种睡眠锁。如果有一个任务试图获得一个已被持有的信号量时,信号量会将其推入等待队列,然后让其睡眠。这时处理器获得自由去执行其它代码。当持有信号量的进程将信号量释放后,在等待队列中的一个任务将被唤醒,从而便可以获得这个信号量。
信号量的睡眠特性,使得信号量适用于锁会被长时间持有的情况;只能在进程上下文中使用,因为中断上下文中是不能被调度的;另外当代码持有信号量时,不可以再持有自旋锁。
Linux 内核中的同步机制:原子操作、信号量、读写信号量和自旋锁的 API,另外一些同步机制,包括大内核锁、读写锁、大读者锁、RCU (Read-Copy Update,顾名思义就是读-拷贝修改),和顺序锁。

# 1011.Linux 中的用户模式和内核模式是什么含意?

> 原文：[https://zwmst.com/5309.html](https://zwmst.com/5309.html)

MS-DOS 等操作系统在单一的 CPU 模式下运行,但是一些类 Unix 的操作系统则使用了双模式,可以有效地实现时间共享。在 Linux 机器上,CPU 要么处于受信任的内核模式,要么处于受限制的用户模式。除了内核本身处于内核模式以外,所有的用户进程都运行在用户模式之中。
内核模式的代码可以无限制地访问所有处理器指令集以及全部内存和 I/O 空间。如果用户模式的进程要享有此特权,它必须通过系统调用向设备驱动程序或其他内核模式的代码发出请求。另外,用户模式的代码允许发生缺页,而内核模式的代码则不允许。
在 2.4 和更早的内核中,仅仅用户模式的进程可以被上下文切换出局,由其他进程抢占。除非发生以下两种情况,否则内核模式代码可以一直独占 CPU:

1.  它自愿放弃 CPU;
2.  发生中断或异常。

2.6 内核引入了内核抢占,大多数内核模式的代码也可以被抢占。

# 1012.怎样申请大块内核内存?

> 原文：[https://zwmst.com/5311.html](https://zwmst.com/5311.html)

在 Linux 内核环境下,申请大块内存的成功率随着系统运行时间的增加而减少,虽然可以通过vmalloc 系列调用申请物理不连续但虚拟地址连续的内存,但毕竟其使用效率不高且在 32 位系统上 vmalloc 的内存地址空间有限。所以,一般的建议是在系统启动阶段申请大块内存,但是其成功的概率也只是比较高而已,而不是 100%。如果程序真的比较在意这个申请的成功与否,只能退用“启动内存”(Boot Memory)。下面就是申请并导出启动内存的一段示例代码:

```
void* x_bootmem = NULL;
EXPORT_SYMBOL(x_bootmem);
unsigned long x_bootmem_size = 0;
EXPORT_SYMBOL(x_bootmem_size);
static int __init x_bootmem_setup(char *str)
{
x_bootmem_size = memparse(str, &str);
x_bootmem = alloc_bootmem(x_bootmem_size);
printk(“Reserved %lu bytes from %p for x\n”, x_bootmem_size, x_bootmem);
return 1;
}
__setup(“x-bootmem=”, x_bootmem_setup);
```

可见其应用还是比较简单的,不过利弊总是共生的,它不可避免也有其自身的限制:
内存申请代码只能连接进内核,不能在模块中使用。
被申请的内存不会被页分配器和 slab 分配器所使用和统计,也就是说它处于系统的可见内存之外,即使在将来的某个地方你释放了它。
一般用户只会申请一大块内存,如果需要在其上实现复杂的内存管理则需要自己实现。
在不允许内存分配失败的场合,通过启动内存预留内存空间将是我们唯一的选择。

# 1013.用户进程间通信主要哪几种方式?

> 原文：[https://zwmst.com/5313.html](https://zwmst.com/5313.html)

1.  管道(Pipe):管道可用于具有亲缘关系进程间的通信,允许一个进程和另一个与它有共同祖先的进程之间进行通信。
2.  命名管道(named pipe):命名管道克服了管道没有名字的限制,因此,除具有管道所具有的功能外,它还允许无亲缘关系进程间的通信。命名管道在文件系统中有对应的文件名。命名管道通过命令 mkfifo 或系统调用 mkfifo 来创建。
3.  信号(Signal):信号是比较复杂的通信方式,用于通知接受进程有某种事件发生,除了用于进程间通信外,进程还可以发送信号给进程本身;linux 除了支持 Unix 早期信号语义函数 sigal外,还支持语义符合 Posix.1 标准的信号函数 sigaction(实际上,该函数是基于 BSD 的,BSD为了实现可靠信号机制,又能够统一对外接口,用 sigaction 函数重新实现了 signal 函数)。
4.  消息(Message)队列:消息队列是消息的链接表,包括 Posix 消息队列 system V 消息队列。有足够权限的进程可以向队列中添加消息,被赋予读权限的进程则可以读走队列中的消息。消息队列克服了信号承载信息量少,管道只能承载无格式字节流以及缓冲区大小受限等缺
5.  共享内存:使得多个进程可以访问同一块内存空间,是最快的可用 IPC 形式。是针对其他通信机制运行效率较低而设计的。往往与其它通信机制,如信号量结合使用,来达到进程间的同步及互斥。
6.  信号量(semaphore):主要作为进程间以及同一进程不同线程之间的同步手段。
7.  套接字(Socket):更为一般的进程间通信机制,可用于不同机器之间的进程间通信。起初是由 Unix 系统的 BSD 分支开发出来的,但现在一般可以移植到其它类 Unix 系统上:Linux 和System V 的变种都支持套接字。

# 1014.通过伙伴系统申请内核内存的函数有哪些?

> 原文：[https://zwmst.com/5315.html](https://zwmst.com/5315.html)

在物理页面管理上实现了基于区的伙伴系统(zone based buddy system)。对不同区的内存使用单独的伙伴系统(buddy system)管理,而且独立地监控空闲页。相应接口alloc_pages(gfp*mask, order),* _get_free_pages(gfp_mask, order)等。

# 1015.Linux 虚拟文件系统的关键数据结构有哪些?(至少写出四个)

> 原文：[https://zwmst.com/5317.html](https://zwmst.com/5317.html)

struct super_block,struct inode,struct file,struct dentry;

# 1016.对文件或设备的操作函数保存在那个数据结构中?

> 原文：[https://zwmst.com/5319.html](https://zwmst.com/5319.html)

struct file_operations

# 1017.Linux 中的文件包括哪些?

> 原文：[https://zwmst.com/5321.html](https://zwmst.com/5321.html)

执行文件,普通文件,目录文件,链接文件和设备文件,管道文件。

# 1018.创建进程的系统调用有那些?

> 原文：[https://zwmst.com/5323.html](https://zwmst.com/5323.html)

clone(),fork(),vfork();系统调用服务例程:sys_clone,sys_fork,sys_vfork;

# 1019.调用 schedule()进行进程切换的方式有几种?

> 原文：[https://zwmst.com/5325.html](https://zwmst.com/5325.html)

1.系统调用 do_fork();
2.定时中断 do_timer();
3.唤醒进程 wake_up_process
4.改变进程的调度策略 setscheduler();
5.系统调用礼让 sys_sched_yield();

# 1020.Linux 调度程序是根据进程的动态优先级还是静态优先级来调度进程的?

> 原文：[https://zwmst.com/5327.html](https://zwmst.com/5327.html)

Liunx 调度程序是根据根据进程的动态优先级来调度进程的,但是动态优先级又是根据静态优先级根据算法计算出来的,两者是两个相关联的值。因为高优先级的进程总是比低优先级的进程先被调度,为防止多个高优先级的进程占用 CPU 资源,导致其他进程不能占有 CPU,所以引用动态优先级概念

# 1021.进程调度的核心数据结构是哪个?

> 原文：[https://zwmst.com/5329.html](https://zwmst.com/5329.html)

struct runqueue

# 1022.如何加载、卸载一个模块?

> 原文：[https://zwmst.com/5332.html](https://zwmst.com/5332.html)

nsmod 加载,rmmod 卸载

# 1023.模块和应用程序分别运行在什么空间?

> 原文：[https://zwmst.com/5334.html](https://zwmst.com/5334.html)

模块运行在内核空间,应用程序运行在用户空间

# 1024\. Linux 中的浮点运算由应用程序实现还是内核实现?

> 原文：[https://zwmst.com/5336.html](https://zwmst.com/5336.html)

应用程序实现,Linux 中的浮点运算是利用数学库函数实现的,库函数能够被应用程序链接后调用,不能被内核链接调用。这些运算是在应用程序中运行的,然后再把结果反馈给系统。Linux 内核如果一定要进行浮点运算,需要在建立内核时选上 math-emu,使用软件模拟计算浮点运算,据说这样做的代价有两个:用户在安装驱动时需要重建内核,可能会影响到其他的应用程序,使得这些应用程序在做浮点运算的时候也使用 math-emu,大大的降低了效率。

# 1025.模块程序能否使用可链接的库函数?

> 原文：[https://zwmst.com/5338.html](https://zwmst.com/5338.html)

模块程序运行在内核空间,不能链接库函数。

# 1026.TLB 中缓存的是什么内容?

> 原文：[https://zwmst.com/5340.html](https://zwmst.com/5340.html)

TLB,页表缓存,当线性地址被第一次转换成物理地址的时候,将线性地址和物理地址的对应放到 TLB 中,用于下次访问这个线性地址时,加快转换速度。

# 1027.Linux 中有哪几种设备?

> 原文：[https://zwmst.com/5342.html](https://zwmst.com/5342.html)

字符设备和块设备。网卡是例外,他不直接与设备文件对应,mknod 系统调用用来创建设备文件。

# 1028.字符设备驱动程序的关键数据结构是哪个?

> 原文：[https://zwmst.com/5344.html](https://zwmst.com/5344.html)

字符设备描述符 struct cdev,cdev_alloc()用于动态的分配 cdev 描述符,cdev_add()用于注册一个 cdev 描述符,cdev 包含一个 struct kobject 类型的数据结构它是核心的数据结构

# 1029.设备驱动程序包括哪些功能函数?

> 原文：[https://zwmst.com/5346.html](https://zwmst.com/5346.html)

open(),read(),write(),llseek(),realse();

# 1030.如何唯一标识一个设备?

> 原文：[https://zwmst.com/5348.html](https://zwmst.com/5348.html)

Linux 使用一个设备编号来唯一的标示一个设备,设备编号分为:主设备号和次设备号,一般主设备号标示设备对应的驱动程序,次设备号对应设备文件指向的设备,在内核中使用 dev_t 来表示设备编号,一般它是 32 位长度,其中 12 位用于表示主设备号,20 位用于表示次设备号,利用 MKDEV(int major,int minor);用于生成一个 dev_t 类型的对象。

# 1031.Linux 通过什么方式实现系统调用

> 原文：[https://zwmst.com/5350.html](https://zwmst.com/5350.html)

靠软件中断实现的,首先,用户程序为系统调用设置参数,其中一个编号是系统调用编号,参数设置完成后,程序执行系统调用指令,x86 上的软中断是有 int 产生的,这个指令会导致一个异常,产生一个事件,这个事件会导致处理器跳转到内核态并跳转到一个新的地址。并开始处理那里的异常处理程序,此时的异常处理就是系统调用程序。

# 1032.Linux 软中断和工作队列的作用是什么?

> 原文：[https://zwmst.com/5352.html](https://zwmst.com/5352.html)

Linux 中的软中断和工作队列是中断处理。

1.  软中断一般是“可延迟函数”的总称,它不能睡眠,不能阻塞,它处于中断上下文,不能进城切换,软中断不能被自己打断,只能被硬件中断打断(上半部),可以并发的运行在多个 CPU 上。
    所以软中断必须设计成可重入的函数,因此也需要自旋锁来保护其数据结构。
2.  工作队列中的函数处在进程上下文中,它可以睡眠,也能被阻塞,能够在不同的进程间切换。已完成不同的工作。
    可延迟函数和工作队列都不能访问用户的进程空间,可延时函数在执行时不可能有任何正在运行的进程,工作队列的函数有内核进程执行,他不能访问用户空间地址
---
title: CS130 Review
date: 2024-09-25 17:34:32
tags:
toc: true
---

## 架构
| processor | memory | disk | node |
|:-:|:-:|:-:|:-:|
| thread | addresses | file |
| process    | 

## 核心概念
**Thread 线程**:
    – Single unique execution context (PC, Registers, Execution Flags, Stack) 

**Process 进程**:
    - 一个地址空间/文件描述符/文件系统. 一或多个线程.

![threads & processes](threads_processes.png)

**TCB (Thread Control Block)**:
    - Holds contents of registers when thread is not running.

**Address Space**:
    - distinct from the memory space of the physical machine.



|Section |Address |  
|-|-|
|Stack| 0xffff |
|Heap| |
|Static Data| |
|Code| 0x0000|

**用户态/内核态**:
![user mode](user-kernel-mode.png)

三种状态切换的方式:
- **Syscall**: 进程对系统服务的请求(read/ write/ exit...), 不包含地址, 系统将id与参数存入寄存器,随后执行. (refer pintos/userprog/syscall.c).
- **Interrupt**: 外部异步的事件启动了上下文切换, 如时钟/io设备, 独立于用户进程.
- **Exception**: 内部同步的实践启动了上下文切换, 如段错误/除以零错误, etc

## 进程管理 
> refer to pintos/userprog/process.c
- **Atomic Operation**: 不可分割的操作. 

### data structure
#### TCB
#### PCB
```c
  pcb = palloc_get_page(0);
  if (pcb == NULL) {
    goto execute_failed;
  }

  // pid is not set yet. Later, in start_process(), it will be determined.
  // so we have to postpone afterward actions (such as putting 'pcb'
  // alongwith (determined) 'pid' into 'child_list'), using context switching.
  pcb->pid = PID_INITIALIZING;
  pcb->parent_thread = thread_current();

  pcb->cmdline = cmdline_copy;
  pcb->waiting = false;
  pcb->exited = false;
  pcb->orphan = false;
  pcb->exitcode = -1; // undefined

  sema_init(&pcb->sema_initialization, 0);
  sema_init(&pcb->sema_wait, 0);
```
来自`pintos > userprog > process.c > process_execute()`

多进程与多线程： multiplexing & context switch: 基于*内存*的交换

<!-- 抽象->具象 signal->syscall: 
- voluntarily yield
- interrupt  -->

### Multiplexing: 多进程处理&调度

**多级队列**: 将队列分入多个子队列(前台/后台,etc),每个子队列有各自的调度算法. 每个队伍获得一定的时间片(16ms, 8ms, 非抢占的, etc).
- **多级反馈队列**:多级队列,每个队列具有不同的优先级. 一个进程可以在队列之间切换(Aging).

多级反馈队列的参数: 
- 队列的数量
- 每队的调度算法
- 其他原则
    - 升级/降级进程的原则
    - 当进程需要系统服务时进入的队列

应对用户不当的使用--例如一个进程使用大量无意义的i/o以维持优先级:   

多级反馈队列的目标:
- 可靠, 低开销, 无starvation, 分优先级, 公平

- **Linux的CFS调度器**: 

- **内存开销, 其他加速方法**:

## 内存的用户/内核区域：地址转换


地址转换
多层 page table 的寻址， inverted page table相关的内容
参考hw2: 页表！


核心：
- offset + limit，( base & bound )  
**基址和边界**是指虚拟内存的一种简单形式，其中对计算机内存的访问由一组或多组称为基址和边界寄存器的处理器寄存器控制. 最简单的形式是为每个用户进程分配**一个连续的主内存段**。操作系统将该段的物理地址加载到基址寄存器中，并将其大小加载到边界寄存器中。程序看到的虚拟地址被添加到基址寄存器的内容中以生成物理地址。根据边界寄存器的内容检查地址，以防止进程访问超出其分配段的内存。

- offset + physical page, ( paging )
- heap & stack, ( segment )
支持离散的地址空间

 
### 减少数据移动：caching data & address (TLB)
核心： hit rate


### conection

critical section - shared resource
目标 : atomic operation, mutal exclusion
实现：lock -> semaphore (counter + lock)


## 持久化数据：文件系统
核心：索引 (inode)
- inode 与 page 的对应

### ext2文件系统
**inode**: 包含关于文件或目录的大小,权限,所有权与磁盘位置的数据.及12个指向块的指针,2个指向1级间接块的指针,1个指向2级间接块的指针.
inode / ext2文件系统

### 内存不足：virtual memory
核心：swapping (memory <-> disk)
#### page fault
page fault 



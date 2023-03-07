# GNU相关命令学习记录
![](/image/20191102195053346.png)
**linux下程序执行流程：**
 - Shell 接收到命令后，在操作系统中使用 fork() 创建一个新的进程。
 - 在子进程中使用 execve() 加载 a.out。操作系统内核中的加载器识别出 a.out 是一个动态链接文件，做出必要的内存映射，从 ld-linux-x86-64.so 的代码开始执行，把动态链接库映射到进程的地址空间中，然后跳转到 a.out 的 _start 执行，初始化 C 语言运行环境，最终开始执行 main。
 - 程序运行过程中，如需进行输入/输出等操作 (如 libc 中的 putchar)，则会使用特殊的指令 (例如 x86 系统上的 int 或syscall) 发出系统调用请求操作系统执行。典型的例子是 printf 会调用 write 系统调用，向编号为 1 的文件描述符写入数据
## 常用编译知识
1. 对源文件直接编译形成的文件一般默认为`Shared object file`,即动态链接库。如果想要编译成可执行文件，需要加`-static`命令
## 常用编译命令
 - `-E`: 预处理,宏展开，生成`.i`文件
 - `-S`: 编译，生成汇编代码，`.s`文件
 - `-c`: 汇编生成目标代码，`.o`文件
 - `-m32`: 编译成32位的程序
 - `-static`: 编译成可执行文件，静态库，会链接`libc`
 - `-fPIC -shared`:生成位置无关的动态库
 - `--verbose`: 可以查看所有编译选项
 - `-Wl,--verbose`: 可以查看所有链接选项
## 链接命令 `ld`
 - `-Ttext`:指定程序执行的入口地址，此地址为虚拟地址
 - `-e`:指定程序起始的函数名为`main`,默认的入口函数为`_start`
## `obj` 命令
- `objcopy`:拷贝文件，一般用于格式转换
    ```makefile
    <!-- 将elf格式的kernel.bin的elf header去掉复制到sysytem.bin中 -->
    $(BUILD)/system.bin:$(BUILD)/kernel.bin
	objcopy -O binary $< $@
    ```
- `objdump`: 反汇编命令
## gdb调试
 - `starti`: 启动程序，并在第一条指令上暂停
 - `b` : 设置断点
 - `c` : continue 继续执行
 - `q` : 退出调试
 - `bt f` :  backtrace full，打印堆栈信息
 - `info inferiors` :  打印进程/线程信息
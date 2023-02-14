# linux相关命令学习记录
 - `man`：列出某个可执行程序的参数选项，例如 `man bochs`
 - `nm`：nm 命令显示关于指定 File 中符号的信息，文件可以是对象文件、可执行文件或对象文件库。所谓符号，通常指定义出的函数，全局变量等等。
    ```bash
    <!-- nm kernel.bin -->
    timer@DESKTOP-O5HGP7D:~/onix/build$ nm kernel.bin 
    00013013 B __bss_start
    00013013 D _edata
    00013420 B _end
    00010000 T _start
    00013020 B buf
    0001000d T kernel_init
    00013000 D magic
    00013004 D message
    <!-- 第一列是当前符号的地址，第二列是当前符号的类型，第三列是当前符号的名称。 -->
    ```
    - B 该符号的值出现在非初始化数据段(BSS)中。例如，在一个文件中定义全局static int test。则该符号test的类型为b，位于bss section中。其值表示该符号在bss段中的偏移。一般而言，bss段分配于RAM中。
    - D 该符号位于初始化数据段中。一般来说，分配到data section中。
    - T 该符号位于代码区text section。
- `sort`:排序命令，可对一个文件排序后输出到另一个文件
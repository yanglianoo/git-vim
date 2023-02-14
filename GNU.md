# GNU相关命令学习记录
![](/image/20191102195053346.png)
## 常用编译知识
1. 对源文件直接编译形成的文件一般默认为`Shared object file`,即动态链接库。如果想要编译成可执行文件，需要加`-static`命令
## 常用编译命令
 - `-E`: 预处理,宏展开，生成`.i`文件
 - `-S`: 编译，生成汇编代码，`.s`文件
 - `-c`: 汇编生成目标代码，`.o`文件
 - `-m32`: 编译成32位的程序
 - `static`: 编译成可执行文件，静态库
## 链接命令 `ld`
 - `-Ttext`:指定程序执行的入口地址，此地址为虚拟地址
 - `-e`:指定程序起始的函数名为`main`
## `obj` 命令
- `objcopy`:拷贝文件，一般用于格式转换
    ```makefile
    <!-- 将elf格式的kernel.bin的elf header去掉复制到sysytem.bin中 -->
    $(BUILD)/system.bin:$(BUILD)/kernel.bin
	objcopy -O binary $< $@
    ```

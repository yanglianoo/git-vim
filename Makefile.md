# Makefile 学习记录

## 变量

- **变量定义**

变量定义语法：

**延时变量**：使用时才确定该值。
**即时变量**：定义时立即确定该值。

|   形式   |                             说明                             |
| :------: | :----------------------------------------------------------: |
| A = xxx  |                           延时变量                           |
| B ?= xxx | 延时变量，只有第一次定义时赋值才成功，若曾被定义过，则此赋值无效。 |
| C := xxx |                           立即变量                           |
| D += yyy | 如果D在前面是延时变量，那么现在它还是**延时变量** 如果D在前面是立即变量，那么它现在还是**立即变量** |

```makefile
#可以直接采用`=`或者`:=`，使用变量时需要`$( )`，例子如下：
#定义变量
BUILD:=../build
SRC:=.
ENTRYPOINT:=0x10000 #内核入口地址
$(BUILD)/boot/%.bin: #使用BUILD变量
```

- 内置变量

```makefile
# $(CC) 指向当前使用的编译器
```

- 自动变量

```makefile
$@ :指代当前目标
$< :指代第一个前置条件
$^ :指代所有前置条件
#例如如下代码
$(BUILD)/boot/%.bin: $(SRC)/boot/%.asm
	$(shell mkdir -p $(dir $@))
	nasm -f bin $< -o $@
$@ 代表$(BUILD)/boot/%.bin
$< 代表$(SRC)/boot/%.asm
```
## 函数
- `wildcard`      
`wildcard`是GNU Make中的一个函数，用于获取指定路径下的文件列表。该函数的基本语法如下：
	```makefile
	$(wildcard pattern)
	```
	
	其中，pattern表示需要匹配的文件名模式，可以包含通配符，如 * 或 ? 等。wildcard函数会根据指定的pattern，返回匹配到的文件列表。如果没有匹配到任何文件，则返回空字符串。
	例如，以下代码将获取src目录下所有以.c为后缀名的文件列表：    

	```makefile
	$(wildcard src/*.c)
	```
	
	如果src目录下有三个.c文件，分别是file1.c、file2.c和file3.c，则该函数的返回值为：

	```makefile
	src/file1.c src/file2.c src/file3.c
	```
	
- `patsubst`        
	patsubst是GNU Make中的一个函数，用于将指定字符串中匹配某个模式的部分替换成另一个字符串。该函数的基本语法如下：     
	```makefile
	$(patsubst pattern,replacement,string)
	```
	其中，pattern表示需要匹配的字符串模式，可以包含通配符，如 * 或 % 等；replacement表示替换后的字符串，可	以使用通配符替换匹配到的部分；string表示需要进行替换的原始字符串。    
	例如，以下代码将把SRCS中所有以.c为后缀名的文件转换成对应的.o文件，并将它们存储在OBJS变量中：
	```makefile
	OBJS=$(patsubst src/%.c,obj/%.o,$(SRCS))
	```
	在这个例子中，pattern是"src/%.c"，其中 % 表示匹配任意非空字符，replacement是"obj/%.o"，用来替换匹配到的部分，string是$(SRCS)，即需要被替换的原始字符串。
## 杂项

- Makefile中使用`shell`命令，

```makefile
#在makefile中要使用shell 命令必须加shell,使用方式为 $(shell )，如下
$(BUILD)/boot/%.bin: $(SRC)/boot/%.asm
	$(shell mkdir -p $(dir $@))
```


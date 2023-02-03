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

## 杂项

- Makefile中使用`shell`命令，

```makefile
#在makefile中要使用shell 命令必须加shell,使用方式为 $(shell )，如下
$(BUILD)/boot/%.bin: $(SRC)/boot/%.asm
	$(shell mkdir -p $(dir $@))
```


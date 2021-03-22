# 第十章 Shell工具

### 1. cut

​	cut的工作就是“剪”，具体的说就是在文件中负责剪切数据用的。cut命令从文件的每一行剪切字节、字符和字段并将这些字节、字符和字段输出。

#### 1. 基本用法

​	cut[选项参数] filename

说明：默认分隔符是制表符

#### 2. 选项参数说明

-f 列号，提取第几列

-d 分隔符，按照指定分隔符分割列

#### 3. 案例实操

（1）切割cut.txt第一列

```
sh-3.2# cut -d " " -f 1 cut.txt 
Java
Python
C
C++
C#
V
```

（2）切割cut.txt第二、三列

```
sh-3.2# cut -d " " -f 2,3 cut.txt 
Java
Pyton
C
 C++
 C#
 VB
```

（3）在cut.txt文件中切割出Python

```
sh-3.2# cut -d " " -f 1 cut.txt | grep Python
Python
```

（4）选取系统PATH变量值，第2个“： ”开始后的所有路径

```
sh-3.2# echo $PATH | cut -d : -f 3-
/bin:/usr/sbin:/sbin:/usr/local/share/dotnet:~/.dotnet/tools:/Library/Apple/usr/bin:/Library/Frameworks/Mono.framework/Versions/Current/Commands
```

（5）切割ifconfig后打印的IP地址

```
sh-3.2# ifconfig en0 | grep "inet " | cut -d " " -f 2 
192.168.1.6
```

### 2. sed

​		sed是一种**流编辑器**，它一次处理一行内容。处理时，把当前处理的行存储在临时缓冲区中，成为“模式空间”，接着用sed命令处理缓冲区中的内容，处理完成后，把缓冲区的内容送往屏幕。接着处理下一行，这样不断重复，直到文件末尾。**文件内容并没有改变**，除非你使用重定向储存输出。

#### 1. 基本用法

sed[选项参数] 	'command' filename

#### 2. 选项参数说明

-e 直接在指定列模式上进行sed的动作编辑

#### 3. 命令功能描述

a 新增，a的后面可以接子串，在下一行出现

d 删除

s 查找并替换

#### 4. 案例实操

（1）将"Java Coding"这个词组插入到sed.txt第二行下，打印

```
root@wells  18:22:16 ~]# sed "2a Java Coding" sed.txt
dong shen
guan zhen
Java Coding
wo  wo
lai  lai
le  le
```

（2）删除sed.txt文件中所有包含wo的行

```
root@wells  18:22:28 ~]# sed "/wo/d" sed.txt
dong shen
guan zhen
lai  lai
le  le
```

```
sh-3.2# sed '/wo/d' sed.txt
dong shen
guan zhen
lai  lai
le  le
```

（3）将sed.txt文件中wo替换为ni

```
sh-3.2# sed "s/wo/ni/g" sed.txt 
dong shen
guan zhen
ni  ni
lai  lai
le  le
```

（4）将sed.txt文件中的第二行删除并将wo替换成ni

```
sh-3.2# sed -e "2d" -e "s/wo/ni/g" sed.txt
dong shen
ni  ni
lai  lai
le  le
```


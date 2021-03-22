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

### 3. awk

​	一个强大的文本分析工具，把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行分析处理。

#### 1. 基本用法

awk[选项参数] 'pattern1{action1} pattern2{action2}...' filename

pattern: 表示awk在数据中查找的内容，就是匹配模式

action: 在找到匹配内容时所执行的一系列命令

#### 2. 选项参数说明

-F 指定输入文件折分隔符

-v 赋值一个用户定义变量

#### 3. 案例实操

（1）数据准备

```
➜  ~ sudo cp /etc/passwd ./
```

（2）搜索passwd文件以root关键字开头的所有行，并输出改行的第7列

```
➜  ~ awk -F : '/^root/{print $7}' passwd
/bin/sh
```

（3）搜索passwd文件以root关键字开头的所有行，并输出该行的第1列和第7列，中间以“，”号隔开

```
➜  ~ awk -F : '/^root/{print $1,$7}' passwd 
root /bin/sh
```

（4）只显示/etc/passwd的第一列和第七列，以逗号分隔，且在所有行前面添加列名user，shell在最后一行添加"dahaige, /bin/zuishuai"

```
➜  ~ awk -F : 'BEGIN{print "user,shell"} {print $1","$7} END{print "dahaige, bin/zuishuai"}' passwd
```

注意：BEGIN在所有数据读取行之前执行；END在所有数据执行之后执行。

（5）将passed文件中的用户id增加数值1并输出

```
➜  ~ awk -F : -v i=1 '{print $3+$i}' passwd
```

#### 4. awk的内置变量

FILENAME 文件名

NR 已读的记录数

NF 浏览记录的域的个数（切割后，列的个数）

#### 5. 案例实操

（1）统计passed文件名，每行的行号，每行的列数

```
➜  ~ awk -F : '{print FILENAME "," NR "," NF}' passwd
```

（2）切割IP

```
➜  ~ ifconfig en0 | grep "inet " | awk -F : '{print $2}' | awk -F " " '{print $1}'
```

（3）查询sed.txt中空行所在的行号

```
➜  ~ awk '/^$/ {print NR}' sed.txt
```

### 4. sort

​	sort命令在Linux里非常有用，它将文件进行排序，并将plexus结果标准输出

#### 1. 基本语法

​	sort(选项)(参数)

-n 依照数值的大小排序

-r 以相反的顺序来排序

-t 设置排序时所用的分隔字符

-k 指定需要排序的列

参数：指定待排序的文件列表

#### 2. 案例实操

（0）数据准备

```
➜  ~ vi sort.sh
bb:40:5.4
hd:20:4.2
xz:50:2.3
cls:10:3.
```

（1）按照": "分割后的第2列排序排序

```
➜  ~ sort -t : -nrk 2 sort.sh 
xz:50:2.3
bb:40:5.4
ss:30:1.6
hd:20:4.2
cls:10:3.5
```




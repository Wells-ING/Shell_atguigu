# 第八章 read读取控制台输入

### 1. 基本语法

​	read(选项)(参数)

​	选项：

​		-p: 指定读取值时的提示符

​		-t: 指定读取值等待的时间（秒）

### 2. 项目实操

​	（1）提示7秒内，读取控制台输入的名称

```shell
#!/bin/bash

read -t 7 -p "input your name " NAME

echo $NAME
```


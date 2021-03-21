# 第三章 Shell脚本入门

### 1. 脚本要求

​		脚本以**#!/bin/bash**开头（指定解释器）

### 2. 第一个Shell脚本：Hello World

（1）需求：创建一个Shell脚本，输出Hello World

1. 创建helloworld.sh文件

2. 写入内容

   ```shell
   #!/bin/bash
   echo "Hello World"
   ```

3. 执行文件
   1. sh helloworld.sh
   2. bash helloworld.sh
   3. zsh helloworld.sh（Mac）
   4. ./helloworld.sh（需要修改文件权限）

### 3. 第二个Shell脚本：多命令处理

（1）需求：在/Users/wells下创建一个wells.txt，在wells.txt文件中增加“I love coding”

1. 创建batch.sh文件

2. 写入内容

   ```shell
   #!/bin/bash
   
   cd /Users/wells/
   touch wells.txt
   echo "I love coding" >> wells.txt
   ```

3. 执行文件
# 第二章 Shell解释器

（1）Mac(Unix内核)提供的Shell解释器有：

```sehll
wells@Wells ~ % cat /etc/shells
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/bash
/bin/csh
/bin/dash
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

（2）CentOS提供的Shell解释器有：

```
root@wells  15:37:04 ~]# cat /etc/shells
/bin/sh
/bin/bash
/usr/bin/sh
/usr/bin/bash
```

​	bash与sh的关系为：sh是bash的软连接

（3）CentOS默认的解析器是bash

```
root@wells  15:38:49 ~]# echo $SHELL
/bin/bash
```

（4）Mac默认的解析器是zsh

```
wells@Wells ~ % echo $SHELL
/bin/zsh
```


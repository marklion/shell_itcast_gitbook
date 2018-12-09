## 2.1 shell脚本

学习目标：

1. 了解 shell脚本的内容小技巧

2. 掌握 shell脚本的标准执行方法
3. 掌握 shell脚本的开发规范和开发小技巧

---

### 2.1.1 创建脚本

**脚本创建工具：**

&ensp;&ensp;&ensp;&ensp;创建脚本的常见编辑器是   vi/vim

**脚本命名：**

1. shell脚本的命名简单来说就是要有意义，方便我们通过脚本名，来知道这个文件是干什么用的
2. 文件名以.sh结尾


 **脚本内容：**
 
1. 首行指定解释器  #!/bin/bash

2. 命令罗列和语法套用


 **注释内容：**

- 单行注释：

&ensp;&ensp;&ensp;&ensp;除了首行的#不是注释外，其他所有行内容，只要首个字符是#,那么就表示该行是注释

```bash
#!/bin/bash
echo '1'
# echo '2'           # 这一行就表示注释
echo '3'
```

- 多行注释：

&ensp;&ensp;&ensp;&ensp;多行注释有两种方法：:<<! ... !  和 :<<字符 ... 字符

```bash
#!/bin/bash
echo '1'
:<<! echo '2'
echo '3'
echo '4'
!
echo '5'
```

### 2.1.2 脚本执行

**shell执行的方式：**

Shell脚本的执行通常可以采用以下几种方式
```bash
bash /path/to/script-name  或   /bin/bash /path/to/script-name    （强烈推荐使用）
/path/to/script-name   或  ./script-name    （当前路径下执行脚本）
source script-name  或  . script-name    （注意“.“点号后面有空格）
```

**执行方式说明：**

1. 脚本文件本身没有可执行权限或者脚本首行没有命令解释器时使用的方法，我们推荐用bash执行。

   使用频率：☆☆☆☆☆

2. 脚本文件具有可执行权限时使用。

   使用频率：☆☆☆☆

3. 使用source或者.点号，加载shell脚本文件内容，使shell脚本内容环境和当前用户环境一致。

   使用频率：☆☆☆

   使用场景：环境一致性
   
区别：source或者.点号与其他执行方式的比较

```bash
  test.sh 脚本内容如下：
  #!/bin/bash
  ps
  
  终端执行命令如下：
  python@ubuntu:~/Desktop$ ps  # 返回当前终端运行的进程
   PID TTY          TIME CMD
  34863 pts/1    00:00:00 bash  # 当前终端开启的bash进程
  34891 pts/1    00:00:00 ps
  python@ubuntu:~/Desktop$ bash test.sh 
   PID TTY          TIME CMD
  34863 pts/1    00:00:00 bash  # 当前终端开启的bash进程
  34894 pts/1    00:00:00 bash  # 执行bash test.sh命令时开启了一个子进程
  34895 pts/1    00:00:00 ps
  python@ubuntu:~/Desktop$ source test.sh 
   PID TTY          TIME CMD
  34863 pts/1    00:00:00 bash  # 只有当前终端开启的bash进程，执行
  34900 pts/1    00:00:00 ps
```

```bash
  test.sh 脚本内容如下：
  #!/bin/bash
  echo $user
  
  终端执行命令如下：
  python@ubuntu:~/Desktop$ user=python  # 当前终端定义变量
  python@ubuntu:~/Desktop$ echo $user  # 打印变量
  python
  python@ubuntu:~/Desktop$ bash test.sh  # 使用bash方式会开子进程，不能使用当前终端定义的变量

  python@ubuntu:~/Desktop$ source test.sh # 使用source方式不会开子进程，能使用当前终端定义的变量
  python
```

总结：source或者.点号执行方式不会开启子进程，能共享当前终端定义的变量，其他执行方式会开启子进程

**执行机制：**

![](/assets/shell_exec.png)

### 2.1.2 脚本开发规范

1. 脚本命名要有意义，文件后缀是.sh

2. 脚本文件首行**是而且必须是**脚本解释器

   ```bash
   #!/bin/bash
   ```

3. 脚本文件解释器后面要有脚本的基本信息等内容

4. 脚本文件中尽量不用中文注释

   ```bash
   尽量用英文注释，防止本机或切换系统环境后中文乱码的困扰
   常见的注释信息：脚本名称、脚本功能描述、脚本版本、脚本作者、联系方式等
   ```

5. 脚本文件常见执行方式：bash 脚本名

6. 脚本内容执行：从上到下，依次执行

7. 代码书写优秀习惯

   ```bash
   1. 成对内容的一次性写出来,防止遗漏。
      如：()、{}、[]、''、``、""
   2. []中括号两端要有空格,书写时即可留出空格[    ],然后再退格书写内容
   3. 流程控制语句一次性书写完，再添加内容
   ```

8. 通过缩进让代码易读(即该有空格的地方就要有空格)


**小结：**

1. shell脚本命名：有意义，便于知道脚本的目的

2. shell脚本的注释：单行(#)、多行(:<<字符 ... 字符)

3. shell脚本标准执行方法： /bin/bash /path/to/script-name

4. shell脚本开发规范重点：2-4-5

5. shell脚本开发小技巧：6-7

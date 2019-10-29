# centos解决bash: service: command not found 错误
 
在centos系统中，如果/sbin目录下没有service这个命令，就会出现
```
bash: service: command not found
```
解决步骤如下：
>1. 输入
```
yum list | grep initscripts
```
> 会出现
```
initscripts.x86_64
```
> （其实一共有三个信息，但是后面根据版本不同，显示的信息也不同）
> 2. 上面给出了可安装软件的yum源版本，然后执行
```
yum install initscripts -y
```
> 3. 此时service命令就可用了
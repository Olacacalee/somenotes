# 通过ockerfile将centos镜像增加ssh服务

> 对应的Dockerfile内容如下：
```
#拉取Centos镜像
FROM centos:7.0
#作者信息
MAINTAINER liuli<1224979840@qq.com>
#设置亚洲时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone
#安装openssh-server
RUN yum install -y openssh-server \
    #修改配置 
    && sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config \
    #安装openssh-clients
    && yum  install -y openssh-clients \
    #修改root密码
    && echo "root" | passwd --stdin root \
    #生成密钥
    && ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key \
    && ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key \
    #清除yum安装缓存
    && yum clean all
#设置支持中文字符
RUN locale \
    && localedef -i zh_CN -c -f UTF-8 zh_CN.UTF-8 \
    && echo "export LC_ALL=zh_CN.UTF-8" >> /etc/profile && source /etc/profile \
ENV LANG zh_CN.UTF-8
ENV LC_CTYPE zh_CN.UTF-8
#暴露22端口
EXPOSE 22
#执行后台启动ssh服务命令
CMD ["/usr/sbin/sshd", "-D"]
```
> 构建镜像
```
docker build -t centos-ssh:7.0 .
```
> 启动容器
```
docker run -d -p10022:22 --name centos centsos
```
# helm安装

Helm 的安装方式很多，这里采用二进制的方式安装。更多安装方法可以参考 Helm 的官方帮助文档。

> 方式一：使用官方提供的脚本一键安装
```
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get > get_helm.sh
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```
> 方式二：手动下载安装
```
#从官网下载最新版本的二进制安装包到本地：https://github.com/kubernetes/helm/releases
tar -zxvf helm-2.9.0.tar.gz # 解压压缩包
# 把 helm 指令放到bin目录下
mv helm-2.9.0/helm /usr/local/bin/helm
helm help # 验证
```

# helm使用

> 创建Chart模板
```
helm create mychart
```
> helm初始化
```
helm init
```
> 先移除原先的仓库
```
helm repo remove stable
```
> 添加新的仓库地址
```
helm repo add stable https://kubernetes.oss-cn-hangzhou.aliyuncs.com/charts

helm repo add  --cert-file /root/harbor/ssl/harbor.crt --key-file /root/harbor/ssl/harbor.key --username=admin --password=Harbor12345 stable https://harbor.google.net/chartrepo/stable
```
> 仓库列表
```
helm repo list
```
> 更新仓库
```
helm repo update
```
> 搜索chart
```
helm search xxx
```
> 安装chart
```
helm install -n releaseName --namespace namespaceName stable/mysql --version 5.6.7
```
> 删除release
```
helm delete --purge releaseName
```
> 安装push插件
```
helm init 
helm plugin install https://github.com/chartmuseum/helm-push
```
> helm打包
```
helm package mychart
```
> helm push
```
helm push --username=admin --password=Harbor12345 app myrepo
```

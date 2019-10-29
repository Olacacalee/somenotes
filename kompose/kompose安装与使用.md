# 安装kompose

> Linux
```
curl -L https://github.com/kubernetes/kompose/releases/download/v1.19.0/kompose-linux-amd64 -o kompose
chmod +x kompose
sudo mv ./kompose /usr/local/bin/kompose
```
> Mac
```
curl -L https://github.com/kubernetes/kompose/releases/download/v1.19.0/kompose-darwin-amd64 -o kompose
chmod +x kompose
sudo mv ./kompose /usr/local/bin/kompose
```
# 使用

> 1. 装换成k8s的文件
```
kompose convert -f xxx.yaml
```
> 2. 装换成Chart
```
kompose convert -c -f xxx.yaml
```
> 3. 生成NodePort需要在docker-compose增加
```
labels:
      kompose.service.type: nodeport
```
> 4. 生成Ingress需要在docker-compose增加
```
labels:
      kompose.service.expose: "xxx.baidu.com"
```

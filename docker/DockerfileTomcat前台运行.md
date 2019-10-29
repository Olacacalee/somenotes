# Dockerfile Tomcat 前台运行

```
如果使用我们常用的startup.sh作为容器启动脚本，容器会自动关闭，此时Tomcat在后台运行，没有在前台运行的线程

Dockerfile 文件最后加上

EXPOSE 8080

CMD ["catalina.sh", "run"]
```
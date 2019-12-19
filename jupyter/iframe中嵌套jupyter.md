### iframe中嵌套jupyter会报



```
在/root/.jupyter/jupyter_notebook_config.py  的文件增加一行
c.NotebookApp.tornado_settings = { 'headers': { 'Content-Security-Policy': "frame-ancestors https://*:* http://*:*   'self' " }} > 
```
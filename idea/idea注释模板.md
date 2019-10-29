##IDEA自定义注释模板（主要解决params和return的问题）


#### 问题
之前设置idea liveTemplate 方法注释的时候，按照网上的教程params,return参数无法获取，现在终于解决这个问题了。

#### 解决
1. settings -> Editor -> Live Templates
2. 新建自己的分组和自己的模板，这都不说了，界面如图
3. 重点：Abbreviation那里不要用/开头的！！！
4. 重点：模板中开头不要/!!!，从*号开始！！！模板如下：
5. 关联文件，如java、scala
6. 编辑变量，Edit variables

>  其中params变量的内容一定要放在Default value中！！！内容为：
```
groovyScript("if(\"${_1}\".length() == 2) {return '';} else {def result=''; def params=\"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split(',').toList();for(i = 0; i < params.size(); i++) {if(i==0){result+='* @Param ' + params[i] + ': '}else{result+='\\n' + ' * @Param ' + params[i] + ': '}}; return result;}", methodParameters());
```
>  其中return变量的内容也一定要放在Default value中！！！内容为：
```
groovyScript("def returnType = \"${_1}\"; def result = '* @return: ' + returnType; return result;", methodReturnType());
```

7. 应用，确定
8. 重点：注释时需要自己打/符号，然后再打*，然后tab，这样就可以获取了！！！


一定要自己打出来/*，然后tab，其实就是自己打的 / 然后 * 再tab让idea自动补充模板的内容，正好是/**…的内容，然后这样就能获取到params内容了！！！
# 一些配置

- [js替换所有空格为&nbsp](#jstihuan)

> 1. java IDE中报OutOfMemory异常一般都是因为给IDE分配的内存不足，导致内存溢出。解决方法：
```
-Xms256M -Xmx1024M -XX:PermSize=64M -XX:MaxPermSize=128M
```
> 2. Spring 启动加载配置选项的参数，以便根据不同的环境加载不同的配置文件：
```
 -Dspring.profiles.active=development  -Dfile.encoding=UTF-8
```
> 3. 我们在写Java实体对象的时候，一般都要写好属性以及属性的getter和setter方法。那么用一个插件就可以解决这个问题，省去很多繁杂的工作 Lombok
```
1.setting→plugins→Browse repositories2.输入lom后选择install plugin3.按照提示重启IDEA4.
```
> 4. 一般我们看到毛玻璃的效果很是漂亮，它们大多是用图片处理工具做的，那么CSS也可以。
```
 -webkit-filter: blur(10px); /* Chrome, Opera */
-moz-filter: blur(10px);
-ms-filter: blur(10px);    
    filter: blur(10px);
```
> 5. 在Chrome中使用临时记事本
```
data:text/html, <html contenteditable> 
```
> 6. 有一种情况就是在浏览器通过http访问服务器的接口或者其它资源，它总是会在调用接口之前自动变成https
```
原因是在Tomcat下的conf目录中的server.xml文件中端口配置加了scheme="https"
```

> 7. docker 如何查看已存在的容器所挂载的目录？
```
docker inspect container_name | grep Mounts -A 20 
```
> 8. linux给用户添加sudo权限： 
有时候，linux下面运行sudo命令，会提示类似： 
xxxis not in the sudoers file.  This incident will be reported. 
这里，xxx是用户名称，然后导致无法执行sudo命令，这时候，如下解决：
```
1. 进入超级用户模式。也就是输入"su -",系统会让你输入超级用户密码，输入密码后就进入了超级用户模式。（当然，你也可以直接用root用）
2. 添加文件的写权限。也就是输入命令"chmod u+w /etc/sudoers"。 
3. 编辑/etc/sudoers文件。也就是输入命令"vim /etc/sudoers",进入编辑模式，找到这一 行："root ALL=(ALL) ALL"在起下面添加"xxx ALL=(ALL) ALL"(这里的xxx是你的用户名)，然后保存退出。
4. 撤销文件的写权限。也就是输入命令"chmod u-w /etc/sudoers"。 
然后就行了。
```
> 9. 在filter里注入被注解的bean

```
filter 可以正常注入bean用org.springframework.web.filter.DelegatingFilterProxy 代理
**web.xml**
<filter>
    <filter-name>YourFilter</filter-name>
    <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
    <init-param> 
        <param-name>targetFilterLifecycle</param-name> 
        <param-value>true</param-value>     
    </init-param>  
</filter>

```
> 10. redis增加密码，在配置redis的地方加上以下配置即可
```
<property name="password" value="123456"/>
```
> 11. 两个域名指向同一个项目，并且Tomcat中只有一个地方配置sessionCookieDomain，解决方法如下:

```
在Tomcat中配置两个host，然后就可以配置两个server.xml
```
> 12. 百度网盘中大文件无法直接下载，那么用以下方法可以。
需要注意的是：必须把文件分享，并且所有人都能看到才能执行以下脚本

```
$.ajax({
type: "POST",
url: "/api/sharedownload?sign="+yunData.SIGN+"&timestamp="+yunData.TIMESTAMP,
data: "encrypt=0&product=share&uk="+yunData.SHARE_UK+"&primaryid="+yunData.SHARE_ID+"&fid_list=%5B"+yunData.FS_ID+"%5D",
dataType: "json",
success: function(d){ 
window.location.href = d.list[0].dlink;
}
});
```
> 13. mysql查询后会自动排序，取消自动排序：

```
select * from programming WHERE  delete_flag=1 and programming_id in ( 4 , 2 , 5 ) ORDER BY field(programming_id, 
4 , 2 , 5 ) 
```
> 14. maven仓库速度慢。配置很简单，修改conf文件夹下的settings.xml文件，添加如下镜像配置：

```
 <mirrors>
    <mirror>
      <id>alimaven</id>
      <name>aliyun maven</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>        
    </mirror>
  </mirrors>
```
> 15. js替换所有空格为&nbsp

```
var s = str.replace(/\s/g, "&nbsp");
```
> 16. 像电影里黑客高手一样敲代码攻击入侵网站！屌到爆的装逼神器 ！

```
[link](http://www.iplaysoft.com/hackertyper.html#0-tsina-1-63150-397232819ff9a47a7b7e80a40613cfe1)
```
> 17. 在线工具

```
https://123.w3cschool.cn/webtools#0-tsina-1-38129-397232819ff9a47a7b7e80a40613cfe1
```
> 18. 两个list合并去重的方法是：

```
 A.removeAll(B); A.addAll(B);
```
> 19. Intellj Idea控制台乱码解决方案：

```
在bin目录下找到idea.exe.vmoptions，如果你的电脑是64位的，那么就找到idea64.exe.vmoptions，在最后加入：
-Dfile.encoding=UTF-8
在tomcat启动中加：
-Dfile.encoding=UTF-8
如果仍然不行，那么在设置中找到File Encoding，把编码设置成UTF-8
```
> 20. Incorrect string value: '\xE7\xA8\x8B\xE5\xBA\x8F...' for column 'course' at row 1
出现这个错误的原因是，数据库的编码格式为latin1 而我要将utf8的中文插入到数据库中。
一开始修改  修改数据库的编码

```
alter table score default character set utf8; 
alter table score change score score varchar(50) character utf8;  
或者直接把表删除重建
```
> 21. 从Excel导入到数据库中数据的时候，由于有某些特殊空格或者字符，导致以后数据的不匹配，解决办法：

```
str.replaceAll("[\\s*|\\u0020*|\\u3000*|\\u2002*|\\u202c*]", "")
```
> 22. 数据库链接超时，默认8小时，解决方案：

```
在spring链接数据库配置中添加如下：
<!-- 获取前检测连接是否有效 -->
<property name="testOnBorrow" value="${jdbc.pool.testOnBorrow}" />
<!-- 验证连接 -->
<property name="validationQuery" value="${jdbc.pool.validationQuery}" />

相关properties中配置：
jdbc.pool.testOnBorrow=true
jdbc.pool.validationQuery=SELECT 1
```
> 23. spring jpa在@ManyToOne时，如果对应的One为空时，会报错：javax.persistence.EntityNotFoundException: Unable to find com.cn.dao.entity.
解决方法如下：
```
@OneToOne(optional=false)
@JoinColumn(name="business_id")

@NotFound(action=NotFoundAction.IGNORE)

private Business business;
```
> 24. mysql添加账号、密码

```
select user,host,authentication_string from mysql.user;
 
grant all privileges on *.* to test@"localhost" identified by "123456";
flush privileges;
 
grant all privileges on *.* to test@"%" identified by "123456";
flush privileges;
 
```
> 25. oss通过服务器挂载的方式将文件放到指定目录后，oss不识别文件类型，文件的contentType为application/octet-stream。该类型通过浏览器直接访问，会下载，不会在浏览器上预览。解决方法如下：

```
可以通过代码去更改OSS上文件的ContentType：
private void changeContentType(String key) {
    OSSClient ossClient = new OSSClient("end-point", "key", "secret");
    OSSObject object = ossClient.getObject("bucket",key);//key是文件路径，但是不能以斜杠/开头
    object.getObjectMetadata().setContentType("text/html");
    ossClient.putObject("bucket",key,object.getObjectContent());
}
```
> 26.  MySQL查询当前数据库中所有记录不为空的表 
 
```
select TABLE_NAME from information_schema.tables where TABLE_SCHEMA='当前数据库' and table_rows>0;
```
 > 27. docker运行一个mysql容器
 
```
sudo docker run --name first-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
```
 > 28. 数据库左右关联以及内关联
 
```
left join 
 查询出左边表的所有数据，右边跟左边有关联的查出来，没有的话显示null
right join
 查询出右边表的所有数据，左边跟右边有关联的查出来，没有的话显示null
inner join 
只查询出左边跟右边都有的数据，如果左边或者右边有一边没有，不显示
```
 > 29. 去除文本中的HTML标签
 
```
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class HTMLSpirit{
    public static String delHTMLTag(String htmlStr){
        String regEx_script="<script[^>]*?>[\\s\\S]*?<\\/script>"; //定义script的正则表达式
        String regEx_style="<style[^>]*?>[\\s\\S]*?<\\/style>"; //定义style的正则表达式
        String regEx_html="<[^>]+>"; //定义HTML标签的正则表达式

        Pattern p_script=Pattern.compile(regEx_script,Pattern.CASE_INSENSITIVE);
        Matcher m_script=p_script.matcher(htmlStr);
        htmlStr=m_script.replaceAll(""); //过滤script标签

        Pattern p_style=Pattern.compile(regEx_style,Pattern.CASE_INSENSITIVE);
        Matcher m_style=p_style.matcher(htmlStr);
        htmlStr=m_style.replaceAll(""); //过滤style标签

        Pattern p_html=Pattern.compile(regEx_html,Pattern.CASE_INSENSITIVE);
        Matcher m_html=p_html.matcher(htmlStr);
        htmlStr=m_html.replaceAll(""); //过滤html标签

        return htmlStr.trim(); //返回文本字符串
    }

    public static void main(String[] args) {
        String str = "<p><strong><span style=\"color: rgb(176, 176, 176); font-family: &quot;Microsoft YaHei&quot;, 微软雅黑, SimSun, 宋体, sans-serif; font-size: 12.6px; background-color: rgb(255, 255, 255);\">德州仪器 (TI) 是一家跨国性的半导体设计与制造公司。 因具有 100,000+ 个以上模拟 IC 和嵌入式处理器而独树一帜、同时兼备软件、工具以及业界最大的销售团队/技术支持团队。</span></strong></p>";
        System.out.println(delHTMLTag(str));
    }
}
```
> 30. centos 7更改字体大小

```
修改文件/boot/grub2/grub.cfg

找到 linux16 /vmlinuz-3.10.0-229.11.1.el7.x86_64 root=/dev/mapper/centos-root ro rd.lvm.lv=centos/root rd.lvm.lv=centos/swap crashkernel=auto rhgb quiet.utf8 systemd.debug

增加
vga=32A

```
> 31. 启动docker，并且把docker设置成开机启动

```
$ sudo systemctl start docker
$ sudo systemctl enable docker
```
> 32. sql：根据分数排名
```

科目     成绩    排名              科目        成绩    排名

数学      90       1                 数学        90      1

语文      90       1                  语文        90     1

政治     85        3                 政治         85     2

#这是第一种的显示
seclet 科目,成绩,(
          select count(成绩）+1 
               from table_name where 成绩>t.成绩)
      from table_name as t 
     order by 成绩 desc
#第二中的显示类似   可以是加distinct 或者 是不加distinct而用分组group by一个意思
seclet 科目,成绩,(
          select count(distinct 成绩) 
               from table_name where 成绩>=t.成绩)
      from table_name as t 
     order by 成绩 desc
```
> 33. MYSQL5.7版本sql_mode=only_full_group_by问题
```
1、查看sql_mode

select @@global.sql_mode
查询出来的值为：

ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION

2、去掉ONLY_FULL_GROUP_BY，重新设置值。

set @@global.sql_mode ='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
```

> 34. Base32编码与解码
```
public static String base36Encoding(long number){
        if(number<36){
            return String.valueOf(ALPHABET.charAt((int)number));
        }
        String b36 = "";
        while (number!=0){
            int n = (int)(number%36);
            number = number/36;
            b36 = String.valueOf(ALPHABET.charAt(n))+b36;
        }
        return b36;

    }

    public static long base36Decoding(String str){
        str = str.trim();
        str = new StringBuilder(str).reverse().toString();
        if(str.length() < 1)
            throw new IllegalArgumentException("str must not be empty.");
        long result = 0;
        for (int i = 0; i < str.length(); i++) {
            result += ALPHABET.indexOf(str.charAt(i)) * Math.pow(36, i);
        }
        return result;
    }
```
### js替换所有空格为&nbsp

> 35. 安装MySQL 8，用root用户在MySQL Workbench连接数据库是报错：

Authentication plugin 'caching_sha2_password' cannot be loaded: dlopen(/usr/local/mysql/lib/plugin/caching_sha2_password.so, 2): image not found
```
查询mysql库的user表：

mysql>use mysql; 
mysql>select user, host, plugin from user\G; 
*************************** 2. row *************************** 
                 user: root 
                 host: % 
               plugin: caching_sha2_password 
root用户使用caching_sha2_password插件加密，原因就是客户端没有caching_sha2_password插件。

修改root密码加密方式为：mysql_native_password

ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
```
> 36. github上的项目树形结构Chrome插件
```
octotree
```
> 37. 在网页调取QQ聊天框
```
<a  href="javascript:;" onclick="loadQQ()">
          <img border="0" style="display: initial;" src="http://wpa.qq.com/pa?p=2:624577661:41 &r=0.28504395019850864" alt="点击这里给我发消息" title="点击这里给我发消息">
         </a>
 var loadQQ = function () {
    /*个人qq*/
    $("#getSignQQ").remove();
    var frame = document.createElement("iframe");
    frame.id = "getSignQQ";
    frame.src = "https://wpa.qq.com/msgrd?v=3&uin=3498761529&site=qq&menu=yes"
    frame.style.display = "none";
    document.body.appendChild(frame);
  }
```
> 38. redis批量删除
```
redis-cli -p 6380 -a 123456 keys "cms:tenant:301*" | xargs redis-cli -p 6380 -a 123456 del
```
> 39. Linux设置系统时间
```
1、查看系统时间
   date                                         
2、设置当前系统时间为2015年5月8日19点48分0秒
   date  -s "2015-5-8 19:48:00" 
```
> 39. mysql查询，group by之后查询出较大的值
```
select max(student_id) from student where tenant_id = 1062 group by no having count(1)>1
```
> 40. 下载网易云音乐
```
http://music.163.com/song/media/outer/url?id=xxxxxxx.mp3
```
> 41. mysql链接数据库总是出现超时或者丢失链接
```
1. 设置timeout时间
2. 在Windows上，是微软的一个补丁引起的，即：KB967723
  解决办法：

打开注册表：

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
在里面添加两项：

数值名称： MaxUserPort 
值类型: DWORD
值数据： 65534
有效范围： 5000-65534 (十进制)
默认值： 0x1388 (5000 十进制)
说明： 此参数将控制程序从系统请求任何可用的用户端口时使用的最大端口数。 通常，1024 的值和包含的 5000 之间分配临时的 （短) 端口。
 

数值名称： TcpTimedWaitDelay
值类型: DWORD
值数据： 30  （十进制）
默认值：  240 ( 十进制)

修改完成后，重启计算机，即可解决问题。

另，网上有一个方法是卸载这个补丁或关闭自动更新，此方法不可取也不安全
3. 之前使用高校邦的框架会出现问题，后来使用JDBC链接数据库解决
```
> 42. 使用navicat 连接 mysql 8.0.11 报  "2059 - authentication plugin 'caching_sha2_password' ..."
```
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';

原因：mysql 8.0 默认使用 caching_sha2_password 身份验证机制 —— 从原来的 mysql_native_password 更改为 caching_sha2_password。 
从 5.7 升级 8.0 版本的不会改变现有用户的身份验证方法，但新用户会默认使用新的 caching_sha2_password 。
客户端不支持新的加密方式。
```
> 43. mybatis 一对多无法返回子对象结果集
```
在配置文件中加入 <setting name="autoMappingBehavior" value="FULL"/>
```
> 44. Google扩展程序
```
  1. 划词翻译
  2. 购物党
  3. Octotree
  4. 掘金
  5. AdBlock Plus
```
> 45. 在CentOS中加入sl命令，跑小火车
```
  1. yum update
  2. yum install wget
  3. wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
  4. rpm -ivh epel-release-6-8.noarch.rpm
  5. yum install sl
  6. sl
```

> 46. java调用elasticsearch的时候总是报错 NoNodeAvailableException[None of the configured nodes are available: [{#transport#-1}{I7ebp0-GS7eI-UKnjb9J-w}{127.0.0.1}{127.0.0.1:9300}]]
```
 1. 端口要用9300，因为9200是用于浏览器访问，9300是tcp是用于client调用
 2. 当前elasticsearch的版本与java中使用的elasticsearch的jar包的版本不一致
```
> 47. 使用logstash-codec-avro插件从kafka中解码时，对于int或者long类型的数字解码后值不正确，原因是配置logstash的input中kafka的配置少了解析配置,正确配置如下
```
input {
    kafka {
        bootstrap_servers => ["127.0.0.1:9092"]
        group_id => "logstash"
        topics => ["json_gxb_modulename_x_test"]
        key_deserializer_class => "org.apache.kafka.common.serialization.StringDeserializer"
        value_deserializer_class => "org.apache.kafka.common.serialization.ByteArrayDeserializer"
        codec => avro {
            schema_uri => "/Users/cayley/Downloads/elk/schema/GxbJSONEventRecord.avsc"
        }
    }
}
output {
     file{
          path => "/Users/cayley/Downloads/file.txt"
     }
}
```
> 48. ELK日志使用index过滤后不起作用
```
在logstash的配置文件中增加type类型，不同的type输出到不同的index，配置如下：
input {
 kafka {
    bootstrap_servers => ["192.168.30.80:9092"]
    group_id => "logstash"
    topics => ["json_gxb_hybrid_signup"]
    type => "json"
    key_deserializer_class => "org.apache.kafka.common.serialization.StringDeserializer"
    value_deserializer_class => "org.apache.kafka.common.serialization.ByteArrayDeserializer"
    consumer_threads => 5
    codec => avro {
        schema_uri => "/usr/share/logstash/schema/GxbJSONEventRecord.avsc"
    }
  }
}
output {

  if[type] == "json"{
    elasticsearch{
       hosts=> "http://192.168.70.27:9200"
       index=> "json-gxb-hybird-%{+YYYY.MM.DD}"
    }
  }

}
```
> 49. Java读取properties配置文件时，中文乱码解决方法
```
public static String getConfig(String key) {
    Properties pros = new Properties();
    String value = "";
    try {
        pros.load(new InputStreamReader(Object.class.getResourceAsStream("/properties.properties"), "UTF-8"));
        value = pros.get(key).toString();
    } catch (IOException e) {
        log.error(e.getMessage());
    }
    return value;
}
```
> 50. 使用Jsoup爬虫访问HTTPS网站报错unable to find valid certification path to requested target。解决方法如下：
```
忽略掉SSL即可：
Jsoup.connect(url)
.timeout(30000)
.userAgent(UA)
.validateTLSCertificates(false)
.get()
```


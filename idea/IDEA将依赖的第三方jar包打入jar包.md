使用Idea编译器，用自定义UDF在hive中清洗数据、处理数据，这时，使用的一些第三方jar包，在服务器上没有，打出来的udf的jar包也只有几k，不包含所依赖的jar包。所以运行时会报错，这时该怎么处理呢？
在pom文件中添加如下代码，然后等待mvn加载完成，点击右边的maven projects，点击life cycle的package。或者在Terminal中输入mvn package。这时去target下看自己打成的jar包里包含了所依赖的jar包。

```
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.4.3</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                    <configuration>
                        <filters>
                            <filter>
                                <artifact>*:*</artifact>
                                <excludes>
                                    <exclude>META-INF/*.SF</exclude>
                                    <exclude>META-INF/*.DSA</exclude>
                                    <exclude>META-INF/*.RSA</exclude>
                                </excludes>
                            </filter>
                        </filters>
                        <transformers>
                            <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                <mainClass></mainClass>
                            </transformer>
                        </transformers>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>

```
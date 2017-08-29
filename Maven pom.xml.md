Maven pom.xml 配置问题
====
## 1、maven-javadoc-plugin 插件报错
### 用Maven打包带javadoc项目，提示错误信息如下：
```
Failed to execute goal org.apache.maven.plugins:maven-javadoc-plugin:2.9.1:jar
MavenReportException: Error while creating archive: 
Unable to find javadoc command: 
The environment variable JAVA_HOME is not correctly set.
```
出现这个问题，是因为JAVA_HOME指向了JRE而不是JDK    
`所以解决办法是在maven javadoc插件中手动配置：`
```
<javadocExecutable>${java.home}/../bin/javadoc</javadocExecutable>
```
讲上面的代码添加到 `<properties>` 即可，就像这样：
```
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <java.version>1.8</java.version>
    <javadocExecutable>${java.home}/../bin/javadoc</javadocExecutable>
</properties>
```



## 2、打包时，不想执行test文件
在 build 里 ，加入如下代码就好
```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>2.18.1</version>
    <configuration>
        <skipTests>true</skipTests>
    </configuration>
</plugin>
```


## 3、将本地Jar包打包到maven项目中
```
<plugins>
    <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>2.3.2</version>
        <configuration>
            <source>1.7</source>
            <target>1.7</target>
            <encoding>UTF-8</encoding>
            <compilerArguments>
                <extdirs>${basedir}/lib</extdirs>
            </compilerArguments>
        </configuration>
    </plugin>
 </plugins> 
```

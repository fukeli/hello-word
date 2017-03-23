这是一个随记文本
===
1、maven下载包慢的问题
---
>在~/.m2/新建一个文件settings.xml，内容如下：
```
<settings>
    <mirrors>
        <mirror>
            <id>nexus-aliyun</id>
            <mirrorOf>*</mirrorOf>
            <name>Nexus aliyun</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public</url>
        </mirror>
    </mirrors>
</settings>
```
欢迎进入我的github，[提出建议](https://github.com/fukeli)

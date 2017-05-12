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

2、强制覆盖本地数据--git
---
```
git fetch --all  
git reset --hard origin/master 
git pull
```

3、idea修改默认注释
----
>在设置里面找到：
```
Editor->File and Code Templates
```
>在选项卡里，找到Includes ，选中File Header 并修改
```
/**
 * @ClassName: 
 * @Description:
 * @author: youname
 * @data: ${YEAR}年${MONTH}月${DAY}日 ${TIME}
 */

```

4、idea 修改快捷键
----
>找到keymap
```
Main menu -> Code -> Completion -> Basic   //修改代码提示
Main menu -> Code -> Folding -> Comment with Line Comment  //注释行
Editor Actions -> Delete Line  //删除行
```

5、mac 卸载jdk
---
>删除 /Library/Java/JavaVirtualMachines/ 下的jdk版本，如：
```
sudo rm -rf /Library/Java/JavaVirtualMachines/jdk1.8.0_40.jdk
```

Elastic 相关bug
====
## 1、java.lang.NoSuchFieldError: FAIL_ON_SYMBOL_HASH_OVERFLOW
该错误是jdk版本冲突导致，检查服务器jdk是否和elastic环境相同


欢迎进入我的github，[提出建议](https://github.com/fukeli)<br>
文件参考[zgj0315](https://github.com/zgj0315)

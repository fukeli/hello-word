Elastic安装部署
====

### max size virtual memory [52729364480] for user [elastic] is too low, increase to [unlimited]
```
vi /etc/security/limit.conf
*  - as unlimited
```

### system call filters failed to install; check the logs and fix your configuration or disable system call filters at your own risk

```
修改es配置文件 添加
bootstrap.system_call_filter: false   
# 针对 system call filters failed to install, 参见 https://www.elastic.co/guide/en/elasticsearch/reference/current/system-call-filter-check.html
```

### max virtual memory areas vm.max_map_count [65530] likely too low, increase to at least [262144]
```
vi /etc/sysctl.conf 
添加：
vm.max_map_count=262144
执行：
sysctl -p
```


### ./bin/kibana: line 24: /home/hx_es/kibana-5.4.0-darwin-x86_64/bin/../node/bin/node: cannot execute binary file
### ./bin/kibana: line 24: /home/hx_es/kibana-5.4.0-darwin-x86_64/bin/../node/bin/node: 成功
这个错误的原因好像是 下载的kibana版本不对 或者 是 系统是32位的可是下载的kibana是64位的



x-pack-transport.jar下载  pom文件
------
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <modelVersion>4.0.0</modelVersion>
  <groupId>org.elasticsearch.client</groupId>
  <artifactId>x-pack-transport</artifactId>
  <version>5.4.1</version>
  <dependencies>
    <dependency>
      <groupId>org.elasticsearch.plugin</groupId>
      <artifactId>x-pack-api</artifactId>
      <version>5.4.1</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.elasticsearch.client</groupId>
      <artifactId>transport</artifactId>
      <version>5.4.1</version>
      <scope>compile</scope>
    </dependency>
  </dependencies>
  <licenses>
    <license>
      <name>Elastic Commercial Software End User License Agreement</name>
      <url>https://www.elastic.co/eula/</url>
      <distribution>repo</distribution>
    </license>
  </licenses>
  <developers>
    <developer>
      <name>Elastic</name>
      <url>http://www.elastic.co</url>
    </developer>
  </developers>
  <name>transport-client</name>
  <description>Elasticsearch subproject :x-pack-elasticsearch:transport-client</description>
  <url>https://github.com/elastic/x-pack-elasticsearch</url>
  <scm>
    <url>git@github.com:elastic/x-pack-elasticsearch.git</url>
  </scm>
</project>

```

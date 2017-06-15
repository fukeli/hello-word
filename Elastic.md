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

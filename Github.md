Mac升级导致git报错：Can't start Git: /usr/bin/git Probably the path to Git executable is not valid
===


Mac从OS X 10.11升级到OS X 10.12后，使用git时报错：

```
Can't start Git: /usr/bin/git Probably the path to Git executable is not valid.
```

使用xcode-select执行安装后就可以了：
```
xcode-select --install
```

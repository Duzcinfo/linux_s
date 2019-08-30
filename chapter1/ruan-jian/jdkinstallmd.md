# jdkinstall.md

```text
# 源文件
jdk-8u171-linux-x64.tar.gz
# 解压
tar xf jdk-8u171-linux-x64.tar.gz  -C /usr/local/
```

* 添加脚本

```text
[root@host jdk1.8.0_171]# more /etc/profile.d/java.sh
export JAVA_HOME=/usr/local/jdk1.8.0_171/
export JRE_HOME=/usr/local/jdk1.8.0_171/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```

`source /etc/profile` 执行脚本

* 结果

  ```text
  [root@host jdk1.8.0_171]# java  -version             
  java version "1.8.0_171"
  Java(TM) SE Runtime Environment (build 1.8.0_171-b11)
  Java HotSpot(TM) 64-Bit Server VM (build 25.171-b11, mixed mode)
  ```


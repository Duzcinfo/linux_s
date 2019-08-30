# apt安装java.md

* ubuntu 安装 java 

```text
sudo add-apt-repository ppa:webupd8team/java  # 添加 Java 的仓库
sudo apt-get update
sudo apt-get install oracle-java8-installer  # 默认安装最新的 java
sudo apt-get install oracle-java8-set-default   # 设置默认的 java 环境

## 安装成功
ubuntu@ubuntu-31-70:~$ java -version
java version "1.8.0_181"
Java(TM) SE Runtime Environment (build 1.8.0_181-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.181-b13, mixed mode)
```


公钥加密算法很少加密数据：速度太慢

名词解释：

* PKI：Public Key Infrastructure
* CA：Certificate Authority

证书格式：x509 pkcs12

x509：公钥、有效期；证书的合法拥有者；证书该如何使用；CA的信息（颁发机构，公司名字）；CA的签名（校验码）

PKI：TLS/SSL：x509

PKI：OPenGPG

TLS/SSL handshake

SSL：Secure Socket Layer安全套接字层。是一个库    SSLv2  SSLv3

TLS：Transport Layer Secure

# 对称加密

DES：Data Encrption Standard\( 数据加密标准\),56bit

**3DES**

AES :高级加密标准  AES192 AES256 AES512   **越长安全越高，速度越慢**

Blowfish

## 单向加密

MD4

MD5

SHA1

SHA192 SHA256 SHA384

CRC-32:校验码机制，不提供安全性。

工具：

OpenSSl：ssl的开源实现

```shell
libcrypto:通用加密库
libssl：TLS/SSl的实现。基于会话，实现了身份认证、数据机密性和会话完整性的库。
openssl：多用途命令行工具。实现私有证书颁发机构。
```

### openssl介绍

```shell
openssl speed #速度测试工具
openssl enc -des3 -salt -a -in pathfile -out newname   #des3加密
openssl enc -d des3 -d -salt -a in newname -out pathfilename    #des3解密
```

* 实现私有RA
* 生成一对秘钥   \(权限600\)
* 生成自签证书

```shell
genrsa 2048  > filename ##默认512
genrsa 2048 -out filename 
(umask 077)  #在子shell执行
（umask 077;openssl genrsa  -out server1024.key 1024）#生成1024密钥

openssl rsa -in server1024.key -pubout ##提取公钥
```

自签签名

```shell
openssl req -new -x509 -key server1024.key -out server.crt -days 365

openssl x509 -text -in server.crt #输出crt文件
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number: 12073255951776250763 (0xa78cd2523ffe7b8b)
    Signature Algorithm: sha256WithRSAEncryption
        Issuer: C=CN, ST=cq, L=cq, O=cq, OU=cq, CN=cq/emailAddress=550923902@qq.com
        Validity
            Not Before: Oct 23 07:19:02 2017 GMT ##证书有效期
            Not After : Oct 23 07:19:02 2018 GMT
            
            ##证书持有者
        Subject: C=CN, ST=cq, L=cq, O=cq, OU=cq, CN=cq/emailAddress=550923902@qq.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption        ##公钥加密
                Public-Key: (1024 bit)
                Modulus:
                    00:c5:24:1c:c9:ef:25:2b:20:17:28:5e:69:81:fb:
                    48:ce:c3:5b:e0:fb:f6:2c:5b:d7:89:84:36:2f:54:
                    49:ef:75:2a:dc:8a:04:9c:e2:26:5f:38:63:3b:db:
                    91:28:0b:ab:a5:e8:bc:66:f0:95:15:92:53:6a:16:
                    ec:9b:6f:d5:05:aa:11:d3:0d:e4:56:11:7a:a5:c2:
                    90:d2:6e:26:c5:54:9d:5b:13:b0:15:dc:08:b4:b0:
                    9b:26:1c:a7:d4:93:57:49:24:37:47:61:50:59:8b:
                    eb:ad:c2:14:1f:8d:ab:8d:1a:69:69:f7:84:b0:30:
                    e5:ff:46:df:49:e8:f3:84:39
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Subject Key Identifier: 
                EF:61:7A:27:FA:5C:EC:52:23:75:BE:5F:A4:A5:40:E0:4F:80:AD:70
            X509v3 Authority Key Identifier: 
            ##颁发机构
                keyid:EF:61:7A:27:FA:5C:EC:52:23:75:BE:5F:A4:A5:40:E0:4F:80:AD:70

            X509v3 Basic Constraints: 
                CA:TRUE
    Signature Algorithm: sha256WithRSAEncryption    #签名信息
         0a:a2:1d:cf:78:5e:a5:4e:88:0d:56:66:83:bc:10:7e:d8:3c:
         3f:c3:bd:06:88:60:42:cc:88:19:6f:b9:b7:53:dc:55:a9:37:
         e5:11:8d:10:21:f7:07:a8:fa:c5:01:40:74:26:40:7f:be:2f:
         41:21:4c:7e:a5:bd:75:9c:d7:bc:8a:c7:76:66:0f:99:99:77:
         cb:e4:18:94:b3:aa:9d:f8:2b:c4:04:2c:2c:e5:07:bf:e6:b1:
         de:3a:2e:5d:b3:8a:e7:8c:cd:ed:9f:30:b3:27:7e:1d:5c:33:
         12:7a:aa:dd:3c:c2:cb:c2:ec:71:cb:25:5c:36:f7:32:90:50:
         41:f3
-----BEGIN CERTIFICATE-----
MIICrDCCAhWgAwIBAgIJAKeM0lI//nuLMA0GCSqGSIb3DQEBCwUAMG8xCzAJBgNV
BAYTAkNOMQswCQYDVQQIDAJjcTELMAkGA1UEBwwCY3ExCzAJBgNVBAoMAmNxMQsw
CQYDVQQLDAJjcTELMAkGA1UEAwwCY3ExHzAdBgkqhkiG9w0BCQEWEDU1MDkyMzkw
MkBxcS5jb20wHhcNMTcxMDIzMDcxOTAyWhcNMTgxMDIzMDcxOTAyWjBvMQswCQYD
VQQGEwJDTjELMAkGA1UECAwCY3ExCzAJBgNVBAcMAmNxMQswCQYDVQQKDAJjcTEL
MAkGA1UECwwCY3ExCzAJBgNVBAMMAmNxMR8wHQYJKoZIhvcNAQkBFhA1NTA5MjM5
MDJAcXEuY29tMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDFJBzJ7yUrIBco
XmmB+0jOw1vg+/YsW9eJhDYvVEnvdSrcigSc4iZfOGM725EoC6ul6Lxm8JUVklNq
Fuybb9UFqhHTDeRWEXqlwpDSbibFVJ1bE7AV3Ai0sJsmHKfUk1dJJDdHYVBZi+ut
whQfjauNGmlp94SwMOX/Rt9J6POEOQIDAQABo1AwTjAdBgNVHQ4EFgQU72F6J/pc
7FIjdb5fpKVA4E+ArXAwHwYDVR0jBBgwFoAU72F6J/pc7FIjdb5fpKVA4E+ArXAw
DAYDVR0TBAUwAwEB/zANBgkqhkiG9w0BAQsFAAOBgQAKoh3PeF6lTogNVmaDvBB+
2Dw/w70GiGBCzIgZb7m3U9xVqTflEY0QIfcHqPrFAUB0JkB/vi9BIUx+pb11nNe8
isd2Zg+ZmXfL5BiUs6qd+CvEBCws5Qe/5rHeOi5ds4rnjM3tnzCzJ34dXDMSeqrd
PMLLwuxxyyVcNvcykFBB8w==
-----END CERTIFICATE-----

```

## 

## 非对称加密（公钥加密）

> 作用：加密和签名

身份认证（数字签名）

数据加密（秘钥交换）

RSA：加密、签名

DSA：签名

ElGamal:

### 工具

rsautl


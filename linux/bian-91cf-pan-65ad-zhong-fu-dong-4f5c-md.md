# 展开运算

```shell
${varname:-word}
#当varname是非空值时，则返回值；当变量为null时，返回word

A=hellow
#A=''
echo ${A:-word}
```




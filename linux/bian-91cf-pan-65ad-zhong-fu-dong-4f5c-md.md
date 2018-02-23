# 

# 展开运算

* 定义默认值

```shell
${varname:-word}
#当varname是非空值时，则返回值；当变量为null时，返回word
#应用：如果变量没有定义，则返回默认值。
A=hellow
#A=''
echo ${A:-word}
```




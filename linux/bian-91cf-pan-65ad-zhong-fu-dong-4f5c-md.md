# 变量-判断-重复动作.md

* 定义默认值

```text
${varname:-word}
#当varname是非空值时，则返回值；当变量为null时，返回word
#应用：如果变量没有定义，则返回默认值。
A=hellow
#A=''

echo ${A:-word}##如果变量没有定义，则返回默认值
${varname:=word}  ##如果变量没有定义，则设置变量为默认值。
${varname:?message}##当varname不为空时，则返回它的值；否者，返回message，并退出当前脚本。为了捕捉因为变量未定义所导致的错误。
${varname:+word}##当varname存在且不为空，则返回word，否者返回null。为测试变量存在。
```


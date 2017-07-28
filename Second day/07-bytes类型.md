# bytes类型

bytes类型（字节系列数据类型），是由8位字节数据组成的系列数据类型。

使用字母b加单引号或双引号括起来的内容，是bytes常量。bytes常量与字符串定义方式类似。



## 字符串的编码与解码

字符串可以通过str.encode()方法编码为字节码，

通过bytes的decode()方法解码为字符串。

```python
>>> msg = "你好，世界"
>>> msg
'你好，世界'
>>> msg.encode(encoding='utf-8')	# python 3.x 中编码默认是'utf-8'
b'\xe4\xbd\xa0\xe5\xa5\xbd\xef\xbc\x8c\xe4\xb8\x96\xe7\x95\x8c'
>>> msg2 = msg.encode(encoding='utf-8')
>>> msg2.decode(encoding='utf-8')
'你好，世界'
```




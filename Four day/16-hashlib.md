# hashlib -  安全散列和消息摘要

> ​	这个模块实现了一个通用的接口来实现多个不同的安全哈希和消息摘要算法。包括FIPS安全散列算法SHA1，SHA224，SHA256，SHA384和SHA512（在FIPS 180-2中定义）以及RSA的MD5算法（在因特网 **RFC 1321**术语“安全散列”和“消息摘要”是可互换的。较旧的算法被称为消息摘要。现代术语是安全哈希。

```python
>>> import hashlib
>>> m = hashlib.md5()
>>> m.update(b"Nobody inspects")
>>> m.update(b" the spammish repetition")
>>> m.digest()
b'\xbbd\x9c\x83\xdd\x1e\xa5\xc9\xd9\xde\xc9\xa1\x8d\xf0\xff\xe9'
>>> m.digest_size
16
>>> m.block_size
64
```

​	如果加密的对象是中文

```python
h = hashlib.md5()
h.update("中国Python".encode(encoding='utf-8'))
print(h.hexdigest())	#		4c65fc1a9946ca90c057cdb086cc7250
```







# hmac - 用于邮件身份验证的键控哈希

* `hmac.new(*key, msg=None, digestmod=None)`

  返回一个新的 hmac 对象。*键*是给出密钥的字节或bytearray对象。如果存在*msg*，则进行方法调用`update(msg)`。

```python
h = hmac.new(b'python',msg="中国".encode(encoding='utf-8'))
print(h.digest())	#	b'\xa8\xf0\xea\x130\\7m\xb5z^\xf16\xdc/I'
```

​	或

```python
h = hmac.new(b'python')
h.update('中国'.encode())
print(h.digest())	#	b'\xa8\xf0\xea\x130\\7m\xb5z^\xf16\xdc/I'

```


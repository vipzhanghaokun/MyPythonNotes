# json

> ​	如果我们要在不同的编程语言之间传递对象，就必须把对象序列化为标准格式，比如XML，但更好的方法是序列化为JSON，因为JSON表示出来就是一个字符串，可以被所有语言读取，也可以方便地存储到磁盘或者通过网络传输。JSON不仅是标准格式，并且比XML更快，而且可以直接在Web页面中读取，非常方便。
>
> ​	Python3中可以使用json模块对json数据进行编解码，它包含两个函数：
>
> * json.dumps()：对数据进行编码
> * json.loads()：对数据进行解码

## 一、Python中的json

​	在python中可序列化的数据对象：dict，list，tuple，str，int，float，True，False，None

## 二、数据对象序列化与反序列化

### 1. 字典

```python
import json

info = {'name':'zhanghk','age':28}
print('python原始数据：',info)

# 将python字典编码为json数据对象
json_data = json.dumps(info)
print('json数据：',json_data)

# 将json数据对象解码为python数据格式
python_data = json.loads(json_data)
print('python数据：',python_data)

```

​	输出结果

```powershell
python原始数据： {'age': 28, 'name': 'zhanghk'}
json数据： {"age": 28, "name": "zhanghk"}
python数据： {'age': 28, 'name': 'zhanghk'}
```

### 2.元组

​	python中的列表和元组都会被json序列化为python中list的格式

```python
info = (1,2,3,4,5)
print('python原始数据：',info)

json_data = json.dumps(info)
print('json数据：',json_data)

python_data = json.loads(json_data)
print('python数据：',python_data)
```

​	输出结果

```pow
python原始数据： (1, 2, 3, 4, 5)
json数据： [1, 2, 3, 4, 5]
python数据： [1, 2, 3, 4, 5]
```



## 三、文件对象序列化与反序列化

​	如果需要将json数据格式写入文件，获取文件中读取，需要使用

* json.dump()：写入文件
* json.load()：读取文件

### 1.字典

* 写入数据

```python
import json

info = {'name':'zhanghk','age':28}

with open('data.json','w') as f:
    json.dump(info,f)
```

​	文件内容

```powershell
{"name": "zhanghk", "age": 28}
```

* 读取数据

```python
import json

with open('data.json','r') as f:
    data = json.load(f)

print(data)
print(data['name'])
```

​	输出结果

```powershell
{'name': 'zhanghk', 'age': 28}
zhanghk
```



### 2.元组

* 写入数据

```python
import json

info = (1,2,3,4,5)

with open('data.json','w') as f:
    json.dump(info,f)
```

​	文件内容

```powershell
[1, 2, 3, 4, 5]
```

* 读取数据

```python
import json

with open('data.json','r') as f:
    data = json.load(f)

print(data)
print(data[0])
```

​	输出结果

```powershell
[1, 2, 3, 4, 5]
1
```




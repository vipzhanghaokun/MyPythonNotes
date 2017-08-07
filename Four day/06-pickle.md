# pickle

> ​	pickle模块实现了python数据对象的系列化和反系列化，是python内部使用的持久化的模块。
>
> ​	pickle.dump(obj,file)：将对象obj保存到文件file中去
>
> ​	pickle.load(file)：从file中读取并重构1个对象
>
> 

## 一、可以支持的类型

* None,True和False
* 整数，浮点数，复数
* 字符串，字节，字节数
* 元组，列表，集合和字典
* 在模块顶层定义的函数（使用def，而不是lambda）
* 內建函数定义在模块的顶层
* 在模块的顶层定义的类

几乎可以支持python内部所有的数据对象。



## 二、系列化

1. 序列化字典

```python
import pickle

info = {'name':'zhanghk','age':18}

with open('info.pk','wb') as f:
    pickle.dump(info, f)
```

2. 序列化函数

```python
import pickle

def info():
    print('in the info')

with open('info.pk','wb') as f:
    pickle.dump(info, f)
```





## 三、反序列化

1. 反序列字典

```python
import pickle

with open('info.pk','rb') as f:
    info = pickle.load(f)

print(info)		# {'age': 18, 'name': 'zhanghk'}
```

2. 反序列函数

```python
import pickle

def info():
    print('in the info2')

with open('info.pkl','rb') as f:
    data = pickle.load(f)

data()		# in the info2
```



## 四、多次序列化与反序列化

1. 序列化

   ```python
   import pickle

   name = 'zhanghk'
   age = 18
   info = {'name':name,'age':age}

   with open('info.pkl','wb') as f:
       pickle.dump(name,f)
       pickle.dump(age,f)
       pickle.dump(info,f)

   ```

   ​

2. 反序列化

   ```python
   import pickle
   with open('info.pkl','rb') as f:
       name = pickle.load(f)
       age = pickle.load(f)
       info = pickle.load(f)
       print(name)
       print(age)
       print(info)
   ```

   ​	输出结果

   ```powershell
   zhanghk
   18
   {'name': 'zhanghk', 'age': 18}
   ```

   ​
#random - 生成伪随机数字

> ​	这个模块实现了对各种分布的伪随机数发生器。
>
> ​	对于整数，有一个范围的均匀选择。对于序列，存在随机元素的均匀选择，产生就地列表的随机置换的函数，以及用于无替换的随机采样的函数。

## 一、常见功能方法

* `random.random()`

  返回下一个在范围 (0.0, 1.0) 中的随机浮点数。

  ```python
  random.random()		#	0.08532333185826213
  ```

  ​

* `random.randint(a,b)`

  返回随机整数，取值范围（a，b）

  ```python
  random.randint(1,3)		#	3
  ```

  ​

* `random.randrange(start,stop[,step])`

  返回一个start到stop范围内的随机整数（start，stop，step都是整数，不包含stop），可以指定step。

  ```python
  random.randrange(1,3)		# 	2
  ```

  ​

* `random.choice(seq)`

  从非空序列*seq*返回一个随机元素。

  ```python
  >>> x = [1,2,3,4,5]
  >>> random.choice(x)
  1
  >>> random.choice(x)
  4
  ```

* `random.sample(population,k)`

  返回从群体序列或集合中选择的唯一元素的*k*长度列表。用于随机抽样，无需更换。

  ```python
  >>> random.sample(range(100),3)
  [82, 35, 85]
  ```

  ​

* `random.uniform(a,b)`

  返回一个随机浮点数N，取值范围a<= N <=b

  ```python
  >>> random.uniform(1,5)
  3.320054517088328
  ```

  ​

* `random.shuffle(x[,random])`

  随机播放序列*x*。可选参数*random*是返回[0.0，1.0]中的随机浮点的0参数函数；默认情况下，这是函数`random()`。

  ```python
  >>> x
  [2, 1, 3, 5, 4]
  >>> random.shuffle(x)
  >>> x
  [3, 2, 5, 4, 1]
  ```



## 二、应用场景

​	随机验证码

```python
import random


def random_code():
    code = ''
    for i in range(6):
        tmp = random.randint(0,9)
        if i == tmp:
            tmp_n = random.randint(65,90)
            tmp = chr(tmp_n)
        code += str(tmp)
    return code

x = random_code()

print(x)
```






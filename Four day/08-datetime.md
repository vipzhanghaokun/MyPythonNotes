# datetime

> ​	`datetime`对象表示日期和时间，包含了date对象和time对象的信息。
>
> ​	`datetime`模块提供处理日期和时间的类，既有简单的方式又有复杂的方式。

## 一、datetime对象的方法

​	需要导入才能使用`from datetime import *`。

* `datetime.today()`

  返回当前本地日期时间，其中`tzinfo`为`None`。

  ```python
  print(datetime.today())

  2017-08-08 22:08:26.124696
  ```

  ​

* `datetime.now(tz=None)`

  获得datetime对象（当前时间，可指定时区），返回本地当前的日期和时间。如果可选参数*tz*为`None`或未指定，则这类似于`today()`，但如果可能，通过`time.time()`时间戳提供更高的精度。

  ```python
  print(datetime.now())

  2017-08-08 22:15:59.880489
  ```

* `datetime.utcnow()`

  返回当前UTC日期和时间，其中`tzinfo`为`None`。

  ```python
  print(datetime.utcnow())

  2017-08-08 14:17:57.894049
  ```

  ​

* `datetime.fromtimestamp(time.time())`

  返回与POSIX时间戳对应的本地日期和时间，例如`time.time()`返回的时间戳。

  ```python
  print(datetime.fromtimestamp(time.time()))
  2017-08-08 22:20:07.340492
  ```

* `datetime.utcfromtimestamp(time.time())`

  返回与POSIX时间戳对应的UTC `datetime`，其中`tzinfo`为`None`。

  ```
  print(datetime.utcfromtimestamp(time.time()))

  2017-08-08 14:21:50.815344
  ```

* `datetime.fromordinal()`

  获得datetime对象（指定从1/1/1的天数）

  ```python
  print(datetime.fromordinal(10))

  0001-01-10 00:00:00
  ```

  ​

* ​

* ​

## 二、timedelta对象


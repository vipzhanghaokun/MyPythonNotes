# time

​	主要用来表示时间的功能。

## 一、模块功能

​	时间的主要显示方式：

* 格式化时间字符串，如：“2017-05-08 10:20:50”等

* 时间戳，如：“1502171895.0858645”，从1970年1月1日到现在的秒数

* 时间元组，如：`time.struct_time(tm_year=2017, tm_mon=8, tm_mday=8, tm_hour=14, tm_min=0, tm_sec=34, tm_wday=1, tm_yday=220, tm_isdst=0)`等，tm_year：年，tm_mon：月，tm_mday：日，

  tm_hour：小时，tm_min：分钟，tm_sec：秒，tm_wday：一周的第几天（0-6），tm_yday：一年中的第几天，tm_isdst：是否开启夏令时（0：关闭，1：开启）



## 二、常见使用方法

​	要想使用time模块，首先要导入

​	`import time`

* `time.time()`:以秒为单位返回作为浮点数的时间。

  ```python
  print(time.time())	
  1502172773.362765
  ```

* `time.timezone`:本地（非DST）时区的偏移量，以UTC以内的秒为单位（西欧大部分地区为负，美国为正，英国为零）。

  ```python
  print(time.timezone)	
  -28800	
  ```

* `time.altzone`:默认情况返回一个以秒为单位UTC的本地DST时区偏移量，如果本地DST时区在UTC的东部（如在西欧，包括英国），则为负。

  ```python
  print(time.altzone)		
  -32400
  ```

* `time.daylight`:如果定义了DST时区，则为非零。

  ```python
  print(time.daylight)	
  0
  ```

* `time.tzname`:两个字符串的元组：第一个是本地非DST时区的名称，第二个是本地DST时区的名称。

  ```python
  print(time.tzname)		

  ('ÖÐ¹ú±ê×¼Ê±¼ä', 'ÖÐ¹úÏÄÁîÊ±')
  ```

* `time.sleep(sec)`:在给定的秒数内挂起调用线程的执行。

* `time.gmtime([secs])`:将从纪元开始以秒表示的时间转换成UTC中的时间元组。如果为提供secs或None，则使用由time()返回的当前时间

  ```python
  print(time.gmtime())	

  time.struct_time(tm_year=2017, tm_mon=8, tm_mday=8, tm_hour=7, tm_min=9, tm_sec=55, tm_wday=1, tm_yday=220, tm_isdst=0)
  ```

* `time.localtime()`:将秒转换为本地时间。如果为提供secs或None，则使用由time()返回的当前时间。

  ```python
  print(time.localtime())

  time.struct_time(tm_year=2017, tm_mon=8, tm_mday=8, tm_hour=15, tm_min=18, tm_sec=41, tm_wday=1, tm_yday=220, tm_isdst=0)
  ```

  ​

* `time.mktime(t)`:将时间元组转换成时间戳

  ```python
  print(time.mktime(time.localtime()))

  1502178227.0
  ```

* `time.strftime(format,[t])`:将时间元组按指定字符串样式格式化输出。如果没有提供时间元组，将使用`localtime()`返回的当前时间。

  ```python
  print(time.strftime('%Y-%m-%d %H:%M:%S'))

  2017-08-08 15:48:08
  ```

  格式字符串支持的参数：

  | 指示   | 含义                                       |
  | ---- | ---------------------------------------- |
  | `%a` | Locale的缩写工作日名称。                          |
  | `%A` | Locale的整个工作日名称。                          |
  | `%b` | 语言环境的缩写月份名称。                             |
  | `%B` | Locale的完整月份名称。                           |
  | `%c` | 语言环境的适当日期和时间表示。                          |
  | `%d` | 一个十进制数字[01,31]。                          |
  | `%H` | 小时（24小时制），十进制数[00,23]。                   |
  | `%I` | 小时（12小时制）十进制数[01,12]。                    |
  | `%j` | 一年中的十进制数[001,366]。                       |
  | `%m` | 月为十进制数[01,12]。                           |
  | `%M` | 以十进制数分钟[00,59]。                          |
  | `%p` | Locale相当于AM或PM。                          |
  | `%S` | 秒为十进制数[00,61]。                           |
  | `%U` | 年的星期数（星期日为星期的第一天）为十进制数[00,53]。在第一个星期日之前的新的一年的所有天被认为是在第0周。 |
  | `%w` | 工作日为十进制数[0（星期日），6]。                      |
  | `%W` | 年的星期数（星期一作为星期的第一天）作为十进制数[00,53]。在第一个星期一之前的新的一年中的所有天被认为是在第0周。 |
  | `%x` | 语言环境的适当日期表示。                             |
  | `%X` | 语言环境的适当时间表示。                             |
  | `%y` | 年，无世纪作为十进制数[00,99]。                      |
  | `%Y` | 年份以世纪为十进制数。                              |
  | `%z` | 指示与+ HHMM或-HHMM形式的UTC / GMT的正或负时差的时区偏移，其中H表示十进制小时数字，M表示十进制分数字[-23：59，+23：59]。 |
  | `%Z` | 时区名称（如果没有时区，则不包含字符）。                     |
  | `%%` | 字面值`'%'`字符。                              |

* `time.strptime(string[,format])`:根据格式解析表示时间的字符串，返回为时间元组的形式

  ```python
  print(time.strptime('2017-08-08 16:35:48','%Y-%m-%d %H:%M:%S'))

  time.struct_time(tm_year=2017, tm_mon=8, tm_mday=8, tm_hour=16, tm_min=35, tm_sec=48, tm_wday=1, tm_yday=220, tm_isdst=-1)
  ```


* `time.asctime([t])`:将表示由`gmtime()`或`localtime()`返回的时间的元组或`struct_time`转换为以下形式的字符串：`'Tue Aug  8 17:19:31 2017'` 。如果未提供*t*，则使用`localtime()`返回的当前时间。

  ```python
  print(time.asctime())

  Tue Aug  8 17:19:31 2017
  ```

* `time.ctime([secs])`:将从纪元开始以秒表示的时间转换为表示本地时间的字符串。如果未提供*secs*或`None`，则使用由`time()`返回的当前时间。

  ```python
  print(time.ctime())

  Tue Aug  8 17:49:47 2017
  ```

  ​

* ​
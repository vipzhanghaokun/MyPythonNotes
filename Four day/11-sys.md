# sys - 系统特定的参数和函数

* `sys.argv`

  传递给Python脚本的命令行参数列表。`argv[0]`是脚本的名称（是否是完整的路径名这要取决于操作系统）。

* `sys.exit([arg])`

  从 Python 退出。

* `sys.getwindowsversion()`

  返回一个已命名的元组，描述当前正在运行的 Windows 版本。

  ```python
  >>> sys.getwindowsversion()
  sys.getwindowsversion(major=10, minor=0, build=15063, platform=2, service_pack='')
  ```

  ​


* `sys.maxsize`

  返回一个python的整数最大的值。

  ```python
  >>> sys.maxsize
  9223372036854775807
  ```

  ​

* `sys.path`

  返回python模块搜索路径的字符串的列表。

  ```python
  >>> sys.path
  ['C:\\Program Files (x86)\\JetBrains\\PyCharm 2016.2.3\\helpers\\pydev', 'C:\\Program Files (x86)\\JetBrains\\PyCharm 2016.2.3\\helpers\\pydev', 'C:\\Program Files\\Python35\\python35.zip', 'C:\\Program Files\\Python35\\DLLs', 'C:\\Program Files\\Python35\\lib', 'C:\\Program Files\\Python35', 'C:\\Program Files\\Python35\\lib\\site-packages', 'G:\\PythonHomeWork\\Test']

  ```

  ​

* `sys.platform`

  返回操作系统平台类型

  ```python
  >>> sys.platform
  'win32'
  ```

  ​

* `sys.stout.write()`

  标准输出。

* `sys.stdin.readline()`

  标准输入

* `sys.version`

  一个字符串，包含Python解释器的版本号以及版本号和使用的编译器的额外信息。

  ```python
  >>> sys.version
  '3.5.3 (v3.5.3:1880cb95a742, Jan 16 2017, 16:02:32) [MSC v.1900 64 bit (AMD64)]'
  ```

  ​

* ​

  ​
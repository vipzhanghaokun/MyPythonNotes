# subprocess - 子进程管理

> ​	`subprocess`模块允许你生成新进程，连接到其输入/输出/错误管道，并获取其返回码。
>
> 此模块旨在替换多个旧的模块和函数：
>
> ​	os.system
>
> ​	os.spawn*
>
> ​	调用subprocess的推荐方法是对于它可以处理的所有使用场景都使用`run()`函数。对于更高级的使用场景，可以直接使用底层的`Popen`接口。

* `subprocess.run(args, *, stdin=None, input=None, stdout=None, stderr=None, shell=False, timeout=None, check=False)`

  运行*args*描述的命令。等待命令完成，然后返回一个`CompletedProcess`实例。

  ​

* `subprocess.``getstatusoutput`(*cmd*)

  返回在shell中执行*cmd*的`(status, output)`。

  ```python
  import subprocess

  res = subprocess.getstatusoutput(["dir"])
  print(res[0])
  print(res[1])
  ```

  ​	输出

  ```python
  0
   驱动器 F 中的卷没有标签。
   卷的序列号是 0000-E526

   F:\PythonCode\test 的目录

  2017/08/23 周三  17:09    <DIR>          .
  2017/08/23 周三  17:09    <DIR>          ..
  2017/08/23 周三  17:04    <DIR>          .idea
  2017/07/26 周三  17:36           112,145 11
  2017/08/16 周三  17:24           112,357 22
  2017/08/04 周五  09:33                15 data.json
  2017/08/22 周二  16:35               927 example.log
  2017/08/17 周四  16:05             1,509 shutil_test.py
  2017/08/23 周三  17:09             1,059 sunprocess_test.py
  2017/08/04 周五  08:24             3,141 test.py
  2017/08/18 周五  15:47               687 test.xml
  2017/08/08 周二  17:49             1,476 time_test.py
  2017/08/18 周五  17:08             1,473 xml_test.py
  2017/08/23 周三  15:52             1,106 正则模式.py
                9 个文件        244,519 字节
                 3 个目录 211,788,840,960 可用字节
  ```

  ​

* ​

  ​
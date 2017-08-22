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

* ​

  ​
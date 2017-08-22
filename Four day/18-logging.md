# logging - Python的日志记录

> ​	该模块定义的函数和类为应用程序和库实现了一个灵活的事件日志系统。
>
> ​	该模块定义的基本类以及它们的函数。
>
> - Loggers 提供应用程序代码直接使用的接口。
> - Handlers 发送日志记录（由loggers创建）到正确的目标。
> - Filters 提供粒度更好的工具用于决定输出哪些日志记录。
> - Formatters 指出最终输出中的日志记录的格式。

​	日志是跟踪软件运行时所发生的事件的一种方法。软件开发者在代码中调用日志函数，表明发生了特定的事件。事件由描述性消息描述，该描述性消息可以可选地包含可变数据（即，对于事件的每次出现都潜在地不同的数据）。事件还具有开发者归因于事件的重要性；重要性也可以称为级别或严重性。

​	logging提供了一组便利的函数，用来做简单的日志。它们是 `debug()`、 `info()`、 `warning()`、 `error()`和 `critical()`。要决定什么时候使用logging，见下表，它描述了常见的任务及对应的最佳工具。



| 你想完成的任务                                | 完成任务的最佳工具                                |
| -------------------------------------- | ---------------------------------------- |
| 在控制台上显示命令行脚本或者程序的常规用法说明                | `print()`                                |
| 报告在程序的正常操作期间发生的事件（例如，用于状态监视或故障调查）      | `logging.info()`（或者 `logging.debug()`，非常详细的输出，用于诊断目的） |
| 对于特定的运行时事件发出警告                         | 在库代码中使用`warnings.warn()` ，表明问题是可以避免的，且客户应用应该修改代码以消除警告使用`logging.warning()` 表示客户应用对此问题无能为力，但是还是应该注意该事件。 |
| 对于特定的运行时事件报告错误                         | 抛出异常                                     |
| 报告错误的抑制而不引发异常（例如，在长时间运行的服务器进程中的错误处理程序） | 根据特定的错误和应用领域，使用合适的`logging.error()`、 `logging.exception()`或者 `logging.critical()` |

​	logging函数根据它们用来跟踪的事件的级别或严重程度来命名。标准级别及其适用性描述如下（以严重程度递增排序）：

| 级别         | 何时使用                                     |
| ---------- | ---------------------------------------- |
| `DEBUG`    | 详细信息，一般只在调试问题时使用。                        |
| `INFO`     | 证明事情按预期工作。                               |
| `WARNING`  | 某些没有预料到的事件的提示，或者在将来可能会出现的问题提示。例如：磁盘空间不足。但是软件还是会照常运行。 |
| `ERROR`    | 由于更严重的问题，软件已不能执行一些功能了。                   |
| `CRITICAL` | 严重错误，表明软件已不能继续运行了。                       |

​	默认等级是`WARNING`，这意味着仅仅这个等级及以上的才会反馈信息，除非logging模块被用来做其它事情。

​	被跟踪的事件能以不同的方式被处理。最简单的处理方法就是把它们在控制台上打印出来。另一种常见的方法就是写入磁盘文件。



# 基础日志



## 一、基本日志功能



```python
import logging

logging.basicConfig(filename='example.log',level=logging.DEBUG)
logging.debug("the msg from debug!")
logging.info("the msg from info!")
logging.warning("the msg from warning!")
```

​	日志内容

```python
DEBUG:root:the msg from debug!
INFO:root:the msg from info!
WARNING:root:the msg from warning!
```





## 二、更改显示消息的格式

​	自定义显示内容

```python
logging.basicConfig(filename='example.log',level=logging.DEBUG,format='%(levelname)s : %(message)s',filemode='w')
logging.debug("the msg from debug!")
logging.info("the msg from info!")
logging.warning("the msg from warning!")
```

​	日志内容

```python
DEBUG : the msg from debug!
INFO : the msg from info!
WARNING : the msg from warning!
```



## 三、在日志中显示日期/时间

​	显示时间

```python
logging.basicConfig(filename='example.log',level=logging.DEBUG,format='%(asctime)s : %(message)s',filemode='w')
logging.debug("the msg from debug!")
logging.info("the msg from info!")
logging.warning("the msg from warning!")
```

​	日志内容

```python
2017-08-22 10:26:14,085 : the msg from debug!
2017-08-22 10:26:14,086 : the msg from info!
2017-08-22 10:26:14,086 : the msg from warning!
```

​	指定日期格式

```python
logging.basicConfig(filename='example.log',datefmt='%m/%d/%Y %I:%M:%S %p',level=logging.DEBUG,format='%(asctime)s : %(message)s',filemode='w')
logging.debug("the msg from debug!")
logging.info("the msg from info!")
logging.warning("the msg from warning!")
```

​	日志内容

```python
08/22/2017 10:50:56 AM : the msg from debug!
08/22/2017 10:50:56 AM : the msg from info!
08/22/2017 10:50:56 AM : the msg from warning!

```





# 高级日志

logging库采取了模块化的设计，提供了许多组件：记录器、处理器、过滤器和格式化器。

- Logger 暴露了应用程序代码能直接使用的接口。
- Handler将（记录器产生的）日志记录发送至合适的目的地。
- Filter提供了更好的粒度控制，它可以决定输出哪些日志记录。
- Formatter 指明了最终输出中日志记录的布局。



日志格式化支持的字符串

| 属性名             | 格式                    | 描述                                       |
| --------------- | --------------------- | ---------------------------------------- |
| args            | 不需要格式化args。           | 参数的元组合并到`msg`中以产生`message`，或者其值用于合并的字典（当只有一个参数时，它是字典）。 |
| asctime         | `%(asctime)s`         | 创建`LogRecord`时的可读时间。默认情况下，它的格式为'2003-07-08 16：49：45,896'（逗号后面的数字是毫秒部分的时间）。 |
| 创建              | `%(created)f`         | `LogRecord`创建的时间（形如`time.time()`的返回值，即epoch跳秒）。 |
| exc_info        | 不需要格式化args。           | 异常元组（形如`sys.exc_info`，如果没有异常为*None*。     |
| 文件名             | `%(filename)s`        | `pathname`的文件名部分。                        |
| funcName        | `%(funcName)s`        | 日志调用所在的函数名。                              |
| levelname       | `%(levelname)s`       | 消息的级别名称（`'DEBUG'`, `'INFO'`, `'WARNING'`, `'ERROR'`, `'CRITICAL'`）。 |
| levelno         | `%(levelno)s`         | 消息的级别数字（`DEBUG`, `INFO`, `WARNING`, `ERROR`, `CRITICAL`）。 |
| 行号              | `%(lineno)d`          | 日志调用所在的源码行号（如果可用）。                       |
| 模块              | `%(module)s`          | 模块（`filename`的名字部分）。                     |
| 毫秒              | `%(msecs)d`           | `LogRecord`创建时间中的毫秒部分。                   |
| 信息              | `%(message)s`         | The logged message, computed as `msg % args`. 当调用`Formatter.format()`时设置。 |
| msg             | 不需要格式化args。           | 在原始日志调用中传递的格式字符串。与`args`合并以产生`message`或任意对象（请参阅Using arbitrary objects as messages）。 |
| 名称              | `%(name)s`            | 记录日志的logger的名字。                          |
| 路径名             | `%(pathname)s`        | 日志调用所在文件的完整路径名（如果可用）。                    |
| 处理              | `%(process)d`         | 进程 ID （如果可用）。                            |
| processName     | `%(processName)s`     | 进程名（如果可用）。                               |
| relativeCreated | `%(relativeCreated)d` | LogRecord创建时离装载日志模块时的毫秒数。                |
| stack_info      | 不需要格式化args。           | 堆栈帧信息（如果可用）从当前线程中堆栈的底部，直到并包括记录调用的堆栈帧，导致创建此记录。 |
| 线               | `%(thread)d`          | 线程 ID （如果可用）。                            |
| threadName      | `%(threadName)s`      | 线程名字（如果可用）。                              |




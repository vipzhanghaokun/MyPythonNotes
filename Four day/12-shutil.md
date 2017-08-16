# shutil - 高级文件操作

> `shutil`模块提供了对文件和容器文件的一些高级操作。特别地，提供了支持文件复制和移除的功能。



## 一、目录和文件操作

* `shutil.copyfileobj(fsrc,fdst[,length])`

  将类似文件的对象*fsrc*的内容复制到类似文件的对象*fdst*。整数*length*（如果给出）是缓冲区大小。

  ```python
  import shutil

  with open(r'D:\1\2\3\03.txt','r') as f,open(r'D:\2\04.txt','w') as f2:
      shutil.copyfileobj(f,f2)
  ```

  ​

* `shutil.copyfile(src,dst, *, follow_symlinks=True)`

  将名为*src*的文件的内容（无元数据）复制到名为*dst*的文件，然后返回*dst*。*src*和*dst*是以字符串形式给出的路径名称。*dst*必须是完整的目标文件名。如果*follow_symlinks*为假且*src*是符号链接，则将创建一个新的符号链接，而不是复制*src*指向的文件。

  ```python
  import shutil

  shutil.copyfile(r'D:\1\2\3\03.txt',r'D:\2\05.txt')
  ```

  ​

* `shutil.copystat(src, dst, *, follow_symlinks=True)`

  将权限位，最后访问时间，上次修改时间和标志从*src*复制到*dst*。文件内容，所有者和组不受影响。*src*和*dst*是以字符串形式给出的路径名称。

  ```python
  shutil.copystat(r'D:\1\2\3\03.txt',r'D:\2\04.txt')
  ```

  ​

* `shutil.copyemode(src, dst, *, follow_symlinks=True)`

  将权限位从*src*复制到*dst*。文件内容，所有者和组不受影响。*src*和*dst*是以字符串形式给出的路径名称。

  ```python
  shutil.copymode(r'D:\1\2\3\03.txt',r'D:\2\04.txt')
  ```

  ​

* `shutil.copy(src,dst)`

  将文件*src*复制到文件或目录*dst*。*src*和*dst*应为字符串。如果*dst*指定目录，则文件将使用*src*的基本文件名复制到*dst*中。返回新创建的文件的路径。

  如果*follow_symlinks*为false，并且*src*是符号链接，则*dst*将创建为符号链接。如果*follow_symlinks*为true且*src*是符号链接，则*dst*将是文件的副本*src* 。

  ```python
  shutil.copy(r'D:\1\2\3\03.txt',r'D:\2\06.txt')
  ```

  ​

* `shutil.copy2(src,dst)`

  与copy()相同

  ```python
  shutil.copy2(r'D:\1\2\3\03.txt',r'D:\2\07.txt')
  ```

  ​

* ​

* ​

* ​













## 二、归档操作








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

* `shutil.copytree(src, dst, symlinks=False, ignore=None, copy_function=copy2, ignore_dangling_symlinks=False)`

  递归地复制以*src*为根的整个目录树，返回目标目录。

  ```python
  import shutil
  	
  x = shutil.copytree(r'd:/1/2/3',r'e:/1/2/3')
  print(x)		#	e:/1/2/3
  ```

  ​

* `shutil.rmtree(path, ignore_errors=False, onerror=None)`

  删除整个目录树； *路径*必须指向目录（而不是指向目录的符号链接）。如果*ignore_errors*为true，则删除失败导致的错误将被忽略；如果为false或省略，则通过调用*onerror*指定的处理程序处理这些错误，如果省略，则引发异常。

  ```python
  import shutil

  # 递归删除目录3以下的目录及内容
  shutil.rmtree(r'e:/1/2/3')	
  ```

  ​

* `shutil.move(src, dst, copy_function=copy2)`

  递归地将文件或目录（*src*）移动到另一个位置（*dst*），并返回目标。

  ```python
  import shutil

  # 将目录3及以下的目录和内容移动到目录1下面
  x = shutil.move(r'd:/1/2/3',r'e:/1')

  print(x)		#	e:/1\3
  ```

  ​

* `shutil.disk_usage(path)`

  将给定路径的磁盘使用情况统计信息作为named tuple返回*总计*，使用和免费是总的，已用和可用空间的量，以字节为单位。

  ```python
  >>> import shutil
  >>> shutil.disk_usage(r'd:')
  usage(total=107372195840, used=72166285312, free=35205910528)
  ```

  ​

* `shutil.chown(path, user=None, group=None)`

  更改给定*路径*的所有者*用户*和/或*组*。

  *用户*可以是系统用户名或uid；这同样适用于*组*。至少需要一个参数。只适用于Unix

* `shutil.which(cmd, mode=os.F_OK | os.X_OK, path=None)`

  返回可执行文件的路径，如果给定的*cmd*被调用，它将运行。如果不调用*cmd*，则返回`None`。

  ```python
  >>> shutil.which('python')
  'C:\\Program Files\\Python35\\python.EXE'
  ```

  ​

* ​





## 二、归档操作

* `shutil.make_archive(base_name, format[, root_dir[, base_dir[, verbose[, dry_run[, owner[, group[, logger]]]]]]])`

  创建归档文件（例如zip或tar）并返回其名称。

  *base_name*是要创建的文件的名称，包括路径，减去任何特定于格式的扩展名。

  *format*是归档格式，可以是“zip”，“tar”，“bztar”，“xztar”，“gztar”其中一个

  *root_dir*是将成为归档的根目录的目录；例如，在创建归档之前，我们通常将chdir插入到*root_dir*中。

  *base_dir*是我们开始归档的目录；即：*base_dir*将是归档中所有文件和目录的公共前缀。

  *root_dir*和*base_dir*都默认为当前目录。

  ```python
  import os
  import shutil

  os.chdir(r'd:/1/2')
  x = shutil.make_archive(base_name=r'f:/test',format='bztar')
  print(x)	#   f:/test.tar.bz2
  ```

  ​

* `shutil.get_archive_formats()`

  返回支持的归档格式列表。返回序列的每个元素都是元组`（名称， 描述）`。

  ```python
  >>> shutil.get_archive_formats()
  [('bztar', "bzip2'ed tar-file"), ('gztar', "gzip'ed tar-file"), ('tar', 'uncompressed tar file'), ('xztar', "xz'ed tar-file"), ('zip', 'ZIP file')]
  ```

  ​


* `shutil.unpack_archive(filename[, extract_dir[, format]])`

  分拆归档。

  *filename*是归档的完整路径。

  *extract_dir*是解压缩归档的目标目录的名称。

  *format*是存档格式，可省略

  ```python
  import shutil

  shutil.unpack_archive(r'f:/test.tar.bz2',extract_dir=r'd:/1')
  ```

  ​

  ```python
  >>> from shutil import make_archive
  >>> import os
  >>> archive_name = os.path.expanduser(os.path.join('~', 'myarchive'))
  >>> root_dir = os.path.expanduser(os.path.join('~', '.ssh'))
  >>> make_archive(archive_name, 'gztar', root_dir)
  '/Users/tarek/myarchive.tar.gz'
  ```

  ​

* `shutil.get_unpack_formats()`

  返回分拆的所有注册格式的列表。返回序列的每个元素都是元组`（名称， 扩展名， 描述）`。

  ```python
  >>> import shutil
  >>> shutil.get_unpack_formats()
  [('bztar', ['.tar.bz2', '.tbz2'], "bzip2'ed tar-file"), ('gztar', ['.tar.gz', '.tgz'], "gzip'ed tar-file"), ('tar', ['.tar'], 'uncompressed tar file'), ('xztar', ['.tar.xz', '.txz'], "xz'ed tar-file"), ('zip', ['.zip'], 'ZIP file')]

  ```

  ​

* ​
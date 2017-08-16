# shelve - Python对象持久性

> ​	“shelf”是一个持久的，类似字典的对象。

* `shelve.open(filename, flag='c', protocol=None, writeback=False)`

  打开持久性字典。指定的文件名是基础数据库的基本文件名。

  ```python
  with shelve.open('spam') as db:
      db['eggs'] = 'eggs'
  ```



* `序列化`

  ```python
  import shelve
  with shelve.open('shelve.log') as  db:
    	db['name'] = 'zhanghk'
  ```

* `反序列化`

  ```python
  import shelve

  with shelve.open('shelve.log') as  db:
      x = db.get('name')

  print(x)		#	zhanghk
  ```

  ​

  ​

  ​
# xml

> ​	xml是实现不同语言或程序之间进行数据交换的协议，根json差不多，但json使用起来更简单，不过，计算机早期，json还没开发出来的时候，大家只能选择xml，像现在一些传统公司，如金融公司，制造业等，主要还是xml来交换数据xml的格式，就是通过<>节点来区别数据结构的

## 一、xml.etree.ElementTree -  ElementTree XML API 

​	`xml.etree.ElementTree`（简称ET）模块实现了用于解析和创建XML数据的简单有效的API。

​	XML是一种固有的分层数据格式，最自然的方式来表示它是一棵树。`ET`有两个类用于此目的 -  `ElementTree`将整个XML文档表示为树，`Element`表示此树中的单个节点。与整个文档（从文件读取和写入文件）的交互通常在`ElementTree`级别上进行。与单个XML元素及其子元素的交互在`Element`级别上完成。

​	xml示例数据：

```xml
<?xml version="1.0"?>
<data>
    <country name="Liechtenstein">
        <rank>1</rank>
        <year>2008</year>
        <gdppc>141100</gdppc>
        <neighbor name="Austria" direction="E"/>
        <neighbor name="Switzerland" direction="W"/>
    </country>
    <country name="Singapore">
        <rank>4</rank>
        <year>2011</year>
        <gdppc>59900</gdppc>
        <neighbor name="Malaysia" direction="N"/>
    </country>
    <country name="Panama">
        <rank>68</rank>
        <year>2011</year>
        <gdppc>13600</gdppc>
        <neighbor name="Costa Rica" direction="W"/>
        <neighbor name="Colombia" direction="E"/>
    </country>
</data>
```

​	从文件读取导入数据

```python
import xml.etree.ElementTree as ET

tree = ET.parse('test.xml')
root = tree.getroot()
```

​	`Element`，`root`具有标记和属性字典

```python
print(root.tag)			#	 data
print(root.attrib)			#    {}
```

​	他们的子节点，可以通过迭代获取：

```python
for child in root:
    print(child.tag,child.attrib)
      
# 输出结果
country {'name': 'Liechtenstein'}
country {'name': 'Singapore'}
country {'name': 'Panama'}
```

​	子节点是可以嵌套的，再增加一层迭代，就可以访问嵌套子节点文档的内容

```python
for child in root:
    print("*" * 60)
    print(child.tag,child.attrib)
    for i in child:
        print(i.tag,i.attrib,i.text)
        
```

​	输出结果

```powershell
************************************************************
country {'name': 'Liechtenstein'}
rank {} 1
year {} 2008
gdppc {} 141100
neighbor {'name': 'Austria', 'direction': 'E'} None
neighbor {'name': 'Switzerland', 'direction': 'W'} None
************************************************************
country {'name': 'Singapore'}
rank {} 4
year {} 2011
gdppc {} 59900
neighbor {'name': 'Malaysia', 'direction': 'N'} None
************************************************************
country {'name': 'Panama'}
rank {} 68
year {} 2011
gdppc {} 13600
neighbor {'name': 'Costa Rica', 'direction': 'W'} None
neighbor {'name': 'Colombia', 'direction': 'E'} None
```

​	或者索引的方式访问

```python
print(root[0][1].text)		# 2008
```



* `Element.iter()`

  对其下的所有子树（子元素，子元素等）进行递归迭代。

  ```python
  for neighbor in root.iter('neighbor'):
      print(neighbor.attrib)
  {'name': 'Austria', 'direction': 'E'}
  {'name': 'Switzerland', 'direction': 'W'}
  {'name': 'Malaysia', 'direction': 'N'}
  {'name': 'Costa Rica', 'direction': 'W'}
  {'name': 'Colombia', 'direction': 'E'}
  ```

  ​

* `Element.findall()`：仅查找具有当前元素的直接子元素的标签的元素。

* `Element.find()`：找到具有特定标签的第一个子元素

* `Element.text`：访问元素的文本内容。

* `Element.get()`：访问元素的属性

  ```python
  for country in root.findall('country'):
      rank = country.find('rank').text
      name = country.get('name')
      print(name,rank)
  ```

  ​	输出结果

  ```python
  Liechtenstein 1
  Singapore 4
  Panama 68
  ```

  ​

  ​

* ​

  ​
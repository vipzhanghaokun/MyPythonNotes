# for 循环

​	for语句用于遍历数据的集合的元素，并对集合中的每个元素执行一次相关的语句。当集合中的所有元素完成迭代后，控制传递给for之后的下一个语句。for循环语句格式：

​	***for 元素 in 数据集合:***

​		**循环体语句/语句块**

```python
for i in (1,2,3):
	print(i)
	
# 输出结果
1
2
3

```

​	在for循环中也可以使用else语句，和while循环中的使用方法一样。

​	如果for、while语句没有被break语句终止，则会执行else字句，否则不执行。

​	***for 元素 in 数据集合:***

​		***循环体语句块1***

​	***else:***

​		***语句块2***



## **range对象**

​	python 3 内置对象range是一个具有迭代循环的对象，迭代时产生指定范围的数字序列。格式：

​		***range(start,stop[,step])***

​	range返回的数值序列从start开始，到stop结束（不包含stop），如果指定了可选的步长step，则序列按照步长进行增长。

```python
for i in range(1,10):
	print(i)
	
# 输出结果
1
2
3
4
5
6
7
8
9

```

​	或者指定步长

```python
for i in range(1,10,2):
	print(i)

# 输出结果
1
3
5
7
9
```

## 

​	现在我们对while循环中的猜数字游戏使用for循环再写一遍：

```python
number = 40

for i in range(3):
    guess_number = int(input("your guess number ?"))
    if guess_number > number:
        print("your guess bigger!")
    elif guess_number < number:
        print("your guess smaller")
    else:
        print("your get it!")
        break
else:
    print("your try too many.")
```

​	通过for循环也可以实现猜数字游戏，现在我们调整一些需求，在尝试了3次之后循环是否继续：

```python
number = 40

count = 0
while count < 3:
    guess_number = int(input("your guess number ?"))

    if guess_number > number:
        print("your guess bigger!")
    elif guess_number < number:
        print("your guess smaller")
    else:
        print("your get it!")
        break
    count += 1

	'''
	当计数器达到3次的时候，询问是否继续，如果输入的不是“n”，那么将计数器归零，继续循环，否则退出循环。
	'''
    if  count == 3:
        cont_guess = input("do you wangt to try ?")
        if cont_guess != 'n':
            count = 0
```



## continue语句

​	continue语句类型于beak语句，也必须在for、while循环中使用。但循环体执行到continue跳出本次循环，也不执行continue下面尚未执行的语句，返回到循环的起始处，并根据循环条件判断是否执行下一次循环。

​	continue语句与break语句的区别在于：continue语句仅结束本次循环，并返回到循环的起始处，循环条件满足的话话就开始执行下一次循环；而break语句则是结束循环，跳转到循环的外层，执行循环后面的语句。

​	与break语句相类似，当多个for、while语句彼此嵌套时，continue语句只应用于最里层的语句。

```python
for i in range(10):
    if i < 5:
        print(i)
    else:
        print(i)
        continue
    print("no continue")

# 输出结果
0
no continue
1
no continue
2
no continue
3
no continue
4
no continue
5
6
7
8
9
```



## 循环的嵌套

下三角形

```
count = 2

for i in range(1,10):
    s = ""
    for j in range(1,count):
        s += str.format("{0:1} * {1:1} = {2:<3}", i,j, i* j)
    count += 1
    print(s)
```

输出效果

```python
1 * 1 = 1  
2 * 1 = 2  2 * 2 = 4  
3 * 1 = 3  3 * 2 = 6  3 * 3 = 9  
4 * 1 = 4  4 * 2 = 8  4 * 3 = 12 4 * 4 = 16 
5 * 1 = 5  5 * 2 = 10 5 * 3 = 15 5 * 4 = 20 5 * 5 = 25 
6 * 1 = 6  6 * 2 = 12 6 * 3 = 18 6 * 4 = 24 6 * 5 = 30 6 * 6 = 36 
7 * 1 = 7  7 * 2 = 14 7 * 3 = 21 7 * 4 = 28 7 * 5 = 35 7 * 6 = 42 7 * 7 = 49 
8 * 1 = 8  8 * 2 = 16 8 * 3 = 24 8 * 4 = 32 8 * 5 = 40 8 * 6 = 48 8 * 7 = 56 8 * 8 = 64 
9 * 1 = 9  9 * 2 = 18 9 * 3 = 27 9 * 4 = 36 9 * 5 = 45 9 * 6 = 54 9 * 7 = 63 9 * 8 = 72 9 * 9 = 81 
```


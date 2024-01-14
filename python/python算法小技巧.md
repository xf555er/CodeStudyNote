# 列表转换成字符串

## 1.使用`join()`

若列表元素均为字符串, 则使用`join()`函数, 其语法如下所示:

```python
String.join(iterable)
```

> String指的是分隔符, iterbale为序列



列表转换字符串实例如下:

```py
list = ["hello","world"]
print("".join(list)) #输出helloworld
```

```python
list = ["hello","world"]
print(" ".join(list)) #输出hello world
```



## 2.使用`map()`

若列表中的元素不全是字符串, 则需要通过`map()`函数将所有元素转换成字符串的形式, 再进行`join()`函数操作

`map`函数对iterables序列的每一个元素调用function函数, 会返回一个迭代器，如果要转换为列表，可以使用 list() 来转换

```
map(function,iterables,.....)
```



列表转换字符串实例如下:

```python
list1 = ("hello","world",110)
print("".join(list(map(str,list1)))) #输出helloworld110
```



## 3.使用循环进行字符串拼接

```python
list = {"hello","world",110}
string = ""
for i in list:
    string +=str(i)

print(string)  #helloworld110
```



# 判断浮点类型是否为整数

## 1.使用is_integer()

```python
a = 2.1
print(a.is_integer()) #输出False,表示该变量为浮点数
```



## 2.求余判断

```python
a = 2.1
print(a%1) #输出0.10000000000000009, 则表示a变量为浮点数

print("该变量为:"+("整数" if(a%1==0) else "浮点数")) #输出'该变量为:浮点数'
```



# 各种输入数据赋值

## 1.直接输入数据至列表

使用`eval()`函数输出数据至列表, 列表的函数会自动识别数据类型

```python
list1 = list(eval(input()))
print(type(list1),list1) 

#输入1,2,3,'hello'
#输出[1, 2, 3, 'hello']
```



若向输入至列表的数据全部为字符串类型,则可使用`str.split()`函数

```python
list1 = input().split(',')
print(list1) 

#输入1,2,3,4  
#输出['1', '2', '3', '4']
```



## 2.若向将输入的数据赋值给多个变量

使用`eval()`函数

```py
a,b = eval(input()) #输出1,'test'
print(a) #输出1
print(b) #输出test
```





# for循环同时遍历多个列表

## `Zip()`函数

**`zip()`** 函数用于将可迭代的对象作为参数，将参数中的元素打包成一个个元组，然后返回由这些元组组成的列表。

如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。



zip语法如下所示,返回值为元组列表

```
zip(iterable,.....)
```

```py
a=[1,2,3]
b=[4,5,6]
c=[7,8,9,10,11]
zipped = zip(a,b)
print(zipped) #返回对象,输出:<zip object at 0x000002108FF86040>

print(list(zipped)) #输出:[(1, 4), (2, 5), (3, 6)]

print(list(zip(a,b,c))) #输出:[(1, 4, 7), (2, 5, 8), (3, 6, 9)]
```



## 实例演示

```python
list1 = [1,2,3,4,5]
list2 = ['张三','李四','大刘','王上','龙飞']
list3 = [17,18,19,20,21]
for i,j,k in zip(list1,list2,list3):
    print(str(i)+":"+j,"年纪:"+str(k))

'''
输出如下:
1:张三 年纪:17
2:李四 年纪:18
3:大刘 年纪:19
4:王上 年纪:20
5:龙飞 年纪:21
'''
```



# 变量值的交换

```python
a=1
b=2
a,b = b,a  #a与b进行值交换
print(a) #输出2
print(b) #输出1
```





# 删除列表重复元素

使用`set()`函数强制转换的集合

```py
lists = [1,1,2,3,4,6,6,2,2,9]
lists = list(set(lists)) #set()函数创建一个无序不重复元素集
print(lists) #输出[1, 2, 3, 4, 6, 9]
```





# 获取字典最大的value以及对应的键值

假设定义一字典为`dict1 = {"a":3,b:"4","c":5}`, 现要求字典中最大的value以及其对应的键值



## 1.通过`dict.values()`和`max()`

先通过`max()`函数寻找到字典中value的最大值,在循环遍历字典找出其对应的键值

```py
dict1 = {"a":3,"e":6,"b":2,"g":7,"f":7,"c":1,"d":5}
for key,value in dict1.item():
    if (value == max(dict1.values())):
        print(key,value)
```



## 2.通过`sort()`函数排序所有的value

先通过sort()函数找出字典中value的最大值, 然后按照第一种方法继续进行后面的步骤

```python
dict1 = {"a":3,"e":6,"b":2,"g":7,"f":7,"c":1,"d":5}
values = list(dict1.values())
values.sort()
for key,value in dict1.items():
    if value == values[len(values)-1]:
        print(key,value)
```










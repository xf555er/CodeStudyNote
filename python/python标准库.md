# OS模块

OS模块提供了丰富的函数用于处理文件及目录

| 函数                                  | 描述                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| `os.access(path,mode)`                | 检验path路径是否有某种访问权限                               |
| `os.chdir(path)`                      | 改变当前目录                                                 |
| `os.chmod(path,mode)`                 | 更改文件或目录权限                                           |
| `os.chown(path,uid,gid)`              | 更改文件所有者                                               |
| `os.chroot(path)`                     | 更改当前进程的根目录                                         |
| `os.getcwd()`                         | 返回当前工作目录                                             |
| `os.listdir(path)`                    | 返回path指定的文件夹包含的文件或文件夹的名字的列表           |
| `os.link(src,dst)`                    | 创建硬链接，名为参数 dst，指向参数 src                       |
| `os.makedirs(path,[mode],[exist_ok])` | 用于递归创建多层目录,mode默认为0511                          |
| `os.mkdir(path,[mode])`               | 创建名为path的目录, mode默认为0777                           |
| `os.pathconf(fd,name)`                | 返回相关文件的系统配置信息。Unix 平台下可用                  |
| `os.remove(path)`                     | 删除路径为path的文件。如果path 是一个文件夹，将抛出OSError; 查看下面的rmdir()删除一个 directory。 |
| `os.removedirs(path)`                 | 递归删除目录                                                 |
| `os.rename(src,dst)`                  | 重命名文件或目录                                             |
| `os.rmdir(path)`                      | 删除path指定的空目录，如果目录非空，则抛出一个OSError异常    |
| `os.symlink(src,dst)`                 | 创建一个软链接                                               |
| `os.utime(path,times)`                | 设置指定路径文件最后的修改和访问时间                         |







## `os.access(path,mode)`

- **path:** 用来检测是否有访问权限的路径

- **mode:** 权限的模式
  - **os.F_OK**: 测试path是否存在
  - **os.R_OK**: 测试path是否可读
  - **os.W_OK**: 测试path是否可写
  - **os.X_OK**: 测试path是否可执行



**实例演示如下:**

```python
import os

# 假定 /tmp/foo.txt 文件存在，并有读写权限

ret = os.access("/tmp/foo.txt", os.F_OK)
print ("F_OK - 返回值 %s"% ret)

ret = os.access("/tmp/foo.txt", os.R_OK)
print ("R_OK - 返回值 %s"% ret)

ret = os.access("/tmp/foo.txt", os.W_OK)
print ("W_OK - 返回值 %s"% ret)

ret = os.access("/tmp/foo.txt", os.X_OK)
print ("X_OK - 返回值 %s"% ret)
```



## `os.chdir(path)`

- **path**: 要修改成的路径



**实例演示:**

```py
import os,sys

CurrentPath = os.getcwd()
print(CurrentPath)  #输出"E:\Source Code\python_code\test"

os.chdir(r'c:\\')

CurrentPath = os.getcwd()
print(CurrentPath) #输出"c:\"
```



## `os.chmod(path,mode)`

- **path**: 文件名路径或目录路径
- **mode**: 要更改的目录权限
  - **stat.S_IXOTH:** 其他用户有执行权0o001
  - **stat.S_IWOTH:** 其他用户有写权限0o002
  - **stat.S_IROTH:** 其他用户有读权限0o004
  - **stat.S_IRWXO:** 其他用户有全部权限(权限掩码)0o007
  - **stat.S_IXGRP:** 组用户有执行权限0o010
  - **stat.S_IWGRP:** 组用户有写权限0o020
  - **stat.S_IRGRP:** 组用户有读权限0o040
  - **stat.S_IRWXG:** 组用户有全部权限(权限掩码)0o070
  - **stat.S_IXUSR:** 拥有者具有执行权限0o100
  - **stat.S_IWUSR:** 拥有者具有写权限0o200
  - **stat.S_IRUSR:** 拥有者具有读权限0o400
  - **stat.S_IRWXU:** 拥有者有全部权限(权限掩码)0o700
  - **stat.S_ISVTX:** 目录里文件目录只有拥有者才可删除更改0o1000
  - **stat.S_ISGID:** 执行此文件其进程有效组为文件所在组0o2000
  - **stat.S_ISUID:** 执行此文件其进程有效用户为文件所有者0o4000
  - **stat.S_IREAD:** windows下设为只读
  - **stat.S_IWRITE:** windows下取消只读



**使用实例:**

```py
import os, sys, stat

#设置test.txt文件可以通过用户组执行
os.chmod("/tmp/test.txt", stat.S_IXGRP)

#设置test.txt文件可以被其他用户写入
os.chmod("/tmp/test.txt", stat.S_IWOTH)
```



## `os.chown(path,uid,gid)`

- **path**: 要更改权限的文件或目录的路径
- **uid**: 新的所有者用户 ID 
- **gid**: 新的用户组ID

请注意，使用 `os.chown()` 需要有适当的权限，否则会抛出 `PermissionError` 异常



**使用实例:**

```python
import os

# 更改文件 test.txt 的所有者和组
path = './test.txt'
os.chown(path, 1000, 100)
```



## `os.chroot(path)`

- **path**: 要设置为根目录的目录



**使用实例:**

```python
import os, sys

#设置根目录为/tmp
os.chroot("/tmp")

#输出当前的根目录
print(os.path.abspath('/'))
```



## `os.listdir(path)`

- `path`: 要查询的目录的路径，默认为当前工作目录

`os.listdir()` 函数返回的是文件和目录名的列表，不包括文件或目录的其他信息，例如文件大小、修改时间等。要获取这些信息，可以使用 `os.stat()` 函数



**使用实例:**

```python
import os

# 获取当前目录中的所有文件和目录
names = os.listdir()

# 输出当前目录下的所有文件和目录名
for name in names:
    print(name)
```



## `os.link(src,dst)`

- **src**: 用于创建硬连接的源地址
- **dst**: 用于创建硬连接的目标地址



**使用实例:**

```python3
import os, sys

# 打开文件
path = "/var/www/html/foo.txt"
fd = os.open( path, os.O_RDWR|os.O_CREAT )

# 关闭文件
os.close( fd )

# 创建以上文件的拷贝
dst = "/tmp/foo.txt"
os.link( path, dst)

print ("创建硬链接成功!!")
```



## `os.symlink(src,dst)`

- src: 文件源地址
- dst: 目标地址



**使用实例:**

```py
import os
src = '/usr/bin/python'
dst = '/tmp/python'

# 创建软链接
os.symlink(src, dst)
```



## `os.makedirs(path,mode,exist_ok)`

- **path**: 需要递归创建的目录，可以是相对或者绝对路径
- **mode**: 权限模式，默认的模式为 511(八进制)
- **exist_ok**: 是否在目录存在时触发异常。如果 exist_ok 为 False(默认值), 则在目标目录已存在的情况下触发 FileExistsError 异常；如果 exist_ok 为 True，则在目标目录已存在的情况下不会触发 FileExistsError 异常



**使用实例:**

```python
import os, sys

# 创建的目录
path = "/tmp/home/monthly/daily"

os.makedirs(path);

print ("路径被创建")
```



## `os.mkdir(path,[mode])`

os.mkdir()方法用于以数字权限模式创建目录。默认的模式为 0777 (八进制)。

如果目录有多级，则创建最后一级，如果最后一级目录的上级目录有不存在的，则会抛出一个 OSError

- **path**: 要创建的目录，可以是相对或者绝对路径

- **mode**: 要为目录设置的权限数字模式



**使用实例:**

```py
import os, sys

# 创建的目录
path = "/tmp/home/monthly/daily/hourly"

os.mkdir(path,0755)

print ("目录已创建")
```



## `os.pathconf(path,name)`

- **fd**: 文件描述符
- **name**: 要查询的文件属性



**使用实例:** 

```python
import os
fd = fopen( "test.txt",'r+')

#获取文件最大连接数
no = os.fpathconf(fd, 'PC_LINK_MAX')
print ("Maximum number of links to the file. :%d" % no)

#获取文件名最大长度
no = os.fpathconf(fd, 'PC_NAME_MAX')
print ("Maximum length of a filename :%d" % no)

#关闭文件
f.close()
```



## `os.remove(path)`

- path: 要移除的文件路径



**使用实例:**

```python
import os, sys

#列出当前目录下的所有文件
print ("目录为: %s" %os.listdir(os.getcwd()))

#移除test.txt
os.remove("test.txt")

#移除后列出目录
print ("移除后 : %s" %os.listdir(os.getcwd()))
```



## `os.removedirs(path)`

- 要移除的目录路径



**使用实例:**

```python
import os, sys

#列出当前目录: ['a1.txt','resume.doc','a3.py','test']
print ("目录为: %s" %os.listdir(os.getcwd()))

# 移除当前目录下的test目录
os.removedirs("/test")

#列出移除后的目录: ['a1.txt','resume.doc','a3.py']
print ("移除后目录为:" %os.listdir(os.getcwd()
```



## `os.utime(path,time)`

- **path**: 要修改的文件路径
- **time**: 包含文件访问时间和最后修改时间的元组



**使用实例:**

下面的代码中的时间单位是秒，因此需要使用 `time.time()` 函数来获取当前时间

```python
import os,time

# 要修改的文件路径
file_path = "test.txt"

# 获取当前时间
current_time = time.time()

# 定义时间元组
time_tuple = (2021,9,9,0,0,0,0,0,0)

# 将日期转换成秒(shi'jian'c)
timestamp = time.mktime(time_tuple)

# 修改文件的访问时间和最后修改时间
os.utime(file_path, (timestamp, timestamp))

# 使用os.stat来获取文件的访问时间和修改时间
atime = os.stat(file_path).st_atime
mtime = os.stat(file_path).st_mtime
print("文件的访问时间为：", atime)
print("文件的最后修改时间为：", mtime)
```





# pickle模块

## 简介

pickle模块能实现任意对象与文本之间的相互转换, 也可实现任意对象和二进制之间的相互转换, 也就是说pickle能实现python对象的存储及恢复

python中几乎所有的数据类型(列表,字典,集合,类等等)都可以用pickle来序列化, 序列化的数据可读性差且难识别, 通常用于存储数据



## 模块方法

### `pickle.dumps(obj)`

dumps功能将数据转换成只有python语言认识的字符串

- 参数`obj`: 要封装的对象

```python
import pickle
data = ['henry','helloworld',123]
p_str = pickle.dumps(data)
print(p_str)
#输出b'\x80\x04\x95\x1c\x00\x00\x00\x00\x00\x00\x00]\x94(\x8c\x05henry\x94\x8c\nhelloworld\x94K{e.'
```



### `pickle.loads(bytes_obj)`

loads功能将pickle数据转换成python的数据结构

- 参数`bytes_obj`: `pickle_dumps`后的数据对象

```python
import pickle
data = ['henry','helloworld',123]
p_str = pickle.dumps(data)
print(p_str)

str = pickle.loads(p_str)
print(str)
#输出:['henry', 'helloworld', 123]
```





### `pickle.dump(obj,file,[protocol])`

序列化对象, 并将结果数据流写入文件file中

- 必填参数`obj`: 将要封装的对象
- 必填参数`file`: 要写入的文件对象, file必须以二进制模式打开

- 参数`protocol`: 代表序列化模式, 默认值为0, 表示以文本的形式进行序列化, protocol的值为1或2时表示以二进制的形式序列化

```python
import pickle
data = ['henry','helloworld',123]

with open('dump.txt','wb') as file:
    pickle.dump(data,file)

with open('dump.txt','rb') as file:
    print(file.read()) #输出:b'\x80\x04\x95\x1c\x00\x00\x00\x00\x00\x00\x00]\x94(\x8c\x05henry\x94\x8c\nhelloworld\x94K{e.'
```



### `pickle.load(file)`

反序列化对象, 将文件中的数据解析为一个python对象

- 必填参数`file`: 存有pickle数据的文件对象

```python
import pickle
data = ['henry','helloworld',123]

with open('dump.txt','wb') as file:
    pickle.dump(data,file)

with open('dump.txt','rb') as file:
    print(pickle.load(file)) #输出:['henry', 'helloworld', 123]
```





# Cryptography

## 简介

Cryptography是python语言中非常著名的加解密库，在算法层面提供了高层次的抽象，使用起来非常简单、直观，同时还保留了各种不同算法的低级别接口，保留灵活性

我们知道加密一般分为对称加密(Symmetric Key Encryption)和非对称加密(Asymmetric Key Encryption)。各自对应多种不同的算法，每种算法又有不同的密钥位长要求，另外还涉及到不同的分组加密模式，以及末尾补齐方式。因此需要高层次的抽象，把这些参数封装起来，让我们使用时，不用关心这么多参数，只要知道这么用足够安全就够了

对称加密又分为分组加密和序列加密，本文只讨论对称分组加密

- 主流对称分组加密算法：DES、3DES、AES
- 主流对称分组加密模式：ECB、CBC、CFB、OFB
- 主流填充标准：PKCS7、ISO 10126、ANSI X.923、Zero padding

在cryptography库中，对称加密算法的抽象是fernet模块，包括了对数据的加解密以及签名验证功能，以及密钥过期机制，该模块采用了如下定义：

- 加解密算法为AES，密钥位长128，CBC模式，填充标准PKCS7
- 签名算法为SHA256的HMAC，密钥位长128位
- 密钥可以设置过期时间



## 使用实例

```python
from cryptography.fernet import Fernet

String = b"Hello World"

#生成密钥
key = Fernet.generate_key()
print(key) #输出key: b'wmCNyvzUekp_JWEHUcTy4vS2qMrWDXbKOfTooYD1WiI='
f_obj = Fernet(key) #定义一个用于实现加密和解密方法的对象

#进行加密
encrypt_String = f_obj.encrypt(String)
print(encrypt_String) #输出加密后的内容: b'gAAAAABjetNK7sjOoosLI-KcPGdwvQQJVnhwYR9JIeGUx3hJ3qKOQXkaKiGgrlj8wr-tMZdhFKcoK75oONPP4rEDVna5cITQ9g=='

#进行解密
decrypt_String = f_obj.decrypt(encrypt_String)
print(decrypt_String) #输出解密后的内容: b'Hello World'
```














一种学习曲线平滑的编程语言.

当在 Windows 中单独安装 Python 3 使用 `python` 作为命令即可.

而在 Linux 中单独安装 Python 3 要严格使用 `python3` 作为命令.

当安装有多个版本的 Python 时, python3-pip 和 python3-venv 建议用 `python3 -m` 指定 Python 解释器.

```
python3 -m pip
python3 -m venv
```

## 1 安装

### 1.1 Debian

```
┌──(root@debian)-[~]
└─# apt install -y python3 python3-pip python3-venv python3-dev
```

### 1.2 Windows

```powershell
PS C:\Users\sec> scoop install python
```

## 2 初始化

配置镜像加速

```
root@debian:~# python3 -m pip config set global.index-url 'https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple'
```

## 3 使用

> 一般情况下， Python 读一行执行一行

### 3.1 print()

打印字符串

```python
print("hello,world")
```

```
hello,world
```

> 当使用 `" "` 时，表示打印的是字符串，否则打印的是变量或者数值
>
> 注意 `" "` 及其外部的标点符号必须是英文（ `" "` 也可以使用 `' '` 、`''' '''`、`""" """` 代替 ）

拼接字符串

```python
print("hello" + " world")
```

```
hello world
```

> 字符串之间的空格需要包含在 `" "` 内

无空格拼接字符串

```python
print("hello" + "world")
```

```
helloworld
```

符号转义

> 由于 `" "` 是成对出现的，当字符串中使用 `" "` 时需要使用 `\` 转义

```python
print("He said \"Let\'s go!\"")
```

```
He said "Let's go!"
```

 `' '` 和 `" "` 使用 `\n` 换行

```python
print("hello\nworld")
```

```
hello
world
```

使用跨行字符字符串 `''' '''` 和 `""" """` 直接换行

```python
print("""hello
world""")
```

```
hello
world
```

### 3.2 变量

在 Python 中，变量名的取名规则如下：

> 1. **标识符的组成**：变量名必须以字母（a-z、A-Z）、下划线（_）或者汉字开头，后面可以跟着任意数量的字母、数字（0-9）、下划线或者汉字（汉字可能会出现乱码）。
> 2. **大小写敏感**：Python 是大小写敏感的，因此变量名中的大小写字母是有区别的。
> 3. **保留字**：不能使用 Python 中的保留字作为变量名，因为它们具有特殊的含义，用于构造语法结构。例如，`if`、`else`、`for`、`while` 等都是保留字，不能用作变量名。而将 `print()` 、`input()` 、`len()`、`type()`  函数作为变量名会使其变为字符串，失去原有功能。
> 4. **命名规范**：通常遵循以下命名规范：
>    - 使用有意义的名字：变量名应该能够清晰地反映出变量的用途或含义。
>    - 采用驼峰命名法或者下划线命名法：驼峰命名法指的是将单词首字母大写并连接起来，例如 `myVariableName`；下划线命名法指的是使用下划线将单词连接起来，例如 `my_variable_name`。在 Python 中，通常推荐使用下划线命名法来命名变量。
>    - 避免使用单个字符作为变量名，除非是临时变量或者循环索引等特殊情况。
> 5. **PEP 8 规范**：PEP 8 是 Python 社区广泛接受的一种编码风格规范，其中包括了关于变量命名的建议。根据 PEP 8，变量名应该是小写的，并且可以使用下划线来增加可读性，例如 `my_variable_name`。

给变量 test 赋值并打印变量

> 由于 python 是从上至下运行，因此要先给变量赋值，才能使用变量

```python
test = "hello,world"
print(test)
```

```
hello,world
```

存储原 test 变量的值到变量 hi 中，给新的 test 变量的赋上新的值

```python
test = "hello,world"
hi = test
test = "666"
print(test)
print(hi)
```

```
666
hello,world
```

> `test = "hello,world"` 给变量 test 赋值
>
> `hi = test` 将变量 test 解释为值存储在 hi 变量
>
> `test = "666"` 创建一个新的变量 test 并附上新的值（之前的 test 变量已经存储在 hi 变量中了）
>
> `print(test)` 打印最新的 test 变量
> 
> 打印 hi 变量

### 3.3 数学运算

> 在 python 中像是 `6`  这类不被引号包裹的整数可用于运算，而 `"6"` 则是字符串，不可用于运算
>
> 在 python 中像是 `6.0` 这类带小数点的数字都是浮点数，不带的是整数
>
> 加减乘除对应的符号分别是 `+` 、 `-` 、 `*` 、 `/` 
>
> 乘方对应的符号是 `**` ，例如 2 的 3 次方写为 `2**3` ，平方根对应的符号是 `**(1/2)` 或者使用 math 模块中的 `sqrt` 的函数
>
> 遵守数学运算优先级， `()` > `**` > `*/` > `+-` 
>
> 若要使用更加复杂的数学运算，例如 三角函数、log、开方等则可以使用 import 导入一个名为 math 的数学函数模块（所有的 python 模块储存在 [Python 模块索引](https://docs.python.org/zh-cn/3/py-modindex.html) 中）

计算 log2(8) 的值并打印

> math 支持的运算显示在 math 模块的文档中

```python
import math
print(math.log2(8))
```

```
3.0
```

> 导入 math 模块
>
> 使用 `math.` 调用 math 模块运算并打印结果

计算一元二次方程
$$
-x^2 - 2x +3 = 0
$$

$$
解：
x =（ -b ^+ _- \sqrt{b ^2 - 4ac} ）/2a
$$

```python
import math
a = -1
b = -2
c = 3
print((-b + math.sqrt(b**2 - 4*a*c))/2*a)
print((-b - math.sqrt(b**2 - 4*a*c))/2*a)
```

```
-3.0
1.0
```

> 计算其它一元二次方程只需要更改变量的值即可

或者使用 `**(1/2)` 代替 `math.sqrt` 运算

```python
import math
a = 1
b = 9
c = 20
print((-b + (b**2 - 4*a*c)**(1/2))/2*a)
print((-b - (b**2 - 4*a*c)**(1/2))/2*a)
```

```
-4.0
-5.0
```

也可以给重复使用的值设置变量

```python
import math
a = 1
b = 9
c = 20
delta = (b**2 - 4*a*c)**(1/2)
print((-b + delta)/2*a)
print((-b - delta)/2*a)
```

```
-4.0
-5.0
```

### 3.4 注释

> 用于解释代码，或者跳过执行

Python 的注释符为 `#` ，不在函数中的 `""" """` 也可以作为注释，添加多行注释可以选中后按 `Ctrl + /` 

```python
print("1")
# print("2")
print("3")
"""
print("4")
print("5")
"""
```

```
1
3
```

### 3.5 数据类型

使用 type 判断变量值的数据库类型

```python
a = "hello"
b = 6
c = 6.0
d = True
e = None
print(type(a))
print(type(b))
print(type(c))
print(type(d))
print(type(e))
```

```
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
<class 'NoneType'>
```

常见的数据类型

> 注意 python 严格区分大小写

<table border="1">
    <tr>
        <td>"hello"</td>
        <td>"哟！"</td>
        <td>字符串 str</td>
    </tr>
    <tr>
        <td>6</td>
        <td>-32</td>
        <td>整数 int</td>
    </tr>
    <tr>
        <td>6.0</td>
        <td>10.07</td>
        <td>浮点数 float</td>
    </tr>
    <tr>
        <td>True</td>
        <td>False</td>
        <td>布尔类型 bool</td>
    </tr>
    <tr>
        <td colspan="2" style="text-align: center;">None</td>
        <td>空值类型 None</td>
    </tr>
</table>

变量的未知值可以定义为 `None` ，例如：

```python
my_wife = None
```

使用 len 计算字符串长度

```python
string = "hello ,\nworld"
print(len(string))
```

```
13
```

>在 `" "` 里，每个字母，数字，符号都各占一个字符，但是 `\n` 为一个字符

提取出字符串中的第一个字符

```python
string = "hello ,\nworld"
print(string[0])
```

```
h
```

> 在这里， `0` 代表第一个字符 `h` 

提取出字符串中的最后一个字符

```python
string = "hello ,\nworld"
print(string[12])
```

```
d
```

### 3.6 交互模式

> 将命令保存到文件中执行叫做命令行模式，在 pycharm 控制台或 python 终端执行叫做交互模式
>
> 交互模式下无需打印，可直接得到结果

打开 Pycharm 控制台进入交互模式

![打开 Pycharm 控制台进入交互模式](./../../../../../images/Python/%E6%89%93%E5%BC%80%20Pycharm%20%E6%8E%A7%E5%88%B6%E5%8F%B0%E8%BF%9B%E5%85%A5%E4%BA%A4%E4%BA%92%E6%A8%A1%E5%BC%8F.png)

打开 python 终端，进入交互模式

![打开 Python 终端，进入交互模式](./../../../../../images/Python/%E6%89%93%E5%BC%80%20Python%20%E7%BB%88%E7%AB%AF%EF%BC%8C%E8%BF%9B%E5%85%A5%E4%BA%A4%E4%BA%92%E6%A8%A1%E5%BC%8F.png)

终端执行命令，进入交互模式

```powershell
PS C:\Users\sec> python
```

![终端执行命令，进入交互模式](./../../../../../images/Python/%E7%BB%88%E7%AB%AF%E6%89%A7%E8%A1%8C%E5%91%BD%E4%BB%A4%EF%BC%8C%E8%BF%9B%E5%85%A5%E4%BA%A4%E4%BA%92%E6%A8%A1%E5%BC%8F.png)

> 在终端进入的交互模式可执行 `quit()` ，或者 `exit()` 函数退出

### 3.7 len()

 `len()` 是 Python 中的一个内置函数，用于返回一个序列对象（如字符串、列表、元组、集合等）的长度或者元素个数。具体来说， `len()` 函数返回序列中包含的项的数量。

语法格式如下：

```python
len(sequence)
```

> 其中，`sequence` 是要计算长度的序列对象。

例如：

```python
my_string = "Hello, world!"
print(len(my_string))  # 输出: 13

my_list = [1, 2, 3, 4, 5]
print(len(my_list))  # 输出: 5

my_tuple = (1, 'a', True)
print(len(my_tuple))  # 输出: 3
```

> 在这些示例中，`len()` 函数分别返回了字符串、列表和元组中的元素数量。

### 3.8 int()

在 Python 中，`int()` 函数用于将指定的值转换为整数类型。它可以接受不同类型的参数，并尝试将其转换为整数。以下是 `int()` 函数的常见用法：

**转换字符串为整数**：如果传入一个字符串参数，`int()` 函数会尝试将这个字符串解析为整数。如果字符串表示的是一个有效的整数值，那么返回对应的整数；否则会抛出 `ValueError` 异常。

```python
print(int(666))
```

```
666
```

**转换浮点数为整数**：如果传入一个浮点数参数，`int()` 函数会将其向下取整，并返回一个整数。

```python
print(int(3.14))
```

```
3
```

**转换布尔值为整数**：布尔值 `True` 被转换为整数 `1`，布尔值 `False` 被转换为整数 `0`。

```python
print(int(True))
print(int(False))
```

```
1
0
```

**转换其他类型为整数**：如果传入其他类型的参数，`int()` 函数会尝试调用该参数对象的 `__int__()` 方法来进行转换。如果对象没有定义 `__int__()` 方法，则会抛出 `TypeError` 异常。

```python
class CustomClass:
    def __int__(self):
        return 42

print(int(CustomClass()))
```

```
42
```

> 如果 `int()` 函数的参数为空，则会返回 `0`。另外，如果传入的参数无法被转换为整数，则会反馈相应的异常。

### 3.9 float()

在 Python 中， `float()` 函数用于将指定的值转换为浮点数类型。它可以接受不同类型的参数，并尝试将其转换为浮点数。以下是 `float()` 函数的常见用法：

**转换字符串为浮点数**：如果传入一个字符串参数， `float()` 函数会尝试将这个字符串解析为浮点数。如果字符串表示的是一个有效的浮点数值，那么返回对应的浮点数；否则会抛出 `ValueError` 异常。

```python
print(float("3.14"))
```

```
3.14
```

**转换整数为浮点数**：如果传入一个整数参数， `float()` 函数会将其转换为对应的浮点数。

```python
print(float(42))
```

```
42.0
```

**转换布尔值为浮点数**：布尔值 `True` 被转换为浮点数 `1.0` ，布尔值 `False` 被转换为浮点数`0.0`。

```python
print(float(True))
print(float(False))
```

```
1.0
0.0
```

**转换其他类型为浮点数**：如果传入其他类型的参数， `float()` 函数会尝试调用该参数对象的 `__float__()` 方法来进行转换。如果对象没有定义 `__float__()` 方法，则会抛出 `TypeError` 异常。

```python
class CustomClass:
    def __float__(self):
        return 3.14

print(float(CustomClass()))
```

```
3.14
```

> 如果`float()`函数的参数为空，则会返回`0.0`。另外，如果传入的参数无法被转换为浮点数，则会抛出相应的异常。

### 3.10 str()

在 Python 中，`str()` 函数用于将指定的值转换为字符串类型。它可以接受不同类型的参数，并尝试将其转换为字符串。以下是 `str()` 函数的常见用法：

**转换数字为字符串**：如果传入一个数字参数，`str()` 函数会将其转换为对应的字符串。

```python
print(str(42))
```

```
42
```

**转换布尔值为字符串**：布尔值 `True` 被转换为字符串 `'True'`，布尔值 `False` 被转换为字符串 `'False'`。

```python
print(str(True))
print(str(False))
```

```
True
False
```

**转换对象为字符串**：如果传入一个对象参数，`str()` 函数会尝试调用该对象的 `__str__()` 方法来进行转换。如果对象没有定义 `__str__()` 方法，则会返回对象的默认字符串表示（通常是对象的类型和内存地址）。

```python
class CustomClass:
    def __str__(self):
        return "CustomClass object"

print(str(CustomClass()))
```

```
CustomClass object
```

如果 `str()` 函数的参数为空，则会返回空字符串 `''`。另外，如果传入的参数无法被转换为字符串，则会抛出相应的异常。

### 3.11 input()

> input 一律返回字符串，即使使用数字也会当作字符串，因此直接使用 input 的值所在的变量运算

使用 input 函数获取用户输入

```python
input("请输入你的年龄：")
```

```
请输入你的年龄：
```

将 input 函数存入变量，并打印

```py
user_age = input("请输入你的年龄：")
print("知道了，你今年" + user_age + "岁了")
```

```
请输入你的年龄：20
知道了，你今年20岁了
```

计算 10 年后的年龄

> 使用 int() 将字符串转换为整数参与运算
>
> 使用 str() 将整数转换为字符串参与拼接
>
> 当整数和字符串一起使用 `+` 时会报错

```python
user_age = input("请输入你的年龄：")
user_age_after_10_years = 10 + int(user_age)
print("知道了，你十年后" + str(user_age_after_10_years) + "岁了")
```

```
请输入你的年龄：20
知道了，你十年后30岁了
```

使用 input 编写一个 bmi 计算器

> 注意这里身高的单位是 m，体重的单位是 kg

$$
BMI=体重/身高^2
$$


```python
user_height = input("你的身高是（cm）：")
user_weight = input("你的体重是（kg）：")
user_bmi = float(user_weight) / (float(user_height) / 100) ** 2
print("你的 bmi 值是" + str(user_bmi))
```

```
你的身高是（cm）：187.6
你的体重是（kg）：87.6
你的 bmi 值是24.890776092125424
```

> 使用 float() 将变量 user_height 和变量 user_weight 转换为浮点数参与运算
>
> 使用 str() 将变量 user_bmi 需要转换为字符串参与拼接

### 3.12 条件语句

在 Python 中，`else` 是与 `if` 语句配合使用的一个关键字，用于在条件表达式为假时执行一组语句。`else` 语句块通常紧跟在 `if` 语句块之后，表示在 `if` 条件不满足时要执行的代码。

基本的 `if-else` 结构如下：

```python
if [条件]:
    条件为 True 时执行的语句 1
    条件为 True 时执行的语句 2
else:
    条件为 False 时执行的语句 1
    条件为 False 时执行的语句 2

不在条件内时执行的语句
```

> 当条件表达式为 True 时，`if` 语句块中的代码会被执行；当条件表达式为 False 时，`else` 语句块中的代码会被执行。
>
> 若没有 `else` 则会跳过执行 `if` 语句块中的代码转而执行 `if` 语句块之后的代码
>
> 使用 `else` 时注意之前执行的语句的缩进，不要跳出 `if` 
>
> 执行语句：根据条件的真假，执行相应的语句。这些语句通常是被缩进的代码块，称为语句块。在 Python 中，使用缩进来表示代码块的开始和结束（缩进一般为 4 个空格）。

条件语句中使用的比较符号

<table border="1">
    <tr>
        <td>==</td>
        <td>3 == 3</td>
        <td>"a" == "b"</td>
    </tr>
    <tr>
        <td>等于</td>
        <td>True</td>
        <td>False</td>
    </tr>
</table>

<table border="1">
    <tr>
        <td>!=</td>
        <td>3 != 3</td>
        <td>"a" != "b"</td>
    </tr>
    <tr>
        <td>不等于</td>
        <td>False</td>
        <td>True</td>
    </tr>
</table>

<table border="1">
    <tr>
        <td>></td>
        <td>>=</td>
        <td><</td>
        <td><=</td>
    </tr>
    <tr>
        <td>3 > 4</td>
        <td>5 >= 20</td>
        <td>5 < 20</td>
        <td> 5 * 3 <= 20</td>
    </tr>
        <tr>
        <td>False</td>
        <td>False</td>
        <td>True</td>
        <td>True</td>
    </tr>
</table>

> 由于 `=` 已经在给变量复制时使用了，因此在条件语句使用 `==` 比较两个值

例如，下面的示例演示了一个简单的条件语句，根据条件的真假输出不同的结果：

```python
index = input("输入一个数字：")
if int(index) > 6:
    print("这个数字大于 6")
else:
    print("这个数字不大于 6")

print("判断完成")
```

> 在这个例子中，如果变量 `index` 的值大于 6，则输出 `这个数字大于 6` ；否则输出 `这个数字不大于 6` 。

写一个判断对象心情指数大小的条件语句，如果心情指数大于 60，则可以打游戏，否则不可以打游戏

```python
mood_index = input("对象今晚的心情指数是（0-100）：")
if int(mood_index) >= 60:
    print("恭喜，今晚应该可以打游戏，去吧！蒜头王八")
    print("o(*￣▽￣*)ブ")
else: # mood_index < 60
    print("为了自个儿的小命，还是别打了。")
    print("(T_T)")
print("")
print("...等等！你并没有对象。 ,,ԾㅂԾ,,")
```

### 3.13 嵌套

当条件为 True 时执行下一个条件语句的嵌套语句

```python
if [条件一]:
    if [条件二]:
        if [条件三]:
            [条件三为 True 时执行的语句]
        else:
            [条件三为 False 时执行的语句]
    else:
        [条件二为 False 时执行的语句]
else:
    [条件一为 False 时执行的语句]
```

当条件为 False 时执行下一个条件语句的嵌套语句

> 相当于 elif

```python
if [条件一]:
    [条件一为 True 时执行的语句]
else:
    if [条件二]:
        [条件一为 False ，条件二为 True 时执行的语句]
    else:
        if [条件三]:
            [条件一和二都为 False ，条件三为 True 时执行的语句]
        else:
            [所有条件都为 False 时执行的代码]
```

写一个判断对象心情指数大小和是否在家的嵌套语句，如果心情指数大于 60，则可以打游戏，否则判断是否在家，如果不在家则可以打游戏

```python
# mood_index 是 0 到 100 之间的整数
# is_at_home 为布尔值
mood_index = int(input("请输入你对象的心情指数（0-100）："))
if mood_index > 60:
    print("开心时刻!")
    print("φ(゜▽゜*)♪")
else:
    is_at_home = input("请输入你的对象是否在家（是/否）：")
    if is_at_home == "是":
        print("放弃游戏，低调做人")
        print("/(ㄒoㄒ)/~~")
    else:
        print("请尽情放飞自我！")
        print("(p≧w≦q)")
```

### 3.14 多条件判断

`elif` 是 Python 中的一个关键字，是 `else if` 的缩写，用于在多个条件之间进行选择。`elif` 语句用于在前一个条件为假时，检查另一个条件是否为真，并在条件为真时执行相应的代码块。

`elif` 语句通常与 `if` 语句一起使用，形成一个多条件的判断结构。基本的语法结构如下：

```python
if 条件一:
    [条件一为 True 时执行的语句]
elif 条件二:
    [条件一为 False ，条件二为 True 时执行的语句]
elif 条件三:
    [条件一和二都为 False ，条件三为 True 时执行的语句]
...
else:
    [所有条件都为 False 时执行的代码]
```

`elif` 语句可以有多个，用于检查多个条件，但只有一个 `if` 和一个 `else`。当满足其中一个 `elif` 语句的条件时，相应的代码块会被执行，然后程序会跳出整个条件判断结构。

以下是一个示例，演示了 `elif` 的使用：

```python
score = int(input("请输入你的分数（0-100）："))

if score >= 90:
    print("优秀")
elif score >= 80:
    print("良好")
elif score >= 70:
    print("中等")
elif score >= 60:
    print("及格")
else:
    print("不及格")
```

> 在这个示例中，根据输入的分数不同，程序会打印出相应的评价，如果分数在不同的区间内，则会执行不同的代码块。

优化 bmi 计算器
$$
BMI=体重/身高^2
$$

```python
# 偏瘦：user_bmi <= 18.5
# 正常：18.5 < user_bmi <= 25
# 偏胖：25 < user_bmi <= 30
# 肥胖：user_bmi > 30

user_gender = input("你的性别是（男/女）：")
if user_gender == "男":
    greet = "先生你好，"
elif user_gender == "女":
    greet = "女士你好，"

user_height = input("你的身高是（cm）：")
user_weight = input("你的体重是（kg）：")
user_bmi = float(user_weight) / (float(user_height) / 100) ** 2
print(greet + "你的 bmi 值是" + str(user_bmi))

if user_bmi <= 18.5:
    print("此 bmi 值属于偏瘦范围")
    print("多吃点吧! ( •̀ ω •́ )✧")
elif 18.4 < user_bmi <= 25:
    print("此 bmi 值属于正常范围")
    print("注意保持 (￣▽￣)")
elif 25 < user_bmi <= 30:
    print("此 bmi 值属于偏胖范围")
    print("该减肥了！ qi（；´д｀）ゞ")
else:
    print("此 bmi 值属于肥胖范围")
    print("无言以对 (￣へ￣)")
```

```
你的身高是（cm）：187.6
你的体重是（kg）：87.6
你的 bmi 值是24.890776092125424
此 bmi 值属于正常范围
注意保持 (￣▽￣)
```

### 3.15 逻辑运算

在 Python 中，`and`、`or` 和 `not` 是用于逻辑运算的关键字。

<table border="1">
    <tr>
        <td>and</td>
        <td>or</td>
        <td>not</td>
    </tr>
    <tr>
        <td>与</td>
        <td>或</td>
        <td>非</td>
    </tr>
</table>

 `and` ：逻辑与运算符。当 `and` 连接的两个条件都为真时，整个表达式的结果才为真。否则，只要有一个条件为假，整个表达式的结果就为假。例如：`x and y` 表示当 `x` 和 `y` 同时为真时，整个表达式为真，否则为假。

 `or` ：逻辑或运算符。当 `or` 连接的两个条件中至少有一个为真时，整个表达式的结果就为真。只有当两个条件都为假时，整个表达式的结果才为假。例如：`x or y` 表示当 `x` 或者 `y` 中至少有一个为真时，整个表达式为真，否则为假。

 `not` ：逻辑非运算符。用于对条件取反。例如：`not x` 表示当 `x` 为假时，整个表达式为真，否则为假。

> 这些逻辑运算符常用于条件语句、循环结构以及逻辑表达式中，用于组合和控制不同条件的逻辑关系。

完成以下任务，对象将心情大好，奖励你一个 Switch 作为新年礼物

```python
# 1.一个月内主动做家务次数超过 10 次
# 2.一个月内发红包次数超过 10 次
# 3.一个月内陪对象逛街的次数超过 4 次
# 4.一个月内没有任何惹 ta 生气的行为出现

house_work = int(input("这个月做的家务次数："))
red_packet = int(input("这个月发过的红包次数："))
go_shopping = int(input("这个月陪对象逛街的次数："))
anger = input("这个月是否惹 ta 生气过（是/否）：")

if house_work > 10 and red_packet > 10 and go_shopping > 4 and not anger == "是":
    print("摩拳擦掌等待 Switch！")
else:
    print("Switch 随风散去...")
```

### 3.16 list = []

在 Python 中，`list` 是一种数据类型，用于存储多个元素的有序集合。方括号 `[ ]` 用来表示列表，列表中的元素可以是任意数据类型，包括整数、浮点数、字符串、甚至其他列表等。

例如，`list = ["a", "b", "c"]` 表示创建了一个包含三个元素的列表，分别是 `a`、`b` 和 `c` 。这个列表可以用来存储任何类型的数据。

列表中的元素可以通过索引来访问，索引从 0 开始计数。例如，`list[0]` 表示访问列表中的第一个元素，`list[1]` 表示访问列表中的第二个元素，依此类推。

`my_list.append()` 是 Python 中列表对象的一个方法，用于向列表末尾添加新的元素。具体语法为：

```python
my_list.append(element)
```

> `append()` 方法接受一个参数，即要追加到列表末尾的元素。
>
> 其中，`element` 是要添加到列表末尾的元素。

`my_list.remove()` 是 Python 中列表对象的一个方法，用于从列表中移除指定的元素。具体语法为：

```python
my_list.remove(element)
```

> `remove()` 方法接受一个参数，即要从列表中移除的元素。
>
> 其中，`element` 是要从列表中移除的元素。
>
> 如果列表中存在多个相同的元素，`remove()` 方法只会移除第一个匹配的元素。如果列表中不存在要移除的元素，则会引发 ValueError 异常。

以下是一个示例，展示了如何创建列表并访问其中的元素：

```python
# 创建一个包含三个元素的列表
my_list = ['apple', 'banana', 'orange']

# 访问列表中的元素
print(my_list[0])
print(my_list[1])
print(my_list[2])
print('长度：' + str(len(my_list)))

# 向列表中追加元素
my_list.append('grape')
my_list.append('66.6')
my_list.append(True)
my_list.append(None)
print('长度：' + str(len(my_list)))
print('元素：' + str(my_list))

# 移除列表中的元素
my_list.remove('apple')

# 修改 orange 为 pear
my_list[1] = 'pear'
print('长度：' + str(len(my_list)))
print('元素：' + str(my_list))
```

```
apple
banana
orange
长度：3
长度：7
元素：['apple', 'banana', 'orange', 'grape', '66.6', True, None]
长度：6
元素：['banana', 'pear', 'grape', '66.6', True, None]
```

> 需要注意的是，列表是可变的数据类型，可以动态地添加、删除或修改其中的元素。

列表专用函数

```python
my_list = [1,13,-7,2,96]

print(max(my_list))		# 打印列表中的最大值（若是字母则比较 ascii 码值）
print(min(my_list))		# 打印列表中的最小值（若是字母则比较 ascii 码值）
print(sorted(my_list))	# 打印排序好的列表
```

```
96
-7
[-7, 1, 2, 13, 96]
```

### 3.17 tuple = ()

在 Python 中，元组（Tuple）是一种有序的、不可变的数据类型。它是由一系列元素组成，每个元素可以是任意数据类型，并且元素之间用逗号 `,` 分隔，通常用小括号 `()` 表示。

元组的特点包括：

- 不可变性：一旦创建了元组，就不能修改其内容，包括添加、删除或修改元素。因此，元组是一种不可变的数据类型。
- 有序性：元组中的元素按照其在元组中的位置顺序存储，可以通过索引来访问。

创建元组的方式包括：

```python
# 创建一个空元组
my_tuple = ()

# 创建一个包含元素的元组
my_tuple = (1, 2, 3)

# 创建一个包含不同类型元素的元组
my_tuple = (1, 'hello', 3.14)

# 创建一个只包含一个元素的元组（需要在元素后面加逗号）
my_tuple = (1,)
```

访问元组中的元素可以通过索引来实现，索引从0开始，例如：

```python
# 获取元组中的值
print(my_tuple[0])  # 输出: 1

# 元组是不可变的，无法修改元素
# my_tuple[0] = 2  # TypeError: 'tuple' object does not support item assignment
```

> 元组适合用于存储不可变的数据集合，例如一些常量、配置参数等。虽然元组的不可变性意味着无法直接修改其内容，但可以通过创建新的元组来实现对元组的更新和修改。

### 3.18 dict = {}

在 Python 中，字典是一种可变的、无序的、键-值对（key-value pair）的集合。每个键对应一个值，键必须是唯一的，但值可以重复。字典通常用大括号 `{}` 来表示，每个键值对之间用逗号 `,` 分隔。

字典的特点包括：

- 键必须是不可变的类型，通常使用字符串、整数、浮点数、元组等作为键（字典和列表不可以）。
- 值可以是任意类型，包括数字、字符串、列表、字典等。
- 字典中的元素没有固定顺序，无法通过索引来访问，而是通过键来查找对应的值。

创建字典的方式包括：

```python
# 创建一个空字典
my_dict = {}

# 创建一个非空字典
my_dict = {'name': 'John', 'age': 30, 'city': 'New York'}

# 使用 dict() 函数创建字典
my_dict = dict(name='John', age=30, city='New York')
```

访问字典中的元素可以通过键来实现，例如：

```python
# 获取字典中的值
print(my_dict['name'])  # 输出: John

# 修改字典中的值
my_dict['age'] = 31

# 添加新的键值对
my_dict['gender'] = 'male'

# 删除键值对（若不存在则会报错）
del my_dict['city']

# 检验键是否存在于字典中（存在返回 True ，否则返回 False）
'city' in my_dict

# 检验字典中有多少个键值对
len(my_dict)
```

> 字典提供了丰富的方法和操作，用于对键值对进行增删改查。字典在 Python 中被广泛应用，是一种非常常用的数据结构类型。

创建一个通讯录以 tuple 作为键

```python
# 创建一个存储多个同名的人的 tuple

my_dict = {('张伟','23'):'15000000000',
          ('张伟','34'):'15000000001',
          ('张伟','56'):'15000000002'}

print(my_dict[('张伟','34')])
```

```
15000000001
```

如果要到了一个美女的手机号，将这个联系方式存入 dict

```python
my_dict = {'小明':'13700000000',
          '小花':'13700000001'}

my_dict['美女'] = '13700000002'
print(my_dict)

# 更新值
my_dict['美女'] = '13700000003'
print(my_dict)
```

```
{'小明': '13700000000', '小花': '13700000001', '美女': '13700000002'}
```

创建一个结合 input、字典、if 判断，做一个查询流行语含义的电子词典程序

```python
my_dict = {'甩锅':'指推卸责任，企图将自身的矛盾转移到其他地方去，让别人来背黑锅的意思。',
       '内卷':'非理性内部竞争，指一种社会或文化模式在发展到一定阶段后停滞不前，或无法转化为更高级模式的现象。'}
print(my_dict)

my_dict['杠精'] = '通过抬杠获取快感的人、总是唱反调的人、争辩时故意持相反意见的人。'
print(my_dict)

my_dict['淦'] = '原意是指水入船中，代表＂干＂，这样说就显得有趣而且文明。'
my_dict['躺平'] = '佛系生存方式，指无论对方做出什么反应，你内心都毫无波澜，对此不会有任何反应或者反抗。'
my_dict['你品，你细品'] = '意思是你体会一下，好好体会一下或者你想一下，你好好想一下。'
my_dict['社死'] = '社会性死亡，其含义多为在公众面前出丑的意思，已经丢脸到没脸见人，只想地上有条缝能钻进去的程度，被称之为“社会性死亡”。'
my_dict['emo'] = 'EMO是“emotional”的缩写，可以理解为颓废、抑郁、傻。'
my_dict['fyq'] = 'for your page的意思，为用户个人随机推荐的页面，意思就是上热门。'
my_dict['什么是快乐星球？'] = '来源于95后00后的童年记忆儿童剧《快乐星球》，一般用于分享简单快乐。'
my_dict['小丑竟是我自己'] = '用于形容一厢情愿地付出或努力没有得到预期的回报，或是发生意料之外事情时的尴尬自嘲。'
my_dict['集美'] = '姐妹'
my_dict['打工人'] = '很多上班族的自称。'
my_dict['朴信男'] = '普通却过于自信的男生'
my_dict['大聪明'] = '不灵光'
my_dict['破防'] = '心理防线被突破'

search = input('请输入你要查询的流行语：')
if search in my_dict:
    print('你要查询的流行语含义如下：')
    print(my_dict[search])
else:
    print('你查询的流行语暂未收录')
    print('当前的字典收录的流行语的条数为：' + str(len(my_dict)) + ' 条。')
```

### 3.19 for 循环

在 Python 中，`for ` 循环是一种用于迭代 (iterate) 序列 (sequence) 或其他可迭代对象 (iterable) 的控制结构。通过 `for` 循环，你可以按顺序访问序列中的每个元素，并对其执行特定的操作。

 `for ` 循环的基本语法如下：

```python
for 变量 in 可迭代对象:
    # 对每个变量做一些事情
    #
```

> 在这个语法中：
>
> - `变量` ：表示在每次迭代中被赋予当前元素的值（可随意构造）。
> - `可迭代对象` ：是一个包含多个元素的数据集合，如列表 (list) 、元组 (tuple) 、集合 (set)  、字典 (dictionary) ，或者是其他支持迭代的对象。
> - `执行操作` ：指的是在循环内部要执行的代码块。这可以是任何 Python 代码，通常用于处理每个元素。
> - 注意缩进

`for` 循环的工作原理是，它会从可迭代对象中依次取出每个元素，并将其赋值给变量，然后执行循环体中的操作，直到可迭代对象中的所有元素都被处理完毕为止。

下面是一个简单的示例，演示了如何使用 `for` 循环遍历列表中的元素并打印它们：

```python
my_list = [1, 2, 3, 4, 5]
for num in my_list:
    print(num)
```

> 这段代码会依次打印出列表 `my_list` 中的每个元素，即 1、2、3、4 和 5。
>
> 需要注意的是，Python 中的 `for` 循环不仅可以遍历序列类型的数据，还可以遍历任何可迭代对象，比如字符串、文件对象等。另外，可以结合 `range()` 函数生成指定范围的整数序列来进行迭代。

打印列表中超过 38.5 的数据

```python
my_list = [36.7,38.5,39.2,37.2,36.6,36.8,36.5,37.3,37.5,38.6,36.2,38.9]
for num in my_list:
    if num >= 38.5:
        print(num)
        print("完犊子了！")
```

打印字典中超过 38.5 的数据的键值对

```python
my_dict = {'111':36.7,'112':38.5,'113':39.2,'114':37.2,'115':36.6,'116':36.8,'117':36.5,'118':37.3,'119':37.5,'120':38.6,'121':36.2,'122':38.9}
for user, num in my_dict.items():
    if num >= 38.5:
        print(user,num)
        print("完犊子了！")
        
my_dict.keys()
# 所有键
my_dict.values()
# 所有值
my_dict.items()
# 所有键值对
```

相当于

```python
my_dict = {'111':36.7,'112':38.5,'113':39.2,'114':37.2,'115':36.6,'116':36.8,'117':36.5,'118':37.3,'119':37.5,'120':38.6,'121':36.2,'122':38.9}
for user_num in my_dict.items():
    user = user_num[0]
    num = user_num[1]
    if num >= 38.5:
        print(user,num)
        print("完犊子了！")
```

### 3.20 range

在 Python 中，`range()` 是一个用于生成整数序列的内置函数。它可以接受一个、两个或三个参数，返回一个表示特定范围的整数序列的可迭代对象。

`range()` 函数的基本语法如下：

```python
range(stop)
range(start, stop, step)
```

> 在这里：
>
> -  `start` ：表示序列的起始值（默认为 0 ）。
> -  `stop` ：表示序列的结束值，但生成的序列不包含该值。
> -  `step` ：表示序列中每个整数之间的步长（默认为 1 ）。
>
>  `range()` 函数生成的序列是一个不可变的序列，它包含从 `start` 到 `stop` （不包含 `stop` ）之间的整数，按照指定的 `step` 增量进行生成。如果省略了 `start` 参数，则默认从 0 开始；如果省略了 `step` 参数，则默认步长为 1。

 `range()` 函数常用于在循环中生成一系列连续的整数，用于控制循环的次数或索引迭代。例如：

```python
for i in range(5):
    print(i)
```

> 这段代码将打印出 0 到 4 之间的整数。

```python
for i in range(1, 10, 2):
    print(i)
```

> 这段代码将打印出 1 到 9 之间的奇数，步长为 2。
>
> 需要注意的是， `range()` 函数返回的是一个可迭代对象，如果需要生成实际的整数序列，可以将其转换为列表或其他序列类型。例如，`list(range(5))` 将生成 `[0, 1, 2, 3, 4]` 。

计算从 `1` 到 `100` 的整数之和

```python
# 给一个变量赋值为 0
num = 0
# 生成 1 到 100 的整数
for i in range(1,101,1):
# 重新定义和的变量为 num + i
    num = num + i
# 打印整数之和
print(num)
```

> 之所以需要使用 num 变量是因为直接带引 `i` ，会打印出 1 - 100 的所有整数

## 4 报错

某些符号需要成对出现

```python
print('hello,world")
```

```
SyntaxError: unterminated string literal (detected at line 1)

进程已结束，退出代码为 1
```

使用了无效字符（如中文字符）

```python
print(“hello,world”)
```

```
SyntaxError: invalid character '“' (U+201C)

进程已结束，退出代码为 1
```

---

参考链接

- [Python](https://www.python.org/)
-  [Python Documentation](https://www.python.org/doc/)

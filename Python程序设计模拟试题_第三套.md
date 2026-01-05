# Python 程序设计模拟试题（第三套）

**适用对象**：高职一年级
**考试时间**：120分钟
**满分**：100分

---

## 一、选择题（每题2分，共40分）

**1. 以下代码的输出结果是（ ）**
```python
a, b = 5, 3
print("A") if a > b else print("B")
```
A. A
B. B
C. AB
D. 语法错误

**2. 嵌套`if`语句中，`else`与哪个`if`配对？（ ）**

A. 最近的`if`
B. 最远的`if`
C. 第一个`if`
D. 随机配对

**3. 以下代码输出几个星号？（ ）**
```python
for i in range(3):
    for j in range(2):
        print("*", end="")
```
A. 3
B. 5
C. 6
D. 9

**4. 以下代码的输出结果是（ ）**
```python
for i in range(5):
    if i == 3:
        continue
    print(i, end="")
```
A. 01234
B. 0124
C. 012
D. 01245

**5. 列表推导式`[x*2 for x in range(5)]`的结果是（ ）**

A. `[0, 1, 2, 3, 4]`
B. `[2, 4, 6, 8, 10]`
C. `[0, 2, 4, 6, 8]`
D. `[1, 2, 3, 4, 5]`

**6. 以下代码的输出结果是（ ）**
```python
lst = [1, 2, 3]
lst2 = lst
lst2.append(4)
print(lst)
```
A. `[1, 2, 3]`
B. `[1, 2, 3, 4]`
C. `[4]`
D. 报错

**7. 以下关于元组和列表的区别，说法正确的是（ ）**

A. 元组可以修改，列表不可以
B. 元组用方括号，列表用圆括号
C. 元组不可变，列表可变
D. 元组不能包含列表

**8. 以下代码的输出结果是（ ）**
```python
t = (1, 2, [3, 4])
t[2].append(5)
print(t)
```
A. 报错
B. `(1, 2, [3, 4])`
C. `(1, 2, [3, 4, 5])`
D. `(1, 2, 3, 4, 5)`

**9. 删除字典中指定键值对的方法是（ ）**

A. `remove()`
B. `delete()`
C. `pop()`
D. `discard()`

**10. 以下代码的输出结果是（ ）**
```python
d = {"x": 1, "y": 2}
d.update({"y": 3, "z": 4})
print(d)
```
A. `{"x": 1, "y": 2}`
B. `{"x": 1, "y": 3, "z": 4}`
C. `{"y": 3, "z": 4}`
D. 报错

**11. 下列操作中，哪个可以创建集合？（ ）**

A. `s = {}`
B. `s = set()`
C. `s = ()`
D. `s = []`

**12. 以下代码的输出结果是（ ）**
```python
s1 = {1, 2, 3}
s2 = {2, 3, 4}
print(s1 ^ s2)
```
A. `{2, 3}`
B. `{1, 4}`
C. `{1, 2, 3, 4}`
D. `set()`

**13. 以下哪种参数传递方式是正确的？（ ）**
```python
def func(a, b, c):
    pass
```
A. `func(1, c=3, 2)`
B. `func(a=1, 2, 3)`
C. `func(1, b=2, c=3)`
D. `func(a=1, b=2, 3)`

**14. `*args`参数的作用是（ ）**

A. 接收关键字参数
B. 接收任意数量的位置参数
C. 接收必需参数
D. 接收默认参数

**15. 以下代码的输出结果是（ ）**
```python
def outer():
    x = 10
    def inner():
        nonlocal x
        x += 5
    inner()
    return x

print(outer())
```
A. 10
B. 15
C. 5
D. 报错

**16. `if __name__ == "__main__":`的作用是（ ）**

A. 定义主函数
B. 判断模块是否被直接运行
C. 导入其他模块
D. 创建主类

**17. 以下哪个不是Python内置模块？（ ）**

A. `os`
B. `sys`
C. `numpy`
D. `json`

**18. 以下代码的执行结果是（ ）**
```python
with open("test.txt", "w") as f:
    f.write("Hello")
print(f.closed)
```
A. `True`
B. `False`
C. `None`
D. 报错

**19. 读取二进制文件应使用的模式是（ ）**

A. `"r"`
B. `"rb"`
C. `"w"`
D. `"rt"`

**20. 以下关于类的继承，说法正确的是（ ）**

A. Python不支持多继承
B. 子类不能重写父类方法
C. 子类可以调用父类的`__init__`方法
D. 继承使用`extends`关键字

---

## 二、判断题（每题2分，共20分）

**1. Python中可以使用`and`、`or`、`not`作为逻辑运算符。（ ）**

**2. `for`循环可以带`else`子句，当循环正常结束时执行`else`。（ ）**

**3. `lst.extend([1,2,3])`和`lst.append([1,2,3])`的效果相同。（ ）**

**4. 元组支持切片操作。（ ）**

**5. 字典的`items()`方法返回所有键值对组成的列表。（ ）**

**6. `frozenset`是不可变的集合类型。（ ）**

**7. 匿名函数使用`lambda`关键字定义。（ ）**

**8. Python标准库中的`json`模块可以处理JSON数据。（ ）**

**9. `seek(0)`方法可以将文件指针移动到文件开头。（ ）**

**10. 私有属性以双下划线`__`开头，完全不能在类外部访问。（ ）**

---

## 三、操作题（每题4分，共40分）

### 第1题（条件语句）

编写一个简单的计算器程序：
- 输入两个数和运算符（+、-、*、/）
- 根据运算符进行相应计算
- 除法时检查除数是否为0

```python
# 请在下面编写代码




```

---

### 第2题（循环）

使用循环打印以下图案（n=5）：
```
    *
   ***
  *****
 *******
*********
```

```python
# 请在下面编写代码
n = 5




```

---

### 第3题（列表）

编写程序实现列表去重，要求：
1. 保持原有顺序
2. 不使用`set()`函数
测试列表：`[1, 3, 2, 1, 5, 3, 2, 4, 1]`

```python
# 请在下面编写代码
original = [1, 3, 2, 1, 5, 3, 2, 4, 1]




```

---

### 第4题（元组）

利用元组实现两个变量值的交换，并扩展为交换列表中指定位置的两个元素。

```python
# 请在下面编写代码
# 1. 交换两个变量
a, b = 10, 20
# 交换后a=20, b=10

# 2. 交换列表中索引为i和j的元素
def swap_elements(lst, i, j):
    pass

# 测试
numbers = [1, 2, 3, 4, 5]
# 交换索引1和3的元素，结果为[1, 4, 3, 2, 5]



```

---

### 第5题（字典）

实现一个简单的电话簿程序，支持以下功能：
1. 添加联系人（姓名和电话）
2. 查找联系人
3. 删除联系人
4. 显示所有联系人

```python
# 请在下面编写代码
phone_book = {}

def add_contact(name, phone):
    pass

def find_contact(name):
    pass

def delete_contact(name):
    pass

def show_all():
    pass

# 测试代码



```

---

### 第6题（集合）

使用集合实现以下功能：
1. 检查一个列表中是否有重复元素
2. 找出两个字符串中共同出现的字符

```python
# 请在下面编写代码

# 1. 检查重复元素
def has_duplicates(lst):
    pass

# 2. 共同字符
def common_chars(str1, str2):
    pass

# 测试
print(has_duplicates([1, 2, 3, 4, 5]))  # False
print(has_duplicates([1, 2, 3, 2, 5]))  # True
print(common_chars("hello", "world"))   # {'l', 'o'}



```

---

### 第7题（函数）

编写一个装饰器`timer`，用于计算函数的执行时间。

```python
# 请在下面编写代码
import time

def timer(func):
    pass

# 使用装饰器
@timer
def slow_function():
    time.sleep(1)
    print("函数执行完毕")

# 测试
slow_function()



```

---

### 第8题（模块）

创建一个自定义模块`mymath.py`，包含以下函数：
1. `add(a, b)` - 加法
2. `subtract(a, b)` - 减法
3. `multiply(a, b)` - 乘法
4. `divide(a, b)` - 除法（处理除零错误）

然后在主程序中导入并使用该模块。

```python
# mymath.py 模块内容：




# 主程序 main.py：




```

---

### 第9题（文件操作）

实现一个简单的日志记录功能：
1. 创建`log.txt`文件
2. 每次调用`log(message)`函数时，将时间戳和消息追加到文件
3. 实现`read_logs()`函数读取所有日志

```python
# 请在下面编写代码
from datetime import datetime

def log(message):
    pass

def read_logs():
    pass

# 测试
log("程序启动")
log("用户登录")
log("执行操作A")
print(read_logs())



```

---

### 第10题（面向对象）

设计一个银行账户系统，包含：
1. `Account`基类：账号、户名、余额，存款、取款方法
2. `SavingsAccount`（储蓄账户）子类：额外属性利率，计算利息方法
3. `CheckingAccount`（支票账户）子类：额外属性透支额度，重写取款方法

```python
# 请在下面编写代码
class Account:
    pass

class SavingsAccount(Account):
    pass

class CheckingAccount(Account):
    pass

# 测试代码



```

---

## 参考答案

### 一、选择题答案

| 题号 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 答案 | A | A | C | B | C | B | C | C | C | B |

| 题号 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 答案 | B | B | C | B | B | B | C | A | B | C |

### 二、判断题答案

| 题号 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 答案 | √ | √ | × | √ | × | √ | √ | √ | √ | × |

**判断题解析**：
- 第3题：`extend()`展开列表添加元素，`append()`将整个列表作为一个元素添加
- 第5题：`items()`返回的是`dict_items`视图对象，不是列表
- 第10题：私有属性可以通过`_类名__属性名`的方式在外部访问（名称改写）

### 三、操作题参考答案

**第1题**
```python
num1 = float(input("请输入第一个数："))
op = input("请输入运算符（+、-、*、/）：")
num2 = float(input("请输入第二个数："))

if op == "+":
    result = num1 + num2
elif op == "-":
    result = num1 - num2
elif op == "*":
    result = num1 * num2
elif op == "/":
    if num2 == 0:
        print("错误：除数不能为0")
        result = None
    else:
        result = num1 / num2
else:
    print("无效的运算符")
    result = None

if result is not None:
    print(f"结果：{result}")
```

**第2题**
```python
n = 5
for i in range(n):
    spaces = " " * (n - i - 1)
    stars = "*" * (2 * i + 1)
    print(spaces + stars)
```

**第3题**
```python
original = [1, 3, 2, 1, 5, 3, 2, 4, 1]
result = []

for item in original:
    if item not in result:
        result.append(item)

print(f"原列表：{original}")
print(f"去重后：{result}")  # [1, 3, 2, 5, 4]
```

**第4题**
```python
# 1. 交换两个变量
a, b = 10, 20
a, b = b, a
print(f"a={a}, b={b}")  # a=20, b=10

# 2. 交换列表中索引为i和j的元素
def swap_elements(lst, i, j):
    lst[i], lst[j] = lst[j], lst[i]
    return lst

# 测试
numbers = [1, 2, 3, 4, 5]
swap_elements(numbers, 1, 3)
print(numbers)  # [1, 4, 3, 2, 5]
```

**第5题**
```python
phone_book = {}

def add_contact(name, phone):
    phone_book[name] = phone
    print(f"已添加：{name} - {phone}")

def find_contact(name):
    if name in phone_book:
        print(f"{name}的电话：{phone_book[name]}")
    else:
        print(f"未找到联系人：{name}")

def delete_contact(name):
    if name in phone_book:
        del phone_book[name]
        print(f"已删除：{name}")
    else:
        print(f"未找到联系人：{name}")

def show_all():
    if phone_book:
        print("所有联系人：")
        for name, phone in phone_book.items():
            print(f"  {name}: {phone}")
    else:
        print("电话簿为空")

# 测试
add_contact("张三", "13800138000")
add_contact("李四", "13900139000")
show_all()
find_contact("张三")
delete_contact("张三")
show_all()
```

**第6题**
```python
# 1. 检查重复元素
def has_duplicates(lst):
    return len(lst) != len(set(lst))

# 2. 共同字符
def common_chars(str1, str2):
    return set(str1) & set(str2)

# 测试
print(has_duplicates([1, 2, 3, 4, 5]))  # False
print(has_duplicates([1, 2, 3, 2, 5]))  # True
print(common_chars("hello", "world"))   # {'l', 'o'}
```

**第7题**
```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"函数 {func.__name__} 执行时间：{end - start:.4f}秒")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
    print("函数执行完毕")

# 测试
slow_function()
```

**第8题**
```python
# mymath.py 模块内容：
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def multiply(a, b):
    return a * b

def divide(a, b):
    if b == 0:
        raise ValueError("除数不能为0")
    return a / b

# 主程序 main.py：
import mymath

print(mymath.add(10, 5))       # 15
print(mymath.subtract(10, 5))  # 5
print(mymath.multiply(10, 5))  # 50
print(mymath.divide(10, 5))    # 2.0
```

**第9题**
```python
from datetime import datetime

def log(message):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open("log.txt", "a", encoding="utf-8") as f:
        f.write(f"[{timestamp}] {message}\n")

def read_logs():
    try:
        with open("log.txt", "r", encoding="utf-8") as f:
            return f.read()
    except FileNotFoundError:
        return "日志文件不存在"

# 测试
log("程序启动")
log("用户登录")
log("执行操作A")
print(read_logs())
```

**第10题**
```python
class Account:
    def __init__(self, account_id, name, balance=0):
        self.account_id = account_id
        self.name = name
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"存入{amount}元，余额：{self.balance}元")
        else:
            print("存款金额必须大于0")

    def withdraw(self, amount):
        if amount > self.balance:
            print("余额不足")
        elif amount <= 0:
            print("取款金额必须大于0")
        else:
            self.balance -= amount
            print(f"取出{amount}元，余额：{self.balance}元")

class SavingsAccount(Account):
    def __init__(self, account_id, name, balance=0, interest_rate=0.03):
        super().__init__(account_id, name, balance)
        self.interest_rate = interest_rate

    def calculate_interest(self):
        interest = self.balance * self.interest_rate
        print(f"利息：{interest:.2f}元")
        return interest

class CheckingAccount(Account):
    def __init__(self, account_id, name, balance=0, overdraft_limit=1000):
        super().__init__(account_id, name, balance)
        self.overdraft_limit = overdraft_limit

    def withdraw(self, amount):
        if amount > self.balance + self.overdraft_limit:
            print(f"超出透支额度，最多可取{self.balance + self.overdraft_limit}元")
        elif amount <= 0:
            print("取款金额必须大于0")
        else:
            self.balance -= amount
            print(f"取出{amount}元，余额：{self.balance}元")

# 测试
savings = SavingsAccount("S001", "张三", 10000, 0.05)
savings.deposit(5000)
savings.calculate_interest()

checking = CheckingAccount("C001", "李四", 1000, 2000)
checking.withdraw(2500)  # 可以透支
checking.withdraw(1000)  # 超出透支额度
```

---

**试卷难度分析**：
- 基础题：约50%
- 中等题：约35%
- 较难题：约15%（装饰器、继承与多态等）

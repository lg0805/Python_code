# Python 程序设计模拟试题

**适用对象**：高职一年级
**考试时间**：120分钟
**满分**：100分

---

## 一、选择题（每题2分，共40分）

**1. 下列关于Python条件语句的说法，正确的是（ ）**

A. `if`语句后面必须有`else`分支
B. `elif`可以单独使用，不需要`if`
C. 条件表达式后面必须加冒号`:`
D. `if`语句的条件必须用括号括起来

**2. 以下代码的输出结果是（ ）**
```python
x = 10
if x > 5:
    print("A", end="")
if x > 8:
    print("B", end="")
if x > 12:
    print("C", end="")
```
A. A
B. AB
C. ABC
D. B

**3. 下列`for`循环执行后，变量`s`的值是（ ）**
```python
s = 0
for i in range(1, 5):
    s += i
```
A. 10
B. 15
C. 5
D. 4

**4. 关于`while`循环，下列说法错误的是（ ）**

A. `while`循环可以使用`break`提前退出
B. `while True`会造成无限循环
C. `while`循环必须有明确的循环次数
D. `continue`可以跳过本次循环的剩余代码

**5. 下列关于列表的说法，正确的是（ ）**

A. 列表中的元素必须是相同类型
B. 列表创建后长度不能改变
C. 列表的索引从0开始
D. 列表不能嵌套列表

**6. 执行以下代码后，`lst`的值是（ ）**
```python
lst = [1, 2, 3, 4, 5]
lst.append(6)
lst.pop(0)
```
A. `[1, 2, 3, 4, 5, 6]`
B. `[2, 3, 4, 5, 6]`
C. `[1, 2, 3, 4, 5]`
D. `[2, 3, 4, 5]`

**7. 下列哪个操作会导致错误？（ ）**
```python
t = (1, 2, 3)
```
A. `print(t[0])`
B. `t[0] = 10`
C. `print(len(t))`
D. `print(t[-1])`

**8. 关于元组，下列说法正确的是（ ）**

A. 元组使用方括号`[]`定义
B. 元组是可变的数据类型
C. 元组可以作为字典的键
D. 元组不支持索引操作

**9. 创建一个空字典的正确方式是（ ）**

A. `d = []`
B. `d = {}`
C. `d = ()`
D. `d = set()`

**10. 执行以下代码后，输出结果是（ ）**
```python
d = {"name": "张三", "age": 18}
print(d.get("score", 0))
```
A. `None`
B. `0`
C. 报错
D. `"score"`

**11. 关于集合(set)，下列说法错误的是（ ）**

A. 集合中的元素不能重复
B. 集合是无序的
C. 集合可以使用索引访问元素
D. 集合可以进行交集、并集运算

**12. 执行以下代码后，`s`中有几个元素？（ ）**
```python
s = {1, 2, 2, 3, 3, 3}
```
A. 6
B. 3
C. 1
D. 0

**13. 下列函数定义正确的是（ ）**

A. `def func[a, b]:`
B. `function func(a, b):`
C. `def func(a, b):`
D. `def func(a, b)`

**14. 以下代码的输出结果是（ ）**
```python
def add(a, b=10):
    return a + b

print(add(5))
```
A. 5
B. 10
C. 15
D. 报错

**15. 关于函数的`return`语句，说法正确的是（ ）**

A. 函数必须有`return`语句
B. `return`后面必须有返回值
C. 函数可以有多个`return`语句
D. `return`只能返回一个值

**16. 在Python中，导入模块的正确方式是（ ）**

A. `include math`
B. `import math`
C. `using math`
D. `require math`

**17. 以下代码的作用是（ ）**
```python
from random import randint
```
A. 导入random模块的所有函数
B. 只导入random模块的randint函数
C. 重命名random模块
D. 删除random模块

**18. 打开文件进行读取操作，正确的模式参数是（ ）**

A. `"w"`
B. `"r"`
C. `"a"`
D. `"x"`

**19. 关于文件操作，下列说法正确的是（ ）**

A. 使用`with`语句打开文件不需要手动关闭
B. `"w"`模式会在文件末尾追加内容
C. 读取文件前不需要打开文件
D. 文件操作不会抛出异常

**20. 关于面向对象编程，下列说法错误的是（ ）**

A. 类使用`class`关键字定义
B. `__init__`是构造方法
C. `self`代表类的实例对象
D. 一个类只能创建一个对象

---

## 二、判断题（每题2分，共20分）

**1. 在Python中，`if`、`elif`、`else`的代码块必须使用缩进表示。（ ）**

**2. `range(5)`生成的序列是`[1, 2, 3, 4, 5]`。（ ）**

**3. 列表的`remove()`方法删除指定位置的元素。（ ）**

**4. 元组一旦创建，其中的元素就不能修改。（ ）**

**5. 字典中的键必须是唯一的，但值可以重复。（ ）**

**6. 集合可以包含列表作为其元素。（ ）**

**7. 函数的参数可以设置默认值。（ ）**

**8. `import math as m`语句将math模块重命名为m。（ ）**

**9. 使用`"a"`模式打开文件会清空原有内容。（ ）**

**10. 在类中，所有方法的第一个参数都必须是`self`。（ ）**

---

## 三、操作题（每题4分，共40分）

### 第1题（条件语句）

编写程序，输入一个学生的成绩（0-100），根据以下规则输出等级：
- 90分及以上：优秀
- 80-89分：良好
- 70-79分：中等
- 60-69分：及格
- 60分以下：不及格

```python
# 请在下面编写代码
score = int(input("请输入成绩："))




```

---

### 第2题（循环）

使用`for`循环计算1到100之间所有偶数的和，并输出结果。

```python
# 请在下面编写代码




```

---

### 第3题（列表）

已知列表`numbers = [3, 1, 4, 1, 5, 9, 2, 6]`，完成以下操作：
1. 在列表末尾添加元素`8`
2. 删除第一个值为`1`的元素
3. 对列表进行升序排序
4. 输出排序后的列表

```python
# 请在下面编写代码
numbers = [3, 1, 4, 1, 5, 9, 2, 6]




```

---

### 第4题（元组）

创建一个元组存储学生信息（学号、姓名、年龄），然后：
1. 分别输出学号、姓名、年龄
2. 使用元组解包的方式将三个值分别赋给三个变量

```python
# 请在下面编写代码




```

---

### 第5题（字典）

创建一个字典存储3本书的信息（书名为键，价格为值），完成以下操作：
1. 添加一本新书
2. 修改某本书的价格
3. 删除一本书
4. 遍历字典，输出所有书名和价格

```python
# 请在下面编写代码




```

---

### 第6题（集合）

已知两个集合：
```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}
```
完成以下操作并输出结果：
1. 求两个集合的并集
2. 求两个集合的交集
3. 求set1与set2的差集

```python
# 请在下面编写代码
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}




```

---

### 第7题（函数）

编写一个函数`is_prime(n)`，判断参数n是否为素数（质数）。
- 如果是素数，返回`True`
- 如果不是素数，返回`False`

然后调用该函数，输出100以内的所有素数。

```python
# 请在下面编写代码
def is_prime(n):
    # 补充代码
    pass




```

---

### 第8题（模块）

使用`random`模块完成以下任务：
1. 生成一个1到100之间的随机整数
2. 从列表`["苹果", "香蕉", "橙子", "葡萄"]`中随机选择一个元素
3. 生成一个包含5个1-10之间随机整数的列表

```python
# 请在下面编写代码




```

---

### 第9题（文件操作）

完成以下文件操作：
1. 创建一个名为`students.txt`的文件
2. 向文件中写入3个学生的姓名（每行一个）
3. 读取文件内容并输出
4. 使用`with`语句确保文件正确关闭

```python
# 请在下面编写代码




```

---

### 第10题（面向对象）

定义一个`Student`类，要求：
1. 包含属性：学号(sid)、姓名(name)、成绩(score)
2. 包含构造方法`__init__`，用于初始化属性
3. 包含方法`show_info()`，用于输出学生信息
4. 包含方法`is_pass()`，判断成绩是否及格（>=60分）

创建两个学生对象并测试所有方法。

```python
# 请在下面编写代码
class Student:
    # 补充代码
    pass




```

---

## 参考答案

### 一、选择题答案

| 题号 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 答案 | C | B | A | C | C | B | B | C | B | B |

| 题号 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 答案 | C | B | C | C | C | B | B | B | A | D |

### 二、判断题答案

| 题号 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 答案 | √ | × | × | √ | √ | × | √ | √ | × | × |

**判断题解析**：
- 第2题：`range(5)`生成的是`[0, 1, 2, 3, 4]`
- 第3题：`remove()`删除指定值的元素，`pop()`删除指定位置的元素
- 第6题：集合元素必须是可哈希的，列表不可哈希
- 第9题：`"a"`模式是追加模式，`"w"`模式才会清空原有内容
- 第10题：静态方法(@staticmethod)和类方法(@classmethod)不需要self

### 三、操作题参考答案

**第1题**
```python
score = int(input("请输入成绩："))
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

**第2题**
```python
total = 0
for i in range(1, 101):
    if i % 2 == 0:
        total += i
print(f"1到100之间所有偶数的和为：{total}")
# 或者更简洁的写法
total = sum(range(2, 101, 2))
print(total)
```

**第3题**
```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
numbers.append(8)
numbers.remove(1)
numbers.sort()
print(numbers)  # [1, 2, 3, 4, 5, 6, 8, 9]
```

**第4题**
```python
student = ("2024001", "张三", 18)
print(f"学号：{student[0]}")
print(f"姓名：{student[1]}")
print(f"年龄：{student[2]}")

sid, name, age = student
print(sid, name, age)
```

**第5题**
```python
books = {"Python入门": 59.9, "Java编程": 69.9, "C语言基础": 49.9}
books["数据结构"] = 79.9  # 添加
books["Python入门"] = 55.0  # 修改
del books["C语言基础"]  # 删除
for name, price in books.items():
    print(f"{name}: {price}元")
```

**第6题**
```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}
print("并集:", set1 | set2)  # 或 set1.union(set2)
print("交集:", set1 & set2)  # 或 set1.intersection(set2)
print("差集:", set1 - set2)  # 或 set1.difference(set2)
```

**第7题**
```python
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

print("100以内的素数：")
for num in range(2, 101):
    if is_prime(num):
        print(num, end=" ")
```

**第8题**
```python
import random

# 1. 生成1-100随机整数
num = random.randint(1, 100)
print(f"随机整数：{num}")

# 2. 随机选择元素
fruits = ["苹果", "香蕉", "橙子", "葡萄"]
chosen = random.choice(fruits)
print(f"随机选择：{chosen}")

# 3. 生成随机列表
random_list = [random.randint(1, 10) for _ in range(5)]
print(f"随机列表：{random_list}")
```

**第9题**
```python
# 写入文件
with open("students.txt", "w", encoding="utf-8") as f:
    f.write("张三\n")
    f.write("李四\n")
    f.write("王五\n")

# 读取文件
with open("students.txt", "r", encoding="utf-8") as f:
    content = f.read()
    print(content)
```

**第10题**
```python
class Student:
    def __init__(self, sid, name, score):
        self.sid = sid
        self.name = name
        self.score = score

    def show_info(self):
        print(f"学号：{self.sid}，姓名：{self.name}，成绩：{self.score}")

    def is_pass(self):
        return self.score >= 60

# 测试
stu1 = Student("2024001", "张三", 85)
stu2 = Student("2024002", "李四", 55)

stu1.show_info()
print(f"是否及格：{stu1.is_pass()}")

stu2.show_info()
print(f"是否及格：{stu2.is_pass()}")
```

---

**试卷难度分析**：
- 基础题：约60%（覆盖基本语法和常用操作）
- 中等题：约30%（需要综合运用知识点）
- 较难题：约10%（涉及算法思维和综合应用）

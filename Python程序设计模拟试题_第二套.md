# Python 程序设计模拟试题（第二套）

**适用对象**：高职一年级
**考试时间**：120分钟
**满分**：100分

---

## 一、选择题（每题2分，共40分）

**1. 以下代码的输出结果是（ ）**
```python
x = 7
if x > 10:
    print("大")
elif x > 5:
    print("中")
else:
    print("小")
```
A. 大
B. 中
C. 小
D. 无输出

**2. Python中多条件判断使用的关键字是（ ）**

A. `else if`
B. `elseif`
C. `elif`
D. `elsif`

**3. 以下代码执行后，`count`的值是（ ）**
```python
count = 0
for i in range(1, 10, 2):
    count += 1
```
A. 10
B. 5
C. 4
D. 9

**4. `break`语句的作用是（ ）**

A. 跳过本次循环
B. 结束整个循环
C. 结束程序
D. 暂停循环

**5. 以下哪个不是列表的方法？（ ）**

A. `append()`
B. `insert()`
C. `add()`
D. `pop()`

**6. 执行以下代码后，输出结果是（ ）**
```python
lst = [1, 2, 3, 4, 5]
print(lst[1:4])
```
A. `[1, 2, 3, 4]`
B. `[2, 3, 4]`
C. `[2, 3, 4, 5]`
D. `[1, 2, 3]`

**7. 创建只有一个元素的元组，正确的写法是（ ）**

A. `t = (1)`
B. `t = (1,)`
C. `t = [1]`
D. `t = {1}`

**8. 以下代码的输出结果是（ ）**
```python
t = (1, 2, 3, 4, 5)
print(t[::2])
```
A. `(1, 2)`
B. `(2, 4)`
C. `(1, 3, 5)`
D. `(1, 2, 3)`

**9. 字典中访问不存在的键，以下哪种方式不会报错？（ ）**

A. `d["key"]`
B. `d.get("key")`
C. `d.key`
D. `d[key]`

**10. 以下代码的输出结果是（ ）**
```python
d = {"a": 1, "b": 2, "c": 3}
print(list(d.keys()))
```
A. `[1, 2, 3]`
B. `["a", "b", "c"]`
C. `[("a", 1), ("b", 2), ("c", 3)]`
D. `{"a", "b", "c"}`

**11. 以下哪个可以作为集合的元素？（ ）**

A. `[1, 2, 3]`
B. `{"a": 1}`
C. `(1, 2, 3)`
D. `{1, 2, 3}`

**12. 执行以下代码后，结果是（ ）**
```python
s = {1, 2, 3}
s.add(2)
s.add(4)
print(len(s))
```
A. 3
B. 4
C. 5
D. 6

**13. 以下函数调用正确的是（ ）**
```python
def greet(name, msg="你好"):
    print(f"{msg}, {name}")
```
A. `greet()`
B. `greet("张三", "早上好")`
C. `greet(msg="早上好")`
D. `greet(name)`

**14. 以下代码的输出结果是（ ）**
```python
def func(lst):
    lst.append(4)

my_list = [1, 2, 3]
func(my_list)
print(my_list)
```
A. `[1, 2, 3]`
B. `[1, 2, 3, 4]`
C. `[4]`
D. `None`

**15. 关于全局变量和局部变量，说法正确的是（ ）**

A. 函数内部可以直接修改全局变量
B. 局部变量在函数外部可以访问
C. 使用`global`关键字可以在函数内修改全局变量
D. 全局变量和局部变量不能同名

**16. 以下代码的作用是（ ）**
```python
import os
```
A. 导入os模块的部分函数
B. 导入整个os模块
C. 创建os对象
D. 删除os模块

**17. 获取当前时间需要导入的模块是（ ）**

A. `time` 或 `datetime`
B. `date`
C. `clock`
D. `calendar`

**18. 以下哪个模式可以同时读写文件？（ ）**

A. `"r"`
B. `"w"`
C. `"r+"`
D. `"a"`

**19. 读取文件所有行并返回列表的方法是（ ）**

A. `read()`
B. `readline()`
C. `readlines()`
D. `readall()`

**20. 在类中，`__init__`方法的作用是（ ）**

A. 销毁对象
B. 初始化对象属性
C. 定义类方法
D. 继承父类

---

## 二、判断题（每题2分，共20分）

**1. `if`语句的条件表达式可以是任何能转换为布尔值的表达式。（ ）**

**2. `for i in range(10, 0, -1)`可以实现从10到1的倒序遍历。（ ）**

**3. 列表的`sort()`方法会返回一个新的排序后的列表。（ ）**

**4. 空元组可以用`()`表示。（ ）**

**5. 字典是有序的数据结构（Python 3.7+）。（ ）**

**6. 两个集合可以使用`+`运算符求并集。（ ）**

**7. Python函数可以返回多个值。（ ）**

**8. 使用`from math import *`可以导入math模块的所有内容。（ ）**

**9. 文件操作完成后必须调用`close()`方法关闭文件。（ ）**

**10. 类的属性必须在`__init__`方法中定义。（ ）**

---

## 三、操作题（每题4分，共40分）

### 第1题（条件语句）

编写程序，输入年份，判断该年是否为闰年。
闰年条件：能被4整除但不能被100整除，或者能被400整除。

```python
# 请在下面编写代码
year = int(input("请输入年份："))




```

---

### 第2题（循环）

使用`while`循环实现：输入若干个整数，直到输入0时停止，计算并输出这些数的平均值（不包括0）。

```python
# 请在下面编写代码




```

---

### 第3题（列表）

编写程序，生成一个包含10个随机整数（1-100）的列表，然后：
1. 找出最大值和最小值
2. 计算平均值
3. 统计大于平均值的元素个数

```python
# 请在下面编写代码
import random




```

---

### 第4题（元组）

创建一个存储RGB颜色值的元组列表，包含至少3种颜色，如红色(255,0,0)。
遍历列表，以友好的格式输出每种颜色的RGB值。

```python
# 请在下面编写代码




```

---

### 第5题（字典）

统计字符串中每个字符出现的次数，使用字典存储结果。
测试字符串：`"hello world"`

```python
# 请在下面编写代码
text = "hello world"




```

---

### 第6题（集合）

编写程序，找出两个列表中的共同元素和各自独有的元素。
```python
list1 = [1, 2, 3, 4, 5, 6]
list2 = [4, 5, 6, 7, 8, 9]
```

```python
# 请在下面编写代码
list1 = [1, 2, 3, 4, 5, 6]
list2 = [4, 5, 6, 7, 8, 9]




```

---

### 第7题（函数）

编写一个函数`factorial(n)`，使用递归计算n的阶乘。
然后编写函数`combination(n, r)`，计算组合数C(n,r) = n! / (r! × (n-r)!)

```python
# 请在下面编写代码
def factorial(n):
    pass

def combination(n, r):
    pass

# 测试：计算C(5,2)



```

---

### 第8题（模块）

使用`math`模块完成以下任务：
1. 计算圆周率π的值（保留小数点后5位）
2. 计算16的平方根
3. 计算2的10次方
4. 计算sin(90°)的值（注意角度转换）

```python
# 请在下面编写代码
import math




```

---

### 第9题（文件操作）

编写程序实现简单的学生成绩管理：
1. 将以下学生成绩写入文件`scores.txt`（格式：姓名,成绩）
   - 张三,85
   - 李四,92
   - 王五,78
2. 从文件读取数据，计算并输出平均分

```python
# 请在下面编写代码




```

---

### 第10题（面向对象）

定义一个`Rectangle`（矩形）类：
1. 属性：长(length)、宽(width)
2. 方法：计算面积`area()`、计算周长`perimeter()`
3. 特殊方法：`__str__`返回矩形信息的字符串表示

创建对象并测试所有功能。

```python
# 请在下面编写代码
class Rectangle:
    pass




```

---

## 参考答案

### 一、选择题答案

| 题号 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 答案 | B | C | B | B | C | B | B | C | B | B |

| 题号 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 答案 | C | B | B | B | C | B | A | C | C | B |

### 二、判断题答案

| 题号 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 答案 | √ | √ | × | √ | √ | × | √ | √ | × | × |

**判断题解析**：
- 第3题：`sort()`方法原地排序，不返回新列表；`sorted()`函数返回新列表
- 第6题：集合使用`|`或`union()`求并集，不支持`+`运算符
- 第9题：使用`with`语句可以自动关闭文件，不必须手动调用`close()`
- 第10题：类属性可以在类体中直接定义，实例属性通常在`__init__`中定义

### 三、操作题参考答案

**第1题**
```python
year = int(input("请输入年份："))
if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    print(f"{year}年是闰年")
else:
    print(f"{year}年不是闰年")
```

**第2题**
```python
total = 0
count = 0
while True:
    num = int(input("请输入整数（0结束）："))
    if num == 0:
        break
    total += num
    count += 1

if count > 0:
    avg = total / count
    print(f"平均值为：{avg:.2f}")
else:
    print("没有输入有效数字")
```

**第3题**
```python
import random

numbers = [random.randint(1, 100) for _ in range(10)]
print(f"列表：{numbers}")

max_val = max(numbers)
min_val = min(numbers)
avg_val = sum(numbers) / len(numbers)

print(f"最大值：{max_val}")
print(f"最小值：{min_val}")
print(f"平均值：{avg_val:.2f}")

count = len([x for x in numbers if x > avg_val])
print(f"大于平均值的元素个数：{count}")
```

**第4题**
```python
colors = [
    ("红色", (255, 0, 0)),
    ("绿色", (0, 255, 0)),
    ("蓝色", (0, 0, 255)),
    ("黄色", (255, 255, 0))
]

for name, (r, g, b) in colors:
    print(f"{name}: R={r}, G={g}, B={b}")
```

**第5题**
```python
text = "hello world"
char_count = {}

for char in text:
    if char in char_count:
        char_count[char] += 1
    else:
        char_count[char] = 1

# 或使用get方法
# for char in text:
#     char_count[char] = char_count.get(char, 0) + 1

for char, count in char_count.items():
    print(f"'{char}': {count}次")
```

**第6题**
```python
list1 = [1, 2, 3, 4, 5, 6]
list2 = [4, 5, 6, 7, 8, 9]

set1 = set(list1)
set2 = set(list2)

common = set1 & set2
only_in_1 = set1 - set2
only_in_2 = set2 - set1

print(f"共同元素：{common}")
print(f"list1独有：{only_in_1}")
print(f"list2独有：{only_in_2}")
```

**第7题**
```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

def combination(n, r):
    return factorial(n) // (factorial(r) * factorial(n - r))

# 测试
print(f"5! = {factorial(5)}")
print(f"C(5,2) = {combination(5, 2)}")  # 结果为10
```

**第8题**
```python
import math

# 1. 圆周率
print(f"π = {math.pi:.5f}")

# 2. 平方根
print(f"√16 = {math.sqrt(16)}")

# 3. 幂运算
print(f"2^10 = {math.pow(2, 10)}")

# 4. sin(90°)
angle_rad = math.radians(90)  # 角度转弧度
print(f"sin(90°) = {math.sin(angle_rad)}")
```

**第9题**
```python
# 写入文件
students = [("张三", 85), ("李四", 92), ("王五", 78)]

with open("scores.txt", "w", encoding="utf-8") as f:
    for name, score in students:
        f.write(f"{name},{score}\n")

# 读取并计算平均分
with open("scores.txt", "r", encoding="utf-8") as f:
    total = 0
    count = 0
    for line in f:
        name, score = line.strip().split(",")
        total += int(score)
        count += 1

avg = total / count
print(f"平均分：{avg:.2f}")
```

**第10题**
```python
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

    def perimeter(self):
        return 2 * (self.length + self.width)

    def __str__(self):
        return f"矩形(长={self.length}, 宽={self.width})"

# 测试
rect = Rectangle(10, 5)
print(rect)
print(f"面积：{rect.area()}")
print(f"周长：{rect.perimeter()}")
```

---

**试卷难度分析**：
- 基础题：约55%
- 中等题：约35%
- 较难题：约10%

# Python程序设计期末试卷

**考试时间：120分钟　　满分：100分**

---

## 一、选择题（每题2分，共40分）

1. Python语言属于（　）
   - A. 机器语言
   - B. 汇编语言
   - C. 高级语言
   - D. 低级语言

2. 下列哪个是Python中合法的变量名？（　）
   - A. 2name
   - B. my-name
   - C. my_name
   - D. class

3. 表达式 `17 // 5` 的结果是（　）
   - A. 3.4
   - B. 3
   - C. 2
   - D. 4

4. 表达式 `17 % 5` 的结果是（　）
   - A. 3.4
   - B. 3
   - C. 2
   - D. 4

5. 下列哪个不是Python的基本数据类型？（　）
   - A. int
   - B. float
   - C. char
   - D. str

6. 已知 `s = "Hello World"`，则 `s[0:5]` 的结果是（　）
   - A. "Hello"
   - B. "Hello "
   - C. "ello"
   - D. "World"

7. 下列关于列表的说法，错误的是（　）
   - A. 列表中的元素可以是不同类型
   - B. 列表是可变的数据类型
   - C. 列表的索引从1开始
   - D. 可以使用append()方法向列表添加元素

8. 已知 `lst = [1, 2, 3, 4, 5]`，执行 `lst.pop(2)` 后，lst的值为（　）
   - A. [1, 2, 4, 5]
   - B. [1, 3, 4, 5]
   - C. [1, 2, 3, 4]
   - D. [2, 3, 4, 5]

9. 下列哪个是创建空字典的正确方式？（　）
   - A. d = []
   - B. d = ()
   - C. d = {}
   - D. d = set()

10. 表达式 `not True or False and True` 的结果是（　）
    - A. True
    - B. False
    - C. None
    - D. 报错

11. 下列关于元组的说法，正确的是（　）
    - A. 元组是可变的
    - B. 元组用方括号表示
    - C. 元组一旦创建就不能修改
    - D. 元组不能包含列表

12. 以下代码的输出结果是（　）
    ```python
    for i in range(1, 5):
        print(i, end=" ")
    ```
    - A. 1 2 3 4 5
    - B. 1 2 3 4
    - C. 0 1 2 3 4
    - D. 0 1 2 3

13. 下列哪个函数可以获取字符串的长度？（　）
    - A. size()
    - B. length()
    - C. len()
    - D. count()

14. 已知 `s = "python"`，则 `s.upper()` 的结果是（　）
    - A. "Python"
    - B. "PYTHON"
    - C. "python"
    - D. 报错

15. 下列关于函数定义的说法，错误的是（　）
    - A. 使用def关键字定义函数
    - B. 函数必须有返回值
    - C. 函数可以有多个参数
    - D. 函数体需要缩进

16. 以下代码的输出结果是（　）
    ```python
    def func(a, b=10):
        return a + b
    print(func(5))
    ```
    - A. 5
    - B. 10
    - C. 15
    - D. 报错

17. 下列哪个是Python中用于捕获异常的关键字？（　）
    - A. catch
    - B. except
    - C. error
    - D. throw

18. 以下代码的输出结果是（　）
    ```python
    lst = [1, 2, 3]
    lst2 = lst
    lst2.append(4)
    print(lst)
    ```
    - A. [1, 2, 3]
    - B. [1, 2, 3, 4]
    - C. [4, 1, 2, 3]
    - D. 报错

19. 打开文件时，模式 `'a'` 表示（　）
    - A. 只读模式
    - B. 写入模式（覆盖）
    - C. 追加模式
    - D. 二进制模式

20. 下列关于列表推导式的写法，正确的是（　）
    - A. `[x*2 for x in range(5)]`
    - B. `[for x in range(5): x*2]`
    - C. `{x*2 for x in range(5)}`
    - D. `(x*2 for x in range(5))`

---

## 二、填空题（每题2分，共20分）

1. Python中单行注释使用 ________ 符号，多行注释可以使用 ________ 或 ________ 。

2. 表达式 `2 ** 3` 的结果是 ________ 。

3. 已知 `s = "Hello"`，则 `s[-1]` 的值是 ________ 。

4. 将字符串 `"123"` 转换为整数的函数是 ________ 。

5. 已知 `lst = [3, 1, 4, 1, 5]`，执行 `lst.sort()` 后，lst的值是 ________ 。

6. 在Python中，使用 ________ 关键字定义函数，使用 ________ 关键字返回函数值。

7. 表达式 `"abc" * 2` 的结果是 ________ 。

8. 已知 `d = {"name": "Tom", "age": 20}`，获取键 `"name"` 对应值的表达式是 ________ 。

9. 用于跳出整个循环的语句是 ________ ，用于跳过本次循环的语句是 ________ 。

10. 在Python中，读取文件的常用函数有 `read()`、________ 和 ________ 。

---

## 三、判断题（每题1分，共10分）

1. Python是一种解释型语言。（　）

2. 在Python中，变量使用前必须先声明类型。（　）

3. 列表和元组都是有序的序列类型。（　）

4. 字典中的键可以重复。（　）

5. `range(5)` 生成的序列包含5个元素。（　）

6. Python中的缩进只是为了美观，不影响程序执行。（　）

7. 字符串是不可变的数据类型。（　）

8. `==` 和 `is` 在Python中的作用完全相同。（　）

9. 函数的形参和实参的名称必须相同。（　）

10. 使用 `with` 语句打开文件可以自动关闭文件。（　）

---

## 四、程序设计题（共30分）

### 第1题（6分）
编写程序，输入一个正整数n，计算并输出1+2+3+...+n的和。

**要求：** 使用for循环实现

```python
# 请在下方编写代码




```

---

### 第2题（7分）
编写程序，输入一个字符串，统计其中大写字母、小写字母和数字的个数。

**示例输入：** `"Hello123World"`
**示例输出：** `大写字母：2个，小写字母：8个，数字：3个`

```python
# 请在下方编写代码




```

---

### 第3题（8分）
编写一个函数 `is_prime(n)`，判断一个正整数n是否为素数。如果是素数返回True，否则返回False。然后调用该函数，输出100以内的所有素数。

**提示：** 素数是只能被1和自身整除的大于1的正整数。

```python
# 请在下方编写代码




```

---

### 第4题（9分）
编写程序，实现学生成绩管理功能：
1. 使用字典存储5名学生的姓名和成绩
2. 计算并输出平均成绩
3. 找出成绩最高的学生姓名和成绩
4. 统计不及格（成绩<60）的学生人数

```python
# 请在下方编写代码




```

---

## 参考答案

### 一、选择题答案
1. C　2. C　3. B　4. C　5. C　6. A　7. C　8. A　9. C　10. B
11. C　12. B　13. C　14. B　15. B　16. C　17. B　18. B　19. C　20. A

### 二、填空题答案
1. `#`；`'''`；`"""`
2. `8`
3. `o`
4. `int()`
5. `[1, 1, 3, 4, 5]`
6. `def`；`return`
7. `"abcabc"`
8. `d["name"]` 或 `d.get("name")`
9. `break`；`continue`
10. `readline()`；`readlines()`

### 三、判断题答案
1. √　2. ×　3. √　4. ×　5. √　6. ×　7. √　8. ×　9. ×　10. √

### 四、程序设计题参考答案

**第1题：**
```python
n = int(input("请输入一个正整数："))
total = 0
for i in range(1, n + 1):
    total += i
print(f"1到{n}的和为：{total}")
```

**第2题：**
```python
s = input("请输入一个字符串：")
upper_count = 0
lower_count = 0
digit_count = 0

for char in s:
    if char.isupper():
        upper_count += 1
    elif char.islower():
        lower_count += 1
    elif char.isdigit():
        digit_count += 1

print(f"大写字母：{upper_count}个，小写字母：{lower_count}个，数字：{digit_count}个")
```

**第3题：**
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

**第4题：**
```python
# 创建学生成绩字典
students = {
    "张三": 85,
    "李四": 72,
    "王五": 58,
    "赵六": 90,
    "钱七": 45
}

# 计算平均成绩
average = sum(students.values()) / len(students)
print(f"平均成绩：{average:.2f}")

# 找出最高成绩的学生
max_student = max(students, key=students.get)
print(f"最高成绩：{max_student}，{students[max_student]}分")

# 统计不及格人数
fail_count = sum(1 for score in students.values() if score < 60)
print(f"不及格人数：{fail_count}人")
```

---

**试卷结束**

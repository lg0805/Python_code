# Python程序设计期末试卷

**考试时间：120分钟**  
**总分：100分**  
**班级：** ______________  **姓名：** ______________  **学号：** ______________

---

## 一、单项选择题（每题1分，共20分）

**请将正确答案的字母填入题前括号内**

（ ）1. Python语言是一种什么类型的编程语言？
A. 编译型语言
B. 解释型语言  
C. 汇编语言
D. 机器语言

（ ）2. 下列哪个不是Python的关键字？
A. if
B. while
C. function
D. def

（ ）3. 在Python中，以下哪个变量的命名是合法的？
A. 2name
B. name-1
C. _name
D. class

（ ）4. 表达式 `3 * 2 ** 3` 的结果是：
A. 24
B. 18
C. 216
D. 64

（ ）5. 下列哪个语句可以正确创建一个空列表？
A. list = ()
B. list = []
C. list = {}
D. list = ""

（ ）6. 字符串 `s = "Python"`，执行 `s[1:4]` 的结果是：
A. "yth"
B. "Pyt"
C. "ytho"
D. "ython"

（ ）7. 以下哪个方法可以删除列表中的最后一个元素？
A. pop()
B. remove()
C. delete()
D. clear()

（ ）8. 字典的键（key）必须是：
A. 可变的
B. 不可变的
C. 数字类型
D. 字符串类型

（ ）9. 执行 `print(type(3.14))` 的输出结果是：
A. <class 'int'>
B. <class 'float'>
C. <class 'str'>
D. <class 'complex'>

（ ）10. 以下哪个循环会无限执行？
A. `for i in range(10):`
B. `while True:`
C. `for i in [1,2,3]:`
D. `while i < 10:`

（ ）11. 函数定义的关键字是：
A. function
B. def
C. define
D. func

（ ）12. 以下哪个模块用于处理日期和时间？
A. math
B. random
C. datetime
D. os

（ ）13. 打开文件进行读取操作，应该使用哪个模式？
A. 'w'
B. 'r'
C. 'a'
D. 'x'

（ ）14. 异常处理中，`try...except` 语句的作用是：
A. 预防错误发生
B. 捕获并处理异常
C. 忽略所有错误
D. 终止程序执行

（ ）15. 以下哪个不是Python的数据类型？
A. list
B. tuple
C. array
D. dict

（ ）16. 表达式 `"hello" + "world"` 的结果是：
A. "hello world"
B. "helloworld"
C. 报错
D. "hello"+"world"

（ ）17. 以下哪个运算符的优先级最高？
A. +
B. *
C. **
D. //

（ ）18. 列表推导式 `[x**2 for x in range(5)]` 的结果是：
A. [0, 1, 4, 9, 16]
B. [1, 4, 9, 16, 25]
C. [0, 1, 2, 3, 4]
D. [1, 2, 3, 4, 5]

（ ）19. 函数 `len()` 可以用于：
A. 字符串
B. 列表
C. 元组
D. 以上都可以

（ ）20. 以下哪个语句可以导入math模块中的所有函数？
A. `import math`
B. `from math import *`
C. `import math as m`
D. `from math import sqrt`

---

## 二、填空题（每空1分，共10分）

1. Python中使用 `__________` 符号表示单行注释。
2. 布尔类型的两个值是 `__________` 和 `__________`。
3. 列表、元组、字符串都支持 `__________` 操作，可以获取元素个数。
4. 在Python中，`and`、`or`、`not` 是 `__________` 运算符。
5. 使用 `__________` 函数可以将字符串转换为整数。
6. 字典使用 `__________` 来存储键值对。
7. 在循环中，`__________` 语句可以跳过当前循环的剩余语句，继续下一次循环。
8. 函数中 `__________` 参数可以有默认值。
9. 使用 `__________` 模块可以生成随机数。
10. 文件操作完成后，应该使用 `__________` 方法关闭文件。

---

## 三、判断题（每题1分，共10分）

**正确的打"√"，错误的打"×"**

（ ）1. Python是区分大小写的编程语言。
（ ）2. 元组（tuple）创建后可以修改其中的元素。
（ ）3. `range(5)` 生成的是 [0, 1, 2, 3, 4] 这个列表。
（ ）4. 在Python中，`=` 是赋值运算符，`==` 是比较运算符。
（ ）5. 列表的索引从0开始，到列表长度减1结束。
（ ）6. 字典中的键必须是唯一的，值可以重复。
（ ）7. `break` 语句可以跳出当前循环，`continue` 语句可以终止整个程序。
（ ）8. 函数可以没有参数，也可以没有返回值。
（ ）9. 使用 `open()` 函数打开文件时，如果文件不存在会报错。
（ ）10. 模块是包含Python定义和语句的文件，文件名就是模块名。

---

## 四、程序设计题（共60分）

### 第1题：基础编程（10分）
**题目：** 编写一个程序，输入一个正整数n，计算并输出1到n之间所有奇数的和。

**要求：**
1. 使用input()函数获取用户输入
2. 使用循环结构
3. 输出格式为："1到n之间所有奇数的和为：X"（其中n和X用实际值替换）

**示例：**
```
请输入一个正整数：10
1到10之间所有奇数的和为：25
```

### 第2题：函数应用（15分）
**题目：** 编写一个函数，判断一个数是否为素数（质数），并编写主程序测试该函数。

**要求：**
1. 定义函数 `is_prime(num)`，接收一个整数参数，返回布尔值
2. 在主程序中，输入一个整数，调用函数判断是否为素数
3. 输出判断结果

**示例：**
```
请输入一个整数：17
17是素数
```

### 第3题：数据处理（15分）
**题目：** 编写程序处理学生成绩数据。

**要求：**
1. 创建一个包含10个学生成绩的列表（成绩范围0-100）
2. 计算并输出：最高分、最低分、平均分
3. 统计并输出：优秀（≥90分）人数、及格（≥60分）人数、不及格人数
4. 将成绩从高到低排序并输出

**示例输出格式：**
```
学生成绩：[85, 92, 78, 65, 95, 88, 72, 60, 45, 100]
最高分：100
最低分：45
平均分：78.0
优秀人数：3
及格人数：8
不及格人数：2
排序后成绩：[100, 95, 92, 88, 85, 78, 72, 65, 60, 45]
```

### 第4题：综合应用（20分）
**题目：** 设计一个简单的学生信息管理系统。

**要求：**
1. 使用字典列表存储学生信息，每个学生包含：学号、姓名、年龄、成绩
2. 实现以下功能菜单：
   ```
   1. 添加学生信息
   2. 删除学生信息
   3. 修改学生信息
   4. 查询学生信息
   5. 显示所有学生信息
   6. 退出系统
   ```
3. 每个功能实现相应的操作
4. 使用循环使程序可以重复选择功能，直到选择退出

**功能说明：**
- 添加：输入学生信息并添加到列表
- 删除：根据学号删除学生信息
- 修改：根据学号修改学生信息
- 查询：根据学号或姓名查询学生信息
- 显示：以表格形式显示所有学生信息

---

## 参考答案（教师用）

### 一、单项选择题
1. B 2. C 3. C 4. A 5. B 6. A 7. A 8. B 9. B 10. B
11. B 12. C 13. B 14. B 15. C 16. B 17. C 18. A 19. D 20. B

### 二、填空题
1. #
2. True, False
3. len()
4. 逻辑
5. int()
6. 大括号{} 或 花括号
7. continue
8. 默认
9. random
10. close()

### 三、判断题
1. √ 2. × 3. × 4. √ 5. √ 6. √ 7. × 8. √ 9. √ 10. √

### 四、程序设计题（参考代码）

**第1题参考代码：**
```python
n = int(input("请输入一个正整数："))
sum_odd = 0
for i in range(1, n+1):
    if i % 2 == 1:
        sum_odd += i
print(f"1到{n}之间所有奇数的和为：{sum_odd}")
```

**第2题参考代码：**
```python
def is_prime(num):
    if num <= 1:
        return False
    for i in range(2, int(num**0.5) + 1):
        if num % i == 0:
            return False
    return True

num = int(input("请输入一个整数："))
if is_prime(num):
    print(f"{num}是素数")
else:
    print(f"{num}不是素数")
```

**第3题参考代码：**
```python
scores = [85, 92, 78, 65, 95, 88, 72, 60, 45, 100]

print(f"学生成绩：{scores}")
print(f"最高分：{max(scores)}")
print(f"最低分：{min(scores)}")
print(f"平均分：{sum(scores)/len(scores)}")

excellent = len([s for s in scores if s >= 90])
passing = len([s for s in scores if s >= 60])
failing = len([s for s in scores if s < 60])

print(f"优秀人数：{excellent}")
print(f"及格人数：{passing}")
print(f"不及格人数：{failing}")

sorted_scores = sorted(scores, reverse=True)
print(f"排序后成绩：{sorted_scores}")
```

**第4题参考代码：**
```python
students = []

def add_student():
    sid = input("请输入学号：")
    name = input("请输入姓名：")
    age = input("请输入年龄：")
    score = input("请输入成绩：")
    student = {"学号": sid, "姓名": name, "年龄": age, "成绩": score}
    students.append(student)
    print("添加成功！")

def delete_student():
    sid = input("请输入要删除的学生学号：")
    for student in students:
        if student["学号"] == sid:
            students.remove(student)
            print("删除成功！")
            return
    print("未找到该学生！")

def modify_student():
    sid = input("请输入要修改的学生学号：")
    for student in students:
        if student["学号"] == sid:
            student["姓名"] = input(f"请输入新姓名（原：{student['姓名']}）：")
            student["年龄"] = input(f"请输入新年龄（原：{student['年龄']}）：")
            student["成绩"] = input(f"请输入新成绩（原：{student['成绩']}）：")
            print("修改成功！")
            return
    print("未找到该学生！")

def search_student():
    keyword = input("请输入学号或姓名进行查询：")
    results = []
    for student in students:
        if student["学号"] == keyword or student["姓名"] == keyword:
            results.append(student)
    
    if results:
        print("查询结果：")
        for student in results:
            print(f"学号：{student['学号']}, 姓名：{student['姓名']}, 年龄：{student['年龄']}, 成绩：{student['成绩']}")
    else:
        print("未找到相关学生！")

def display_all():
    if not students:
        print("暂无学生信息！")
        return
    
    print("="*40)
    print("学号\t姓名\t年龄\t成绩")
    print("-"*40)
    for student in students:
        print(f"{student['学号']}\t{student['姓名']}\t{student['年龄']}\t{student['成绩']}")
    print("="*40)

def main():
    while True:
        print("\n学生信息管理系统")
        print("1. 添加学生信息")
        print("2. 删除学生信息")
        print("3. 修改学生信息")
        print("4. 查询学生信息")
        print("5. 显示所有学生信息")
        print("6. 退出系统")
        
        choice = input("请选择功能（1-6）：")
        
        if choice == "1":
            add_student()
        elif choice == "2":
            delete_student()
        elif choice == "3":
            modify_student()
        elif choice == "4":
            search_student()
        elif choice == "5":
            display_all()
        elif choice == "6":
            print("感谢使用，再见！")
            break
        else:
            print("输入错误，请重新选择！")

if __name__ == "__main__":
    main()
```

---

**试卷说明：**
1. 本试卷涵盖Python基础语法、数据类型、控制结构、函数、模块、文件操作等核心知识点
2. 题目难度由易到难，适合高职学生水平
3. 程序设计题注重实际应用能力培养
4. 参考答案提供了完整的代码实现，方便教师批改

**评分标准建议：**
- 选择题、填空题、判断题：按标准答案评分
- 程序设计题：根据代码正确性、完整性、规范性综合评分
- 第4题可根据功能实现程度给予部分分数
# Python Schedule 模块使用教程

## 目录
1. [简介](#简介)
2. [安装](#安装)
3. [基础用法](#基础用法)
4. [高级功能](#高级功能)
5. [实战示例](#实战示例)
6. [与其他库集成](#与其他库集成)
7. [最佳实践](#最佳实践)
8. [常见问题](#常见问题)
9. [性能优化](#性能优化)

## 简介

Schedule 是一个轻量级的 Python 任务调度库，它使用简洁的语法让你能够轻松地安排任务在特定时间运行。与 cron 不同，schedule 使用更加人性化的语法，让代码更易读和维护。

### 主要特点
- **简单易用**：类似自然语言的 API 设计
- **轻量级**：无外部依赖，纯 Python 实现
- **灵活**：支持多种时间间隔和时间点
- **可靠**：经过充分测试，稳定性高
- **跨平台**：支持 Windows、Linux、macOS

### 适用场景
- 定时数据备份
- 定期发送报告
- 系统监控和告警
- 自动化任务执行
- 定时数据采集

### 不适用场景
- 需要分布式任务调度
- 需要持久化任务（重启后自动恢复）
- 需要精确到毫秒级的调度
- 需要复杂的任务依赖管理

## 安装

```bash
# 使用 pip 安装
pip install schedule

# 升级到最新版本
pip install --upgrade schedule

# 安装开发版本
pip install git+https://github.com/dbader/schedule.git
```

## 基础用法

### 1. 最简单的例子

```python
import schedule
import time

def job():
    print("我是一个定时任务！")

# 每10秒执行一次
schedule.every(10).seconds.do(job)

# 每10分钟执行一次
schedule.every(10).minutes.do(job)

# 每小时执行一次
schedule.every().hour.do(job)

# 每天的10:30执行
schedule.every().day.at("10:30").do(job)

# 每周一执行
schedule.every().monday.do(job)

# 每周三的13:15执行
schedule.every().wednesday.at("13:15").do(job)

# 保持程序运行
while True:
    schedule.run_pending()
    time.sleep(1)
```

### 2. 传递参数给任务函数

```python
import schedule
import time

def greet(name, greeting="你好"):
    print(f"{greeting}, {name}!")

# 传递位置参数
schedule.every(5).seconds.do(greet, "张三")

# 传递关键字参数
schedule.every(10).seconds.do(greet, name="李四", greeting="早上好")

# 使用 lambda 函数
schedule.every().day.at("09:00").do(lambda: greet("老板", "早安"))

while True:
    schedule.run_pending()
    time.sleep(1)
```

### 3. 所有时间单位

```python
import schedule

def task():
    print("执行任务")

# 秒
schedule.every(5).seconds.do(task)
schedule.every(10).to(30).seconds.do(task)  # 随机10-30秒

# 分钟
schedule.every(15).minutes.do(task)
schedule.every().minute.at(":30").do(task)  # 每分钟的30秒时

# 小时
schedule.every().hour.do(task)
schedule.every(2).hours.do(task)
schedule.every().hour.at(":30").do(task)  # 每小时的30分时

# 天
schedule.every().day.do(task)
schedule.every().day.at("10:30").do(task)
schedule.every().day.at("10:30:45").do(task)  # 支持秒

# 周
schedule.every().week.do(task)
schedule.every().monday.do(task)
schedule.every().tuesday.at("18:00").do(task)
schedule.every().wednesday.do(task)
schedule.every().thursday.do(task)
schedule.every().friday.do(task)
schedule.every().saturday.do(task)
schedule.every().sunday.do(task)
```

### 4. 任务管理

```python
import schedule

def job1():
    print("任务1")
    return schedule.CancelJob  # 执行后取消该任务

def job2():
    print("任务2")

def job3():
    print("任务3")

# 添加任务并获取任务对象
job1_task = schedule.every(5).seconds.do(job1)
job2_task = schedule.every(10).seconds.do(job2)
job3_task = schedule.every(15).seconds.do(job3)

# 获取所有任务
all_jobs = schedule.get_jobs()
print(f"当前有 {len(all_jobs)} 个任务")

# 取消特定任务
schedule.cancel_job(job2_task)

# 清除所有任务
schedule.clear()

# 按标签清除任务
schedule.clear('daily-tasks')
```

### 5. 任务标签

```python
import schedule

def job():
    print("执行任务")

# 添加标签
schedule.every().hour.do(job).tag('hourly', 'stats')
schedule.every().day.do(job).tag('daily', 'backup')
schedule.every().monday.do(job).tag('weekly', 'report')

# 按标签获取任务
daily_jobs = schedule.get_jobs('daily')
print(f"每日任务数量: {len(daily_jobs)}")

# 按标签清除任务
schedule.clear('weekly')
```

## 高级功能

### 1. 随机时间间隔

```python
import schedule
import random

def job():
    print(f"在随机时间执行: {time.strftime('%Y-%m-%d %H:%M:%S')}")

# 每5到10秒之间随机执行
schedule.every(5).to(10).seconds.do(job)

# 每1到3小时之间随机执行
schedule.every(1).to(3).hours.do(job)

# 每天在指定时间范围内随机执行
def job_with_random_delay():
    # 添加随机延迟
    delay = random.randint(0, 120)  # 0-120秒随机延迟
    time.sleep(delay)
    print(f"带随机延迟的任务执行")

schedule.every().day.at("09:00").do(job_with_random_delay)
```

### 2. 任务装饰器

```python
import schedule
import functools
import time

def with_logging(func):
    """记录任务执行的装饰器"""
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f"[{time.strftime('%Y-%m-%d %H:%M:%S')}] 开始执行: {func.__name__}")
        result = func(*args, **kwargs)
        print(f"[{time.strftime('%Y-%m-%d %H:%M:%S')}] 完成执行: {func.__name__}")
        return result
    return wrapper

def catch_exceptions(cancel_on_failure=False):
    """异常处理装饰器"""
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            try:
                return func(*args, **kwargs)
            except Exception as e:
                print(f"任务执行失败: {e}")
                if cancel_on_failure:
                    return schedule.CancelJob
        return wrapper
    return decorator

@with_logging
@catch_exceptions(cancel_on_failure=False)
def critical_task():
    print("执行关键任务")
    # 可能会抛出异常的代码
    if random.random() < 0.1:
        raise Exception("随机错误")

schedule.every(10).seconds.do(critical_task)
```

### 3. 任务链和依赖

```python
import schedule
import time

class TaskChain:
    """任务链管理器"""
    def __init__(self):
        self.completed_tasks = set()

    def task_a(self):
        print("执行任务 A")
        self.completed_tasks.add('A')

    def task_b(self):
        # 任务B依赖任务A
        if 'A' in self.completed_tasks:
            print("执行任务 B (依赖 A)")
            self.completed_tasks.add('B')
        else:
            print("等待任务 A 完成...")

    def task_c(self):
        # 任务C依赖任务A和B
        if {'A', 'B'}.issubset(self.completed_tasks):
            print("执行任务 C (依赖 A 和 B)")
            self.completed_tasks.add('C')
            # 重置以便下次循环
            self.completed_tasks.clear()
        else:
            print("等待任务 A 和 B 完成...")

chain = TaskChain()
schedule.every(5).seconds.do(chain.task_a)
schedule.every(10).seconds.do(chain.task_b)
schedule.every(15).seconds.do(chain.task_c)
```

### 4. 动态任务管理

```python
import schedule
import time
from datetime import datetime, timedelta

class DynamicScheduler:
    """动态任务调度器"""

    def __init__(self):
        self.task_count = 0
        self.max_tasks = 5

    def create_task(self):
        """动态创建新任务"""
        self.task_count += 1
        task_id = self.task_count

        def new_task():
            print(f"执行动态任务 #{task_id}")
            # 任务完成后可能创建新任务
            if self.task_count < self.max_tasks:
                self.add_random_task()

        return new_task

    def add_random_task(self):
        """添加随机时间的任务"""
        task = self.create_task()
        interval = random.randint(5, 20)
        schedule.every(interval).seconds.do(task).tag('dynamic')
        print(f"添加了新任务，间隔 {interval} 秒")

    def cleanup_old_tasks(self):
        """清理旧任务"""
        dynamic_jobs = schedule.get_jobs('dynamic')
        if len(dynamic_jobs) > 10:
            # 保留最新的10个任务
            for job in dynamic_jobs[:-10]:
                schedule.cancel_job(job)
            print(f"清理了 {len(dynamic_jobs) - 10} 个旧任务")

scheduler = DynamicScheduler()
# 初始添加一些任务
for _ in range(3):
    scheduler.add_random_task()

# 定期清理
schedule.every(30).seconds.do(scheduler.cleanup_old_tasks)
```

### 5. 任务执行统计

```python
import schedule
import time
from collections import defaultdict
from datetime import datetime

class TaskMonitor:
    """任务执行监控器"""

    def __init__(self):
        self.stats = defaultdict(lambda: {
            'count': 0,
            'total_time': 0,
            'last_run': None,
            'errors': 0
        })

    def monitor(self, task_name):
        """监控装饰器"""
        def decorator(func):
            def wrapper(*args, **kwargs):
                start_time = time.time()
                try:
                    result = func(*args, **kwargs)
                    self.stats[task_name]['count'] += 1
                    return result
                except Exception as e:
                    self.stats[task_name]['errors'] += 1
                    print(f"任务 {task_name} 执行失败: {e}")
                finally:
                    elapsed = time.time() - start_time
                    self.stats[task_name]['total_time'] += elapsed
                    self.stats[task_name]['last_run'] = datetime.now()
            return wrapper
        return decorator

    def print_stats(self):
        """打印统计信息"""
        print("\n" + "="*50)
        print("任务执行统计")
        print("="*50)
        for task_name, stats in self.stats.items():
            avg_time = stats['total_time'] / stats['count'] if stats['count'] > 0 else 0
            print(f"\n任务: {task_name}")
            print(f"  执行次数: {stats['count']}")
            print(f"  错误次数: {stats['errors']}")
            print(f"  平均耗时: {avg_time:.2f} 秒")
            print(f"  总耗时: {stats['total_time']:.2f} 秒")
            if stats['last_run']:
                print(f"  最后执行: {stats['last_run'].strftime('%Y-%m-%d %H:%M:%S')}")
        print("="*50)

monitor = TaskMonitor()

@monitor.monitor("数据备份")
def backup_data():
    time.sleep(random.uniform(0.5, 2))  # 模拟备份
    print("数据备份完成")

@monitor.monitor("发送报告")
def send_report():
    time.sleep(random.uniform(1, 3))  # 模拟发送
    if random.random() < 0.1:  # 10%概率失败
        raise Exception("网络错误")
    print("报告发送完成")

schedule.every(5).seconds.do(backup_data)
schedule.every(8).seconds.do(send_report)
schedule.every(20).seconds.do(monitor.print_stats)
```

## 实战示例

### 示例1：自动化数据备份系统

```python
"""
自动化数据备份系统
- 定期备份数据库
- 清理旧备份
- 发送备份报告
"""
import schedule
import time
import os
import shutil
from datetime import datetime, timedelta
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

class BackupSystem:
    def __init__(self, source_dir, backup_dir, retention_days=7):
        self.source_dir = source_dir
        self.backup_dir = backup_dir
        self.retention_days = retention_days
        self.backup_history = []

        # 确保备份目录存在
        os.makedirs(backup_dir, exist_ok=True)

    def backup_database(self):
        """执行数据库备份"""
        timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
        backup_name = f"backup_{timestamp}"
        backup_path = os.path.join(self.backup_dir, backup_name)

        try:
            # 模拟数据库备份（实际应用中使用相应的数据库备份命令）
            print(f"开始备份数据库到 {backup_path}")

            # 示例：复制文件作为备份
            if os.path.exists(self.source_dir):
                shutil.copytree(self.source_dir, backup_path)

            # 记录备份信息
            backup_info = {
                'path': backup_path,
                'time': datetime.now(),
                'size': self.get_dir_size(backup_path)
            }
            self.backup_history.append(backup_info)

            print(f"✓ 备份完成: {backup_name}")
            return True

        except Exception as e:
            print(f"✗ 备份失败: {e}")
            return False

    def cleanup_old_backups(self):
        """清理旧备份"""
        cutoff_date = datetime.now() - timedelta(days=self.retention_days)
        removed_count = 0

        for backup_dir in os.listdir(self.backup_dir):
            backup_path = os.path.join(self.backup_dir, backup_dir)

            # 检查目录修改时间
            if os.path.isdir(backup_path):
                mtime = datetime.fromtimestamp(os.path.getmtime(backup_path))

                if mtime < cutoff_date:
                    try:
                        shutil.rmtree(backup_path)
                        removed_count += 1
                        print(f"删除旧备份: {backup_dir}")
                    except Exception as e:
                        print(f"删除失败: {backup_dir} - {e}")

        if removed_count > 0:
            print(f"✓ 清理了 {removed_count} 个旧备份")

        return removed_count

    def get_dir_size(self, path):
        """获取目录大小"""
        total = 0
        for dirpath, dirnames, filenames in os.walk(path):
            for f in filenames:
                fp = os.path.join(dirpath, f)
                if os.path.exists(fp):
                    total += os.path.getsize(fp)
        return total

    def send_backup_report(self):
        """发送备份报告"""
        # 生成报告内容
        report = self.generate_report()

        # 打印报告（实际应用中可以发送邮件）
        print("\n" + "="*60)
        print("备份系统日报")
        print("="*60)
        print(report)
        print("="*60 + "\n")

        # 实际应用中发送邮件
        # self.send_email(report)

    def generate_report(self):
        """生成备份报告"""
        total_backups = len(os.listdir(self.backup_dir))
        total_size = sum(self.get_dir_size(os.path.join(self.backup_dir, d))
                        for d in os.listdir(self.backup_dir))

        recent_backups = self.backup_history[-5:] if self.backup_history else []

        report = f"""
备份系统报告 - {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}

系统状态：
- 备份目录: {self.backup_dir}
- 总备份数: {total_backups}
- 总占用空间: {self.format_bytes(total_size)}
- 保留天数: {self.retention_days}

最近备份记录：
"""
        for backup in recent_backups:
            report += f"- {backup['time'].strftime('%Y-%m-%d %H:%M:%S')} - "
            report += f"大小: {self.format_bytes(backup['size'])}\n"

        return report

    def format_bytes(self, size):
        """格式化字节大小"""
        for unit in ['B', 'KB', 'MB', 'GB', 'TB']:
            if size < 1024.0:
                return f"{size:.2f} {unit}"
            size /= 1024.0
        return f"{size:.2f} PB"

    def verify_backup(self):
        """验证最新备份的完整性"""
        if not self.backup_history:
            print("没有备份历史")
            return False

        latest_backup = self.backup_history[-1]
        backup_path = latest_backup['path']

        if os.path.exists(backup_path):
            # 执行验证逻辑
            file_count = sum(len(files) for _, _, files in os.walk(backup_path))
            print(f"✓ 最新备份验证成功，包含 {file_count} 个文件")
            return True
        else:
            print("✗ 最新备份验证失败：文件不存在")
            return False

def setup_backup_schedule():
    """设置备份计划"""
    # 创建备份系统实例
    backup_system = BackupSystem(
        source_dir="./data",  # 源数据目录
        backup_dir="./backups",  # 备份目录
        retention_days=7  # 保留7天
    )

    # 设置备份计划
    # 每天凌晨2点执行完整备份
    schedule.every().day.at("02:00").do(backup_system.backup_database).tag('backup', 'daily')

    # 每6小时执行增量备份
    schedule.every(6).hours.do(backup_system.backup_database).tag('backup', 'incremental')

    # 每天凌晨3点清理旧备份
    schedule.every().day.at("03:00").do(backup_system.cleanup_old_backups).tag('cleanup', 'daily')

    # 每天早上8点发送备份报告
    schedule.every().day.at("08:00").do(backup_system.send_backup_report).tag('report', 'daily')

    # 每小时验证最新备份
    schedule.every().hour.do(backup_system.verify_backup).tag('verify', 'hourly')

    print("备份系统已启动，计划任务：")
    for job in schedule.get_jobs():
        print(f"- {job}")

    return backup_system

# 使用示例
if __name__ == "__main__":
    backup_system = setup_backup_schedule()

    # 立即执行一次备份（用于测试）
    backup_system.backup_database()

    # 运行调度器
    while True:
        schedule.run_pending()
        time.sleep(1)
```

### 示例2：网站监控系统

```python
"""
网站监控系统
- 定期检查网站可用性
- 监控响应时间
- 发送告警通知
"""
import schedule
import time
import requests
from datetime import datetime
from collections import deque
import statistics

class WebsiteMonitor:
    def __init__(self, sites, alert_threshold=3):
        self.sites = sites  # 要监控的网站列表
        self.alert_threshold = alert_threshold  # 连续失败次数阈值
        self.status_history = {site: deque(maxlen=100) for site in sites}
        self.failure_count = {site: 0 for site in sites}
        self.alerts_sent = {site: False for site in sites}

    def check_website(self, url):
        """检查单个网站"""
        try:
            start_time = time.time()
            response = requests.get(url, timeout=10)
            response_time = (time.time() - start_time) * 1000  # 转换为毫秒

            status = {
                'url': url,
                'status_code': response.status_code,
                'response_time': response_time,
                'is_up': response.status_code == 200,
                'timestamp': datetime.now(),
                'error': None
            }

            # 更新失败计数
            if status['is_up']:
                self.failure_count[url] = 0
                if self.alerts_sent[url]:
                    self.send_recovery_alert(url)
                    self.alerts_sent[url] = False
            else:
                self.failure_count[url] += 1

        except requests.RequestException as e:
            status = {
                'url': url,
                'status_code': None,
                'response_time': None,
                'is_up': False,
                'timestamp': datetime.now(),
                'error': str(e)
            }
            self.failure_count[url] += 1

        # 记录状态
        self.status_history[url].append(status)

        # 检查是否需要发送告警
        if self.failure_count[url] >= self.alert_threshold and not self.alerts_sent[url]:
            self.send_alert(url, status)
            self.alerts_sent[url] = True

        return status

    def check_all_websites(self):
        """检查所有网站"""
        print(f"\n[{datetime.now().strftime('%Y-%m-%d %H:%M:%S')}] 开始检查网站...")

        for url in self.sites:
            status = self.check_website(url)
            self.print_status(status)

    def print_status(self, status):
        """打印网站状态"""
        if status['is_up']:
            symbol = "✓"
            message = f"{status['response_time']:.0f}ms"
        else:
            symbol = "✗"
            message = status['error'] or f"HTTP {status['status_code']}"

        print(f"{symbol} {status['url']}: {message}")

    def send_alert(self, url, status):
        """发送告警通知"""
        print("\n" + "!"*60)
        print(f"🚨 告警: {url} 不可访问!")
        print(f"连续失败次数: {self.failure_count[url]}")
        if status['error']:
            print(f"错误信息: {status['error']}")
        print("!"*60 + "\n")

        # 实际应用中可以：
        # - 发送邮件
        # - 发送短信
        # - 调用 Webhook
        # - 写入日志

    def send_recovery_alert(self, url):
        """发送恢复通知"""
        print("\n" + "="*60)
        print(f"✅ 恢复: {url} 已恢复正常!")
        print("="*60 + "\n")

    def generate_daily_report(self):
        """生成每日报告"""
        print("\n" + "#"*60)
        print(f"网站监控日报 - {datetime.now().strftime('%Y-%m-%d')}")
        print("#"*60)

        for url in self.sites:
            history = list(self.status_history[url])
            if not history:
                continue

            # 计算统计信息
            total_checks = len(history)
            successful_checks = sum(1 for s in history if s['is_up'])
            uptime_percentage = (successful_checks / total_checks) * 100 if total_checks > 0 else 0

            response_times = [s['response_time'] for s in history if s['response_time'] is not None]

            print(f"\n{url}:")
            print(f"  检查次数: {total_checks}")
            print(f"  可用性: {uptime_percentage:.2f}%")

            if response_times:
                print(f"  平均响应时间: {statistics.mean(response_times):.0f}ms")
                print(f"  最快响应时间: {min(response_times):.0f}ms")
                print(f"  最慢响应时间: {max(response_times):.0f}ms")
                if len(response_times) > 1:
                    print(f"  响应时间中位数: {statistics.median(response_times):.0f}ms")

        print("#"*60 + "\n")

    def check_performance_degradation(self):
        """检查性能下降"""
        for url in self.sites:
            history = list(self.status_history[url])
            if len(history) < 10:
                continue

            # 获取最近10次的响应时间
            recent_times = [s['response_time'] for s in history[-10:]
                          if s['response_time'] is not None]

            if len(recent_times) < 5:
                continue

            # 计算平均响应时间
            avg_time = statistics.mean(recent_times)

            # 获取历史平均（排除最近10次）
            historical_times = [s['response_time'] for s in history[:-10]
                              if s['response_time'] is not None]

            if historical_times:
                historical_avg = statistics.mean(historical_times)

                # 如果最近的平均响应时间比历史平均高50%以上
                if avg_time > historical_avg * 1.5:
                    print(f"⚠️ 性能告警: {url}")
                    print(f"   当前平均响应: {avg_time:.0f}ms")
                    print(f"   历史平均响应: {historical_avg:.0f}ms")

def setup_monitoring():
    """设置监控计划"""
    # 要监控的网站列表
    sites = [
        "https://www.google.com",
        "https://www.github.com",
        "https://www.stackoverflow.com",
        # 添加一个可能失败的URL用于测试
        "https://www.this-website-definitely-does-not-exist-12345.com"
    ]

    monitor = WebsiteMonitor(sites, alert_threshold=3)

    # 每分钟检查一次所有网站
    schedule.every(1).minutes.do(monitor.check_all_websites).tag('monitor', 'critical')

    # 每30分钟检查性能下降
    schedule.every(30).minutes.do(monitor.check_performance_degradation).tag('performance')

    # 每天早上9点生成日报
    schedule.every().day.at("09:00").do(monitor.generate_daily_report).tag('report')

    # 立即执行一次检查
    monitor.check_all_websites()

    return monitor

# 使用示例
if __name__ == "__main__":
    monitor = setup_monitoring()

    print("\n监控系统已启动...")
    print("按 Ctrl+C 停止\n")

    try:
        while True:
            schedule.run_pending()
            time.sleep(1)
    except KeyboardInterrupt:
        print("\n监控系统已停止")
```

### 示例3：数据采集和分析系统

```python
"""
数据采集和分析系统
- 定期采集数据
- 实时分析处理
- 生成可视化报告
"""
import schedule
import time
import random
import json
from datetime import datetime, timedelta
from collections import defaultdict
import statistics

class DataCollector:
    """数据采集器"""

    def __init__(self, data_file="collected_data.json"):
        self.data_file = data_file
        self.current_batch = []
        self.load_historical_data()

    def load_historical_data(self):
        """加载历史数据"""
        try:
            with open(self.data_file, 'r') as f:
                self.historical_data = json.load(f)
        except FileNotFoundError:
            self.historical_data = []

    def collect_sensor_data(self):
        """采集传感器数据（模拟）"""
        data_point = {
            'timestamp': datetime.now().isoformat(),
            'temperature': random.uniform(20, 30),
            'humidity': random.uniform(40, 80),
            'pressure': random.uniform(1000, 1020),
            'cpu_usage': random.uniform(10, 90),
            'memory_usage': random.uniform(30, 80),
            'disk_io': random.uniform(0, 100)
        }

        self.current_batch.append(data_point)
        print(f"📊 采集数据: Temp={data_point['temperature']:.1f}°C, "
              f"CPU={data_point['cpu_usage']:.1f}%")

        return data_point

    def save_batch(self):
        """保存批次数据"""
        if not self.current_batch:
            return

        self.historical_data.extend(self.current_batch)

        # 只保留最近7天的数据
        cutoff = datetime.now() - timedelta(days=7)
        self.historical_data = [
            d for d in self.historical_data
            if datetime.fromisoformat(d['timestamp']) > cutoff
        ]

        # 保存到文件
        with open(self.data_file, 'w') as f:
            json.dump(self.historical_data, f)

        print(f"💾 保存了 {len(self.current_batch)} 条数据")
        self.current_batch = []

class DataAnalyzer:
    """数据分析器"""

    def __init__(self, collector):
        self.collector = collector
        self.anomalies = []
        self.alerts = defaultdict(list)

    def analyze_realtime(self):
        """实时分析"""
        if not self.collector.current_batch:
            return

        latest = self.collector.current_batch[-1]

        # 检测异常
        anomalies = []

        # 温度异常
        if latest['temperature'] > 28:
            anomalies.append(f"高温警告: {latest['temperature']:.1f}°C")

        # CPU使用率异常
        if latest['cpu_usage'] > 80:
            anomalies.append(f"CPU使用率过高: {latest['cpu_usage']:.1f}%")

        # 内存使用率异常
        if latest['memory_usage'] > 75:
            anomalies.append(f"内存使用率过高: {latest['memory_usage']:.1f}%")

        if anomalies:
            print("⚠️ 检测到异常:")
            for anomaly in anomalies:
                print(f"   - {anomaly}")
                self.anomalies.append({
                    'time': latest['timestamp'],
                    'message': anomaly
                })

    def generate_hourly_summary(self):
        """生成每小时摘要"""
        all_data = self.collector.historical_data + self.collector.current_batch

        if not all_data:
            return

        # 获取最近一小时的数据
        cutoff = datetime.now() - timedelta(hours=1)
        recent_data = [
            d for d in all_data
            if datetime.fromisoformat(d['timestamp']) > cutoff
        ]

        if not recent_data:
            return

        print("\n" + "="*60)
        print(f"📈 每小时数据摘要 - {datetime.now().strftime('%Y-%m-%d %H:%M')}")
        print("="*60)

        # 计算各项指标的统计信息
        metrics = ['temperature', 'humidity', 'cpu_usage', 'memory_usage']

        for metric in metrics:
            values = [d[metric] for d in recent_data]
            if values:
                print(f"\n{metric.replace('_', ' ').title()}:")
                print(f"  平均值: {statistics.mean(values):.2f}")
                print(f"  最小值: {min(values):.2f}")
                print(f"  最大值: {max(values):.2f}")
                print(f"  标准差: {statistics.stdev(values):.2f}" if len(values) > 1 else "")

        # 显示异常统计
        recent_anomalies = [
            a for a in self.anomalies
            if datetime.fromisoformat(a['time']) > cutoff
        ]

        if recent_anomalies:
            print(f"\n异常事件: {len(recent_anomalies)} 次")
            for anomaly in recent_anomalies[-5:]:  # 显示最近5个
                print(f"  - {anomaly['message']}")

        print("="*60 + "\n")

    def predict_trends(self):
        """趋势预测"""
        all_data = self.collector.historical_data + self.collector.current_batch

        if len(all_data) < 20:
            return

        # 简单的移动平均预测
        recent_temps = [d['temperature'] for d in all_data[-20:]]
        recent_cpu = [d['cpu_usage'] for d in all_data[-20:]]

        temp_trend = recent_temps[-1] - statistics.mean(recent_temps[:-1])
        cpu_trend = recent_cpu[-1] - statistics.mean(recent_cpu[:-1])

        print("\n🔮 趋势分析:")

        if abs(temp_trend) > 1:
            direction = "上升" if temp_trend > 0 else "下降"
            print(f"  温度趋势: {direction} ({temp_trend:+.1f}°C)")

        if abs(cpu_trend) > 10:
            direction = "上升" if cpu_trend > 0 else "下降"
            print(f"  CPU使用趋势: {direction} ({cpu_trend:+.1f}%)")

class ReportGenerator:
    """报告生成器"""

    def __init__(self, collector, analyzer):
        self.collector = collector
        self.analyzer = analyzer

    def generate_daily_report(self):
        """生成每日报告"""
        all_data = self.collector.historical_data + self.collector.current_batch

        # 获取今天的数据
        today = datetime.now().date()
        today_data = [
            d for d in all_data
            if datetime.fromisoformat(d['timestamp']).date() == today
        ]

        if not today_data:
            print("今日暂无数据")
            return

        print("\n" + "#"*70)
        print(f"📊 数据采集系统日报 - {today}")
        print("#"*70)

        print(f"\n总体统计:")
        print(f"  数据点数量: {len(today_data)}")
        print(f"  采集时长: {(datetime.fromisoformat(today_data[-1]['timestamp']) - datetime.fromisoformat(today_data[0]['timestamp'])).total_seconds() / 3600:.1f} 小时")

        # 各指标的日统计
        metrics = {
            'temperature': '温度 (°C)',
            'humidity': '湿度 (%)',
            'pressure': '气压 (hPa)',
            'cpu_usage': 'CPU使用率 (%)',
            'memory_usage': '内存使用率 (%)',
            'disk_io': '磁盘IO (MB/s)'
        }

        for metric, label in metrics.items():
            values = [d[metric] for d in today_data]
            if values:
                print(f"\n{label}:")
                print(f"  平均: {statistics.mean(values):.2f}")
                print(f"  范围: {min(values):.2f} - {max(values):.2f}")

                # 绘制简单的ASCII图表
                self.draw_ascii_chart(values[-24:], label)  # 最近24个数据点

        # 异常事件统计
        today_anomalies = [
            a for a in self.analyzer.anomalies
            if datetime.fromisoformat(a['time']).date() == today
        ]

        if today_anomalies:
            print(f"\n异常事件汇总 (共 {len(today_anomalies)} 次):")
            anomaly_types = defaultdict(int)
            for a in today_anomalies:
                # 简单分类
                if '温度' in a['message']:
                    anomaly_types['温度异常'] += 1
                elif 'CPU' in a['message']:
                    anomaly_types['CPU异常'] += 1
                elif '内存' in a['message']:
                    anomaly_types['内存异常'] += 1

            for atype, count in anomaly_types.items():
                print(f"  - {atype}: {count} 次")

        print("\n" + "#"*70 + "\n")

    def draw_ascii_chart(self, values, label, width=50, height=10):
        """绘制ASCII图表"""
        if not values:
            return

        print(f"\n  {label} 趋势图:")

        # 归一化数据到0-height范围
        min_val = min(values)
        max_val = max(values)
        range_val = max_val - min_val if max_val != min_val else 1

        normalized = [
            int((v - min_val) / range_val * height)
            for v in values
        ]

        # 采样数据以适应宽度
        if len(normalized) > width:
            step = len(normalized) / width
            sampled = [normalized[int(i * step)] for i in range(width)]
        else:
            sampled = normalized

        # 绘制图表
        for row in range(height, -1, -1):
            line = "  │"
            for val in sampled:
                if val >= row:
                    line += "█"
                else:
                    line += " "
            print(line)

        print("  └" + "─" * len(sampled))
        print(f"   {min_val:.1f}" + " " * (len(sampled) - 10) + f"{max_val:.1f}")

def setup_data_pipeline():
    """设置数据处理管道"""
    collector = DataCollector()
    analyzer = DataAnalyzer(collector)
    reporter = ReportGenerator(collector, analyzer)

    # 数据采集 - 每30秒
    schedule.every(30).seconds.do(collector.collect_sensor_data).tag('collect')

    # 实时分析 - 每分钟
    schedule.every(1).minutes.do(analyzer.analyze_realtime).tag('analyze')

    # 批次保存 - 每5分钟
    schedule.every(5).minutes.do(collector.save_batch).tag('save')

    # 趋势预测 - 每15分钟
    schedule.every(15).minutes.do(analyzer.predict_trends).tag('predict')

    # 小时摘要 - 每小时
    schedule.every().hour.do(analyzer.generate_hourly_summary).tag('summary')

    # 日报 - 每天晚上9点
    schedule.every().day.at("21:00").do(reporter.generate_daily_report).tag('report')

    print("数据处理管道已启动")
    print("计划任务:")
    for job in schedule.get_jobs():
        print(f"  - {job}")

    return collector, analyzer, reporter

# 使用示例
if __name__ == "__main__":
    collector, analyzer, reporter = setup_data_pipeline()

    # 立即采集一些数据用于测试
    for _ in range(5):
        collector.collect_sensor_data()
        time.sleep(1)

    print("\n系统运行中... (按 Ctrl+C 停止)\n")

    try:
        while True:
            schedule.run_pending()
            time.sleep(1)
    except KeyboardInterrupt:
        print("\n系统已停止")
        # 保存未保存的数据
        collector.save_batch()
```

## 与其他库集成

### 1. 与 Threading 集成

```python
import schedule
import time
import threading

def run_threaded(job_func):
    """在新线程中运行任务"""
    job_thread = threading.Thread(target=job_func)
    job_thread.daemon = True
    job_thread.start()

def heavy_task():
    """耗时任务"""
    print(f"开始执行耗时任务 - {threading.current_thread().name}")
    time.sleep(10)  # 模拟耗时操作
    print(f"耗时任务完成 - {threading.current_thread().name}")

def quick_task():
    """快速任务"""
    print(f"执行快速任务 - {threading.current_thread().name}")

# 在新线程中运行耗时任务，避免阻塞
schedule.every(30).seconds.do(run_threaded, heavy_task)
schedule.every(5).seconds.do(quick_task)

# 在独立线程中运行调度器
def run_scheduler():
    while True:
        schedule.run_pending()
        time.sleep(1)

scheduler_thread = threading.Thread(target=run_scheduler)
scheduler_thread.daemon = True
scheduler_thread.start()

# 主线程可以做其他事情
while True:
    time.sleep(1)
```

### 2. 与 Asyncio 集成

```python
import asyncio
import schedule
import time
from datetime import datetime

class AsyncScheduler:
    """异步任务调度器"""

    def __init__(self):
        self.loop = asyncio.get_event_loop()

    async def async_job(self, name):
        """异步任务"""
        print(f"[{datetime.now().strftime('%H:%M:%S')}] 开始异步任务: {name}")
        await asyncio.sleep(3)  # 模拟异步操作
        print(f"[{datetime.now().strftime('%H:%M:%S')}] 完成异步任务: {name}")

    def schedule_async(self, coro):
        """调度异步任务"""
        asyncio.create_task(coro)

    async def run_schedule(self):
        """运行调度循环"""
        while True:
            schedule.run_pending()
            await asyncio.sleep(1)

async def main():
    scheduler = AsyncScheduler()

    # 设置定时任务
    schedule.every(5).seconds.do(
        scheduler.schedule_async,
        scheduler.async_job("任务A")
    )
    schedule.every(8).seconds.do(
        scheduler.schedule_async,
        scheduler.async_job("任务B")
    )

    # 运行调度器
    await scheduler.run_schedule()

# 运行
if __name__ == "__main__":
    asyncio.run(main())
```

### 3. 与数据库集成

```python
import schedule
import sqlite3
from datetime import datetime
import json

class ScheduledDatabaseTasks:
    """数据库定时任务"""

    def __init__(self, db_path="schedule_tasks.db"):
        self.db_path = db_path
        self.init_database()

    def init_database(self):
        """初始化数据库"""
        with sqlite3.connect(self.db_path) as conn:
            conn.execute('''
                CREATE TABLE IF NOT EXISTS task_history (
                    id INTEGER PRIMARY KEY AUTOINCREMENT,
                    task_name TEXT,
                    execution_time TIMESTAMP,
                    status TEXT,
                    result TEXT
                )
            ''')

            conn.execute('''
                CREATE TABLE IF NOT EXISTS scheduled_tasks (
                    id INTEGER PRIMARY KEY AUTOINCREMENT,
                    task_name TEXT UNIQUE,
                    schedule_expression TEXT,
                    is_active BOOLEAN,
                    last_run TIMESTAMP,
                    next_run TIMESTAMP
                )
            ''')

    def log_execution(self, task_name, status, result=None):
        """记录任务执行"""
        with sqlite3.connect(self.db_path) as conn:
            conn.execute(
                "INSERT INTO task_history (task_name, execution_time, status, result) VALUES (?, ?, ?, ?)",
                (task_name, datetime.now(), status, json.dumps(result) if result else None)
            )

    def database_backup(self):
        """数据库备份任务"""
        try:
            # 执行备份逻辑
            backup_file = f"backup_{datetime.now().strftime('%Y%m%d_%H%M%S')}.db"
            # 实际备份代码...

            self.log_execution("database_backup", "success", {"file": backup_file})
            print(f"✓ 数据库备份完成: {backup_file}")
        except Exception as e:
            self.log_execution("database_backup", "failed", {"error": str(e)})
            print(f"✗ 数据库备份失败: {e}")

    def cleanup_old_records(self):
        """清理旧记录"""
        try:
            with sqlite3.connect(self.db_path) as conn:
                # 删除30天前的记录
                result = conn.execute(
                    "DELETE FROM task_history WHERE execution_time < datetime('now', '-30 days')"
                )
                deleted_count = result.rowcount

            self.log_execution("cleanup_old_records", "success", {"deleted": deleted_count})
            print(f"✓ 清理了 {deleted_count} 条旧记录")
        except Exception as e:
            self.log_execution("cleanup_old_records", "failed", {"error": str(e)})
            print(f"✗ 清理失败: {e}")

    def generate_statistics(self):
        """生成统计报告"""
        try:
            with sqlite3.connect(self.db_path) as conn:
                # 统计任务执行情况
                stats = conn.execute('''
                    SELECT
                        task_name,
                        COUNT(*) as total_runs,
                        SUM(CASE WHEN status = 'success' THEN 1 ELSE 0 END) as successful_runs,
                        MAX(execution_time) as last_run
                    FROM task_history
                    WHERE execution_time > datetime('now', '-7 days')
                    GROUP BY task_name
                ''').fetchall()

            print("\n📊 任务执行统计（最近7天）:")
            for task_name, total, successful, last_run in stats:
                success_rate = (successful / total * 100) if total > 0 else 0
                print(f"  {task_name}:")
                print(f"    执行次数: {total}")
                print(f"    成功率: {success_rate:.1f}%")
                print(f"    最后执行: {last_run}")

            self.log_execution("generate_statistics", "success")
        except Exception as e:
            self.log_execution("generate_statistics", "failed", {"error": str(e)})
            print(f"✗ 统计失败: {e}")

# 使用示例
db_tasks = ScheduledDatabaseTasks()

# 设置定时任务
schedule.every().day.at("02:00").do(db_tasks.database_backup)
schedule.every().sunday.at("03:00").do(db_tasks.cleanup_old_records)
schedule.every().day.at("09:00").do(db_tasks.generate_statistics)

# 运行
while True:
    schedule.run_pending()
    time.sleep(1)
```

## 最佳实践

### 1. 错误处理和重试机制

```python
import schedule
import time
from functools import wraps
import logging

# 配置日志
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

def retry_on_failure(max_retries=3, delay=60):
    """重试装饰器"""
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            retries = 0
            while retries < max_retries:
                try:
                    result = func(*args, **kwargs)
                    if retries > 0:
                        logging.info(f"{func.__name__} 在重试 {retries} 次后成功")
                    return result
                except Exception as e:
                    retries += 1
                    logging.error(f"{func.__name__} 失败 (尝试 {retries}/{max_retries}): {e}")

                    if retries < max_retries:
                        logging.info(f"等待 {delay} 秒后重试...")
                        time.sleep(delay)
                    else:
                        logging.error(f"{func.__name__} 在 {max_retries} 次尝试后彻底失败")
                        # 可以发送告警通知
                        raise

            return schedule.CancelJob
        return wrapper
    return decorator

@retry_on_failure(max_retries=3, delay=30)
def unreliable_task():
    """可能失败的任务"""
    import random
    if random.random() < 0.7:  # 70%概率失败
        raise Exception("模拟任务失败")
    print("✓ 任务执行成功")
    return "success"

# 设置任务
schedule.every(10).seconds.do(unreliable_task)
```

### 2. 任务依赖管理

```python
import schedule
from enum import Enum
from typing import Dict, Set, Callable

class TaskStatus(Enum):
    PENDING = "pending"
    RUNNING = "running"
    COMPLETED = "completed"
    FAILED = "failed"

class DependencyManager:
    """任务依赖管理器"""

    def __init__(self):
        self.tasks: Dict[str, Callable] = {}
        self.dependencies: Dict[str, Set[str]] = {}
        self.status: Dict[str, TaskStatus] = {}
        self.results: Dict[str, any] = {}

    def register_task(self, name: str, func: Callable, depends_on: Set[str] = None):
        """注册任务及其依赖"""
        self.tasks[name] = func
        self.dependencies[name] = depends_on or set()
        self.status[name] = TaskStatus.PENDING

    def can_run(self, task_name: str) -> bool:
        """检查任务是否可以运行"""
        deps = self.dependencies.get(task_name, set())
        for dep in deps:
            if self.status.get(dep) != TaskStatus.COMPLETED:
                return False
        return True

    def run_task(self, task_name: str):
        """运行任务"""
        if not self.can_run(task_name):
            print(f"⏳ {task_name} 正在等待依赖完成")
            return

        if self.status[task_name] == TaskStatus.COMPLETED:
            print(f"✅ {task_name} 已经完成")
            return

        print(f"▶️ 开始执行 {task_name}")
        self.status[task_name] = TaskStatus.RUNNING

        try:
            # 传递依赖任务的结果
            dep_results = {dep: self.results.get(dep) for dep in self.dependencies[task_name]}
            result = self.tasks[task_name](dep_results) if dep_results else self.tasks[task_name]()

            self.results[task_name] = result
            self.status[task_name] = TaskStatus.COMPLETED
            print(f"✓ {task_name} 完成")

            # 尝试运行依赖此任务的其他任务
            self.check_and_run_dependent_tasks(task_name)

        except Exception as e:
            self.status[task_name] = TaskStatus.FAILED
            print(f"✗ {task_name} 失败: {e}")

    def check_and_run_dependent_tasks(self, completed_task: str):
        """检查并运行依赖已完成任务的其他任务"""
        for task_name, deps in self.dependencies.items():
            if completed_task in deps and self.status[task_name] == TaskStatus.PENDING:
                self.run_task(task_name)

    def reset_daily(self):
        """重置每日任务状态"""
        for task_name in self.tasks:
            self.status[task_name] = TaskStatus.PENDING
        self.results.clear()
        print("📅 任务状态已重置")

# 使用示例
dep_manager = DependencyManager()

# 定义任务函数
def extract_data():
    print("  提取数据...")
    return {"data": [1, 2, 3, 4, 5]}

def transform_data(deps):
    data = deps['extract']['data']
    print(f"  转换数据: {data}")
    return {"transformed": [x * 2 for x in data]}

def load_data(deps):
    data = deps['transform']['transformed']
    print(f"  加载数据: {data}")
    return "success"

# 注册任务及依赖关系
dep_manager.register_task('extract', extract_data)
dep_manager.register_task('transform', transform_data, {'extract'})
dep_manager.register_task('load', load_data, {'transform'})

# 设置调度
def run_etl_pipeline():
    """运行ETL管道"""
    print("\n🚀 开始ETL管道")
    dep_manager.run_task('extract')

# 每天运行一次ETL
schedule.every().day.at("01:00").do(run_etl_pipeline)
schedule.every().day.at("00:00").do(dep_manager.reset_daily)
```

### 3. 配置文件驱动的调度

```python
import schedule
import yaml
import json
from typing import Dict, Any

class ConfigurableScheduler:
    """基于配置文件的调度器"""

    def __init__(self, config_file: str):
        self.config_file = config_file
        self.tasks = {}
        self.load_config()

    def load_config(self):
        """加载配置文件"""
        with open(self.config_file, 'r') as f:
            if self.config_file.endswith('.yaml') or self.config_file.endswith('.yml'):
                config = yaml.safe_load(f)
            else:
                config = json.load(f)

        self.setup_tasks(config['tasks'])

    def setup_tasks(self, tasks_config: list):
        """根据配置设置任务"""
        for task_config in tasks_config:
            self.create_task(task_config)

    def create_task(self, config: Dict[str, Any]):
        """创建单个任务"""
        task_name = config['name']
        task_type = config['type']
        schedule_expr = config['schedule']
        enabled = config.get('enabled', True)

        if not enabled:
            print(f"⏸️ 任务 {task_name} 已禁用")
            return

        # 根据任务类型创建任务函数
        if task_type == 'command':
            task_func = self.create_command_task(config['command'])
        elif task_type == 'script':
            task_func = self.create_script_task(config['script'])
        elif task_type == 'http':
            task_func = self.create_http_task(config['url'], config.get('method', 'GET'))
        else:
            print(f"❌ 未知任务类型: {task_type}")
            return

        # 解析调度表达式
        self.parse_schedule(schedule_expr, task_func, task_name)
        print(f"✓ 已配置任务: {task_name} ({schedule_expr})")

    def create_command_task(self, command: str):
        """创建命令任务"""
        def task():
            import subprocess
            try:
                result = subprocess.run(command, shell=True, capture_output=True, text=True)
                print(f"命令执行: {command[:50]}...")
                if result.returncode != 0:
                    print(f"命令失败: {result.stderr}")
            except Exception as e:
                print(f"命令错误: {e}")
        return task

    def create_script_task(self, script_path: str):
        """创建脚本任务"""
        def task():
            try:
                with open(script_path, 'r') as f:
                    exec(f.read())
                print(f"脚本执行: {script_path}")
            except Exception as e:
                print(f"脚本错误: {e}")
        return task

    def create_http_task(self, url: str, method: str):
        """创建HTTP任务"""
        def task():
            import requests
            try:
                response = requests.request(method, url, timeout=30)
                print(f"HTTP {method} {url}: {response.status_code}")
            except Exception as e:
                print(f"HTTP错误: {e}")
        return task

    def parse_schedule(self, expr: str, func: Callable, name: str):
        """解析调度表达式"""
        parts = expr.split()

        if parts[0] == 'every':
            if len(parts) == 2:
                # every minute, every hour, etc.
                interval = parts[1].lower()
                if interval == 'minute':
                    schedule.every().minute.do(func).tag(name)
                elif interval == 'hour':
                    schedule.every().hour.do(func).tag(name)
                elif interval == 'day':
                    schedule.every().day.do(func).tag(name)
                elif interval == 'week':
                    schedule.every().week.do(func).tag(name)
            elif len(parts) == 3:
                # every 5 minutes, every 2 hours, etc.
                count = int(parts[1])
                interval = parts[2].lower()
                if interval == 'seconds':
                    schedule.every(count).seconds.do(func).tag(name)
                elif interval == 'minutes':
                    schedule.every(count).minutes.do(func).tag(name)
                elif interval == 'hours':
                    schedule.every(count).hours.do(func).tag(name)
        elif parts[0] == 'at':
            # at 10:30, at 15:00, etc.
            time_str = parts[1]
            schedule.every().day.at(time_str).do(func).tag(name)
        elif parts[0] in ['monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday']:
            # monday at 10:00
            day = parts[0]
            if len(parts) > 2 and parts[1] == 'at':
                time_str = parts[2]
                getattr(schedule.every(), day).at(time_str).do(func).tag(name)
            else:
                getattr(schedule.every(), day).do(func).tag(name)

# 配置文件示例 (config.yaml)
config_example = """
tasks:
  - name: backup_database
    type: command
    command: "pg_dump mydb > backup.sql"
    schedule: "every day at 02:00"
    enabled: true

  - name: cleanup_logs
    type: script
    script: "./scripts/cleanup.py"
    schedule: "every sunday at 03:00"
    enabled: true

  - name: health_check
    type: http
    url: "https://api.example.com/health"
    method: GET
    schedule: "every 5 minutes"
    enabled: true

  - name: send_report
    type: command
    command: "python send_report.py"
    schedule: "monday at 09:00"
    enabled: false
"""

# 使用示例
# 保存配置到文件
with open('schedule_config.yaml', 'w') as f:
    f.write(config_example)

# 创建调度器
scheduler = ConfigurableScheduler('schedule_config.yaml')

# 运行
while True:
    schedule.run_pending()
    time.sleep(1)
```

## 性能优化

### 1. 避免阻塞主循环

```python
import schedule
import time
import concurrent.futures
from threading import Lock

class NonBlockingScheduler:
    """非阻塞调度器"""

    def __init__(self, max_workers=5):
        self.executor = concurrent.futures.ThreadPoolExecutor(max_workers=max_workers)
        self.running_tasks = set()
        self.lock = Lock()

    def run_async(self, func, *args, **kwargs):
        """异步运行任务"""
        task_name = func.__name__

        with self.lock:
            if task_name in self.running_tasks:
                print(f"⚠️ {task_name} 仍在运行，跳过本次执行")
                return
            self.running_tasks.add(task_name)

        def wrapper():
            try:
                result = func(*args, **kwargs)
                return result
            finally:
                with self.lock:
                    self.running_tasks.discard(task_name)

        future = self.executor.submit(wrapper)
        return future

    def shutdown(self):
        """关闭执行器"""
        self.executor.shutdown(wait=True)

# 使用示例
scheduler = NonBlockingScheduler(max_workers=10)

def slow_task(duration):
    """模拟耗时任务"""
    print(f"开始耗时任务 ({duration}秒)")
    time.sleep(duration)
    print(f"耗时任务完成 ({duration}秒)")

# 设置异步任务
schedule.every(5).seconds.do(scheduler.run_async, slow_task, 10)
schedule.every(3).seconds.do(scheduler.run_async, slow_task, 5)

try:
    while True:
        schedule.run_pending()
        time.sleep(0.1)  # 更短的检查间隔
except KeyboardInterrupt:
    scheduler.shutdown()
```

### 2. 内存优化

```python
import schedule
import gc
import psutil
import os

class MemoryOptimizedScheduler:
    """内存优化的调度器"""

    def __init__(self, memory_threshold_mb=500):
        self.memory_threshold = memory_threshold_mb * 1024 * 1024
        self.process = psutil.Process(os.getpid())

    def check_memory(self):
        """检查内存使用"""
        memory_info = self.process.memory_info()
        memory_usage_mb = memory_info.rss / (1024 * 1024)
        print(f"当前内存使用: {memory_usage_mb:.2f} MB")

        if memory_info.rss > self.memory_threshold:
            print("⚠️ 内存使用过高，执行垃圾回收")
            gc.collect()

            # 再次检查
            memory_info_after = self.process.memory_info()
            memory_usage_mb_after = memory_info_after.rss / (1024 * 1024)
            freed = memory_usage_mb - memory_usage_mb_after
            print(f"释放内存: {freed:.2f} MB")

    def memory_aware_task(self, func):
        """内存感知的任务包装器"""
        def wrapper(*args, **kwargs):
            # 任务执行前检查内存
            self.check_memory()

            # 执行任务
            result = func(*args, **kwargs)

            # 任务执行后清理
            gc.collect()

            return result
        return wrapper

# 使用示例
mem_scheduler = MemoryOptimizedScheduler(memory_threshold_mb=100)

@mem_scheduler.memory_aware_task
def data_processing_task():
    """数据处理任务"""
    # 模拟大量数据处理
    data = [i for i in range(1000000)]
    processed = [x * 2 for x in data]
    print(f"处理了 {len(processed)} 条数据")
    # 清理局部变量
    del data
    del processed

schedule.every(10).seconds.do(data_processing_task)
schedule.every(30).seconds.do(mem_scheduler.check_memory)
```

## 常见问题

### Q1: 如何精确控制任务执行时间？

```python
import schedule
import time
from datetime import datetime

def precise_timing_task():
    """需要精确时间的任务"""
    current_time = datetime.now()
    print(f"任务执行时间: {current_time.strftime('%H:%M:%S.%f')[:-3]}")

# 使用更短的检查间隔
schedule.every(10).seconds.do(precise_timing_task)

while True:
    schedule.run_pending()
    time.sleep(0.01)  # 10ms 检查间隔，提高精度
```

### Q2: 如何处理时区问题？

```python
import schedule
import pytz
from datetime import datetime

def task_with_timezone():
    """处理时区的任务"""
    # 获取不同时区的时间
    utc_time = datetime.now(pytz.UTC)
    eastern = datetime.now(pytz.timezone('US/Eastern'))
    shanghai = datetime.now(pytz.timezone('Asia/Shanghai'))

    print(f"UTC: {utc_time.strftime('%Y-%m-%d %H:%M:%S')}")
    print(f"Eastern: {eastern.strftime('%Y-%m-%d %H:%M:%S')}")
    print(f"Shanghai: {shanghai.strftime('%Y-%m-%d %H:%M:%S')}")

# 根据特定时区设置任务
def schedule_in_timezone(time_str, timezone_str, job_func):
    """在特定时区调度任务"""
    tz = pytz.timezone(timezone_str)
    local_tz = pytz.timezone('Asia/Shanghai')  # 本地时区

    # 转换时间
    # 这里需要更复杂的逻辑来处理时区转换
    schedule.every().day.at(time_str).do(job_func)

# 每天北京时间9点执行
schedule.every().day.at("09:00").do(task_with_timezone)
```

### Q3: 如何实现任务持久化？

```python
import schedule
import pickle
import json
from datetime import datetime

class PersistentScheduler:
    """支持持久化的调度器"""

    def __init__(self, state_file="scheduler_state.json"):
        self.state_file = state_file
        self.load_state()

    def save_state(self):
        """保存调度器状态"""
        state = {
            'last_save': datetime.now().isoformat(),
            'jobs': []
        }

        for job in schedule.get_jobs():
            job_info = {
                'next_run': job.next_run.isoformat() if job.next_run else None,
                'interval': str(job.interval),
                'tags': list(job.tags) if job.tags else []
            }
            state['jobs'].append(job_info)

        with open(self.state_file, 'w') as f:
            json.dump(state, f, indent=2)

        print(f"✓ 状态已保存 ({len(state['jobs'])} 个任务)")

    def load_state(self):
        """加载调度器状态"""
        try:
            with open(self.state_file, 'r') as f:
                state = json.load(f)

            print(f"✓ 加载了 {len(state['jobs'])} 个任务状态")
            print(f"  最后保存时间: {state['last_save']}")

            # 这里需要根据保存的状态重新创建任务
            # 实际应用中需要更复杂的逻辑

        except FileNotFoundError:
            print("没有找到保存的状态文件")

# 使用示例
persistent = PersistentScheduler()

# 定期保存状态
schedule.every(5).minutes.do(persistent.save_state)

# 程序退出时保存
import atexit
atexit.register(persistent.save_state)
```

### Q4: 如何实现分布式调度？

```python
import schedule
import redis
import time
from datetime import datetime
import socket

class DistributedScheduler:
    """分布式调度器（使用Redis锁）"""

    def __init__(self, redis_host='localhost', redis_port=6379):
        self.redis_client = redis.Redis(host=redis_host, port=redis_port, db=0)
        self.hostname = socket.gethostname()

    def acquire_lock(self, task_name, ttl=60):
        """获取分布式锁"""
        lock_key = f"schedule_lock:{task_name}"
        lock_value = f"{self.hostname}:{datetime.now().isoformat()}"

        # 尝试获取锁
        acquired = self.redis_client.set(
            lock_key,
            lock_value,
            nx=True,  # 仅当key不存在时设置
            ex=ttl    # 过期时间（秒）
        )

        return acquired

    def release_lock(self, task_name):
        """释放分布式锁"""
        lock_key = f"schedule_lock:{task_name}"
        self.redis_client.delete(lock_key)

    def distributed_task(self, task_name, task_func):
        """分布式任务包装器"""
        def wrapper():
            if self.acquire_lock(task_name):
                try:
                    print(f"[{self.hostname}] 执行任务: {task_name}")
                    result = task_func()
                    return result
                finally:
                    self.release_lock(task_name)
            else:
                print(f"[{self.hostname}] 任务 {task_name} 已被其他节点执行")

        return wrapper

# 使用示例
dist_scheduler = DistributedScheduler()

def shared_task():
    """多个节点共享的任务"""
    print(f"执行共享任务 - {datetime.now()}")
    time.sleep(5)  # 模拟任务执行

# 包装任务以支持分布式执行
wrapped_task = dist_scheduler.distributed_task("shared_task", shared_task)

# 所有节点都设置相同的调度，但只有一个会执行
schedule.every(10).seconds.do(wrapped_task)

while True:
    schedule.run_pending()
    time.sleep(1)
```

## 总结

Schedule 是一个优秀的 Python 任务调度库，具有以下优势：

**优点**：
1. **简单易用**：API 设计直观，学习成本低
2. **轻量级**：无外部依赖，易于部署
3. **灵活性高**：支持多种调度方式
4. **可扩展**：易于与其他库集成

**缺点**：
1. **不支持分布式**：需要自行实现分布式逻辑
2. **无持久化**：重启后任务状态丢失
3. **精度有限**：依赖于检查间隔
4. **单线程**：需要额外处理并发

**适用场景**：
- 小型到中型应用的任务调度
- 简单的定时任务和自动化脚本
- 不需要分布式的单机应用
- 快速原型开发和测试

**替代方案**：
- **Celery**：适合分布式任务队列
- **APScheduler**：功能更丰富，支持持久化
- **Cron**：系统级调度，适合服务器环境
- **Airflow**：适合复杂的工作流调度

## 参考资源

- [Schedule 官方文档](https://schedule.readthedocs.io/)
- [GitHub 仓库](https://github.com/dbader/schedule)
- [PyPI 页面](https://pypi.org/project/schedule/)

---

*本教程持续更新，欢迎提供反馈和建议！*
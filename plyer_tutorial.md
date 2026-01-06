# Python Plyer 模块使用教程

## 目录
1. [简介](#简介)
2. [安装](#安装)
3. [核心功能](#核心功能)
4. [详细使用示例](#详细使用示例)
5. [跨平台注意事项](#跨平台注意事项)
6. [常见问题](#常见问题)

## 简介

Plyer 是一个纯 Python 编写的跨平台库，提供了访问设备硬件功能的统一 API。它支持 Windows、macOS、Linux、Android 和 iOS 平台，让开发者能够轻松访问各种系统功能，如通知、相机、GPS、加速计等。

### 主要特点
- **跨平台支持**：一套代码可在多个平台运行
- **简单易用**：API 设计简洁直观
- **功能丰富**：支持多种硬件和系统功能
- **纯 Python**：无需编译，易于部署

## 安装

```bash
# 使用 pip 安装
pip install plyer

# 或者从源码安装
git clone https://github.com/kivy/plyer.git
cd plyer
python setup.py install
```

### 依赖项（可选）
某些功能可能需要额外的依赖：
```bash
# Windows 通知功能
pip install plyer[dev]

# Android 开发
pip install python-for-android
```

## 核心功能

Plyer 提供以下主要功能模块：

| 功能 | 描述 | 平台支持 |
|------|------|----------|
| notification | 系统通知 | 全平台 |
| audio | 音频录制/播放 | 全平台 |
| camera | 相机访问 | Android, iOS, macOS |
| email | 发送邮件 | 全平台 |
| filechooser | 文件选择器 | 全平台 |
| gps | GPS 定位 | Android, iOS |
| accelerometer | 加速计 | Android, iOS, macOS |
| battery | 电池信息 | 全平台 |
| brightness | 屏幕亮度 | Android, iOS, Linux |
| call | 拨打电话 | Android, iOS |
| sms | 发送短信 | Android |
| tts | 文字转语音 | 全平台 |
| uniqueid | 设备唯一ID | 全平台 |
| vibrator | 震动 | Android, iOS |
| wifi | WiFi 信息 | Android, iOS, macOS |

## 详细使用示例

### 1. 系统通知

```python
from plyer import notification

# 发送简单通知
notification.notify(
    title='提醒',
    message='这是一条测试通知',
    app_name='My App',
    timeout=10  # 通知显示时间（秒）
)

# 带图标的通知（需要.ico文件）
notification.notify(
    title='带图标通知',
    message='这是一条带自定义图标的通知',
    app_icon='path/to/icon.ico',  # Windows需要.ico格式
    timeout=5
)
```

### 2. 文件选择器

```python
from plyer import filechooser

# 选择文件打开
def open_file():
    path = filechooser.open_file(
        title="选择文件",
        filters=[("文本文件", "*.txt"), ("所有文件", "*.*")]
    )
    if path:
        print(f"选择的文件: {path[0]}")
        with open(path[0], 'r', encoding='utf-8') as f:
            content = f.read()
            print(content)

# 选择保存位置
def save_file():
    path = filechooser.save_file(
        title="保存文件",
        path="document.txt",
        filters=[("文本文件", "*.txt")]
    )
    if path:
        with open(path[0], 'w', encoding='utf-8') as f:
            f.write("这是要保存的内容")
        print(f"文件已保存到: {path[0]}")

# 选择目录
def choose_dir():
    path = filechooser.choose_dir(title="选择目录")
    if path:
        print(f"选择的目录: {path[0]}")

# 多选文件
def select_multiple():
    paths = filechooser.open_file(
        title="选择多个文件",
        multiple=True
    )
    if paths:
        for path in paths:
            print(f"选择的文件: {path}")
```

### 3. 电池信息

```python
from plyer import battery

# 获取电池状态
status = battery.status
print(f"电池状态: {status}")

# 获取电量百分比
if status['isCharging'] is not None:
    print(f"是否充电中: {status['isCharging']}")
    print(f"电量: {status.get('percentage', 'N/A')}%")
```

### 4. 文字转语音 (TTS)

```python
from plyer import tts

# 简单的文字转语音
tts.speak("你好，这是文字转语音测试")

# 如果需要等待语音播放完成
import time
tts.speak("正在播放语音")
time.sleep(3)  # 等待3秒
```

### 5. 获取设备唯一ID

```python
from plyer import uniqueid

# 获取设备ID
device_id = uniqueid.id
print(f"设备唯一ID: {device_id}")
```

### 6. 发送邮件

```python
from plyer import email

# 创建邮件（会打开默认邮件客户端）
email.send(
    recipient='example@email.com',
    subject='测试邮件',
    text='这是邮件正文内容',
    create_chooser=True  # Android上显示应用选择器
)
```

### 7. 音频录制

```python
from plyer import audio
import time

# 开始录音
audio.file_path = 'recording.wav'
audio.start()

print("录音中...")
time.sleep(5)  # 录制5秒

# 停止录音
audio.stop()
print(f"录音已保存到: {audio.file_path}")

# 播放录音
audio.play()
```

### 8. GPS 定位（移动设备）

```python
from plyer import gps

def on_location(**kwargs):
    """位置更新回调函数"""
    print(f"纬度: {kwargs.get('lat')}")
    print(f"经度: {kwargs.get('lon')}")
    print(f"速度: {kwargs.get('speed')}")
    print(f"精度: {kwargs.get('accuracy')}")

def on_status(stype, status):
    """GPS状态回调"""
    print(f"GPS {stype}: {status}")

# 配置GPS
gps.configure(
    on_location=on_location,
    on_status=on_status
)

# 开始定位（需要权限）
gps.start(minTime=1000, minDistance=1)  # 每1秒或移动1米更新

# 运行一段时间后停止
import time
time.sleep(30)
gps.stop()
```

### 9. 震动（移动设备）

```python
from plyer import vibrator

# 震动1秒
vibrator.vibrate(1)

# 模式震动（震动-暂停-震动）
vibrator.pattern([0, 1000, 500, 2000])  # 延迟0ms，震动1s，暂停0.5s，震动2s

# 取消震动
vibrator.cancel()
```

### 10. 屏幕亮度控制

```python
from plyer import brightness

# 获取当前亮度（0-1之间的值）
current = brightness.current_brightness()
print(f"当前亮度: {current}")

# 设置亮度（0-1之间）
brightness.set_level(0.5)  # 设置为50%亮度
```

## 完整示例应用

```python
"""
一个简单的系统工具应用示例
"""
import tkinter as tk
from tkinter import ttk, messagebox
from plyer import notification, filechooser, battery, tts
import threading

class SystemToolsApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Plyer 系统工具演示")
        self.root.geometry("500x400")

        self.create_widgets()

    def create_widgets(self):
        # 标题
        title = ttk.Label(self.root, text="Plyer 功能演示",
                         font=("Arial", 16, "bold"))
        title.pack(pady=10)

        # 通知功能
        notif_frame = ttk.LabelFrame(self.root, text="通知功能", padding=10)
        notif_frame.pack(fill="x", padx=20, pady=5)

        self.notif_entry = ttk.Entry(notif_frame, width=40)
        self.notif_entry.insert(0, "输入通知内容")
        self.notif_entry.pack(side="left", padx=5)

        ttk.Button(notif_frame, text="发送通知",
                  command=self.send_notification).pack(side="left")

        # 文件选择
        file_frame = ttk.LabelFrame(self.root, text="文件操作", padding=10)
        file_frame.pack(fill="x", padx=20, pady=5)

        ttk.Button(file_frame, text="选择文件",
                  command=self.choose_file).pack(side="left", padx=5)
        ttk.Button(file_frame, text="选择目录",
                  command=self.choose_directory).pack(side="left", padx=5)

        # TTS功能
        tts_frame = ttk.LabelFrame(self.root, text="文字转语音", padding=10)
        tts_frame.pack(fill="x", padx=20, pady=5)

        self.tts_entry = ttk.Entry(tts_frame, width=40)
        self.tts_entry.insert(0, "输入要朗读的文字")
        self.tts_entry.pack(side="left", padx=5)

        ttk.Button(tts_frame, text="朗读",
                  command=self.speak_text).pack(side="left")

        # 系统信息
        info_frame = ttk.LabelFrame(self.root, text="系统信息", padding=10)
        info_frame.pack(fill="x", padx=20, pady=5)

        ttk.Button(info_frame, text="获取电池信息",
                  command=self.get_battery_info).pack(side="left", padx=5)

        # 输出区域
        output_frame = ttk.LabelFrame(self.root, text="输出信息", padding=10)
        output_frame.pack(fill="both", expand=True, padx=20, pady=5)

        self.output_text = tk.Text(output_frame, height=8, width=60)
        self.output_text.pack(fill="both", expand=True)

        # 滚动条
        scrollbar = ttk.Scrollbar(output_frame, command=self.output_text.yview)
        scrollbar.pack(side="right", fill="y")
        self.output_text.config(yscrollcommand=scrollbar.set)

    def log_output(self, message):
        """向输出区域添加日志"""
        self.output_text.insert("end", f"{message}\n")
        self.output_text.see("end")

    def send_notification(self):
        """发送系统通知"""
        message = self.notif_entry.get()
        try:
            notification.notify(
                title="演示通知",
                message=message,
                app_name="Plyer Demo",
                timeout=5
            )
            self.log_output(f"✓ 通知已发送: {message}")
        except Exception as e:
            self.log_output(f"✗ 发送通知失败: {e}")

    def choose_file(self):
        """选择文件"""
        try:
            selection = filechooser.open_file(title="选择文件")
            if selection:
                self.log_output(f"✓ 选择的文件: {selection[0]}")
            else:
                self.log_output("✗ 未选择文件")
        except Exception as e:
            self.log_output(f"✗ 文件选择失败: {e}")

    def choose_directory(self):
        """选择目录"""
        try:
            selection = filechooser.choose_dir(title="选择目录")
            if selection:
                self.log_output(f"✓ 选择的目录: {selection[0]}")
            else:
                self.log_output("✗ 未选择目录")
        except Exception as e:
            self.log_output(f"✗ 目录选择失败: {e}")

    def speak_text(self):
        """文字转语音"""
        text = self.tts_entry.get()
        try:
            # 在新线程中执行TTS，避免阻塞UI
            threading.Thread(target=lambda: tts.speak(text)).start()
            self.log_output(f"✓ 正在朗读: {text}")
        except Exception as e:
            self.log_output(f"✗ TTS失败: {e}")

    def get_battery_info(self):
        """获取电池信息"""
        try:
            status = battery.status
            if status:
                info = []
                if status.get('isCharging') is not None:
                    charging = "充电中" if status['isCharging'] else "未充电"
                    info.append(f"状态: {charging}")
                if status.get('percentage') is not None:
                    info.append(f"电量: {status['percentage']}%")

                if info:
                    self.log_output(f"✓ 电池信息: {', '.join(info)}")
                else:
                    self.log_output("✗ 无法获取电池信息")
            else:
                self.log_output("✗ 该平台不支持电池信息获取")
        except Exception as e:
            self.log_output(f"✗ 获取电池信息失败: {e}")

def main():
    root = tk.Tk()
    app = SystemToolsApp(root)
    root.mainloop()

if __name__ == "__main__":
    main()
```

## 跨平台注意事项

### Windows
- 通知功能需要 Windows 10/11
- 图标文件必须是 `.ico` 格式
- 某些功能可能需要管理员权限

### macOS
- 需要系统权限授权（如通知、相机等）
- 使用 `osascript` 实现某些功能
- 图标支持 `.icns` 格式

### Linux
- 通知功能依赖 `notify-send`
- 某些发行版需要安装额外包
- 桌面环境影响功能可用性

### Android
- 需要在 `buildozer.spec` 中声明权限
- 使用 Kivy 或 BeeWare 打包
- 某些功能需要运行时权限请求

```python
# Android 权限示例（buildozer.spec）
android.permissions = INTERNET, CAMERA, VIBRATE, READ_EXTERNAL_STORAGE, WRITE_EXTERNAL_STORAGE, ACCESS_FINE_LOCATION
```

### iOS
- 需要在 Info.plist 中声明权限
- 某些功能需要用户授权
- 必须通过 Xcode 编译部署

## 错误处理最佳实践

```python
from plyer import notification
from plyer.utils import platform

def safe_notify(title, message):
    """安全的通知函数，包含错误处理"""
    try:
        # 检查平台
        if platform == 'win':
            # Windows特定处理
            notification.notify(
                title=title[:64],  # Windows标题长度限制
                message=message[:256],  # Windows消息长度限制
                timeout=10
            )
        else:
            # 其他平台
            notification.notify(
                title=title,
                message=message,
                timeout=10
            )
        return True
    except NotImplementedError:
        print(f"通知功能在 {platform} 平台上不可用")
        return False
    except Exception as e:
        print(f"发送通知时出错: {e}")
        return False

# 使用示例
if not safe_notify("测试", "这是一条测试消息"):
    print("使用备用方案...")
    # 实现备用通知方案
```

## 自定义实现

如果 Plyer 没有提供某个平台的实现，可以自定义：

```python
from plyer.facades import UniqueID
from plyer.utils import platform

class WindowsUniqueID(UniqueID):
    def _get_uid(self):
        """Windows平台获取唯一ID的实现"""
        import subprocess
        try:
            output = subprocess.check_output(
                'wmic csproduct get UUID',
                shell=True
            ).decode()
            return output.split('\n')[1].strip()
        except:
            return None

# 注册自定义实现
if platform == 'win':
    from plyer import uniqueid
    uniqueid._uniqueid = WindowsUniqueID()
```

## 常见问题

### Q1: ImportError: No module named 'plyer'
**解决方案**：确保已安装 plyer
```bash
pip install --upgrade plyer
```

### Q2: NotImplementedError
**原因**：当前平台不支持该功能
**解决方案**：检查平台兼容性，使用 try-except 处理

### Q3: 权限被拒绝
**解决方案**：
- Android: 在 buildozer.spec 中添加权限
- iOS: 在 Info.plist 中添加权限描述
- macOS: 系统偏好设置中授权
- Windows: 以管理员身份运行

### Q4: 通知不显示
**可能原因**：
1. Windows: 焦点助手/勿扰模式开启
2. macOS: 通知中心设置问题
3. Linux: 缺少 notify-send

### Q5: TTS 无声音
**解决方案**：
- Windows: 检查系统 TTS 引擎
- Linux: 安装 espeak 或 festival
- macOS: 检查系统语音设置

## 实战项目示例

### 项目1：桌面提醒工具

```python
"""
定时提醒工具
"""
import schedule
import time
from plyer import notification
from datetime import datetime
import json

class ReminderApp:
    def __init__(self):
        self.reminders = []
        self.load_reminders()

    def load_reminders(self):
        """加载提醒配置"""
        try:
            with open('reminders.json', 'r', encoding='utf-8') as f:
                self.reminders = json.load(f)
        except FileNotFoundError:
            # 默认提醒
            self.reminders = [
                {"time": "09:00", "message": "开始工作"},
                {"time": "12:00", "message": "午餐时间"},
                {"time": "15:00", "message": "休息一下"},
                {"time": "18:00", "message": "下班时间"}
            ]
            self.save_reminders()

    def save_reminders(self):
        """保存提醒配置"""
        with open('reminders.json', 'w', encoding='utf-8') as f:
            json.dump(self.reminders, f, ensure_ascii=False, indent=2)

    def send_reminder(self, message):
        """发送提醒通知"""
        notification.notify(
            title="定时提醒",
            message=message,
            app_name="Reminder",
            timeout=10
        )
        print(f"[{datetime.now().strftime('%H:%M:%S')}] 提醒: {message}")

    def setup_schedule(self):
        """设置定时任务"""
        for reminder in self.reminders:
            schedule.every().day.at(reminder['time']).do(
                self.send_reminder,
                reminder['message']
            )
        print(f"已设置 {len(self.reminders)} 个提醒")

    def run(self):
        """运行提醒服务"""
        self.setup_schedule()
        print("提醒服务已启动...")

        while True:
            schedule.run_pending()
            time.sleep(1)

if __name__ == "__main__":
    app = ReminderApp()
    app.run()
```

### 项目2：系统监控工具

```python
"""
系统资源监控工具
"""
import psutil
import time
from plyer import notification, battery
import threading

class SystemMonitor:
    def __init__(self):
        self.cpu_threshold = 80  # CPU使用率阈值
        self.memory_threshold = 85  # 内存使用率阈值
        self.battery_low = 20  # 低电量阈值
        self.check_interval = 60  # 检查间隔（秒）

    def check_cpu(self):
        """检查CPU使用率"""
        cpu_percent = psutil.cpu_percent(interval=1)
        if cpu_percent > self.cpu_threshold:
            notification.notify(
                title="CPU 使用率警告",
                message=f"CPU 使用率已达 {cpu_percent}%",
                timeout=10
            )
            return False
        return True

    def check_memory(self):
        """检查内存使用率"""
        memory = psutil.virtual_memory()
        if memory.percent > self.memory_threshold:
            notification.notify(
                title="内存使用警告",
                message=f"内存使用率已达 {memory.percent}%\n"
                       f"可用: {memory.available / (1024**3):.1f} GB",
                timeout=10
            )
            return False
        return True

    def check_battery(self):
        """检查电池状态"""
        try:
            status = battery.status
            if status and status.get('percentage'):
                if status['percentage'] < self.battery_low:
                    if not status.get('isCharging'):
                        notification.notify(
                            title="电池电量低",
                            message=f"电量仅剩 {status['percentage']}%\n"
                                   f"请连接充电器",
                            timeout=10
                        )
                        return False
        except:
            pass
        return True

    def check_disk(self):
        """检查磁盘空间"""
        for partition in psutil.disk_partitions():
            try:
                usage = psutil.disk_usage(partition.mountpoint)
                if usage.percent > 90:
                    notification.notify(
                        title="磁盘空间警告",
                        message=f"磁盘 {partition.mountpoint} 使用率: {usage.percent}%\n"
                               f"剩余: {usage.free / (1024**3):.1f} GB",
                        timeout=10
                    )
                    return False
            except:
                continue
        return True

    def monitor_loop(self):
        """监控循环"""
        print("系统监控已启动...")

        while True:
            all_ok = True

            # 执行各项检查
            all_ok &= self.check_cpu()
            all_ok &= self.check_memory()
            all_ok &= self.check_battery()
            all_ok &= self.check_disk()

            if all_ok:
                print(f"[{time.strftime('%H:%M:%S')}] 系统运行正常")

            time.sleep(self.check_interval)

    def start(self):
        """启动监控"""
        monitor_thread = threading.Thread(target=self.monitor_loop)
        monitor_thread.daemon = True
        monitor_thread.start()

        # 保持主线程运行
        try:
            while True:
                time.sleep(1)
        except KeyboardInterrupt:
            print("\n监控已停止")

if __name__ == "__main__":
    monitor = SystemMonitor()
    monitor.start()
```

## 总结

Plyer 是一个强大的跨平台 Python 库，能够让开发者轻松访问各种系统功能。主要优势：

1. **统一API**：不同平台使用相同的接口
2. **易于使用**：简洁的 API 设计
3. **广泛支持**：覆盖主流桌面和移动平台
4. **持续更新**：活跃的社区和维护

适用场景：
- 桌面应用开发
- 移动应用开发（配合 Kivy/BeeWare）
- 系统工具开发
- 自动化脚本
- 跨平台项目

## 参考资源

- [Plyer 官方文档](https://plyer.readthedocs.io/)
- [GitHub 仓库](https://github.com/kivy/plyer)
- [API 参考](https://plyer.readthedocs.io/en/latest/api.html)
- [示例代码](https://github.com/kivy/plyer/tree/master/examples)

## 更新日志

- **v2.1.0** - 添加更多平台支持
- **v2.0.0** - 重构API，提升性能
- **v1.4.3** - 修复Windows通知问题
- **v1.4.0** - 新增多个硬件访问功能

---

*本教程持续更新中，欢迎提供反馈和建议！*
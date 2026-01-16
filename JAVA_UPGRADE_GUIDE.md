# Java 11 升级指南

## 当前状态
- 当前 Java 版本：Java 8 (1.8.0_101)
- 需要升级到：Java 11 或更高版本

## 推荐版本
**Java 11 LTS (长期支持版本)**
- 支持到 2026 年 9 月
- 稳定可靠，适合生产环境
- 完全满足 Android 构建需求

## 下载地址

### 方案1：Oracle JDK 11（推荐）
1. 访问：https://www.oracle.com/java/technologies/javase/jdk11-archive-downloads.html
2. 向下滚动找到 "Java SE 11.0.xx" 部分
3. 选择 Windows x64 Installer
4. 下载 .exe 安装文件

### 方案2：OpenJDK 11（免费开源）
1. 访问：https://adoptium.net/temurin/releases/?version=11
2. 选择：
   - Version: 11 (LTS)
   - Operating System: Windows
   - Architecture: x64
   - Package Type: JDK
   - Download Type: .msi (安装程序)
3. 点击下载

## 安装步骤

### 1. 安装 JDK
1. 双击下载的安装文件
2. 点击"下一步"
3. 选择安装路径（建议：`C:\Program Files\Java\jdk-11`）
4. 等待安装完成
5. 点击"关闭"

### 2. 配置环境变量

#### 方法1：通过系统设置（推荐）
1. 右键点击"此电脑" → "属性"
2. 点击"高级系统设置"
3. 点击"环境变量"
4. 在"系统变量"中：
   - 新建变量：
     - 变量名：`JAVA_HOME`
     - 变量值：`C:\Program Files\Java\jdk-11`（根据实际安装路径）
   - 编辑 `Path` 变量：
     - 添加：`%JAVA_HOME%\bin`
     - 将其移到列表顶部
5. 点击"确定"保存所有设置

#### 方法2：通过 PowerShell（快速）
```powershell
# 设置 JAVA_HOME
[System.Environment]::SetEnvironmentVariable('JAVA_HOME', 'C:\Program Files\Java\jdk-11', 'Machine')

# 添加到 PATH
$path = [System.Environment]::GetEnvironmentVariable('Path', 'Machine')
$newPath = 'C:\Program Files\Java\jdk-11\bin;' + $path
[System.Environment]::SetEnvironmentVariable('Path', $newPath, 'Machine')
```

### 3. 验证安装

**重要**：需要重启终端或重新登录才能使环境变量生效

1. 打开新的 PowerShell 窗口
2. 运行：
```powershell
java -version
```

应该看到类似输出：
```
java version "11.0.xx"
Java(TM) SE Runtime Environment (build 11.0.xx+xx)
Java HotSpot(TM) 64-Bit Server VM (build 11.0.xx+xx, mixed mode)
```

## 构建 APK

安装 Java 11 后，在项目目录运行：

```powershell
cd android
.\gradlew assembleDebug
```

构建成功后，APK 文件位于：
```
android/app/build/outputs/apk/debug/app-debug.apk
```

## 常见问题

### Q1: 安装后仍然显示 Java 8？
**A**: 需要重启终端或重新登录电脑，环境变量才会生效。

### Q2: 如何切换回 Java 8？
**A**: 修改 JAVA_HOME 环境变量指向 Java 8 路径即可。

### Q3: 可以同时安装多个 Java 版本吗？
**A**: 可以。安装多个版本后，通过修改 JAVA_HOME 环境变量来切换。

### Q4: 构建仍然失败？
**A**: 检查是否安装了 Android SDK 和必要的构建工具：
- Android SDK Platform-Tools
- Android SDK Build-Tools

## 下一步

安装 Java 11 后，运行以下命令构建 APK：

```powershell
cd C:\库存管理\android
.\gradlew assembleDebug
```

需要帮助？请告诉我安装过程中遇到的问题。

# GitHub Actions 构建指南

## 已完成的工作

✅ 创建了 GitHub Actions 工作流配置文件  
✅ 创建了 .gitignore 文件  
✅ 配置了自动构建流程  

## 需要安装 Git

你的系统还没有安装 Git。需要先安装 Git 才能推送到 GitHub。

### 安装 Git

1. **下载 Git**
   - 访问：https://git-scm.com/download/win
   - 下载 Windows 版本（64-bit）

2. **安装 Git**
   - 双击下载的安装文件
   - 点击 "Next" 使用默认设置
   - 在 "Choosing HTTPS transport backend" 选择 "Use the OpenSSL library"
   - 其他选项保持默认
   - 点击 "Install" 安装
   - 安装完成后点击 "Finish"

3. **验证安装**
   打开新的 PowerShell 窗口，运行：
   ```powershell
   git --version
   ```
   应该看到版本号，如：`git version 2.xx.x`

## 推送到 GitHub

### 步骤1：创建 GitHub 仓库

1. 访问 https://github.com/new
2. 仓库名称：`inventory-management`
3. 设置为 Public 或 Private（都可以）
4. 不要勾选 "Initialize this repository with a README"
5. 点击 "Create repository"

### 步骤2：配置 Git

在 PowerShell 中运行（替换你的用户名和邮箱）：

```powershell
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱@example.com"
```

### 步骤3：初始化并提交

```powershell
cd C:\库存管理
git init
git add .
git commit -m "Initial commit - Inventory Management App"
```

### 步骤4：推送到 GitHub

```powershell
git remote add origin https://github.com/你的用户名/inventory-management.git
git branch -M main
git push -u origin main
```

## 自动构建

推送成功后，GitHub Actions 会自动开始构建！

### 查看构建进度

1. 访问你的 GitHub 仓库
2. 点击 "Actions" 标签
3. 可以看到正在运行的工作流
4. 构建通常需要 5-10 分钟

### 下载 APK

构建完成后：

1. 在 Actions 页面点击构建任务
2. 滚动到底部 "Artifacts" 部分
3. 点击 "app-debug" 下载 ZIP 文件
4. 解压后得到 `app-debug.apk`

## 手动触发构建

如果不想推送代码，也可以手动触发：

1. 访问 GitHub 仓库
2. 点击 "Actions" 标签
3. 选择 "Build Android APK" 工作流
4. 点击 "Run workflow" → "Run workflow"

## 更新应用

每次修改代码后：

```powershell
cd C:\库存管理
git add .
git commit -m "描述你的更改"
git push
```

推送后自动触发构建！

## 工作流配置说明

已创建的 `.github/workflows/android.yml` 包含：

- **触发条件**：推送到 main 分支或手动触发
- **构建环境**：Ubuntu 最新版
- **Node.js**：版本 18
- **构建类型**：Debug 版本
- **APK 保留**：30 天

## 构建输出

构建成功后，APK 文件位于：
```
android/app/build/outputs/apk/debug/app-debug.apk
```

## 免费额度

GitHub Actions 免费计划：
- 每月 2000 分钟构建时间
- 公开仓库：无限分钟
- 私有仓库：2000 分钟/月

完全够用！

## 常见问题

### Q1: 构建失败怎么办？
**A**: 在 Actions 页面查看错误日志，常见问题：
- 依赖安装失败：检查 package.json
- 构建错误：检查代码语法
- 权限问题：检查仓库设置

### Q2: 如何构建 Release 版本？
**A**: 修改工作流文件，将 `assembleDebug` 改为 `assembleRelease`

### Q3: 可以同时构建 iOS 吗？
**A**: 可以，但需要 macOS runner 或配置自托管 runner

### Q4: 如何自定义应用图标和启动页？
**A**: 在 Appflow 中配置，或使用 Capacitor 资源插件

## 下一步

1. 安装 Git
2. 创建 GitHub 仓库
3. 推送代码
4. 等待自动构建完成
5. 下载 APK 安装到手机

需要帮助？告诉我安装 Git 或推送代码时遇到的问题！

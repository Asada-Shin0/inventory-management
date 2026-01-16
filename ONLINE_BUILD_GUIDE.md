# 使用 Ionic Appflow 在线构建 APK

## 为什么选择 Ionic Appflow？

✅ 与 Capacitor 完美集成  
✅ 无需配置本地环境  
✅ 自动化构建流程  
✅ 支持多平台（Android、iOS）  
✅ 免费额度足够个人使用  

## 准备工作

### 1. 注册账号
1. 访问：https://ionic.io/appflow
2. 点击 "Sign Up" 注册账号
3. 可以使用 GitHub、Google 或邮箱注册

### 2. 连接 Git 仓库
Appflow 需要从 Git 仓库拉取代码。

#### 方案A：使用 GitHub（推荐）
1. 在 GitHub 创建新仓库
2. 将本地代码推送到 GitHub

#### 方案B：使用本地 Git
1. 初始化本地 Git 仓库
2. 推送到远程仓库

## 详细步骤

### 步骤1：初始化 Git 仓库

```powershell
cd C:\库存管理
git init
git add .
git commit -m "Initial commit"
```

### 步骤2：推送到 GitHub

1. 在 GitHub 创建新仓库（名称：inventory-management）
2. 复制仓库 URL
3. 运行：

```powershell
git remote add origin https://github.com/你的用户名/inventory-management.git
git branch -M main
git push -u origin main
```

### 步骤3：在 Appflow 创建应用

1. 登录 Appflow：https://ionic.io/appflow
2. 点击 "New App"
3. 选择 "Import from GitHub"
4. 选择刚创建的仓库
5. 配置应用信息：
   - App Name: 库存管理系统
   - Icon: 可以稍后上传
   - Splash Screen: 可以稍后上传

### 步骤4：配置构建

1. 在 Appflow 中选择你的应用
2. 点击 "Builds" → "Android Builds"
3. 点击 "New Build"
4. 配置构建选项：
   - **Build Type**: Debug（测试）或 Release（正式发布）
   - **Platform**: Android
   - **Native Config**: 使用现有的 capacitor.config.json
5. 点击 "Start Build"

### 步骤5：下载 APK

1. 等待构建完成（通常 5-10 分钟）
2. 构建完成后，点击 "Download"
3. 下载 APK 文件到本地

## 免费额度

Appflow 免费计划：
- 每月 10 次构建
- 团队成员：1 人
- 存储空间：1 GB

对于个人项目完全够用！

## 更新应用

每次修改代码后：

1. 提交更改：
```powershell
git add .
git commit -m "Update features"
git push
```

2. 在 Appflow 点击 "New Build" 重新构建

## 替代方案：GitHub Actions

如果你有 GitHub 账号，也可以使用 GitHub Actions：

### 1. 创建工作流文件

在项目根目录创建 `.github/workflows/android.yml`：

```yaml
name: Build Android APK

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          
      - name: Install dependencies
        run: npm ci
        
      - name: Build Android
        run: |
          npm install -g @capacitor/cli
          npx cap sync android
          cd android
          ./gradlew assembleDebug
          
      - name: Upload APK
        uses: actions/upload-artifact@v3
        with:
          name: app-debug
          path: android/app/build/outputs/apk/debug/app-debug.apk
```

### 2. 推送到 GitHub

```powershell
git add .
git commit -m "Add GitHub Actions workflow"
git push
```

### 3. 触发构建

- 推送代码后自动构建
- 或在 GitHub Actions 页面手动触发

## 对比

| 特性 | Appflow | GitHub Actions |
|------|----------|---------------|
| 易用性 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| 配置难度 | 简单 | 中等 |
| 免费额度 | 10次/月 | 2000分钟/月 |
| 多平台支持 | 是 | 需要配置 |
| iOS 构建 | 支持 | 需要Mac |

## 推荐方案

**如果你是新手**：使用 Appflow，配置简单，界面友好

**如果你熟悉 GitHub**：使用 GitHub Actions，完全免费，更灵活

## 需要帮助？

如果需要我帮你配置具体的构建方案，请告诉我：
1. 你选择哪个平台（Appflow 或 GitHub Actions）
2. 你是否有 GitHub 账号
3. 你需要 Debug 版本还是 Release 版本

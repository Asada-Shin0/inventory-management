# 库存管理系统 - 安卓APP打包说明

## 当前状态

已成功初始化 Capacitor 项目并添加了 Android 平台支持。

## 需要的环境

### 1. Java 11 或更高版本
当前系统使用的是 Java 8，需要升级到 Java 11 或更高版本。

**下载地址**：
- Oracle JDK 11: https://www.oracle.com/java/technologies/javase/jdk11-archive-downloads.html
- OpenJDK 11: https://adoptium.net/temurin/releases/?version=11

**安装步骤**：
1. 下载并安装 JDK 11
2. 配置 JAVA_HOME 环境变量
3. 更新 PATH 环境变量

### 2. Android SDK
需要安装 Android SDK 和构建工具。

**推荐使用 Android Studio**：
- 下载地址：https://developer.android.com/studio
- 安装后自动配置 Android SDK

## 项目结构

```
库存管理/
├── index.html              # 原始HTML文件
├── www/
│   └── index.html         # 复制到www目录的文件
├── android/               # Android项目目录
│   ├── app/
│   ├── build.gradle
│   └── gradlew           # Gradle构建脚本
├── capacitor.config.json    # Capacitor配置
└── package.json           # Node.js依赖
```

## 构建步骤

### 1. 同步代码到Android项目
```bash
npx cap sync android
```

### 2. 构建APK
```bash
cd android
.\gradlew assembleDebug
```

构建成功后，APK文件位于：
```
android/app/build/outputs/apk/debug/app-debug.apk
```

### 3. 安装到手机
- 将 APK 文件传输到手机
- 在手机上点击安装
- 或使用 `adb install android/app/build/outputs/apk/debug/app-debug.apk`

## 更新应用

每次修改 index.html 后：
1. 将修改复制到 www/index.html
2. 运行 `npx cap sync android`
3. 重新构建 APK

## 注意事项

1. **数据存储**：应用使用 localStorage，数据存储在应用内部
2. **导出功能**：在Android中导出文件需要文件权限
3. **应用签名**：debug版本仅用于测试，正式发布需要签名

## 替代方案：使用在线构建服务

如果不想配置本地环境，可以使用：
- **Appflow** (Ionic官方)：https://ionic.io/appflow
- **Codemagic**：https://codemagic.io
- **GitHub Actions**：配置自动化构建

## 联系支持

如有问题，请查看：
- Capacitor文档：https://capacitorjs.com/docs
- Android开发文档：https://developer.android.com/docs

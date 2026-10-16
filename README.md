# Welcome App

使用 Kotlin、Jetpack Compose Material 3 和 Gradle Kotlin DSL 的单模块 Android 欢迎应用。支持系统深浅色主题、系统栏安全区域和内容滚动。

## 本地构建

需要 JDK 17、Gradle 8.9 和 Android SDK（Platform 35、Build Tools 35.0.0）；最低支持 Android 6.0（API 23）。

1. 用 Android Studio 打开仓库根目录，选择 JDK 17，并在 SDK Manager 安装以上 SDK 包。
2. 配置 `ANDROID_HOME`，或在不纳入版本控制的 `local.properties` 中设置 `sdk.dir=/你的/Android/Sdk`。
3. 安装 Gradle 8.9 后，在根目录执行：

```sh
gradle --no-daemon :app:assembleDebug :app:lintDebug
```

APK 路径：`app/build/outputs/apk/debug/app-debug.apk`。

连接 Android 设备或启动模拟器后安装并打开：

```sh
adb install -r app/build/outputs/apk/debug/app-debug.apk
adb shell am start -n com.example.welcome/.MainActivity
```

项目固定 AGP 8.7.3、Kotlin/Compose 编译器插件 2.0.21、Compose BOM 2024.12.01。当前不包含 Gradle Wrapper；命令使用 Gradle 8.9，CI 由 setup-gradle 安装该版本。可以使用 `gradle wrapper --gradle-version 8.9 --distribution-type bin` 生成标准 Wrapper 并提交生成文件。

## GitHub Actions

Push、Pull Request 和手动触发都会安装 JDK、Android SDK 与固定版本的 Gradle，执行 Debug APK 构建及 Android Lint。成功后可在对应 Actions 运行页面的 Artifacts 下载 `welcome-app-debug`。Debug APK 使用默认调试签名，仅供开发安装。

## 当前验证状态

已通过 GitHub Actions 执行 `:app:assembleDebug :app:lintDebug`，并成功上传 Debug APK：[构建记录](https://github.com/alexwuhao2001-gif/alexwuhao/actions/runs/38933430150)。

本地创建环境没有 Gradle 和 Android SDK，且网络代理不可达；尚未执行设备或模拟器运行验证。

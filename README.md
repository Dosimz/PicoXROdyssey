### 在 Pico4 上运行示例 demo
- 开发环境准备
- demo 代码运行

### 开发环境准备
下载 Android Studio 并通过其安装 Android SDK、相应的 NDK 以进行 Pico4 设备上的原生 c++ 混合应用开发。

> 注意问题 ⚠️：
> Android sdk、 Cmake、 JDK 等开发环境版本和项目代码中使用的版本对应。  
> `Could not GET ‘https://dl.google.com/dl/android/maven2/com/android/tools/b***.pom` 报错解决办法，取消 Android Studio 代理设置，在 gradle.property(global) 中注释掉代理设置代码，重启 Android Studio.

### demo 代码运行
从 pico4 开发者官网下载原生开发的 Pico_openXR_SDK 文件，其中包含对应 pico4 版本的 helloXR 项目。

使用 Android Studio 打开该项目，构建 gradle 运行环境。

连接 pico4 物理设备到电脑，检测到设备后，点击运行。
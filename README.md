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


### 项目浅识
- 一级目录文件及其作用
```
├── CMakeLists.txt  // CMake 构建系统的配置文件
├── build  // 这个目录通常是构建过程中生成的。包含编译后的代码、生成的资源文件和构建过程中产生的文件
├── build.gradle  //Gradle 构建脚本。它定义了项目的构建过程、依赖关系和所需的插件等
├── gradle
├── gradle.properties
├── gradlew
├── gradlew.bat
├── hello_xr    // 主要包含源代码
├── local.properties // 本地机器特定的配置，比如 Android SDK 和 NDK 的路径
├── openxr_loader
└── settings.gradle    // 配置整个 Gradle 项目的设置
```
- 源代码目录文件
```
├── AndroidManifest.xml
├── CMakeLists.txt
├── check.h
├── common.h
├── d3d_common.cpp
├── d3d_common.h
├── geometry.h
├── graphicsapi.h
├── graphicsplugin.h
├── graphicsplugin_d3d11.cpp
├── graphicsplugin_d3d12.cpp
├── graphicsplugin_factory.cpp
├── graphicsplugin_opengl.cpp
├── graphicsplugin_opengles.cpp
├── graphicsplugin_vulkan.cpp
├── hello_xr.1
├── java
├── logger.cpp
├── logger.h
├── main.cpp
├── openxr_program.cpp
├── openxr_program.h
├── options.h
├── pch.cpp
├── pch.h
├── platformdata.h
├── platformplugin.h
├── platformplugin_android.cpp
├── platformplugin_factory.cpp
├── platformplugin_win32.cpp
├── platformplugin_xlib.cpp
└── vulkan_shaders
```

这些文件是你的 `hello_xr` 项目的核心组成部分，每个文件都有其特定的用途和功能。

### 基本文件
- **`AndroidManifest.xml`**: 这是 Android 应用的清单文件，定义了应用的基本特性，如权限、活动（Activities）和服务（Services）等。
- **`CMakeLists.txt`**: CMake 配置文件，用于指导项目的编译和构建过程。

### 头文件和实现文件
- **`check.h`, `common.h`, `geometry.h`, `graphicsapi.h`, `graphicsplugin.h`, `options.h`, `pch.h`, `platformdata.h`, `platformplugin.h`**: 这些 `.h` 文件是 C++ 头文件，定义了类、函数原型和其他类型的声明。
- **`d3d_common.cpp`, `graphicsplugin_d3d11.cpp`, `graphicsplugin_d3d12.cpp`, `graphicsplugin_factory.cpp`, `graphicsplugin_opengl.cpp`, `graphicsplugin_opengles.cpp`, `graphicsplugin_vulkan.cpp`, `logger.cpp`, `main.cpp`, `openxr_program.cpp`, `platformplugin_android.cpp`, `platformplugin_factory.cpp`, `platformplugin_win32.cpp`, `platformplugin_xlib.cpp`, `pch.cpp`**: 这些 `.cpp` 文件包含了上述头文件中声明的函数和类的具体实现。

### 特定功能文件
- **`d3d_common.cpp/h`**: 可能包含与 Direct3D（一种图形接口）相关的通用函数和定义。
- **`graphicsplugin_*.cpp`**: 这些文件可能是针对不同图形 API（如 Direct3D 11, Direct3D 12, OpenGL, Vulkan 等）的实现。
- **`logger.cpp/h`**: 定义了日志记录功能，用于记录程序运行时的信息。
- **`openxr_program.cpp/h`**: 这些文件可能与 OpenXR API 的使用有关，用于创建和管理 VR/AR 体验。
- **`platformplugin_*.cpp`**: 这些文件可能是针对不同平台（如 Android, Windows, Xlib 等）的特定功能实现。
- **`vulkan_shaders`**: 这个目录可能包含用于 Vulkan 图形 API 的着色器代码。

### 其他文件
- **`hello_xr.1`**: 这可能是一个文档文件，例如 man page（手册页）。
- **`java` 目录**: 包含 Java 源代码，通常用于 Android 应用的 Java 层实现。

每个文件都是项目的一部分，共同协作以实现 VR/AR 应用的功能。🌟📚

### main.cpp 代码逻辑

如果定义了 XR_USE_PLATFORM_ANDROID，即程序在 Android 平台上运行，代码将执行以下操作：

ShowHelp() 和 UpdateOptionsFromSystemProperties() 函数提供了帮助信息，并从系统属性中更新配置选项。
AndroidAppState 结构体和 app_handle_cmd() 函数用于处理 Android 应用的生命周期事件。
android_main() 函数是 Android 应用的入口点，它初始化了 OpenXR 程序，并且循环处理事件和渲染帧。


创建和初始化 OpenXR 程序：无论是在 Android 还是其他平台上，代码都会创建和初始化一个 OpenXR 程序。这包括创建实例、初始化系统、创建会话和交换链。
事件循环：程序进入一个循环，不断处理事件、轮询动作，并渲染新的帧。这个循环是 VR 应用的核心，确保了持续的用户交互和图形更新。
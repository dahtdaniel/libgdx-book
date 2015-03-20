### 新建libgdx项目
Libgdx提供了一个初始化工具 `gdx-setup.jar` ，包含了一个可执行的UI和命令行模式。直接执行该文件你就可以看到该工具界面。

如果你希望从命令行启动，使用命令: `java -jar gdx-setup.jar`

## [下载gdx-setup.jar](https://bitly.com/1i3C7i3)

指定你的应用名称，Java包名以及启动类名称，输出目录和Android SDK目录。

然后选择你希望支持的平台。
**提示: 一旦项目生成，你只能手动自行添加新的平台支持!**。

Libgdx提供了一些扩展，有部分扩展不能兼容所有平台，对于这些扩展，一旦你选择以后软件会给出你提示。

一切完成后点击"Generate"。

**项目文件生成后，你就可以导入到IDE并运行和调试了。**

  * [[Eclipse|Eclipse]]
  * [[Intellij IDEA|Intellij-Idea]]
  * [[NetBeans|NetBeans]]
  * [[Commandline|Commandline]]

点击"Advanced"按钮可以设置是否生成Eclipse或者IDEA项目文件，也可以设置一个依赖仓库的镜像去下载依赖包。

国内访问Maven中央仓库有时候很慢，可以考虑使用oschina提供的镜像服务。

[[../Images/gdx-setup.png]]


### 使用命令行创建Libgdx项目

如果你不喜欢使用UI界面，或者不具备使用UI界面的条件，你可以使用命令行直接调用创建工具。

命令行参数有以下几个：

* **dir**: 项目地址，绝对路径和相对路径都可以
* **name**: 项目的名字
* **package**: Java包名，比如com.badlogic.mygame
* **mainClass**: 启动类的名称，比如MyGame
* **sdkLocation**: Android SDK地址

提供以上参数即可创建项目，比如:

`java -jar gdx-setup.jar --dir mygame --name mygame --package com.badlogic.mygame --mainClass MyGame --sdkLocation mySdkLocation`

### 项目结构

创建好的项目结构如下：

```
settings.gradle            <- 定义子模块，比如core, desktop, android, html, ios
build.gradle               <- Gradle的主要配置文件，声明了依赖和插件
gradlew                    <- Gradle在Unix 环境的执行脚本
gradlew.bat                <- Gradle在Windows 环境的执行脚本
gradle                     <- 本地包装器
local.properties           <- Intellij专有配置文件，定义android sdk位置

core/
    build.gradle           <- Gradle针对core的配置文件
    src/                   <- 项目代码，包含游戏的主要代码（平台无关）

desktop/
    build.gradle           <- Gradle针对desktop的配置文件
    src/                   <- 桌面项目的启动器和其他平台相关代码

android/
    build.gradle           <- Gradle针对android的配置文件
    AndroidManifest.xml    <- Android配置
    assets/                <- 游戏所需的所有资源文件，包括音乐，图片等等
    res/                   <- app的图标和其他资源
    src/                   <- Android项目的启动器和平台相关代码

html/
    build.gradle           <- Gradle针对html的配置文件
    src/                   <- Html项目的启动器和平台相关代码
    webapp/                <- War包模板，包含了启动页面和web.xml配置

ios/
    build.gradle           <- Gradle针对iOS的配置文件
    src/                   <- iOS项目的启动器和平台相关代码
```

生成的项目中包含了所有打包本地文件和针对不同的平台的打包分发。请小心修改这些文件，如果你熟悉Gradle和Libgdx项目，那么你可以手动添加或者修改一些任务。
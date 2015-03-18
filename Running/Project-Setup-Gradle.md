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

Note that the Advanced button lets you set the project generation to generate Eclipse and/or IDEA projects **without** Gradle integration, as described in more detail in the wiki article about [workflow without Gradle](Improving-workflow-with-Gradle#how-to-remove-gradle-ide-integration-from-your-project), as well as options to use an alternative repository to Maven Central and to not force downloading dependencies.

[[images/Screen%20Shot%202014-04-16%20at%2023.59.48-qVxlZr2zxk.png]]


### Creating a libgdx project on the command line
IF you run it from the command line, specify the following arguments.

* **dir**: the directory to write the project to, relative or absolute
* **name**: the name of the application, lower-case with minuses is usually a good idea, e.g. mygame
* **package**: the Java package under which your code will live, e.g. com.badlogic.mygame
* **mainClass**: the name of the main ApplicationListener of your app, e.g. MyGame
* **sdkLocation**: the location of your android sdk, Intellij uses this if ANDROID_HOME is not set

Putting it all together, you can run the project generator on the command line as follows:

`java -jar gdx-setup.jar --dir mygame --name mygame --package com.badlogic.mygame --mainClass MyGame --sdkLocation mySdkLocation`

### Project layout
This will create a directory called `mygame`with the following layout:

```
settings.gradle            <- definition of sub-modules. By default core, desktop, android, html, ios
build.gradle               <- main Gradle build file, defines dependencies and plugins
gradlew                    <- script that will run Gradle on Unix systems
gradlew.bat                <- script that will run Gradle on Windows
gradle                     <- local gradle wrapper
local.properties           <- Intellij only file, defines android sdk location

core/
    build.gradle           <- Gradle build file for core project*
    src/                   <- Source folder for all your game's code

desktop/
    build.gradle           <- Gradle build file for desktop project*
    src/                   <- Source folder for your desktop project, contains Lwjgl launcher class

android/
    build.gradle           <- Gradle build file for android project*
    AndroidManifest.xml    <- Android specific config
    assets/                <- contains for your graphics, audio, etc.  Shared with other projects.
    res/                   <- contains icons for your app and other resources
    src/                   <- Source folder for your Android project, contains android launcher class

html/
    build.gradle           <- Gradle build file for the html project*
    src/                   <- Source folder for your html project, contains launcher and html definition
    webapp/                <- War template, on generation the contents are copied to war. Contains startup url index page and web.xml


ios/
    build.gradle           <- Gradle build file for the ios project*
    src/                   <- Source folder for your ios project, contains launcher
```
\* These scripts contain tasks that package natives and distribute your applications on the respective platforms, you can add/maintain these tasks yourself, but only do so if you are familiar with Gradle, and what these tasks are doing, otherwise you will break your project.

### What is Gradle?
[Gradle](http://www.gradle.org/) is a dependency management and build system.

A dependency management system is an easy way to pull in 3rd party libraries into your project, without having to store the libraries in your source tree. Instead, the dependency management system relies on a file in your source tree that specifies the names and versions of the libraries you need to be included in your application. Adding, removing and changing the version of a 3rd party library is as easy as changing a few lines in that configuration file. The dependency management system will pull in the libraries you specified from a central repository (in our case [Maven Central](http://search.maven.org/)) and store them in a directory outside of your project.

A build system helps with building and packaging your application, without being tied to a specific IDE. This is especially useful if you use a build or continuous integration server, where IDEs aren't readily available. Instead, the build server can call the build system, providing it with a build configuration so it knows how to build your application for different platforms.

In case of Gradle, both dependency management and build system go hand in hand. Both are configured in the same set of files. See the [[Dependency management with Gradle]] and "Packaging" sections below for more information.
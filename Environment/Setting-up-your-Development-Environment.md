Libgdx使用 [Gradle](http://www.gradle.org/)来管理依赖，编译，构建和IDE集成。

这样你就可以在不同的开发环境开发你的游戏或者应用了。整个项目组中的成员可以任意选择自己喜欢的开发环境。不要将IDE相关的文件纳入版本控制中。
Git中的`.gitignore`可以帮助你排除不需要纳入版本控制的文件。如果你并不熟悉如何编写这个文件，你可以在github找到不同类型的项目常用的`.gitignore`例子。

不同的开发环境需要的基础环境稍有区别，这里我们简单提及，之后的章节会详细涉及怎么在不同的开发环境中开发Libgdx。

### Eclipse环境
使用Eclipse开发Libgdx项目，你需要以下软件和工具包：

  * [Java Development Kit 7+ (JDK) (6 will not work!)](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
  * [Eclipse](http://www.eclipse.org/downloads/), "Eclipse IDE for Java Developers" 是较为合适的选择。
  * [Android SDK](http://developer.android.com/sdk/installing.html), 你只需要下载SDK，不需要下载ADT。通过SDK Manager来下载对应的目标平台。
  * [Android Development Tools for Eclipse](http://developer.android.com/tools/sdk/eclipse-adt.html), 插件的安装升级地址: https://dl-ssl.google.com/android/eclipse/
  * [Eclipse Integration Gradle](https://github.com/spring-projects/eclipse-integration-gradle/), 插件的安装升级地址e: http://dist.springsource.com/snapshot/TOOLS/gradle/nightly (for Eclipse 4.4) or http://dist.springsource.com/release/TOOLS/gradle。该插件要求Eclipse版本在1.4以上。

如果你的目标平台包含iOS

  * 一个Mac，iOS的开发不能在Windows/Linux进行，谢谢苹果。
  * 最新的XCode，你可以从Mac OS X App Store免费获取。
  * [RoboVM](http://www.robovm.com/docs#robovm-for-eclipse), 安装它的Eclipse插件即可。

我个人既不喜欢Mac，如果你有其他顺手的笔记本电脑，可以考虑购买一个Mac mini作为编译和少量开发使用。

### Intellij IDEA环境
使用Intellij IDEA开发Libgdx项目，你需要以下软件和工具包：

  * [Java Development Kit 7+ (JDK) (6 will not work!)](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
  * [Intellij IDEA 14.+](http://www.jetbrains.com/idea/download/), 社区版本即可。
  * [Android SDK](http://developer.android.com/sdk/installing.html), 你只需要下载SDK，不需要下载ADT。通过SDK Manager来下载对应的目标平台。

对于iOS的环境需求，和Eclipse一样。

### NetBeans环境
使用NetBeans开发Libgdx项目，你需要以下软件和工具包：

  * [Java Development Kit 7+ (JDK) (6 will not work!)](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
  * [NetBeans 7.3+](https://netbeans.org/downloads/), "Java SE"版本即可
  * [Android SDK](http://developer.android.com/sdk/installing.html), 你只需要下载SDK，不需要下载ADT。通过SDK Manager来下载对应的目标平台。
  * [NBAndroid](http://www.nbandroid.org), 安装升级地址: http://nbandroid.org/updates/updates.xml
  * [Gradle Support for NetBeans](https://github.com/kelemen/netbeans-gradle-project), 使用NetBeans IDE升级中心。

对于iOS的环境需求，和Eclipse一样。

一旦你的环境准备就绪，你可以开始下一章。
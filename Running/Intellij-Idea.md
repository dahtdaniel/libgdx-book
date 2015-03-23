你已经生成你的libgdx项目,现在是时候开始使用IntelliJ IDEA了。
你您可以将项目导入到IntelliJ IDEA之前,请确保你设置好了你的开发环境。

## 导入项目
点击`Import Project`,定位到你的项目文件夹,然后选择`build.gradle`文件，点击`OK`。
在下一个对话框中,请将所有设置并再次单击`OK`。
IntelliJ IDEA现在开始导入你的项目。

第一次导入可能要花一段时间,因为它会下载gradle wrapper和一些依赖。

### 常见问题
如果您在使用过程中遇到缺少validation-api:1.0.0.GA的问题,删除Maven缓存，它们通常位于`C:\Users\username\.m2` 或者` /home/username/.m2`。
如果在Mac OS X上出现“Unsupported major.minor version 51.0”错误且这是你使用IntelliJ IDEA的第一个项目,请确保正确设置了JDK。

请参阅[帮助页面]((https://www.jetbrains.com/idea/help/configuring-global-project-and-module-sdks.html#d2125997e12)),或者从欢迎屏幕转到Configure -> Project Defaults -> Project Structure then add your JDK in Platform Settings -> SDKs。

如果你遇到“Error:org.gradle.tooling.GradleConnectionException：Could not execute build using Gradle installation“错误，
检查项目结构(Ctrl+Alt+Shift+S)并添加Java JDK设置。

## 运行项目

### 桌面
`Run ->Edit Configurations...`,单击加号(+)按钮,然后选择`Application`。
运行桌面程序之前，选择使用桌面的模块的classpath,然后选择desktoplauncher类作为`Main Class`。
将工作目录设置为`android/assets/`(或core/assets/)文件夹。
点击`Apply`,然后单击OK。
现在,您已经创建了一个运行的桌面项目配置。
现在,您可以选择配置并运行它。

### Android
导入项目时会自动创建一个Android项目的配置。
因此,您只需要选择配置,然后运行它即可。

### iOS
`Run ->Edit Configurations...`,单击加号(+)按钮,然后选择`Gradle`。
在gradle列表中选择launchiphonesimulator任务。你还可以选择launchIPadSimulator或者launchIOSDevicefor任务。
点击`Apply`,然后单击OK。
现在,你已经创建了一个运行iOS项目的配置。

第一次运行会花费较长的时间，因为robovm会编译整个JDK。
随后的运行编译速度将要快得多!

### HTML
选择`View -> Tool Window -> Terminal`，确保此时你位于项目根目录。
执行`gradlew.bat html:superDev` (Windows) 或者 `./gradlew html:superDev` (Linux, Mac OS X)。

这将需要一些时间,因为你的Java代码被编译为JavaScript。
一旦你看到了代码服务器已准备就绪的消息,启动你的浏览器并转到http://localhost:8080/html。
就可以看到你的应用程序在浏览器中运行。

当你更改任何Java代码或assert中的资源文件时时,只需单击“refresh”按钮，服务将重新编译你的代码并重新加载该页面。
终止该进程,只需简单地在终端窗口中按下Ctrl+C。

提示，端口9876会被GWT开发过程中会被占用。
此外,以任何其他方式尝试使用端口8080访问游戏都不会自动启动你的项目。

该进程将一直运行gradle直到被取消。
## 调试项目
请按照以下步骤操作,运行该项目,唯一区别在于不要通过运行按钮与西宁，而是启动调试按钮。
请注意,RoboVM当前不支持调试。
调试的HTML项目可以直接在浏览器操作，参考以下步骤：

* 运行superdev gradle任务。
* 跳转到[http://localhost:8080/html](http://localhost:8080/html)，点击刷新按钮。
* 在Chrome浏览器中,按下F12开启开发人员工具,请转至“Source”选项卡,然后找到你要调试的Java文件。
* 你可以设置断点、单步跟进和检查变量。

## 打包项目
最简便的方法是从命令行,或使用IntelliJ IDEA内的gradle任务打包应用程序。
相关细节查看gradle有关任务或者看到gradle命令行的文档。
你已经生成你的libgdx项目,现在是时候开始使用IntelliJ IDEA了。
你您可以将项目导入到IntelliJ IDEA之前,请确保你设置好了你的开发环境。


## 导入项目
点击`Import Project`,定位到你的项目文件夹,然后选择`build.gradle`文件。点击`OK`。
在下一个对话框中,请将所有设置并再次单击`OK`。
IntelliJ IDEA现在开始导入你的项目。
第一次导入可能要花一段时间,因为它会下载gradle wrapper和一些依赖。

### 常见问题
如果您在使用过程中遇到缺少validation-api:1.0.0.GA的问题,删除Maven缓存，它们通常位于`C:\Users\username\.m2` 或者` /home/username/.m2`。
在Mac OS X上出现“Unsupported major.minor version 51.0”错误。如果这是你使用IntelliJ IDEA的第一个项目,请确保设置了JDK。
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
现在,你已经创建了一个运行iOS项目的配置

  * **HTML**: `View -> Tool Window -> Terminal`, in the terminal, make sure you are in the root folder of your project. Then execute `gradlew.bat html:superDev` (Windows) or `./gradlew html:superDev` (Linux, Mac OS X). This will take a while, as your Java code is compiled to Javascript. Once you see the message `The code server is ready`, fire up your browser and go to  [http://localhost:8080/html](http://localhost:8080/html). This is your app running in the browser! When you change any of your Java code or assets, just click the `SuperDev refresh` button while you are on the site and the server will recompile your code and reload the page! To kill the process, simply press `CTRL + C` in the terminal window.

  **IMPORTANT** The port `9876` is used when doing normal GWT development. Therefore, trying to access the game in any other way than using the port `8080` will not launch your project.

Once this [bug in the Gradle tooling API](http://issues.gradle.org/browse/GRADLE-1539) is fixed, we can simplify running the HTML5 by using the Gradle integration. At the moment, the Gradle process will run forever even if canceled.
## Debugging Your Project
Follow the steps for running the project, but instead of launching via the run (Play) button, launch your configuration via the debug (bug) button. Note that RoboVM currently does not support debugging. Debugging of the html build can be done in the browser as follows:

Run the superDev Gradle task as before. Go to [http://localhost:8080/html](http://localhost:8080/html), click on the `SuperDev Refresh` button and hit `Compile`. In Chrome, press `F12` to bring up the developer tools, go to the sources tab and find the Java file you want to debug. Set breakpoints, step and inspect variables using the power of source maps!

[[images/Screen%20Shot%202014-03-23%20at%2019.11.27-BkaIpjttPQ.png]]

## Packaging your Project
It's easiest to package your application from the command line, or using the Gradle task within Intellij IDEA. To see the relevant Gradle tasks, check the [[Gradle command line documentation|Gradle on the Commandline]].
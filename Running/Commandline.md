这一章节将向你展示如何在命令行中运行你的程序，并且打包到不同的平台。

## 配置ANDROID_HOME
在你做任何命令行操作之前，ANDROID_HOME环境变量必须指向一个有效的Android SDK。

Windows: `set ANDROID_HOME=C:/Path/To/Your/Android/Sdk`

Linux, Mac OS X: `export ANDROID_HOME=/Path/To/Your/Android/Sdk`

或者你也可以创建一个命名为"local.properties"的文件，内容如下：`sdk.dir /Path/To/Your/Android/Sdk`

## 运行项目
Gradle让你很方便地在命令行中运行项目。只需要使用gradlew命令行指定你的目标平台，以及使用该平台的运行命令。

[**Desktop**](#运行desktop项目) - [**Android**](#运行android项目) - [**iOS**](#运行ios项目) - [**HTML**](#运行html项目)

### 运行desktop项目
`gradlew desktop:run`

这条命令编译你的core项目和desktop项目，并且运行desktop启动器。工作路径是android项目的assets文件夹。

如果你运行时遇到了找不到文件的错误，请确保项目路径是正确的。

### 运行Android项目

`gradlew android:installDebug android:run`

这条命令将为你的应用创建一个debug APK(调试安装包)，把它安装在第一次连接的虚拟机或者真机，并且启动main activity。
进程被分到两个任务中，因为Android Gradle插件可以让你为你的应用创建多个flavors。

你可以在[Android Gradle Plugin site](http://tools.android.com/tech-docs/new-build-system/user-guide)找到更多信息。

### 运行 iOS 项目
`gradlew ios:launchIPhoneSimulator`

`gradlew ios:launchIPadSimulator`

`gradlew ios:launchIOSDevice`

前两条命令将在iPhone或ipad模拟器中启动你的程序，最后一条命令将在一个已连接的真机上运行你的iOS项目，如果已经配置好的话。请参阅Apple的文档关于如何配置真机。请注意，当你第一次运行iOS项目，编译需要很长的时间。编译时间将会在以后的运行中显著降低！

### 运行HTML项目
`gradlew html:superDev`

这条命令将以[GWT Super Dev模式](http://www.badlogicgames.com/wordpress/?p=3073)启动你的应用，此模式将你的Java代码编译成Javascript，并允许你在你的浏览器中直接调试Java代码。
如果你在命令行窗口看到这条信息`Next, visit: http://localhost:9876`，打开你的浏览器并跳转到这个地址。拖拽"Dev Mode On"标签到你浏览器的书签栏。
接下来，打开[http://localhost:8080/html](http://localhost:8080/html)。这里就是你运行在浏览器上的应用！如果你改变了core项目中的任何JAVA代码，只需要点一下书签，然后点击“Compile”。改变的代码几秒钟后就会产生效果。如果你修改了你的资源，你必须用上面的命令重启服务。

## 打包项目
每个平台都有不同的发布方式。在这一节我们来看看如何通过Gradle来打包发布。

[**Desktop**](#为desktop项目打包) - [**Android**](#为android项目打包) - [**iOS**](#为ios项目打包) - [**HTML**](#为web项目打包)

### 为desktop项目打包

`gradlew desktop:dist`

这条命令将在`desktop/build/libs/`目录下创建一个可执行的JAR文件。它包含了所有的必需代码，也包含了所有你在android/assets目录下的资源，并且可以通过双击它或者使用命令行`java -jar jar-file-name.jar`来运行。
你的用户必需已经为此安装了一个JVM才能运行。JAR文件可以运行在Windows，Linux和Mac OS X!

**如果你想要打包成一个带有JVM的JAR来发布，你可以使用我们的 [packr tool!](https://github.com/libgdx/packr)。用这种方式你的用户就不需要安装JVM，那将花费大约每个平台23-30mb的下载量。

### 为android项目打包
`gradlew android:assembleRelease`

这条命令将在`android/build/outputs/apk`目录下创建一个未签名的APK。在你安装或者发布这个APK之前，你必需对它进行签名 [sign it](http://developer.android.com/tools/publishing/app-signing.html)。通过上面的命，APK就以release模式创建完成，你只需要遵循Keytool和Jarsigner步骤。
你可以安装这个APK文件到任何允许未知源安装的Android设备 [installation from unknown sources](http://developer.android.com/distribute/open.html#unknown-sources)。

### 为ios项目打包
`gradlew ios:createIPA`

这条命令将在 `ios/build/robovm` 目录下创建一个你将发布到Apple App Store的IPA。你可以按照Apple的引导来做 [app store distribution](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html)。
###为web项目打包

`gradlew html:dist`

This will compile your your app to Javascript and place the resulting Javascript, HTML and asset files in the `html/build/dist/` folder. The contents of this folder have to be served up by a web server, e.g. Apache or Nginx. Just treat the contents like you'd treat any other static HTML/Javascript site. There is no Java or Java Applets involved!
这条命令会将你的应用编译成为Javascript，并且将编译好的Javascript，Html和资源文件放到`html/build/dist/`目录下。这个目录下的内容必须部署到一个Web服务器上，例如Apache或者Nginx。就像你对待其他的静态HTML/Javascript站点一样。这里不再涉及到Java或者Java Applets。
如果你已经安装了Python，你可以通过在 `html/build/dist`目录下执行以下命令来测试你发布的应用。

`python -m SimpleHTTPServer`

然后你打开一个浏览器跳转到 [http://localhost:8000](http://localhost:8000)就能看到你的项目在运行。

## 调试与常见问题
### Gradle任务失败

如果当你调用gradle时，构建或者刷新未能获得更多信息时(即失败，译者注)，请重新运行同样的命令，并增加 --debug 参数到命令中。例如：
```./gradlew tasks --debug```
这将为你提供堆栈跟踪，并让你更好了解为什么Gradle失败。

### 常见问题
(已确认) AVG - 当运行 gradlew desktop:dist 时，杀软会导致失败。 请增加一个例外到杀软来允许运行。
### 调试项目

## 调整

你可能会和我一样，希望从dist任务获得一个jar。Gradle的目录规则是目录加上版本号，像desktop-1.0。
你可能也希望让每次构建都有一个以某种方式命名的独特版本号或构建日期，可以这样做：

在项目根目录的build.gradle文件，增加：

    def getDate() {
        def date = new Date()
        def formattedDate = date.format('yyyyMMddHHmmss')
        return formattedDate
    }
    

在allprojects配置快中新增'version = "0.1-build-" + getDate()'

在桌面项目中的dist任务中新增

'baseName = "myproject"'

可以肯定还有其他更好的处理方法，你可以花些时间来研究。
现在在你desktop/libs目录下有一个命名类似'project-0.1-build-20150120033412.jar'的jar文件，这将使发布更加容易，更易追踪，更少冲突等等。
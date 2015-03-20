你之前[[生成了libgdx项目|用Gradle生成项目]], 现在该是大胆的用eclipse开发的时候了!

**在导入项目到Eclipse之前,确保你已经[[配置好开发环境|设置好了开发环境(Eclispe, Intellij IDEA, NetBeans)]]! **

## 导入项目
到 `File -> Import -> Gradle -> Gradle Project`, 选中你的项目根目录, 然后点击 `Build Model`. 等待一会儿, 你将会看到一个根项目和几个子项目 (android, core, desktop, html, ios). 选中所有的项目,然后点击 `Finish`. 注意第一次操作这个过程可能会花费一两分钟,因为后台会下载Gradle和一些必要的依赖文件.

### 常见问题
你的项目根文件夹和Eclipse工作区(workspace)文件夹一定不能相同(详情见[issue](https://github.com/libgdx/libgdx/issues/1537))

假如你在运行的时候由于丢失 validation-api:1.0.0.GA 出现问题, 请删除 Maven缓存, 一般在`C:\Users\username\.m2` or `/Users/username/.m2` or `/home/username/.m2`.
[[images/URxvrYe.png]]

当你在第一次导入项目的时候遇到如下问题:
`com/github/jtakakura/gradle/plugins/robovm/RoboVMPlugin : Unsupported major.minor version 51.0`
请确保你的java运行环境版本在jdk 7以上

## 运行项目 ##

  * **Desktop**: 在你的桌面项目上点击鼠标右键, `Run As -> Java Application`. 选中你的桌面启动类 (例如 DesktopLauncher.java).
  * **Android**: 确保在DDMS里面已经显示了一个连接成功的android设备 (见 [Android Developer Guide](http://developer.android.com/guide/index.html)). 在Android项目上点击右键, `Run As -> Android Application`.
  * **iOS RoboVM**: 在robovm项目上点击鼠标右键, `Run As -> iOS Device App` 在连接成功的设备上运行, 或者 `Run As -> iOS Simulator App` 在IOS模拟器上运行. 假如需要在真机上运行, 你需要 [provision](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html) 它能让你把app部署到真机里面运行!
  * **HTML5**: 在html项目上点击鼠标右键, `Run As -> External Tools Configuration`. 在左侧边栏上双击’Program’,创建一个新的配置(configuration). 给新配置设置一个名字, 例如 GWT SuperDev. 给’gradlew.vat’(Windows), 或者’gradlew’ (Linux, Mac)文件设置一个本地的环境变量. 把working directory设置成项目的根目录. 指定`html:superDev`作为参数. 点击 'Apply', 然后点击 'Run'. 等到命令行视图(console view)里面显示’The code server is ready.’, 然后打开链接 [http://localhost:8080/html](http://localhost:8080/html). 你可以让服务器一直保持运行. 假如修改了代码或者资源文件, 你只需要在浏览器里面点击按钮’SuperDev Refresh’, 然后编译器就会重新编译app,重新载入网站

由于这个 [bug in the Gradle tooling API](http://issues.gradle.org/browse/GRADLE-1539) 被修复后, 我们只需要简单运行HTML5通过使用Gradle集成(integration), 这个Gradle进程会一直运行知道手动取消.

## 调试项目 ##
只需要把正常运行项目步骤中通过’Run as’运行程序改为使用’Debug as’即可进入调试程序的过程. 最新的libgdx版本已经支持调试ios项目
如果想调试html项目,可以在浏览器中按照如下步骤进行调试:

和之前一样运行’superDev’配置项. 在[http://localhost:8080/html](http://localhost:8080/html)点击 ’SuperDev Refresh’按钮. 在Chrome浏览器中,按’F12’ 唤起开发工具箱, 在sources标签中找到你需要调试的java文件. 设置断点, 单步调试 然后使用source maps检查变量! 当改变了代码或者资源文件的时候,点击’SuperDev Refresh’按钮(保持服务器一直运行!).

[[images/Screen%20Shot%202014-03-23%20at%2019.11.27-BkaIpjttPQ.png]]

## 程序打包
在命令行里面打包你的程序非常容易, 或者在Eclipse里面用Gradle tasks打包. 如果想查看Gradle tasks的yong用法, 请在命令行里面敲Gradle -help或者查看Gradle的文档.
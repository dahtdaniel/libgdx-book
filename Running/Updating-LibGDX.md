#### Libgdx版本管理

Libgdx是一个活跃的开源项目，使用较新的版本是一个不错的选择，你可以通过以下网址获取相关信息
[http://libgdx.badlogicgames.com/versions.html](http://libgdx.badlogicgames.com/versions.html)

Libgdx使用Gradle管理依赖，所以切换Libgdx版本是一件很轻松的事情。

Libgdx和大多数开源项目一样，有两种版本：

* Release版本: 稳定版本。你可以在[Maven Central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.badlogicgames.gdx%22%20AND%20a%3A%22gdx%22)查看版本号。
* Nightly版本: 俗称快照版本。每个提交到代码仓库的修改都会触发快照版本的生成。快照版本一般为版本号加上SNAPSHOT，比如 1.0.1-SNAPSHOT. 你可以在 [这里](https://github.com/libgdx/libgdx/blob/master/pom.xml#L13)查看快照版本。

基于Gradle的项目更换版本是一件非常轻松的事情。打开`build.gradle` 文件，然后找到如下声明:

```Groovy
 gdxVersion = "1.5.2"
```
你现在看到的版本可能已经高于1.5.2了。在你需要的时候，你只需要确定版本字段的内容，你就可以简单地升级Libgdx版本（或者降级）。同样的，你还可以升级在Gradle管理下的依赖。编辑完成后保存`build.gradle`文件。

接下来的步骤和你的IDE有关:

* **Eclipse**: 在package explore中选择所有项目，右键选择 `Gradle -> Refresh All`。 Eclipse会自动下载依赖然后将下载的jar文件配置到项目中。
* **Intellij IDEA**: 一旦你的build.gradle文件修改，IDE会自动显示一个刷新按钮供。点击以后，IDE会自动下载依赖。你也可以到Gradle视图中找到刷新按钮或者'builddependents'任务并点击。
* **Netbeans**: in the "Projects" view, right-click the top-most project node and select "Reload Project".  All sub-projects will also be reloaded with the new files.
* **Command Line**: invoking any of the tasks will usually check for changes in dependency versions and redownload anything that changed.

And that's it! No need to manually juggle JAR files, .so files or anything else. Just change a string in a file and update via your IDE or the command line.
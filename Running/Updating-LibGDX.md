#### Libgdx版本升级

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

The version you see may be higher than 1.5.2 already. Once you've located that string, you can simply change it to the latest release (or an older release) or to the current SNAPSHOT version. You may also have to update other modules in that same section of the build.gradle file, based on the [versions listing](http://libgdx.badlogicgames.com/versions.html). Once edited, save the build.gradle file.

The next step is dependent on your IDE:

* **Eclipse**: Select all your projects in the package explorer, right click, then click `Gradle -> Refresh All`. This will download the libGDX version you specified in build.gradle and wire up the JAR files with your projects correctly.
* **Intellij IDEA**: will usually detect that your build.gradle has been updated and show a refresh button. Just click it and IDEA will update libGDX to the version you specified in build.gradle. Go into the gradle tasks panel/tool view and click the refresh button. Running a task like 'builddependents' also tends to do this.
* **Netbeans**: in the "Projects" view, right-click the top-most project node and select "Reload Project".  All sub-projects will also be reloaded with the new files.
* **Command Line**: invoking any of the tasks will usually check for changes in dependency versions and redownload anything that changed.

And that's it! No need to manually juggle JAR files, .so files or anything else. Just change a string in a file and update via your IDE or the command line.
为Libgdx项目做出贡献的渠道有很多：

  * 在Github上Fork项目
  * 了解如何运行demo和测试
  * 编写代码并在Github上申请Pull Request

### API变动 ###

如果你修改的代码涉及了公开的API或者你增加了新的API，你确保你添加相关信息到[CHANGES](https://github.com/libgdx/libgdx/blob/master/CHANGES)文件中。
除了这个CHANGES文件，相关的变动也会发布在[blog](http://www.badlogicgames.com)和[Twitter](http://www.twitter.com/badlogicgames)上，以便整个社区知晓。

如果你希望和其他开发人员交流，你可以选择申请Pull Request来分享你的代码。也可以在论坛中[this sub-forum](http://www.badlogicgames.com/forum/viewforum.php?f=23)发起一个新的话题。在论坛中你可能需要特别的授权才能在这个版块发帖，请给contact@badlogicgames.com发送一封邮件并附上你的论坛ID。在论坛页面的底部有一个订阅按钮，你最好通过邮件订阅该板块的信息。当然你也可以访问IRC (irc.freenode.org, #libgdx)，这里常常有核心开发者在线。

### 贡献者许可协议 ###

Libgdx基于[Apache 2.0 license](http://en.wikipedia.org/wiki/Apache_License)协议发行。在我们接受你的代码贡献之前，你需要签署[贡献者协议](https://github.com/libgdx/libgdx/blob/master/CLA.txt)。将它打印出来，然后填写相关信息并发送到邮箱即可。

签署这份协议将允许我们使用并分发你的代码。这是一个非独占许可，所以你保留所有你的代码的权利。这是一个安全防范，特别是某人贡献了重要的代码，随后又希望将其收回。

### Eclipse格式 ###

如果你在编写libgdx源代码，我们要求你使用[Eclipse formatter](https://github.com/libgdx/libgdx/blob/master/eclipse-formatter.xml)。

Eclipse formatter可以保证所有开发者使用的常用格式设置的一致性。

如果你是用IntelliJ IDEA，请参考这篇文章：[this article](http://blog.jetbrains.com/idea/2014/01/intellij-idea-13-importing-code-formatter-settings-from-eclipse/?utm_source=hootsuite&utm_campaign=hootsuite)

### 代码风格 ###

Libgdx没有官方的编码规范。我们遵循常见的Java风格，同时我们也希望你也遵守。

我们不希望看到以下情况：
  * 在任何类型的标识符的下划线
  * [匈牙利标记法](http://en.wikipedia.org/wiki/Hungarian_notation)
  * 带前缀的字段或者参数
  * 大括号换行

如果你修改了任何以后的代码，请遵循这些代码风格。如果不影响可读性，部分大括号将被移除。

如果你添加了新文件，确保它们包含[Apache文件头部说明](https://github.com/libgdx/libgdx/blob/master/gdx/src/com/badlogic/gdx/Application.java)。

If you create a new class, please add at least class documentation that explains the usage and scope of the class. You can omit Javadoc for methods that are self-explanatory.

If your class is explicitly thread-safe, mention it in the Javadoc. The default assumption is that classes are not thread-safe, to reduce the number of costly locks in the code base.

### Cross-platform compatibility ###

The GWT backend [doesn't support](http://www.gwtproject.org/doc/latest/DevGuideCodingBasicsCompatibility.html) all Java features. When writing generic code, please be aware of some common limitations:
  * Formatting. String.format() is unavailable, use StringBuilder instead or concatenate Strings directly.
  * Regular expressions. A basic emulation of [Pattern](https://github.com/libgdx/libgdx/blob/master/backends/gdx-backends-gwt/src/com/badlogic/gdx/backends/gwt/emu/java/util/regex/Pattern.java) and [Matcher](https://github.com/libgdx/libgdx/blob/master/backends/gdx-backends-gwt/src/com/badlogic/gdx/backends/gwt/emu/java/util/regex/Matcher.java) is provided.
  * Reflection. Use the utilities in [com.badlogic.gdx.utils.reflect](https://github.com/libgdx/libgdx/tree/master/gdx/src/com/badlogic/gdx/utils/reflect) package instead.
  * Multithreading. There is only support for [Timers](https://github.com/libgdx/libgdx/tree/master/gdx/src/com/badlogic/gdx/utils/Timer.java).

If you add any new classes, determine if they are compatible with GWT and add either include or exclude elements to the [GWT module](https://github.com/libgdx/libgdx/blob/master/gdx/src/com/badlogic/gdx.gwt.xml).

Some classes (such as Matrix4 or BufferUtils) are emulated in the GWT backend due to certain compatibility requirements or native code. If you modify any these classes, please make sure that your changes get ported to the emulated version.

### Performance Considerations ###

Libgdx is meant to run on both desktop and mobile platforms, including browsers (JavaScript!). While the desktop HotSpot VM can take quite a beating in terms of unnecessary allocations, Dalvik and consorts don't.

A couple of guidelines:

  * Avoid temporary object allocation wherever possible
  * Do not make defensive copies
  * Avoid locking, libgdx classes are by default not thread-safe unless explicitly specified
  * Do not use boxed primitives
  * Use the collection classes in the [com.badlogic.gdx.utils package](https://github.com/libgdx/libgdx/tree/master/gdx/src/com/badlogic/gdx/utils)
  * Do not perform argument checks for methods that may be called thousands of times per frame
  * Use pooling if necessary, if possible, avoid exposing the pooling to the user as it complicates the API

### Git ###

Most of the libdgx team members are Git novices, as such we are just learning the ropes ourselves. To lower the risk of getting something wrong, we'd kindly ask you to keep your pull requests small if possible. A change-set of 3000 files is likely not to get merged.

We do open new branches for bigger API changes. If you help out with a new API, make sure your pull request targets that specific branch.

Pull requests for the master repository will be checked by multiple core contributors before inclusion. We may reject your pull requests to master if we do not deem them to be ready or fitting. Please don't take offense in that case. Libgdx is used by thousands of projects around the world, we need to make sure things stay somewhat sane and stable.
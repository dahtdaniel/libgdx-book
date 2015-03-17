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

如果你创建了一个新的类，请至少添加文档来说明类的使用方法和范围。当然，你可以省略一些简单的、不言自明的方法。

如果你的类是显式线程安全的，请在Javadoc中提及这点。默认的假设是类不是线程安全的，锁的使用时昂贵的，我们希望减少它们在代码库的数量。

### 跨平台兼容性 ###

GWT的实现[不能支持]((http://www.gwtproject.org/doc/latest/DevGuideCodingBasicsCompatibility.html))所有的java特性。在编写代码的时候，请注意一些常见的局限性：
  * 格式化。 String.format()是不支持的，使用StringBuilder或者直接拼接字符串。
  * 正则表达式。 一个有限功能的[Pattern](https://github.com/libgdx/libgdx/blob/master/backends/gdx-backends-gwt/src/com/badlogic/gdx/backends/gwt/emu/java/util/regex/Pattern.java)和[Matcher(https://github
  .com/libgdx/libgdx/blob/master/backends/gdx-backends-gwt/src/com/badlogic/gdx/backends/gwt/emu/java/util/regex/Matcher.java)是可用的。
  * 反射. 使用Libgdx提供的反射工具[com.badlogic.gdx.utils.reflect](https://github.com/libgdx/libgdx/tree/master/gdx/src/com/badlogic/gdx/utils/reflect)。
  * 多线程. 只支持[Timers](https://github.com/libgdx/libgdx/tree/master/gdx/src/com/badlogic/gdx/utils/Timer.java)。

如果你添加了新的类，请判断它是否与GWT兼容，并添加信息到[GWT module](https://github.com/libgdx/libgdx/blob/master/gdx/src/com/badlogic/gdx.gwt.xml)中。

一些类（比如Matrix4或者BufferUtils）为了保证GWT的兼容性在本地代码中做了特殊处理。如果你修改了这些类，请确保你的修改同样在这些地方体现。

### 性能方面的考虑 ###

Libgdx可以运行在桌面和移动环境，包括浏览器（Javascript）。但是需要注意的是桌面环境的性能远远超过其他环境。桌面环境的HotSpot VM可以提供一些不必要的资源来运行程序，但是Dalvik等其他环境不能。

一些常见指导准则:

  * 尽可能避免临时对象分配
  * 不要拷贝副本
  * 避免锁，Libgdx中的类都是默认非线程安全的，除非明确说明
  * 使用Libgdx提供的集合类[com.badlogic.gdx.utils package](https://github.com/libgdx/libgdx/tree/master/gdx/src/com/badlogic/gdx/utils)
  * 不要进行参数检查，有时候这样会导致大量的调用
  * 尽可能使用池，如果可能也不要暴露池给开发人员，它们是复杂的API。

### Git ###

Libgdx的大部分成员是Git新手。为了避免一些问题，请保持你的Pull Request尽可能小。如果一个提交修改了超过过多文件，很可能它们不会被合并。

对于较大的API修改，我们会新建一个分支。如果你的提交和它们相关，请确保你的Pull Request指定了正确的分支。

提交到master分支的Pull Request会被多个核心开发人员检查。如果我们认为它们还不适合合并，我们将会拒绝你的合并请求。
希望你能够理解这种情况。Libgdx被大量项目使用，我们必须确保它健壮而可用。
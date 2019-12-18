搜索: Xamarin

- [Xamarin 百度百科](https://baike.baidu.com/item/Xamarin)。
  + Xamarin始创于2011年。
  + 跨平台开发框架。
  + 在Visual Studio之中使用C#与.NET Framework进行开发。
  + 目标是 用C#开发iOS、Android和Windows Phone原生应用程序。

- [Xamarin 文档](https://docs.microsoft.com/zh-cn/xamarin/)。

- [用xamarin开发App的体验如何？](https://www.zhihu.com/question/31159902)。
  + 2015-09-06
    - 技术上最大的感受是资料和第三方库比较少，特别是中文资料。
    - 英文资料还是比较全面的，首先是Xamarin的官网，文档非常详细。遇到的问题的话stackoverflow几乎都能找到。
    - 第三方库就比较苦逼，直接提供或者有现成绑定的库还是很少。
    - 优点：使用Visual Studio和C#是Xamarin最大的优势吧。还有很多.net的类库都可以直接使用。
    - 优点：逻辑层面代码的复用，特别是配合MVVM ，可以做到业务（例如网络通信）可以完全与界面分离。
    - Xamarin的学习路线还是比较陡峭的，需要学习iOS和Android对应平台的知识才能用好Xamarin。绝对不是只懂C#就能写App的。
  + 2016-06-14
    - 最大的好处就是MVVM，以及网络部分通用，但是做到界面统一以及第三方库的调用的时候就开始蛋疼了。
  + 2016-09-05
    - 只用过xamarin.forms，感受和大家一致，没有各种原生的库。
    - 想做个大的东西，光凭自己的能力就不够了。大公司有人才还好说，小团体或者个人的话还是算了吧。
  + 2016-10-20
    - 想做好Xamarin，必须能对原生开发理解并会，并且C#水准也不能低。
  + 2017-06-23
    - C#的学习成本还是比较高，确实需要对原生开发有所理解。
    - 绑定第三方框架麻烦。
    - 提供的UI相对比较简单。
    - 建议：UI相对比较简单，不需要太复杂动画和自定义控件（极致的简洁就是Xamarin.Froms，简单UI多平台直接实现）。
    - 建议：不牵扯或尽量少使用第三方SDK调用的APP。
    - 建议：至少具备独立阅读全英文文档/论坛的能力，最好达到能和他国程序员用英文讨论问题的水准。
    - 建议：别只是想图省事、省钱，早点想清楚吧。
  + 2017-06-23
    - Xamarin 的精华在于 Xamarin.Forms，Xamarin.Forms 的主要用途是界面要求不高的应用。
    - Xamarin.Forms 用来做面向消费者的应用想都不要想。
    - 把业务逻辑都放手机端那基本就是错的设计。剩下都是些个 UI 逻辑，Xamarin 的代码复用优点根本体现不出来。
    - Xamarin 本身可以自动 Wrap 原生库的。无非是需要自己写个简单的抽象层把 iOS 和 Android 的调用统一一下。
  + 2018-04-24
    - 主要还是看你对原生平台的掌握程度了，要想做出高质量的Xamarin app，主要还是依赖原生Api。
    - 业务逻辑部分可以独立出来便于维护，类似Mvvm。
    - 学习过程还是比较曲折的。
    - 个人觉得开发效率不敢说是优势，除非有靠谱大牛。
    - 优点就是灵活性了吧，在保证App品质（Xamarin+Native 运行效率与原生App相差无几）的同时，最大化可维护性。
  + 2018-08-13
    - 没有统一的api，安卓和ios各有一套，你要分别绑定。
    - UI也不统一，同一个UI控件，比如滑动条，在安卓和ios上显示是完全不一样的，因为他显示的是安卓和ios上的原生控件。
    - 完全违背了跨平台的一致性需求。这就是xamarin不火的原因。
    - xamarin当初像flutter那样提供安卓和ios统一的api，统一的UI显示效果，它就会和unity3d一样火，就没flutter什么事情了。
    - 哪怕xamarin用户在官方论坛叫了这么多年，他还是没这么做，因为官方就是看不到这个需求。
    - flutter预览版发布几个月，热度就后来居上了，xamarin眼睁睁的看着这一切发生，依然无动于衷。
  + 2018-12-10
    - 个人感觉，Xamarin.Android和原生开发差不多，不过Xamarin能吃到C#甜甜的语法糖就是了。
    - Xamarin.Forms个人感觉还是有点不方便，至少在写UI的时候，不能预览。
    - Xamarin有一个Xamarin Player，手机和开发机连同一个网络即可不插线调试。不过可惜的是，Xamarin Player目前仍然不是很鲁棒，在某些时候会闪退，而且log也不是好。
    - 实际上，我就是因为太喜欢C#，才选择的Xamarin。
  + 2018-12-15
    - VS里面的Android XAML应用(Xamarin.Forms)。
    - 很不愉快的开发体验，关键是资料太少了。
    - PS：没系统学过原生开发。
  + 2018-12-30
    - VS2017+基于Xamarin工程的安卓
    - 在VS里建了8.0的项目，结果发现VS按8.1来编译。无论建工程时选择什么版本，工程设置的版本编译里，都是8.1。
    - 果然，微软系就是不适应Java-安卓这种开源系的东西。
    - 建议：想做安卓开发的朋友，还是老老实实去学Java，然后用谷歌原生的Android Studio吧。
    - 还是推荐大家，开发安卓，用谷歌原生的Android Studio吧。
  + 引申阅读。
    - [Xamarin 免费且开源会对跨平台移动应用开发有什么影响？](https://www.zhihu.com/question/42005619)。
    - [Flutter和Xamarin二选一，选哪个？](https://www.zhihu.com/question/333817230)。
    - [微软已经开源免费Xamarin，为什么很多公司还是选择用React Native做跨平台app开发？](https://www.zhihu.com/question/57932046)。
    - [WindowsPhone被宣布失败后，微软开发生态中的Xamarin会是怎样的走向？](https://www.zhihu.com/question/66428775)。

- [Xamarin 技术全解析](https://www.imooc.com/article/27420)。
  + Xamarin 是一套基于C#语言的跨平台移动应用开发工具。
  + 2018年2月份微软宣布收购Xamarin，而后在4月份进行的Build大会上微软宣布将会在各个版本的Visual Studio中免费提供Xamarin，并且宣布Xamarin SDK开源。

- [Xamarin环境搭建与app各种demo实例 ——Xamarin.forms（一）](https://blog.csdn.net/qq_41647999/article/details/84844357)。
  + 本人总结的内容绝非照抄。
    - Xamarin可跨Android、IOS、Windows（手机）三端。
    - Xamarin微软收购的，原来是收费的，现在免费了。
    - Xamarin的前身是mono，所以编译的时候会用到mono的包。
    - 我们现在使用的是Xamarin.forms而不是Xamarin了。
    - 用Xamarin开发安卓app的朋友请收藏：https://developer.xamarin.com/api/root/MonoAndroid-lib/

- 总结：需要学习 C# 语言和 .NET 框架，以及有一定的了解 Android 的原生开发。

搜索: React Native

- [react-native现阶段的前景怎么样？](https://www.zhihu.com/question/325111592)。

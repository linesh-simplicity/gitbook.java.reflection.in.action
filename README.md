## Java Reflection in Action - Java反射实战(翻译稿)

#### 林从羽, Linesh.                                      08 Aug, 2015

Java反射，本质上是Java程序能够对自身程序要素（类名、方法、注解等）进行自我检查及自我修改的能力，是通过维护语言层级元信息的手段来有效地对应用层级进行解耦的解决方案。因而，它必须由Java虚拟机从底层提供支持。这本书是我大四做“Java反射机制研究与应用”毕业设计时候接触的书，书中讲解了Java反射的基本要素以及实际的应用场合，涉及代理、调用栈信息、类加载器、代码生成及性能评估等方面，虽然写于2004年，但其中使用方式及思想仍大有可借鉴之处。

这本书和周志明的《深入理解Java虚拟机：JVM高级特性与最佳实践（第2版）》，分别提供了应用层面和虚拟机层面上Java反射涉及以及实现范围的参考。若要深入了解反射的具体理论及实现，可以参阅本书作者之一Ira R.Forman的另一本著作"Putting Metaclasses to Work"，以及JVM底层的实现源码。具体的链接我会再补上。

#### 翻译进度
本书目前翻译了第1章，第2章翻译了一部分，不过仍需做一次小校正才能发出。目前主要进行的是第4章的翻译工作，会陆续发出。

#### 本书目录
[请戳这里：Contents](SUMMARY.md)

#### 翻译阶段安排
 * 第一轮：忠于原意，对全书内容做一次总体的翻译，保留翻译难度高的部分到下一个阶段完成。这个阶段需要保持稳定的输出；
 * 第二轮：斟酌第一轮留下的高难翻译，完成一个内容比较精细的翻译版本；
 * 第三轮：完成主体内容以外（前言、致谢、参考文献等）的翻译；校对全稿，进行一次精细的审阅和修改，定下最终版本的内容；
 * 第四轮：将内容整合到可阅读的样式中去，制作出一个pdf成品。这是本翻译项目的最终目标。

#### 感谢
感谢jimmylv给我介绍纯文本+gitbook+github同步集成的协作翻译方式，并且经常为我激情地哔哔前端的未来和提高工作效率的插件和软件。

感谢我喜欢吃西兰花的女朋友小耳朵。因为有你的支持，我才可以安心做自己喜欢的事，也才会开始喜欢自己的文字。这衷心的喜欢，写出来送给爱笑温暖的你。

感谢所有有缘前来与这本译书相遇的读者。

#### 致辞
欢迎任何关于翻译或与本书相关的建议、见解、观点和看法等，关于本话题的个人观点在这里可以是安全的。希望思考、表达和交换，会让我们彼此都学习和成长。

本翻译项目在于**内容**和**协作**。中英的对比，既是为了阅读时查证原文的方便，也为了通过此种方式使协作变得直观方便，获得各位对于翻译的建议。对内容的注重胜于其样式，既体现在纯文本的编辑方式，也体现在对样式（除了图片）最大限度的削弱。

想要完成对反射从头到尾的研究。  
向这个小小的梦想致敬。
# George's tracing problem

> George has been assigned the task of creating tracing versions of several of the classes that he maintains. In a tracing class, each method records information about its entry and, after method execution, records information about its return. George’s employer, WCI, wants tracing available for their classes because tracing helps with problem determination in deployed software.

George刚刚接到一个任务，要他为自己维护的几个类创建其可追踪版本。可追踪类中的每个方法都需要记录一些信息，包括进入方法前的信息、方法执行完毕后的返回信息等。George的雇主WCI希望这些类也具备追踪功能，因为这对软件发布后的问题诊断很有帮助。

> Consider the following scenario. A customer calls WCI technical support with a defect report. Tech support asks the customer to turn tracing on in their software and follow the steps to reproduce the defect. Because tracing is turned on, the customer can then send WCI a file containing the path through the WCI source code.

考虑这样一个场景。有一位客户发现了软件的一个重大缺陷，于是他打电话向WCI公司的技术部门反映。技术支持让这位客户打开软件的追踪功能，按照步骤来重现这个缺陷。因为打开了追踪特性，这样客户就可以给WCI发送一份包含了源代码执行路径的出错报告。

> This information solves many problems for the WCI technical team. It tells them a great deal about the state of the program during the failure. It also may prevent them from having to replicate their customer’s environment and data.

这些信息为WCI的技术团队省却了不少麻烦。它让维护人员清楚地了解到，程序出错时的状态是怎样的。同时，也免去了他们去重现客户环境和数据的麻烦。

> While tracing is a useful feature, it is also very I/O intensive. Therefore, classes should be able to turn tracing on and off. However, including tracing code and guards to turn it on and off in each class bloats the classes and makes them slower because of the execution of the if statements. Due to these constraints, George decides to make tracing and nontracing versions of his classes.

尽管追踪功能很有用，但同时，它对I/O也很敏感。因此，类应该可以轻松地打开或关闭追踪功能。但是，若选择使用大量的条件语句来实现开闭的判断，可想而知这些开关将撒得满地都是。此外大量if语句的执行也会使程序的运行速度变慢。由于存在这些限制，George决定为他的类分别编写带追踪和不带追踪的版本。

> One option George considers is subclassing each nontraced class and overriding each method with traces and super calls. He can then set up a process for either instantiating the traced or nontraced version depending upon some command-line argument. George quickly realizes that this option has the following shortcomings:

George考虑一种可能的方案是继承每个不带追踪的类，然后重写每个方法，先做追踪后再做super调用。然后，他可以创建一个例程，根据命令行的参数来选择实例化带追踪的或不带追踪的类。George很快意识到，这个方案有以下的缺点：

> * _Tedium_ — Executing this option is boring and mechanical. In fact, a computer program can be written to do this job.
> * _Error-proneness_ — George can easily misdeclare an override, misspelling the method name or including the wrong parameter list. He could also forget or overlook a method. At best, he may have a compile error to warn him that his process broke. Otherwise, the class may not behave as expected.
> * _Fragility_ — If anyone in George’s department adds, deletes, or changes the signature on a method in the superclass, the traced subclass breaks either by not building or by not tracing as expected.

* _重复_。做这些工作非常乏味无聊。事实上，写一个程序，让计算机来做这些重复工作就可以了。
* _易出错_。George很可能定义错重写方法，或者拼错方法的名字，可能给出了错误的参数列表。甚至他可能直接忘记了重写某一个方法等。幸运的话他会得到编译器的出错提示，警告他工作出错了。但糟糕的是，类可能不按预期的方式工作。
* _程序很脆弱_。假设George的部门中有人或添加或删除或改变了基类方法的签名，继承来的追踪类就崩溃了。可能是不能正常工作，可能是不以预期的方式工作等。

> Clearly, George is in need of a better solution. George needs to separate the concern of tracing from the rest of the source code and implement it in a separate module. George reasons that this can be done with a proxy, where the proxy traces the call before and after delegating the method invocation to the target. Although there will be one proxy object for every target, with the use of reflection, all of the proxies can be instances of one proxy class, which addresses the shortcomings raised previously. Before presenting George’s solution, let’s examine `java.lang.reflect.Proxy.`

很明显，George需要更好的方案。他需要把追踪特性从代码的其他部分中分离出来，在一个独立的模块里来实现它。George认为这可以通过代理来完成，因为代理在把方法调用委托给目标对象的前后都会进行记录和追踪。尽管这样一来，每个目标对象都需要一个代理对象，但通过使用反射，所有的代理都可以是一个代理类的实例，__(再翻译)which addresses the shortcomings raised previously__.在展示George的最终方案前，我们先来看看`java.lang.reflect.Proxy`这个类。


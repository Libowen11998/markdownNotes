作者：菜鸡想去大厂
链接：https://www.nowcoder.com/discuss/380801?type=post&order=time&pos=&page=1&channel=-1&source_id=search_post_nctrack
来源：牛客

1：Java异常了解吗？说说平时遇到的异常？ 

  2：JVM运行时内存区域划分？哪些线程私有？ 

  3：对象的生命周期？ 

  4：说说垃圾收集器（我简历上写了垃圾收集，但是只知道垃圾收集[算法]()） 

  5：类加载机制？如何自定义实现类加载器？（没实现过，盲猜继承应用程序类加载器） 

  6：synchronized锁的升级过程？ 

  7：说说你理解的悲观锁和乐观锁？乐观锁有哪些？（只知道CAS、后悔没说MySQL的MVCC）乐观锁有什么缺点？（没说出来，然后问了ABA问题怎么解决，我说加版本号） 

  8：线程池了解吧，说说如何实现线程池？核心参数哪些？有哪些阻塞队列呢？ 

  9：如何优雅的关闭线程池（我不会，面试官引导我） 

  10：MySQL的存储引擎有哪些？它们之间的区别？（说了InnoDB和MyISAM的之间的两三点） 

  11：怎么判断一个SQL语句有没有走索引？紧接着问explain知道哪些字段吗 

  12：说说你了解的设计模式？手撕单例模式？（我说写个双检索吧，面试官说写个简单的，那就饿汉） 

  13：为什么选择后端开发？有什么要问我的吗？













https://www.nowcoder.com/discuss/284487?type=post&order=time&pos=&page=1&channel=-1&source_id=search_post_nctrack

# vivo java面经(50min左右)

<img src="https://uploadfiles.nowcoder.com/images/20190929/7612822_1569728823065_18F7F7DDB65EBA65979BA8C3FFB37CCC" alt="img" style="zoom: 50%;" />











作者：腐草为萤201904101657559
链接：https://www.nowcoder.com/discuss/293156?type=post&order=time&pos=&page=1&channel=-1&source_id=search_post_nctrack
来源：牛客网

一面技术 

  hashmap，concurrentHashmap，hashtable各介绍一下 

  [红黑树]()介绍一下，跟[平衡二叉树]()比较一下，[红黑树]()有哪些应用场景 

  zoo[keep]()er了解吗 

  StringBuffer和StringBuilder 

  接口和抽象类区别 

  面对对象的几大特性 

  反射机制介绍一下 

  类加载机制，过程 

  线程的集中状态 

  volatile介绍一下 

  java内存模型 

  双亲委派模型 

  类加载器类别 

  bio，nio，aio分别介绍一下，nio的实现方式 

  数据库隔离级别以及分别解决了什么问题 

  [redis]()数据类型，[redis]()的应用场景，为什么[redis]()快， 

  线程实现方式 

  死锁条件，怎么预防 

  锁有哪些 

  序列化相关 

  sql查询过程

  二面hr 

  问一些为什么想加入[vivo]()啊，了解[vivo]()吗的问题，主要看你是不是真想加入[vivo]()。其他都是闲聊





作者：tankily_
链接：https://www.nowcoder.com/discuss/198717?type=post&order=time&pos=&page=1&channel=-1&source_id=search_post_nctrack
来源：牛客网

如果某个用户同时请求创建活动接口100次，如果防止它被重复创建？创建前查看该记录是否存在、使用锁、如果是分布式的使用分布式锁—这样解决了99.99%的问题。除了使用这些方案，还能使用什么方法解决吗？

讲讲分布式锁的实现

你用过Java的J.U.C并发包吧，给我讲一下AQS的原理

能讲下ConcurrentHashMap的实现原理么 JDK7或者8都行

MySQL InnoDB存储引擎中的MVCC解决了什么问题，能说下MVCC的实现原理么

你平时是怎么创建线程的？

为什么用线程池，线程池有什么好处？

创建线程池需要的关键参数有哪些？

线程池有哪几种任务拒绝策略

我看了一下你简历上写了很多[redis]()字眼，那你知道[redis]()的什么东西

Redis的key的写入和删除的原理

怎么保证Redis的高可用

你还用过rabbitMQ呀，它能够做什么？

给你一道进阶题，rabbitMQ是怎么保证消息不丢的，从[客户端]()—消息队列， 消息队列—服务器端的角度考虑

SQL语句经常写吧，那我给你出一道SQL题（分组求和[排序]()）

CAS的原理给我讲一下

他是怎么保证内存的可见性的 

CAS会产生什么问题

知道Java中的内存模型吧，它有8个指令你给我说一下

双亲委派模型本质是解决了什么问题？安全性

有哪几种类加载器？

你认为什么情况下不应该建立索引

RPC你了解过吗？

你有什么问题问我的吗？

面试官超nice的，最后还跟我握手，说我基础不错，还给我一些以后工作上指引😐

### HR 面

你认为你觉得做过最有成就感的[项目]()是哪个？以及遇到了什么困难，是怎么解决的

你了解[vivo]()吗？

你对薪资的期望是多少？

你认为选择一个公司，什么重要

你认为怎么对新人进行培养比较好

你认为你要具备什么样的软件工程师素质才能胜任你的工作？

你认为自己有什么优点？

你在实习的公司工作的感受是什么？

你有什么问题问我的吗？










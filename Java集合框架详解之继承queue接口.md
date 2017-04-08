趁着最近比较闲，静下心来准备把关于集合框架的东西好好整理一下，边学边整理。近阶段先是整理整体的知识点，一些接口，一些继承类以及它们的特性,用法，后续还会有一些常用的，比较重要的类的jdk源码剖析。<br>

Java集合框架详解之继承set接口：http://blog.csdn.net/JasonZhangOO/article/details/55807103<br>
Java集合框架详解之继承list接口：http://blog.csdn.net/JasonZhangOO/article/details/55807177<br>
Java集合框架详解之继承queue接口：http://blog.csdn.net/JasonZhangOO/article/details/55807197<br>
Java集合框架详解之继承map接口：http://blog.csdn.net/JasonZhangOO/article/details/55807685<<br>br>
Java集合框架详解之一点小总结：http://blog.csdn.net/JasonZhangOO/article/details/55808011

继承queue接口
---------
Queue接口与List、Set同一级别，都是继承了Collection接口。LinkedList实现了Queue接口。<br>
队列数据结构有先进先出的特性，在满队列中添加元素或者空队列中删除数据都会引起线程阻塞。<br>
-add：增加元素。 如果队列已满，则抛出一个IIIegaISlabEepeplian异常；<br>
-remove： 移除并返回队列头部的元素。 如果队列为空，则抛出一个NoSuchElementException异常；<br>
-element： 返回队列头部的元素。 如果队列为空，则抛出一个NoSuchElementException异常；<br>
-offer：添加一个元素并返回true。如果队列已满，则返回false，避免像add一样报错；<br>
-poll：移除并返问队列头部的元素。如果队列为空，则返回null，避免抛出异常；<br>
-peek：返回队列头部的元素。如果队列为空，则返回null；<br>
-put：添加一个元素。如果队列满，则阻塞；<br>
-take：移除并返回队列头部的元素。如果队列为空，则阻塞。<br>

五种队列：<br>
-ArrayBlockingQueue ：由数组支持的有界队列。基于数组的阻塞循环队列，先进先出原则排序。<br>
-LinkedBlockingQueue：由链接节点支持的可选有界队列。基于链表的队列，先进先出排序元素。<br>
-PriorityBlockingQueue：由优先级堆支持的无界优先级队列。PriorityBlockingQueue是对PriorityQueue的再次包装，是基于堆数据结构的，当资源耗尽，避免out of memory，添加会阻塞，空队列取元素也会阻塞。<br>
-DelayQueue：由优先级堆支持的、基于时间的调度队列。（基于PriorityQueue来实现的）是一个存放Delayed 元素的无界阻塞队列，只有在延迟期满时才能从中提取元素。<br>
-SynchronousQueue：一个利用BlockingQueue接口的简单聚集（rendezvous）机制。元素就直接在消费者和生产者之间传递，永远不会加入到阻塞队列中。<br>

参考文章：<br>
http://www.codeceo.com/article/java-collection-summary.html<br>
http://www.codeceo.com/article/java-collection-class.html<br>
http://www.imooc.com/article/1893<br>
http://blog.csdn.net/softwave/article/details/4166598<br>

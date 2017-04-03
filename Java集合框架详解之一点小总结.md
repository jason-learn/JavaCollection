趁着最近比较闲，静下心来准备把关于集合框架的东西好好整理一下，边学边整理。近阶段先是整理整体的知识点，一些接口，一些继承类以及它们的特性,用法，后续还会有一些常用的，比较重要的类的jdk源码剖析。

Java集合框架详解之继承set接口：http://blog.csdn.net/JasonZhangOO/article/details/55807103<br>
Java集合框架详解之继承list接口：http://blog.csdn.net/JasonZhangOO/article/details/55807177<br>
Java集合框架详解之继承queue接口：http://blog.csdn.net/JasonZhangOO/article/details/55807197<br>
Java集合框架详解之继承map接口：http://blog.csdn.net/JasonZhangOO/article/details/55807685<br>
Java集合框架详解之一点小总结：http://blog.csdn.net/JasonZhangOO/article/details/55808011<br>

Java集合框架图
---------
 ![这里写图片描述](http://img.blog.csdn.net/20170219195943856?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFzb25aaGFuZ09P/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**插入一段：Arrays**

array是Java中数组，对于知道元素个数时好用。java.util.Arrays 包含了许多处理数据的实用方法：<br>
Arrays.asList：可以从 Array 转换成 List。可以作为其他集合类型构造器的参数。<br>
Arrays.binarySearch：在一个已排序的或者其中一段中快速查找。<br>
Arrays.copyOf：如果你想扩大数组容量又不想改变它的内容的时候可以使用这个方法。<br>
Arrays.copyOfRange：可以复制整个数组或其中的一部分。<br>
Arrays.equals：如果你想要比较两个数组是否相等，应该调用这个方法。 方法——所以这个方法在比较了对象的类型之后是直接传值进去比较的。<br>
Arrays.fill：用一个给定的值填充整个数组或其中的一部分。<br>
Arrays.hashCode：用来根据数组的内容计算其哈希值（数组对象的hashCode()不可用）。这个方法集合了Java 5的自动装箱和无参变量的特性，只是传值进去，不是对象。<br>
Arrays.sort：对整个数组或者数组的一部分排序。 <br>
Arrays.toString：打印数组的内容。<br>

**Java集合框架总结**

　　1）如果涉及到堆栈，队列等操作，应该考虑用List，对于需要快速插入，删除元素，应该使用LinkedList，如果需要快速随机访问元素，应该使用ArrayList。<br>
　　2）如果操作在单线程中进行，考虑非同步的类ArrayList,LinkedList,HashMap，不要求线程安全，其效率较高；如果多个线程可能同时操作一个类，应该使用同步的类Vector（数据量很大）、Hashtable，考虑线程安全问题。<br>
　　3）要求key和value键值，则使用HashMap（较常用）,Hashtable。<br>
　　3）要注意对hash的操作，作为key的对象要复写equals和hashCode方法。<br>
　　4）尽量返回接口而非实际类型，如返回List而非ArrayList，如果以后需要将ArrayList换成LinkedList，客户端代码不用改变（针对抽象编程）。<br>


参考文章：
http://www.codeceo.com/article/java-collection-summary.html<br>
http://www.codeceo.com/article/java-collection-class.html<br>
http://www.imooc.com/article/1893<br>
http://blog.csdn.net/softwave/article/details/4166598

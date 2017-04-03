 Java集合框架详解
=================================
趁着最近比较闲，静下心来准备把关于集合框架的东西好好整理一下，边学边整理。近阶段先是整理整体的知识点，一些接口，一些继承类以及它们的特性,用法，后续还会有一些常用的，比较重要的类的jdk源码剖析。<br>

首先在集合框架的类继承体系中包含两个最顶层的接口：collection和map接口<br>
1）collection表示纯数据；map表示key-value键值对<br>
2）集合框架的两个“标准”的构造函数：<br>
-没有参数的构造函数，创建一个空的集合类<br>
-有一个类型与基类（Collection或Map）相同参数的构造函数，创建一个与给定参数具有相同元素的新集合类<br>
 
**collection接口：**
-----------------
![这里写图片描述](http://img.blog.csdn.net/20170219193422565?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFzb25aaGFuZ09P/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)<br>
有三个接口继承自collection：<br>
-set：表示数据不能有重复的集合<br>
-list：表示的集合可以数据重复，有序的collection<br>
-queue：jkd1.5新增，用于存储数据，不能处理数据（不常用）<br>
jdk不提供直接继承collection接口的类，必须继承子接口，有的类支持元素重复，有的支持排序，继承自collection的子类都有一个iterator方法，该方法返回一个迭代子，可以逐一访问collection中每一个元素。<br>

Java集合框架详解之继承set接口：http://blog.csdn.net/JasonZhangOO/article/details/55807103<br>
Java集合框架详解之继承list接口：http://blog.csdn.net/JasonZhangOO/article/details/55807177<br>
Java集合框架详解之继承queue接口：http://blog.csdn.net/JasonZhangOO/article/details/55807197<br>
Java集合框架详解之继承map接口：http://blog.csdn.net/JasonZhangOO/article/details/55807685<br>
Java集合框架详解之一点小总结：http://blog.csdn.net/JasonZhangOO/article/details/55808011<br>

Collection 接口提供的主要方法：<br>
boolean add(Object o) 添加对象到集合；<br>
boolean remove(Object o) 删除指定的对象；<br>
int size() 返回当前集合中元素的数量；<br>
boolean contains(Object o) 查找集合中是否有指定的对象；<br>
boolean isEmpty() 判断集合是否为空；<br>
Iterator iterator() 返回一个迭代器；<br>
boolean containsAll(Collection c) 查找集合中是否有集合 C 中的元素；<br>
boolean addAll(Collection c) 将集合 C 中所有的元素添加给该集合；<br>
void clear() 删除集合中所有元素；<br>
void removeAll(Collection c) 从集合中删除 C 集合中也有的元素；<br>
void retainAll(Collection c) 从集合中删除集合 C 中不包含的元素。<br>


继承set接口
-------
set中不包含重复元素，有m，n，则m.equals(n)=false,可以有null元素，最多一个。<br>
**HashSet：**<br>
HashSet低层是基于HashMap实现的set，用HashMap保存数据，和HashMap一样的性能，消耗较多内存。<br>
-hashCode和equal()是HashMap用的，因为无需排序所以只需要关注定位和唯一性即可。<br>
-hashCode是用来计算hash值的，hash值是用来确定hash表索引的。<br>
-hash表中的一个索引存放的是一张链表，所以还要通过equal方法循环比较链上的每一个对象才可以真正定位到键值对应的Entry。<br>
-put时，如果hash表中没定位到，就在链表前加一个Entry，如果定位到了，则更换Entry中的value(值)并返回旧value(值)<br>
-（关于HashMap）覆写key的hashCode()和equal()时不要关联可变属性，否则属性变了hashCode会变，equal也会为false，这样在Map中就找不到它了，而且这样的对象因为找不到它，所以得不到释放，这样就变成了一个无效引用。(相当于内存泄漏)<br>

Hashset的使用：

        HashSet hashSet= new HashSet();
		String s1 = "hello";
		String s2 = "abc";
		String s3 = "edf";
		
		hashSet.add(s1); //在集合末尾添加
		hashSet.add(s2); //计算hashcode，hello排在abc后面
		hashSet.add(s3); //计算hashcode，edf排在hello前面
		 
		hashSet.add(s1); //重复的元素会覆盖		
		Object[] object = hashSet.toArray();//返回包含全部键的object类型数组
			
		System.out.println(object[0].toString());
 
**TreeSet：** <br>
treeset底层是基于treemap实现的一个tree形有序set，需要实现comparable接口可以实现定位，按升序排列。<br>
treeset和HashSet访问元素都是使用iterator。<br>

treeset的使用：

        TreeSet treeSet = new TreeSet();
		String s1 = "hello";
		String s2 = "abc";
		String s3 = "edf";
		
		treeSet.add(s1);
		treeSet.add(s2);
		treeSet.add(s3);
		
		for(Iterator it = treeSet.iterator(); it.hasNext();){  //使用iterator访问元素
			String tmp = it.next().toString();
			System.out.println(tmp + "--");
		}
		
		treeSet.floor(s2); //返回此 set 中小于等于s2的最大元素；不存在返回 null		
		treeSet.ceiling(s2); //返回此 set 中大于等于s2的最小元素；不存在返回 null
		treeSet.lower(s2);  //返回此 set 中小于s2的最大元素；不存在返回 null
		treeSet.higher(s2); //返回此 set 中大于s2的最小元素；不存在返回 null
		treeSet.pollFirst(); //获取并移除最小的元素
		String string=(String)treeSet.pollLast(); //获取并移除最大的元素
		System.out.println(string);

**HashSet和treeset比较：**<br>
1）HashSet是基于hash算法的，底层使用HashMap保存数据；treeset使用tree树形结构，treemap实现。<br>
2）HashSet性能优于treeset，通常使用HashSet，需要排序时使用treeset。<br>

参考文章：<br>
http://www.codeceo.com/article/java-collection-summary.html<br>
http://www.codeceo.com/article/java-collection-class.html<br>
http://www.imooc.com/article/1893<br>
http://blog.csdn.net/softwave/article/details/4166598<br>

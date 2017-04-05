趁着最近比较闲，静下心来准备把关于集合框架的东西好好整理一下，边学边整理。近阶段先是整理整体的知识点，一些接口，一些继承类以及它们的特性,用法，后续还会有一些常用的，比较重要的类的jdk源码剖析。<br>

Java集合框架详解之继承set接口：http://blog.csdn.net/JasonZhangOO/article/details/55807103<br>
Java集合框架详解之继承list接口：http://blog.csdn.net/JasonZhangOO/article/details/55807177<br>
Java集合框架详解之继承queue接口：http://blog.csdn.net/JasonZhangOO/article/details/55807197<br>
Java集合框架详解之继承map接口：http://blog.csdn.net/JasonZhangOO/article/details/55807685<br>
Java集合框架详解之一点小总结：http://blog.csdn.net/JasonZhangOO/article/details/55808011<br>

继承list接口
--------
list中允许有相同的元素，用户可以使用索引（类似数组下标）访问list元素，控制插入位置<br>
**ArrayList：**<br>
ArrayList实现了可变大小的数组，可以有null值，每个ArrayList实例都有一个容量（capacity），用来记录数组大小。ArrayList和linkedlist都是非同步的（unsynchronized），线程不安全，即如果多个线程同时访问，需要自己实现访问同步。<br>

ArrayList的使用：<br>

        ArrayList a1 = new ArrayList();		 
        String s1 = "hello";
        String s2 = "abc";
        String s3 = "edf";
        a1.add(s2);   //在集合末尾添加元素
        a1.add(0,s1); //在集合指定位置添加元素
        a1.add(s3);   //在集合可以添加重复元素
		 
        ArrayList a2 = new ArrayList();
        a2.add(s1);
		 
        a1.addAll(a2); //将指定集合添加到末尾
		a1.ensureCapacity(5);  //增加ArrayList容量 
        String s = (String)a1.get(a1.size()-1); //找到指定位置末尾的元素并强制转换类型

**linkedlist：**<br>
linkedlist可以有null值，提供额外的Get、Remove、Insert等方法在LinkedList的首部或尾部操作数据。这些操作使得 LinkedList 可被用作堆栈（Stack）、队列（Queue）或双向队列（Deque）。<br>

LinkedList的使用：<br>

        	LinkedList l = new LinkedList();
		String s1 = "hello";
		String s2 = "abc";
		String s3 = "edf";
		
		l.add(s2);      //在集合中添加元素
		l.addFirst(s1); //在集合首部添加元素
		l.addLast(s3);  //在集合尾部添加元素
		
		String s = (String)l.getFirst(); //查询首部的元素
		String ss = (String)l.get(2);    //查询指定位置的元素
		
		l.removeLast();              //删除尾部元素
		l.removeFirstOccurrence(s);  //删除从首到尾第一个和s相同的元素

**vector:**<br>
Vector可以实现可增长的对象数组,Vector的大小可以根据需要增大或缩小，以适应创建Vector后进行添加或移除项的操作。<br>
vector与ArrayList类似，但vector是同步的，即线程安全，当一个Iterator被创建而且正在被使用，另一个线程改变了 Vector的状态（例如，添加或删除了一些元素），这时调用Iterator的方法时将抛出 ConcurrentModificationException，因此必须捕获该异常。<br>

vector的使用：

        	Vector v = new Vector();
		String v1 = "hello";
		String v2 = "abc";
		String v3 = "edf";
		
		v.addElement(v1);  //添加元素到向量末尾
		v.addElement(v2);
		//v.addElement(v3); 
		String s1 = (String)v.firstElement(); //查找向量的第一个元素
		String s2 = (String)v.lastElement();  //查找向量的最后一个元素
		v.ensureCapacity(10);                 //扩大向量大小
		v.removeElement(0);                   //去除第一个元素
		v.removeElement(s2);                  //去除第一个和s2相同的元素
		v.removeAllElements();                //去除所有的元素
		
		System.out.println(v.capacity());  //查询向量的大小
		System.out.println(v.isEmpty());   //查询向量是否为空

**stack：**<br>
上面有ArrayList，linkedlist，vector继承list接口，还有一个stack栈继承vector，实现了一个后进先出的栈结构。除了基本的 Push 和 Pop方法，还有Peek方法得到栈顶的元素，Empty方法测试堆栈是否为空，Search 方法检测一个元素在堆栈中的位置。<br>

stack的使用：

        	Stack s = new Stack();
		String s1 = "hello";
		String s2 = "abc";
		String s3 = "edf";
		
		s.push(s1);  //push进栈
		s.push(s2);
		s.push(s3);
		
		s.peek();   //取栈顶元素
		s.pop();    //pop出栈
		
		System.out.println(s.isEmpty());  //判断堆栈是否为空
		System.out.println(s.search(s2)); //在栈中查找元素并返回到栈顶的距离，栈顶为1


**Vector和ArrayList比较**<br>
1）首先现在vector工业上的用的比较少了，但是和ArrayList还是有一定的可比性。<br>
2）vector类中有synchronized方法保证其同步，所以vector类的对象是线程安全的，但是同步的同时会很影响执行的效率，如果不需要线程安全，ArrayList可以节约不必要的性能开销，效率较高。<br>
3）vector和ArrayList内部机制都是以数组的方式存储数据，当集合元素超过数组大小时需要扩充数组大小，vector每次增加1个数组大小，ArrayList每次增加0.5个数组大小，对于数据量比较大的集合使用vector较好。<br>
4）vector和ArrayList内部机制都是以数组的方式存储数据，所以有数组的特性，查询指定位置元素（随机存取），时间复杂度O（1）；移动指定位置元素（需要移动后面的所有元素）时间复杂度O(n-i）。<br>
linkedlist内部机制是链表方式存储，所以有链表的特性，查询指定位置元素，时间复杂度O(i）；移动指定位置元素时间复杂度O(1)。<br>

**ArrayList和linkedlist比较**<br>
1）ArrayList 和Vector是采用动态数组方式存储数据，LinkedList使用双向链表实现存储。<br>
2）ArrayList索引数据快，插入数据慢。LinkedList按序号索引数据需要移动指针，向前或向后遍历，所以索引指定位置元素慢；插入数据只需要记录元素的前后项即可，所以插入数度快。<br>

参考文章：<br>
http://www.codeceo.com/article/java-collection-summary.html<br>
http://www.codeceo.com/article/java-collection-class.html<br>
http://www.imooc.com/article/1893<br>
http://blog.csdn.net/softwave/article/details/4166598<br>

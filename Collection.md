
## <a name="t0"></a><a name="t0"></a><a id="JavaListSetMaphttpsblogcsdnnetzhangqunshuaiarticledetails80660974_0"></a>转载自:[Java集合中List,Set以及Map等集合体系详解(史上最全)](https://blog.csdn.net/zhangqunshuai/article/details/80660974)

## <a name="t1"></a><a name="t1"></a><a id="_2"></a>概述:

*   List , Set,  Map都是接口，前两个继承至Collection接口，Map为独立接口
*   Set下有HashSet，LinkedHashSet，TreeSet
*   List下有ArrayList，Vector，LinkedList
*   Map下有Hashtable，LinkedHashMap，HashMap，TreeMap
*   Collection接口下还有个Queue接口，有PriorityQueue类

![](https://img-blog.csdn.net/20180612094225630?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW5ncXVuc2h1YWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

## <a name="t2"></a><a name="t2"></a><a id="_13"></a>注意:

*   Queue接口与List、Set同一级别，都是继承了Collection接口。

    看图你会发现,LinkedList既可以实现Queue接口,也可以实现List接口.只不过呢, LinkedList实现了Queue接口。Queue接口窄化了对LinkedList的方法的访问权限（即在方法中的参数类型如果是Queue时，就完全只能访问Queue接口所定义的方法 了，而不能直接访问 LinkedList的非Queue的方法），以使得只有恰当的方法才可以使用。

*   SortedSet是个接口，它里面的（只有TreeSet这一个实现可用）中的元素一定是有序的。

## <a name="t3"></a><a name="t3"></a><a id="_20"></a>总结:

### <a name="t4"></a><a name="t4"></a><a id="Connection_21"></a>Connection接口:

—  **List 有序,可重复**

*   ArrayList

    **优点:** 底层数据结构是数组，查询快，增删慢。

    **缺点:** 线程不安全，效率高
*   Vector

    **优点:** 底层数据结构是数组，查询快，增删慢。

    **缺点:** 线程安全，效率低
*   LinkedList

    **优点:** 底层数据结构是链表，查询慢，增删快。

    **缺点:** 线程不安全，效率高

—**Set    无序,唯一**

*   HashSet

    底层数据结构是哈希表。(无序,唯一)

    如何来保证元素唯一性?

    1.依赖两个方法：hashCode()和equals()

*   LinkedHashSet

    底层数据结构是链表和哈希表。(FIFO插入有序,唯一)

    1.由链表保证元素有序

    2.由哈希表保证元素唯一

*   TreeSet

    底层数据结构是红黑树。(唯一，有序)
    
    1.如何保证元素排序的呢?

    自然排序

    比较器排序

    2.如何保证元素唯一性的呢?

    根据比较的返回值是否是0来决定

**针对Collection集合我们到底使用谁呢?(掌握)**

> 唯一吗?
> 
> > 是：Set
> > 
> > > 排序吗?
> > > 
> > > > 是：TreeSet或LinkedHashSet
> > > > 
> > > > 否：HashSet
> > > > 
> > > > 如果你知道是Set，但是不知道是哪个Set，就用HashSet。
> 否：List
> 
> > 要安全吗?
> > 
> > > 是：Vector
> > > 
> > > 否：ArrayList或者LinkedList
> > > 
> > > > 查询多：ArrayList
> > > > 
> > > > 增删多：LinkedList
> > > > 
> > > > 如果你知道是List，但是不知道是哪个List，就用ArrayList。
> 如果你知道是Collection集合，但是不知道使用谁，就用ArrayList。
> 
> 如果你知道用集合，就用ArrayList。

说完了Collection,来简单说一下Map.

### <a name="t5"></a><a name="t5"></a><a id="Map_76"></a>Map接口:

上图:

![这里写图片描述](https://img-blog.csdn.net/20180612135157564?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW5ncXVuc2h1YWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

Map接口有三个比较重要的实现类，分别是HashMap、TreeMap和HashTable。

*   TreeMap是有序的，HashMap和HashTable是无序的。
*   Hashtable的方法是同步的，HashMap的方法不是同步的。这是两者最主要的区别。

这就意味着:

*   Hashtable是线程安全的，HashMap不是线程安全的。
*   HashMap效率较高，Hashtable效率较低。

    如果对同步性或与遗留代码的兼容性没有任何要求，建议使用HashMap。 查看Hashtable的源代码就可以发现，除构造函数外，Hashtable的所有 public 方法声明中都有 synchronized关键字，而HashMap的源码中则没有。
*   Hashtable不允许null值，HashMap允许null值（key和value都允许）
*   父类不同：Hashtable的父类是Dictionary，HashMap的父类是AbstractMap

## <a name="t6"></a><a name="t6"></a><a id="_94"></a>重点问题重点分析:

### <a name="t7"></a><a name="t7"></a><a id="TreeSet_LinkedHashSet_and_HashSet__95"></a>(一).TreeSet, LinkedHashSet and HashSet 的区别

> **1. 介绍**
*   TreeSet, LinkedHashSet and HashSet 在java中都是实现Set的数据结构

*   TreeSet的主要功能用于排序
*   LinkedHashSet的主要功能用于保证FIFO即有序的集合(先进先出)
*   HashSet只是通用的存储数据的集合
> **2. 相同点**
*   Duplicates elements: 因为三者都实现Set interface，所以三者都不包含duplicate elements
*   Thread safety: 三者都不是线程安全的，如果要使用线程安全可以Collections.synchronizedSet()
> **3. 不同点**
*   Performance and Speed: HashSet插入数据最快，其次LinkHashSet，最慢的是TreeSet因为内部实现排序

*   Ordering: HashSet不保证有序，LinkHashSet保证FIFO即按插入顺序排序，**TreeSet安装内部实现排序，也可以自定义排序规则**
*   null:HashSet和LinkHashSet允许存在null数据，但是TreeSet中插入null数据时会报NullPointerException
> **4. 代码比较**
<pre class="prettyprint">  <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String args<span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        HashSet<span class="token generics function"><span class="token punctuation">&lt;</span>String<span class="token punctuation">&gt;</span></span> hashSet <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">HashSet</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        LinkedHashSet<span class="token generics function"><span class="token punctuation">&lt;</span>String<span class="token punctuation">&gt;</span></span> linkedHashSet <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">LinkedHashSet</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        TreeSet<span class="token generics function"><span class="token punctuation">&lt;</span>String<span class="token punctuation">&gt;</span></span> treeSet <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">TreeSet</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token keyword">for</span> <span class="token punctuation">(</span>String data <span class="token operator">:</span> Arrays<span class="token punctuation">.</span><span class="token function">asList</span><span class="token punctuation">(</span><span class="token string">"B"</span><span class="token punctuation">,</span> <span class="token string">"E"</span><span class="token punctuation">,</span> <span class="token string">"D"</span><span class="token punctuation">,</span> <span class="token string">"C"</span><span class="token punctuation">,</span> <span class="token string">"A"</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            hashSet<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">;</span>
            linkedHashSet<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">;</span>
            treeSet<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>

        <span class="token comment">//不保证有序</span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Ordering in HashSet :"</span> <span class="token operator">+</span> hashSet<span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">//FIFO保证安装插入顺序排序</span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Order of element in LinkedHashSet :"</span> <span class="token operator">+</span> linkedHashSet<span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">//内部实现排序</span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Order of objects in TreeSet :"</span> <span class="token operator">+</span> treeSet<span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div>
</pre>
> 运行结果:
> 
> Ordering in HashSet :[A, B, C, D, E] (无顺序)
> 
> Order of element in LinkedHashSet :[B, E, D, C, A] (FIFO插入有序)
> 
> Order of objects in TreeSet :[A, B, C, D, E] (排序)

### <a name="t8"></a><a name="t8"></a><a id="TreeSet_147"></a>(二).TreeSet的两种排序方式比较

##### <a id="1_148"></a>1.排序的引入(以基本数据类型的排序为例)

由于TreeSet可以实现对元素按照某种规则进行排序，例如下面的例子

<pre class="prettyprint"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyClass</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// 创建集合对象</span>
        <span class="token comment">// 自然顺序进行排序</span>
        TreeSet<span class="token generics function"><span class="token punctuation">&lt;</span>Integer<span class="token punctuation">&gt;</span></span> ts <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">TreeSet</span><span class="token generics function"><span class="token punctuation">&lt;</span>Integer<span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">// 创建元素并添加</span>
        <span class="token comment">// 20,18,23,22,17,24,19,18,24</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">20</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">18</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">23</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">22</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">17</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">24</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">19</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">18</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">24</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">// 遍历</span>
        <span class="token keyword">for</span> <span class="token punctuation">(</span>Integer i <span class="token operator">:</span> ts<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>i<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<div class="hljs-button {2}" data-title="复制"></div>
</pre>
> 运行结果:
> 
> 17
> 
> 18
> 
> 19
> 
> 20
> 
> 22
> 
> 23
> 
> 24

##### <a id="2_187"></a>2.如果是引用数据类型呢,比如自定义对象,又该如何排序呢?

测试类:

<pre class="prettyprint"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyClass</span> <span class="token punctuation">{</span>
    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        TreeSet<span class="token generics function"><span class="token punctuation">&lt;</span>Student<span class="token punctuation">&gt;</span></span> ts<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">TreeSet</span><span class="token generics function"><span class="token punctuation">&lt;</span>Student<span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">//创建元素对象</span>
        Student s1<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"zhangsan"</span><span class="token punctuation">,</span><span class="token number">20</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s2<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"lis"</span><span class="token punctuation">,</span><span class="token number">22</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s3<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"wangwu"</span><span class="token punctuation">,</span><span class="token number">24</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s4<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"chenliu"</span><span class="token punctuation">,</span><span class="token number">26</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s5<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"zhangsan"</span><span class="token punctuation">,</span><span class="token number">22</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s6<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"qianqi"</span><span class="token punctuation">,</span><span class="token number">24</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">//将元素对象添加到集合对象中</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s1<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s2<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s3<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s4<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s5<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s6<span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">//遍历</span>
        <span class="token keyword">for</span><span class="token punctuation">(</span>Student s<span class="token operator">:</span>ts<span class="token punctuation">)</span><span class="token punctuation">{</span>
            System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>s<span class="token punctuation">.</span><span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token operator">+</span><span class="token string">"-----------"</span><span class="token operator">+</span>s<span class="token punctuation">.</span><span class="token function">getAge</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div>
</pre>

Student.java:

<pre class="prettyprint"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Student</span> <span class="token punctuation">{</span>
    <span class="token keyword">private</span> String name<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> age<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token function">Student</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">super</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">// TODO Auto-generated constructor stub</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token function">Student</span><span class="token punctuation">(</span>String name<span class="token punctuation">,</span> <span class="token keyword">int</span> age<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">super</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>name <span class="token operator">=</span> name<span class="token punctuation">;</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>age <span class="token operator">=</span> age<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> String <span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> name<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setName</span><span class="token punctuation">(</span>String name<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>name <span class="token operator">=</span> name<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">getAge</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> age<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setAge</span><span class="token punctuation">(</span><span class="token keyword">int</span> age<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>age <span class="token operator">=</span> age<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<div class="hljs-button {2}" data-title="复制"></div>
</pre>

结果报错:

> ![](https://img-blog.csdn.net/20180612112054186?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW5ncXVuc2h1YWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
> 
> 原因分析：
> 
> 由于不知道该安照那一中排序方式排序，所以会报错。
> 
> 解决方法：
> 
> 1.自然排序
> 
> 2.比较器排序

###### <a id="1_260"></a>(1).自然排序

自然排序要进行一下操作：

1.Student类中实现  Comparable接口

2.重写Comparable接口中的Compareto方法

<pre class="prettyprint"><span class="token function">compareTo</span><span class="token punctuation">(</span>T o<span class="token punctuation">)</span>  比较此对象与指定对象的顺序。
<div class="hljs-button {2}" data-title="复制"></div>`

</pre>
<pre class="prettyprint"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Student</span> <span class="token keyword">implements</span> <span class="token class-name">Comparable</span><span class="token generics function"><span class="token punctuation">&lt;</span>Student<span class="token punctuation">&gt;</span></span><span class="token punctuation">{</span>
    <span class="token keyword">private</span> String name<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> age<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token function">Student</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">super</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">// TODO Auto-generated constructor stub</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token function">Student</span><span class="token punctuation">(</span>String name<span class="token punctuation">,</span> <span class="token keyword">int</span> age<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">super</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>name <span class="token operator">=</span> name<span class="token punctuation">;</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>age <span class="token operator">=</span> age<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> String <span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> name<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setName</span><span class="token punctuation">(</span>String name<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>name <span class="token operator">=</span> name<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">getAge</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> age<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setAge</span><span class="token punctuation">(</span><span class="token keyword">int</span> age<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>age <span class="token operator">=</span> age<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">compareTo</span><span class="token punctuation">(</span>Student s<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">//return -1; //-1表示放在红黑树的左边,即逆序输出</span>
        <span class="token comment">//return 1;  //1表示放在红黑树的右边，即顺序输出</span>
        <span class="token comment">//return o;  //表示元素相同，仅存放第一个元素</span>
        <span class="token comment">//主要条件 姓名的长度,如果姓名长度小的就放在左子树，否则放在右子树</span>
        <span class="token keyword">int</span> num<span class="token operator">=</span><span class="token keyword">this</span><span class="token punctuation">.</span>name<span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token operator">-</span>s<span class="token punctuation">.</span>name<span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">//姓名的长度相同，不代表内容相同,如果按字典顺序此 String 对象位于参数字符串之前，则比较结果为一个负整数。</span>
        <span class="token comment">//如果按字典顺序此 String 对象位于参数字符串之后，则比较结果为一个正整数。</span>
        <span class="token comment">//如果这两个字符串相等，则结果为 0</span>
        <span class="token keyword">int</span> num1<span class="token operator">=</span>num<span class="token operator">==</span><span class="token number">0</span><span class="token operator">?</span><span class="token keyword">this</span><span class="token punctuation">.</span>name<span class="token punctuation">.</span><span class="token function">compareTo</span><span class="token punctuation">(</span>s<span class="token punctuation">.</span>name<span class="token punctuation">)</span><span class="token operator">:</span>num<span class="token punctuation">;</span>
        <span class="token comment">//姓名的长度和内容相同，不代表年龄相同，所以还要判断年龄</span>
        <span class="token keyword">int</span> num2<span class="token operator">=</span>num1<span class="token operator">==</span><span class="token number">0</span><span class="token operator">?</span><span class="token keyword">this</span><span class="token punctuation">.</span>age<span class="token operator">-</span>s<span class="token punctuation">.</span>age<span class="token operator">:</span>num1<span class="token punctuation">;</span>
        <span class="token keyword">return</span> num2<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<div class="hljs-button {2}" data-title="复制"></div>
</pre>

运行结果:

> lis-----------22
> 
> qianqi-----------24
> 
> wangwu-----------24
> 
> chenliu-----------26
> 
> zhangsan-----------20
> 
> zhangsan-----------22

###### <a id="2_327"></a>(2).比较器排序

比较器排序步骤：

1.单独创建一个比较类，这里以MyComparator为例，并且要让其继承Comparator接口

2.重写Comparator接口中的Compare方法

<pre class="prettyprint"><span class="token function">compare</span><span class="token punctuation">(</span>T o1<span class="token punctuation">,</span>T o2<span class="token punctuation">)</span>      比较用来排序的两个参数。
<div class="hljs-button {2}" data-title="复制"></div>`

*   1</pre>

3.在主类中使用下面的 构造方法

<pre class="prettyprint"><span class="token function">TreeSet</span><span class="token punctuation">(</span>Comparator<span class="token operator">&lt;</span><span class="token operator">?</span> superE<span class="token operator">&gt;</span> comparator<span class="token punctuation">)</span>
          构造一个新的空 TreeSet，它根据指定比较器进行排序。
<div class="hljs-button {2}" data-title="复制"></div>`

*   1
*   2</pre>

测试类:

<pre class="prettyprint"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyClass</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">//创建集合对象</span>
        <span class="token comment">//TreeSet(Comparator&lt;? super E&gt; comparator) 构造一个新的空 TreeSet，它根据指定比较器进行排序。</span>
        TreeSet<span class="token generics function"><span class="token punctuation">&lt;</span>Student<span class="token punctuation">&gt;</span></span> ts<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">TreeSet</span><span class="token generics function"><span class="token punctuation">&lt;</span>Student<span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">MyComparator</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">//创建元素对象</span>
        Student s1<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"zhangsan"</span><span class="token punctuation">,</span><span class="token number">20</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s2<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"lis"</span><span class="token punctuation">,</span><span class="token number">22</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s3<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"wangwu"</span><span class="token punctuation">,</span><span class="token number">24</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s4<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"chenliu"</span><span class="token punctuation">,</span><span class="token number">26</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s5<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"zhangsan"</span><span class="token punctuation">,</span><span class="token number">22</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Student s6<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">Student</span><span class="token punctuation">(</span><span class="token string">"qianqi"</span><span class="token punctuation">,</span><span class="token number">24</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">//将元素对象添加到集合对象中</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s1<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s2<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s3<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s4<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s5<span class="token punctuation">)</span><span class="token punctuation">;</span>
        ts<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>s6<span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">//遍历</span>
        <span class="token keyword">for</span><span class="token punctuation">(</span>Student s<span class="token operator">:</span>ts<span class="token punctuation">)</span><span class="token punctuation">{</span>
            System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>s<span class="token punctuation">.</span><span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token operator">+</span><span class="token string">"-----------"</span><span class="token operator">+</span>s<span class="token punctuation">.</span><span class="token function">getAge</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<div class="hljs-button {2}" data-title="复制"></div>
</pre>

Student.java:

<pre class="prettyprint"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Student</span> <span class="token punctuation">{</span>
    <span class="token keyword">private</span> String name<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> age<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token function">Student</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">super</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">// TODO Auto-generated constructor stub</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token function">Student</span><span class="token punctuation">(</span>String name<span class="token punctuation">,</span> <span class="token keyword">int</span> age<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">super</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>name <span class="token operator">=</span> name<span class="token punctuation">;</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>age <span class="token operator">=</span> age<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> String <span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> name<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setName</span><span class="token punctuation">(</span>String name<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>name <span class="token operator">=</span> name<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">getAge</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> age<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setAge</span><span class="token punctuation">(</span><span class="token keyword">int</span> age<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>age <span class="token operator">=</span> age<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>

<div class="hljs-button {2}" data-title="复制"></div>
</pre>

MyComparator类：

<pre class="prettyprint"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyComparator</span> <span class="token keyword">implements</span> <span class="token class-name">Comparator</span><span class="token generics function"><span class="token punctuation">&lt;</span>Student<span class="token punctuation">&gt;</span></span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">compare</span><span class="token punctuation">(</span>Student s1<span class="token punctuation">,</span>Student s2<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// 姓名长度</span>
        <span class="token keyword">int</span> num <span class="token operator">=</span> s1<span class="token punctuation">.</span><span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span> s2<span class="token punctuation">.</span><span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">// 姓名内容</span>
        <span class="token keyword">int</span> num2 <span class="token operator">=</span> num <span class="token operator">==</span> <span class="token number">0</span> <span class="token operator">?</span> s1<span class="token punctuation">.</span><span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">compareTo</span><span class="token punctuation">(</span>s2<span class="token punctuation">.</span><span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">:</span> num<span class="token punctuation">;</span>
        <span class="token comment">// 年龄</span>
        <span class="token keyword">int</span> num3 <span class="token operator">=</span> num2 <span class="token operator">==</span> <span class="token number">0</span> <span class="token operator">?</span> s1<span class="token punctuation">.</span><span class="token function">getAge</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span> s2<span class="token punctuation">.</span><span class="token function">getAge</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">:</span> num2<span class="token punctuation">;</span>
        <span class="token keyword">return</span> num3<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></pre>

运行结果:

> lis-----------22
> 
> qianqi-----------24
> 
> wangwu-----------24
> 
> chenliu-----------26
> 
> zhangsan-----------20
> 
> zhangsan-----------22

#### <a id="__436"></a>(三). 性能测试

对象类:

<pre class="prettyprint"><span class="token keyword">class</span> <span class="token class-name">Dog</span> <span class="token keyword">implements</span> <span class="token class-name">Comparable</span><span class="token generics function"><span class="token punctuation">&lt;</span>Dog<span class="token punctuation">&gt;</span></span> <span class="token punctuation">{</span>
    <span class="token keyword">int</span> size<span class="token punctuation">;</span>
    <span class="token keyword">public</span> <span class="token function">Dog</span><span class="token punctuation">(</span><span class="token keyword">int</span> s<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        size <span class="token operator">=</span> s<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">public</span> String <span class="token function">toString</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> size <span class="token operator">+</span> <span class="token string">""</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">compareTo</span><span class="token punctuation">(</span>Dog o<span class="token punctuation">)</span> <span class="token punctuation">{</span>
       <span class="token comment">//数值大小比较</span>
        <span class="token keyword">return</span> size <span class="token operator">-</span> o<span class="token punctuation">.</span>size<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></pre>

主类:

<pre class="prettyprint"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyClass</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>

        Random r <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Random</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        HashSet<span class="token generics function"><span class="token punctuation">&lt;</span>Dog<span class="token punctuation">&gt;</span></span> hashSet <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">HashSet</span><span class="token generics function"><span class="token punctuation">&lt;</span>Dog<span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        TreeSet<span class="token generics function"><span class="token punctuation">&lt;</span>Dog<span class="token punctuation">&gt;</span></span> treeSet <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">TreeSet</span><span class="token generics function"><span class="token punctuation">&lt;</span>Dog<span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        LinkedHashSet<span class="token generics function"><span class="token punctuation">&lt;</span>Dog<span class="token punctuation">&gt;</span></span> linkedSet <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">LinkedHashSet</span><span class="token generics function"><span class="token punctuation">&lt;</span>Dog<span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">// start time</span>
        <span class="token keyword">long</span> startTime <span class="token operator">=</span> System<span class="token punctuation">.</span><span class="token function">nanoTime</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;</span> <span class="token number">1000</span><span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">int</span> x <span class="token operator">=</span> r<span class="token punctuation">.</span><span class="token function">nextInt</span><span class="token punctuation">(</span><span class="token number">1000</span> <span class="token operator">-</span> <span class="token number">10</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">10</span><span class="token punctuation">;</span>
            hashSet<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Dog</span><span class="token punctuation">(</span>x<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>

        <span class="token comment">// end time</span>
        <span class="token keyword">long</span> endTime <span class="token operator">=</span> System<span class="token punctuation">.</span><span class="token function">nanoTime</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">long</span> duration <span class="token operator">=</span> endTime <span class="token operator">-</span> startTime<span class="token punctuation">;</span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"HashSet: "</span> <span class="token operator">+</span> duration<span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">// start time</span>
        startTime <span class="token operator">=</span> System<span class="token punctuation">.</span><span class="token function">nanoTime</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;</span> <span class="token number">1000</span><span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">int</span> x <span class="token operator">=</span> r<span class="token punctuation">.</span><span class="token function">nextInt</span><span class="token punctuation">(</span><span class="token number">1000</span> <span class="token operator">-</span> <span class="token number">10</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">10</span><span class="token punctuation">;</span>
            treeSet<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Dog</span><span class="token punctuation">(</span>x<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        <span class="token comment">// end time</span>
        endTime <span class="token operator">=</span> System<span class="token punctuation">.</span><span class="token function">nanoTime</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        duration <span class="token operator">=</span> endTime <span class="token operator">-</span> startTime<span class="token punctuation">;</span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"TreeSet: "</span> <span class="token operator">+</span> duration<span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token comment">// start time</span>
        startTime <span class="token operator">=</span> System<span class="token punctuation">.</span><span class="token function">nanoTime</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;</span> <span class="token number">1000</span><span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">int</span> x <span class="token operator">=</span> r<span class="token punctuation">.</span><span class="token function">nextInt</span><span class="token punctuation">(</span><span class="token number">1000</span> <span class="token operator">-</span> <span class="token number">10</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">10</span><span class="token punctuation">;</span>
            linkedSet<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Dog</span><span class="token punctuation">(</span>x<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>

        <span class="token comment">// end time</span>
        endTime <span class="token operator">=</span> System<span class="token punctuation">.</span><span class="token function">nanoTime</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        duration <span class="token operator">=</span> endTime <span class="token operator">-</span> startTime<span class="token punctuation">;</span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"LinkedHashSet: "</span> <span class="token operator">+</span> duration<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>

<div class="hljs-button {2}" data-title="复制"></div>`

</pre>

运行结果:

> HashSet: 1544313
> 
> TreeSet: 2066049
> 
> LinkedHashSet: 629826
> 
> 虽然测试不够准确,但能反映得出，TreeSet要慢得多,因为它是有序的。

![嘿嘿](https://img-blog.csdn.net/20180612133411137?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW5ncXVuc2h1YWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

好了,至此完结.小伙伴有问题的话,请留言

参考文章:

[HashSet、TreeSet和LinkedHashSet的使用区别](https://www.jianshu.com/p/14bd5d9654fe)

[Collection集合总结](https://blog.csdn.net/czwx_24/article/details/51308706)

[HashMap、TreeMap和HashTable的区别](https://www.cnblogs.com/sidekick/p/8010522.html)

                                    </div>

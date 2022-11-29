## Java基础

### Java的特点

1. 面向对象的编程语言，具有继承，封装，多态三大特点。

   | 问题                             | 答案                                                         |
   | -------------------------------- | ------------------------------------------------------------ |
   | 什么是面向对象呢？               | 通过对事物进行建模来进行编程。例如：人是一个抽象的概念，我们可以将人具有的共同特征抽象出来，放在一个类中，把眼睛，鼻子，嘴巴作为类的属性，把跑，唱，跳等行为作为类的方法。 |
   | 面向对象和面向过程有什么区别呢？ | 面向过程是先想出解决问题的步骤，然后按照顺序逐步解决整个问题。而面向对象则是对问题进行建模，构建对象，通过对象之间的交互来解决整个问题。 |
   | 什么是多态呢？                   | 父类引用可以使用（指向）子类对象。有通过接口和抽象类两种方式来实现多态。 |
   |                                  |                                                              |

   

2. 跨平台。

   是指同一套`Java`代码可以多个不同的平台上运行。

   如何实现：通过将`Java`源代码编译生成得到字节码，然后再将字节码交给`JVM`去运行，不同平台的JVM是不同的。

   

3. 支持泛型

   参数化类型，即事先不确定具体类型，让类型成为一个参数，在具体运行的时候才确定具体的类型。

   好处：

   - 在源代码里面使用泛型，能大幅减少代码量。例如：`ArrayList`，它既可以保存`Integer`类型变量，也能保存`Double`类型变量，以及其他未知类型，在编译的时候就确定其中的具体类型，程序在编译的时候能够检查数据类型，避免在运行的时候拿数据的时候，发生`类型转换异常`。

4. 支持多线程



### 为什么说Java语言编译与解释并存

Java语言编写的程序到运行需要经过编译[^1]和解释[^2]两个阶段，首先将Java源代码编译为字节码，然后由JVM再对字节码进行解释。

好处：传统的编译型语言的跨平台能力不好，例如：`C++语言`，在windows平台上得到可执行文件（机器码），不能在Linux平台上运行[^3]。但是Java编译后得到的字节码，却能在各个平台上经过解释运行。



### 字符`型`常量和字符`串`常量的区别

所占空间大小：字符型常量占`2个字节`，字符串常量占`0`个或者`多个`字节。



### 重载与重写的区别

重写`override`：对于继承来自父类中的方法，对方法体中的内容重新编写，且抛出的异常必须是父类抛出异常的子类；方法的访问修饰符大于等于父类。

父类中若方法的返回值为引用类型，则子类中重写的方法返回值类型可以是被重写方法的子类。

重载`overload`：方法的参数不一样，其它的保持一致。



### 静态方法和实例方法的区别（N）

调用方式

- 静态方法是属于某个类，因此采用`类名.方法名`调用。而实例方法是属于某个对象，因此，采用`对象.方法名`调用。

访问类成员限制

- 静态方法只能访问静态成员（即静态方法，静态变量）。而实例方法没有这个限制，既能访问静态成员，也能访问非静态成员。



### 标识符和关键字的区别

标识符是我们用来为类，方法，变量取得一个名字，具有标识的作用，而关键字是java语言自带的，并且具有某种特殊功能的标识符，程序员不能命名和关键字同名的标识符。



### ==与equals的区别（N）

`equals`方法的底层实现还是`==`。该方法继承自`Object`超类。

```java
int a = 10;
int b = 10;
a == b // true
```

```java
String a = "HelloWorld";
String b = "HelloWorld";//首先JVM会从字符串常量池中检查是否存在该字符串对象，若存在该对象，则会重用该对象，即不会创建一个新的String类型对象，而是返回已存在的HelloWorld字符串对象的引用。
//特殊情况
Integer i6 = 100;
Integer i7 = 100;
//i6 == i7 是true
Integer i8 = 128;
Integer i9 = 128;
//i6 == i7 是false
```

```
在Java中，对于==，不管是基本数据类型还是引用数据类型，都是比较数值。
==对于基本数据类型，比较的两个数值是否相等；对于引用数据类型，比较是对象的内存地址。
```

`equals`只能用于判断两个引用类型的`对象`是否相等。

[参考文档]: https://segmentfault.com/a/1190000039132885	"参考链接"

### final关键字（N）

`final`声明的类是最终类，不能被继承。

`final`声明的接口是不合法的。

### hashcode()（待学习）

`Integer`类型对象的`hashcode()`就是那个值本身。

`String`的`hashcode()`就是这个`hashcode()`返回的值，

所以他们的`hashcode()`返回值只是为了在别的地方使用hash算法提供输入值吗？

对象`.hashcode()`：返回的是把该对象在内存中的地址经过哈希函数运算后得到的哈希码。



### Java中的基本数据类型，各自占用的空间，以及对应的包装类是什么？（N）

数字类型：byte(1)，**<u>short(2</u>**)，int(4)，<u>**long(8)**</u>，float(4)，double(8)

字符类型：char(1)——Character

布尔类型：boolean



### 包装类型的常量池技术（N）

当我们给`Integer`类型变量赋值时，实际上调用了`Integer.valueOf()`方法。但是首先会在`IntegerCache`内部创建一个包含了`-128-127`这个范围的`Integer[] cache`数组。

Java中的基本数据类型的包装类型，在内存中都有一个`常量池`（Integer,Byte,Character，除了`Float`和`Double`）

### 自动装箱和自动拆箱

装箱：将基本数据类型转换为对应的包装数据类型。

```java
Integer a = 10; //实际上是Integer a = Integer.valueOf(10)
```

拆箱：将`包装数据类型`转换为对应的`基本数据类型`。

```java
int b = a.intValue();
```

### 面向对象和面向过程的区别（N）

面向过程：将解决一个问题的分为若干步骤，然后用函数来实现每一个步骤，通过按照顺序调用这些函数解决最终问题。

优点：

- 符合人们日常的思维习惯

缺点：

- 扩展能力差。

- 不方便维护。

面向对象：通过对问题中涉及到的事物进行抽象建模，得到一些对象，对象中包含在这个问题中的一些属性和行为，然后通过这些对象的相互合作，共同解决这个问题。

优点：

- 易扩展。（继承，多态）
- 易维护。
- 易复用。（封装）

缺点：

- 代码量比面向过程更多。

### 成员变量和局部变量的区别(N)

1. 成员变量是属于`类`或者`对象`的，但是局部变量属于代码块或者方法的参数。即成员变量能被`private`,`protected`,`static`修饰，但是局部变量不能被`private`，`static`修饰。
2. 成员变量`有默认初始化值`（除了`final`修饰的变量以外），局部变量`没有默认初始值`。
3. 成员变量伴随着对象在内存中的存在而存在，伴随着对象的消失而消失。静态成员变量随着类在内存中的存在而存在，随着类的消失而消失。但是局部变量随着代码块的开始执行而存在，随着代码块的执行完毕或者方法的执行完毕就会消失。

### 对象实体和对象引用的区别

对象实体是内存中的某块具体的区域，而对象引用是这块内存区域在内存中的位置。



### 对象相等和指向他们的引用相等有什么不同

对象对应`java`中的一块内存区域。因此从物理存储的角度理解，不可能有两个一样的对象（内存区域）。但是在实际开发中，我们认为若两个对象的内容（成员变量值）相等时，两个对象就相等。

在`java`实际开发中，若两个对象的对应的成员变量值相等时，我们就认为两个对象相等。但是引用相等是指两个引用指向内存中的同一块区域。

### 一个类中的构造方法的作用？若一个类没有声明构造方法，该程序还能正确运行吗？

作用：构造方法既有无参，也有有参的，构造方法就是为了初始化对象的成员变量。

可以正常运行，因为若一个类中没有声明构造方法，java编译器在编译阶段会在字节码中加入无参的构造方法。



### 构造方法有哪些特点（N）

1. 没有返回值。
2. 不可以被重写`(override)`，但是可以被重载`(overload)`。
3. 方法名与类名相同。

### 面向对象的三大特征

#### 继承

#### 封装

#### 多态

相同的行为，不同的实现。语法：父类引用指向`子类的实例`或者接口指向`实现类对象`。

参数多态

子类型多态

- 接口多态。

- 抽象类多态。





## 集合

### 概述

​                          ![Collection_Structure](https://cdn.jsdelivr.net/gh/1907-peng/pictures/img/Collection_Structure.jpg)

容器主要分为存储对象（一个一个的）的`Collection`和存储键值对（一对一对）的`Map`。

#### List，Set，Queue，Map的区别(N)

`List`：存储的元素有序，可重复。

`Set`：存储的元素无序，不能重复。

`Queue`：按照`特定规则`确认先后顺序，存储的元素有序，可重复。

`Map`：存储键值对(`key-value`)，`key`不可以重复，无序；`value`可以重复，无序。

#### List和Queue的区别（N）

`Queue`只能在`头部`删除元素，在尾部`添加元素`。

`List`能在`任意位置删除`元素，在`任意位置添加`元素。

#### 底层数据结构(N)

List

`Vector`：`Object[]`数组，和`ArrayList`非常相似，但是`Vector`是线程安全的，因此性能比`ArrayList`差。

`ArrayList`：`Object[]`数组。

`LinkedList`：双链表。

Set

`HashSet`（无序）：基于`HashMap`实现

`LinkedHashSet`：是`HashSet`的子类，内部是通过`LinkedHashMap`实现的

Map

`HashMap`：JDK1.8之前是由数组+链表实现的

Queue

`PriorityQueue`：`Object[]`

Deque(Double Ended Queue)

`ArrayDeque`：`Object[]`+ `双指针`

Map

`HashMap`：`jdk1.8`之前一直都是`数组+链表`(链表用来解决`哈希冲突`，业内叫做采用`拉链法`解决哈希冲突)，`jdk1.8`以及之后改成了`数组+链表+红黑树`。

`LinkedHashMap`：在`HashMap`的基础上增加了一条双向链表来维持键值对的`插入顺序`。

`Hashtable`： `数组+链表`组成的，数组是 `Hashtable` 的主体，链表则是为了解决哈希冲突。

`TreeMap`：红黑树。

#### List接口

##### `ArrayList`和`Vector`的区别(N)

`ArrayList` 是 `List` 的主要实现类，底层使用 `Object[ ]`存储，线程不安全。

`Vector` 是 `List` 的古老实现类，底层使用`Object[ ]` 存储，线程安全的。

##### `Arraylist`与 `LinkedList`区别

- 是否线程安全：`ArrayList` 和 `LinkedList` 都是不保证线程安全。
- 底层数据结构：`Arraylist` 底层使用的是 **`Object` 数组**；`LinkedList` 底层使用的是 **双向链表** 数据结构。
- 插入和删除元素的时间复杂度是否受元素位置的影响。
   - `ArrayList`：由于底层是`Oject[]`数组，因此在进行删除或者插入元素操作的时候，如果在数组的最后插入元素，如果此时`Object[]`还没满，时间复杂度：`O(1)`，如果再加入最后一个元素的时候需要扩容，那么时间复杂度是多少
   - `LinkedList`：

##### ArrayList源码

以无参数构造方法创建 `ArrayList` 时，实际上初始化赋值的是一个空数组。当真正对数组进行添加元素操作时，才真正分配容量。

##### ArrayList扩容机制

最后成了调用`native`方法，有啥看的——就算是底层，操作也需要时间啊，更何况算法的时间复杂度已经脱离了具体的语言和机器。

研究源码的目的是为了减少扩容的次数，从而提升性能。

```java
/*
 * Copyright (c) 1997, 2013, Oracle and/or its affiliates. All rights reserved.
 * DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
 *
 * This code is free software; you can redistribute it and/or modify it
 * under the terms of the GNU General Public License version 2 only, as
 * published by the Free Software Foundation.  Oracle designates this
 * particular file as subject to the "Classpath" exception as provided
 * by Oracle in the LICENSE file that accompanied this code.
 *
 * This code is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
 * version 2 for more details (a copy is included in the LICENSE file that
 * accompanied this code).
 *
 * You should have received a copy of the GNU General Public License version
 * 2 along with this work; if not, write to the Free Software Foundation,
 * Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA.
 *
 * Please contact Oracle, 500 Oracle Parkway, Redwood Shores, CA 94065 USA
 * or visit www.oracle.com if you need additional information or have any
 * questions.
 */

package java.util;

import java.util.function.Consumer;
import java.util.function.Predicate;
import java.util.function.UnaryOperator;

/**
 * Resizable-array implementation of the <tt>List</tt> interface.  Implements
 * all optional list operations, and permits all elements, including
 * <tt>null</tt>.  In addition to implementing the <tt>List</tt> interface,
 * this class provides methods to manipulate the size of the array that is
 * used internally to store the list.  (This class is roughly equivalent to
 * <tt>Vector</tt>, except that it is unsynchronized.)
 *
 * <p>The <tt>size</tt>, <tt>isEmpty</tt>, <tt>get</tt>, <tt>set</tt>,
 * <tt>iterator</tt>, and <tt>listIterator</tt> operations run in constant
 * time.  The <tt>add</tt> operation runs in <i>amortized constant time</i>,
 * that is, adding n elements requires O(n) time.  All of the other operations
 * run in linear time (roughly speaking).  The constant factor is low compared
 * to that for the <tt>LinkedList</tt> implementation.
 *
 * <p>Each <tt>ArrayList</tt> instance has a <i>capacity</i>.  The capacity is
 * the size of the array used to store the elements in the list.  It is always
 * at least as large as the list size.  As elements are added to an ArrayList,
 * its capacity grows automatically.  The details of the growth policy are not
 * specified beyond the fact that adding an element has constant amortized
 * time cost.
 *
 * <p>An application can increase the capacity of an <tt>ArrayList</tt> instance
 * before adding a large number of elements using the <tt>ensureCapacity</tt>
 * operation.  This may reduce the amount of incremental reallocation.
 *
 * <p><strong>Note that this implementation is not synchronized.</strong>
 * If multiple threads access an <tt>ArrayList</tt> instance concurrently,
 * and at least one of the threads modifies the list structurally, it
 * <i>must</i> be synchronized externally.  (A structural modification is
 * any operation that adds or deletes one or more elements, or explicitly
 * resizes the backing array; merely setting the value of an element is not
 * a structural modification.)  This is typically accomplished by
 * synchronizing on some object that naturally encapsulates the list.
 *
 * If no such object exists, the list should be "wrapped" using the
 * {@link Collections#synchronizedList Collections.synchronizedList}
 * method.  This is best done at creation time, to prevent accidental
 * unsynchronized access to the list:<pre>
 *   List list = Collections.synchronizedList(new ArrayList(...));</pre>
 *
 * <p><a name="fail-fast">
 * The iterators returned by this class's {@link #iterator() iterator} and
 * {@link #listIterator(int) listIterator} methods are <em>fail-fast</em>:</a>
 * if the list is structurally modified at any time after the iterator is
 * created, in any way except through the iterator's own
 * {@link ListIterator#remove() remove} or
 * {@link ListIterator#add(Object) add} methods, the iterator will throw a
 * {@link ConcurrentModificationException}.  Thus, in the face of
 * concurrent modification, the iterator fails quickly and cleanly, rather
 * than risking arbitrary, non-deterministic behavior at an undetermined
 * time in the future.
 *
 * <p>Note that the fail-fast behavior of an iterator cannot be guaranteed
 * as it is, generally speaking, impossible to make any hard guarantees in the
 * presence of unsynchronized concurrent modification.  Fail-fast iterators
 * throw {@code ConcurrentModificationException} on a best-effort basis.
 * Therefore, it would be wrong to write a program that depended on this
 * exception for its correctness:  <i>the fail-fast behavior of iterators
 * should be used only to detect bugs.</i>
 *
 * <p>This class is a member of the
 * <a href="{@docRoot}/../technotes/guides/collections/index.html">
 * Java Collections Framework</a>.
 *
 * @author  Josh Bloch
 * @author  Neal Gafter
 * @see     Collection
 * @see     List
 * @see     LinkedList
 * @see     Vector
 * @since   1.2
 */

public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{
    private static final long serialVersionUID = 8683452581122892189L;

    /**
     * Default initial capacity.
     */
    private static final int DEFAULT_CAPACITY = 10;

    /**
     * Shared empty array instance used for empty instances.
     */
    private static final Object[] EMPTY_ELEMENTDATA = {};

    /**
     * Shared empty array instance used for default sized empty instances. We
     * distinguish this from EMPTY_ELEMENTDATA to know how much to inflate when
     * first element is added.
     */
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

    /**
     * The array buffer into which the elements of the ArrayList are stored.
     * The capacity of the ArrayList is the length of this array buffer. Any
     * empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
     * will be expanded to DEFAULT_CAPACITY when the first element is added.
     */
    transient Object[] elementData; // non-private to simplify nested class access

    /**
     * The size of the ArrayList (the number of elements it contains).
     *
     * @serial
     */
    private int size;

    /**
     * Constructs an empty list with the specified initial capacity.
     *
     * @param  initialCapacity  the initial capacity of the list
     * @throws IllegalArgumentException if the specified initial capacity
     *         is negative
     */
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+
                    initialCapacity);
        }
    }

    /**
     * Constructs an empty list with an initial capacity of ten.
     */
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }

    /**
     * Constructs a list containing the elements of the specified
     * collection, in the order they are returned by the collection's
     * iterator.
     *
     * @param c the collection whose elements are to be placed into this list
     * @throws NullPointerException if the specified collection is null
     */
    public ArrayList(Collection<? extends E> c) {
        elementData = c.toArray();
        if ((size = elementData.length) != 0) {
            // c.toArray might (incorrectly) not return Object[] (see 6260652)
            if (elementData.getClass() != Object[].class)
                elementData = Arrays.copyOf(elementData, size, Object[].class);
        } else {
            // replace with empty array.
            this.elementData = EMPTY_ELEMENTDATA;
        }
    }

    /**
     * Trims the capacity of this <tt>ArrayList</tt> instance to be the
     * list's current size.  An application can use this operation to minimize
     * the storage of an <tt>ArrayList</tt> instance.
     */
    public void trimToSize() {
        modCount++;
        if (size < elementData.length) {
            elementData = (size == 0)
                    ? EMPTY_ELEMENTDATA
                    : Arrays.copyOf(elementData, size);
        }
    }

    /**
     * Increases the capacity of this <tt>ArrayList</tt> instance, if
     * necessary, to ensure that it can hold at least the number of elements
     * specified by the minimum capacity argument.
     *
     * @param   minCapacity   the desired minimum capacity
     */
    public void ensureCapacity(int minCapacity) {
        int minExpand = (elementData != DEFAULTCAPACITY_EMPTY_ELEMENTDATA)
                // any size if not default element table
                ? 0
                // larger than default for default empty table. It's already
                // supposed to be at default size.
                : DEFAULT_CAPACITY;

        if (minCapacity > minExpand) {
            ensureExplicitCapacity(minCapacity);
        }
    }

    /**
     *
     * @param minCapacity size + 1
     */
    private void ensureCapacityInternal(int minCapacity) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            // DEFAULT_CAPACITY 10
            minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);
        }

        ensureExplicitCapacity(minCapacity);
    }

    private void ensureExplicitCapacity(int minCapacity) {
        //modCount add元素或者remove元素的次数 计数
        modCount++;

        // overflow-conscious code
        if (minCapacity - elementData.length > 0)
            grow(minCapacity);
    }

    /**
     * The maximum size of array to allocate.
     * Some VMs reserve some header words in an array.
     * Attempts to allocate larger arrays may result in
     * OutOfMemoryError: Requested array size exceeds VM limit
     */
    private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;

    /**
     * Increases the capacity to ensure that it can hold at least the
     * number of elements specified by the minimum capacity argument.
     *
     * @param minCapacity the desired minimum capacity
     */
    private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        //新容量是原容量的1.5倍
        int newCapacity = oldCapacity + (oldCapacity >> 1); //oldCapacity >> 1等价于 oldCapacity / 2
        //检查newCapacity是否溢出
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
    
    private static int hugeCapacity(int minCapacity) {
        if (minCapacity < 0) // overflow
            throw new OutOfMemoryError();
        return (minCapacity > MAX_ARRAY_SIZE) ? Integer.MAX_VALUE : MAX_ARRAY_SIZE;
    }


}
```

```java
public class Arrays {
    // Object[] elementData;
	public static <T> T[] copyOf(T[] original, int newLength) {
        return (T[]) copyOf(original, newLength, original.getClass());
    }

    public static <T,U> T[] copyOf(U[] original, int newLength, Class<? extends T[]> newType) {
        @SuppressWarnings("unchecked")
        T[] copy = ((Object)newType == (Object)Object[].class)
            ? (T[]) new Object[newLength]
            : (T[]) Array.newInstance(newType.getComponentType(), newLength);
        System.arraycopy(original, 0, copy, 0,
                         Math.min(original.length, newLength));
        return copy;
    }
}
```

add(E e)方法分析

```java
    /*
    先确保内部存放元素的数组的capacity(容量)能存放新的元素，然后再添加到数组中。
    */
	public boolean add(E e) {
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        elementData[size++] = e;
        return true;
    }
    private void ensureCapacityInternal(int minCapacity) {
        ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
    }
    private static int calculateCapacity(Object[] elementData, int minCapacity) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        }
        return minCapacity;
    }
```



#### Map接口

看它的源码，为什么不去准备`SpringSecurity`的源码？因为这样的话更加可控，并且`SpringSecurity`可以作为框架那块的重点复习内容。

##### `HashMap`和`HashTable`的区别

1. 线程安全：`HashMap` 是非线程安全的，`Hashtable` 是线程安全的，`Hashtable` 内部的方法基本都经过`synchronized` 修饰。（`Hashtable` 基本被淘汰）
2. 效率：因为`HashTable`保证了线程安全，所以效率肯定比`HashMap`低。

##### `HashMap`的底层实现

`jdk1.7`以前如何实现对`HashMap`进行元素添加：首先，通过得到`Key`对象的`hashCode()`方法得到值`A`，然后再调用`HashMap`中的`hash()`[^5]方法对`A`进行处理得到`B`，再通过`（n-1）& B`得到在数组中的位置（注：这里的`n`是指数组的长度）

`jdk1.8`以及以后当数组的长度`大于等于64`，且链表的长度`大于等于8`以后，会将该链表转换为`红黑树`。首先判断链表的长度是否大于8，若大于，再判断数组的大小，若小于64，默认大小是16，则对数组进行扩容。若发现数组的大小大于等于64，则把该链表转换为红黑树。

- `loadFactor`加载因子

   控制数组的疏密程度。默认是0.75，例如：默认数组的长度是16，当数组中的元素数量大于等于`16*0.75=12`时，就会对数组进行扩容，扩容会把原来所有的元素重新计算hash值（rehash）放入到扩容后的数组中，时间复杂度是多少？O（N）（需要遍历所有元素——包括链表，二叉树，数组，并把该元素重新放入新容器）



##### `HashMap`的长度为什么是 2 的幂次方

```java

    /**
     * The default initial capacity - MUST be a power of two.
     */
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16

    /**
     * The maximum capacity, used if a higher value is implicitly specified
     * by either of the constructors with arguments.
     * MUST be a power of two <= 1<<30.
     */
    static final int MAXIMUM_CAPACITY = 1 << 30;

    static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16); //1 ^ 1 = 0, 1 ^ 0 = 1,>>> 无符号右移16位，符号位也会跟着动，空位用0补齐。
    }
```

我们对`key`进行`hash`计算后，方法返回的值是`int`类型，也就是在`-2147483648 到 2147483647`之间，那为什么是`int`类型，而不是别的类型呢？`key.hashCode()`是`int`类型，而且为什么`h右移`正好是`32`的一半？

但是我们知道不能把40亿多个数作为数组的下标，但是我们只提供了一块连续的区域来存储这些数据，你只能访问内存的某块区域啊！因此我们就能利用`hash%n(map的长度)`来得到`数组的下标`。但是在程序里面却是`hash&(n-1)(n是2的整数次幂)`，采用这种方式的原因：`二进制位运算的速度`比`%`快[^8]。所以`hashmap`的长度必须是2的整数次幂。

两个疑问：`hash % n和hash & (n-1)(n是2的整数次幂)`是等价的吗？

`Hash % 2`的余数要么是`0，要么是1`，其实就是Hash值的二进制表示的最后一位就是余数，即`Hash&(2-1)`。

`Hash % 3`的余数只能是`0，1，2`其中一个，2的二进制是`10`，我们不能使用Hash值的二进制

`Hash % 4`的余数只能是`0，1，2，3`其中一个，3的二进制是`11`，Hash值的二进制表示的最后两位就是余数，即`Hash&(4-1)`

`Hash % 2^n`的余数就是Hash值得二进制表示得最后n位，即`Hash&(n-1)`。



[&代替%的参考文章]: https://keitzu.com/2021/use-bit-instead-of-modulo/



##### `HashMap`的遍历方式

迭代器

- `map.entrySet().iterator()`
- `map.keySet().iterator()`

Foreach

- `for(Map.Entry<,> entry: map.entrySet())`
- `for(Integer key: map.keySet())`

Lambda

- 

Stream API


##### 扩展

为什么`HashMap`的加载因子是0.75？

`HashMap`的两个主要问题：查询速度和数组空间大小，若我们为了尽可能地让`HashMap`的查询速度快，那么我们就要尽可能地减少哈希冲突，即我们可以尽可能让数组的大小更大，但是，这样的话，会导致数组的空间利用率不高，浪费了计算机资源；若为了提高数组的空间利用率，减小数组的大小，就会导致发生哈希冲突的可能性增加，查询速度减慢。所以：我们要保证一定的`查询速度`和`空间利用率`。

[参考文献]: https://www.jianshu.com/p/4176c0e929f1



##### `ConcurrentHashMap`和 `Hashtable`的区别

<img src="https://cdn.jsdelivr.net/gh/1907-peng/pictures/img/HashTable_Lock.png" alt="HashTable_Lock" style="zoom: 33%;" />

<img src="https://cdn.jsdelivr.net/gh/1907-peng/pictures/img/ConcurrentHashMap_Segment_Lock.jpg" alt="ConcurrentHashMap_Segment_Lock" style="zoom: 33%;" />

- 实现线程安全的方式：`Hashtable`在任意时刻只能由一个线程进行读写，相当于整个`Hashtable`被锁上了，其它线程在此时既不能对`Hashtable`进行读操作，也不能进行写操作，但事实上，多个线程对同一个资源进行读操作，不会出现错误。但是`Hashtable`的设计导致多个线程同时进行`读操作`时会出现阻塞，不能运行，效率变低。jdk1.7版本的`ConcurrentHashMap`通过把`桶数据`进行分段`segment`，对某一个`segment`进行写操作的时候，就获得这个`segment`的锁，实现了多个写操作并发执行。
- 底层数据结构：jdk1.7中`ConcurrentHashMap`是使用`分段的数组+链表`，jdk1.8中`ConcurrentHashMap`使用`Node数组+链表/红黑树`。`Hashtable`使用`数组+链表`。

##### `ConcurrentHashMap` 线程安全的具体实现方式

jdk1.7

底层：通过对桶数据进行分段`(segment)`，一个`segment`里面是由`HashEntry`数组组成，每个`HashEntry`是一个链表结构的元素，存储键值对数据。

```java
static class Segment<K,V> extends ReentrantLock implements Serializable {
}
```

jdk1.8

底层：数组+链表/红黑树，通过`CAS`和`synchronized`来保证线程安全，`synchronized`只锁定`当前链表`或者红黑树的头节点，	

##### `ConcurrentHashMap`源码

![ConcurrentHashMap_1.7_Structure](https://cdn.jsdelivr.net/gh/1907-peng/pictures/img/ConcurrentHashMap_1.7_Structure.png)

整个结构由一个`Segment`数组构成，数组的长度初始化之后不能改变（默认16），一个`Segment`就是一个类似`HashMap`的结构，且该`Segment`能够进行扩容

![Concurrent_HashMap_Java8](https://cdn.jsdelivr.net/gh/1907-peng/pictures/img/Concurrent_HashMap_Java8.png)

结构：Node 数组 + 链表 / 红黑树。当冲突链表达到一定长度时，链表会转换成红黑树。





[参考文档]: https://zhuanlan.zhihu.com/p/79219960

## I/O流

序列化：将对象（包括对象的类型，对象中的数据，对象中的数据的类型）转换为可以通过`网络传输`或者`能够存储在硬盘`的`字节序列`的过程。

反序列化：将字节序列重新转换为内存中对象的过程。



### 若在Java中不想对某个字段序列化，该如何处理？

用`transient`修饰修饰该字段。即当某个实例对象被序列化的时候，该字段的值就不会存储到字节序列中，且对该对象进行反序列化的时候，该字段的值是其对应数据类型的默认值，例如：该字段是`int`类型，那么反序列化之后，它的值就是0。

注意：

- 被`static`修饰的变量不属于任何对象，因此，该变量也不会被序列化。
- `transient`只能用于修饰变量，不能修饰类或者方法。

### 获取键盘输入的方法（待学习）

方法 1：通过 `Scanner`

```java
Scanner input = new Scanner(System.in);
String s  = input.nextLine();
input.close();
```

方法2：通过`BufferedReader`

方法3：通过`System.in.read`

### Java中的I/O流分为几种？

按照数据流向分为输入流和输出流。

按照操作单元来分，分为字节流和字符流。

按照流的角色来分，分为节点流和处理流。



### 既然有了字节流，为什么还要字符流？

[参考链接]: https://www.cnblogs.com/happyone/p/12663145.html



## Java并发

### 什么是进程，什么是线程，它们有什么关系和区别（N）

关系：进程是一个`运行的程序`，线程是进程中的`一段执行序列`，也就是说一个进程`至少有一段执行序列`，即至少有`一个线程`。如何理解执行序列，例如：小明写家庭作业，小明的任务是写完所有的家庭作业，进程的任务就是写完家庭作业，但是家庭作业有语文作业和数学作业，由于小明在任何一个时刻只能写一个作业，他可以选择先做完数学作业（线程A），再写语文作业（线程B），也可以选择做`5min数学作业`，然后做`5min语文作业`，然后再做`5min`数学作业。

区别：

1. 内存角度：进程拥有独立的内存单元，不同的进程占用不同的内存空间，但是一个进程内的线程共享该进程的内存。
2. 切换的开销：进程切换需要保存当前进程运行的所有信息，再重新加载新进程的必要信息。但是线程切换[^4]是指在一个进程内部进行线程之间的切换，但是线程共享进程的一些信息，因此，开销肯定比进程切换要小。
3. 进程是`资源分配的最小单位`，线程是`CPU调度的最小单位`。

### 并发和并行的区别

并发在某一时刻，只有一个任务在进行，但是在一段时间内，多个任务交替进行。

并行在某一个时刻，有多个任务同时进行。





### 线程的生命周期和状态（N）

| 状态名       | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| NEW          | `new Thread()`。这里所说的线程被创建，是指在`编程语言`的角度，在操作系统中，线程并没有被创建。 |
| RUNNABLE     | 线程处于运行状态，包括了操作系统中的Ready[^6]和Running[^7]状态。 |
| BLOCKED      | 阻塞状态，线程想要运行`一段被锁住的代码`，线程需要获得锁才能继续运行。 |
| WAITING[^9]  | 等待状态，需要别的线程叫ta一下（例如：通知），释放当前线程持有的锁。 |
| TIME_WAITING | 时限等待，**sleep(3000)**，睡醒之后进行RUNNABLE状态。        |
| TERMINATED   | 线程运行完毕。                                               |



### 为什么使用多线程（待学习）

- 使用多线程是为了实现多任务，提高系统资源利用率；不使用多线程就不能同时进行多个任务，计算机得资源利用率低，例如：整个程序就一个执行顺序流，当该进程在进行I/O操作的时候，CPU就只能空闲。但是若有多个执行流，当一个线程在进行I/O的时候，我们就可以让其它线程来运行。
- 多线程除了能够实现多任务之外，多进程也能实现多任务，多进程也能提高资源的利用率，那为什么使用多线程呢？多任务分为两种A和B：A是多个任务需要共同协作，最终完成一个共同的任务；B是多个任务之间，互不影响，没有联系，自己做自己的。多线程适合完成A种多任务。



对于一个程序来说，如果使用单线程，则整个系统只有一条执行流，若在执行过程中出现问题，即整个程序出现问题，不能运行下去。



### 使用多线程可能带来的问题（待学习）

[线程活跃性问题]: D:\天翼云盘同步盘\Markdown笔记\学习笔记\计算机\Java\基础\多线程.md



### 什么是上下文切换

上下文：线程运行到某个时间点，能够再次使该线程能够重新运行的所有状态信息，包括程序计数器，通用目的寄存器，栈。

切换：主动和被动。

主动：

- 主动让出CPU，例如调用了`sleep()`或者`wait()`等。
- 运行完毕或者被迫中止运行。

被动：

- 时间片用完。

- 调用了系统中断（待学习）

   

### sleep()方法和wait()方法的区别和共同点

区别

- `sleep()`可以在线程的任意地方执行，但是wait()必须要在`synchronized`块里面。

共同点：

- 都能让当前线程停止运行，都需要捕获`InterruptedException`。



### 为什么调用start()方法时会执行run()方法，那我们不能直接调用run()方法？（待学习）

因为`创建线程是操作系统`的事情，java语言不能自己创建线程，因此`start()`便是向操作系统发送请求创建线程，但是线程肯定要有执行的代码，`run()`便是作为线程的执行代码。（我的理解）因为`java虚拟机`会运行`run()`方法

`new`一个线程对象，此时该线程处于`NEW`状态，而调用`start()`完成线程的准备工作（为什么要这样设计？这里的准备工作是指什么？），线程`才进入就绪状态`，等待分配时间片，执行`run()`方法。但是直接调用`run()`方法，不会把`run()`放在另外一个线程中执行，而是当成`main`线程中的一个普通方法执行。

[参考链接1]: https://youle.zhipin.com/questions/e636924dc21c5095tnZ62dS1Elo~.html
[参考链接2]: https://zhuanlan.zhihu.com/p/95785186





### 讲一下Synchronized关键字

synchronized是一种`悲观锁`。

作用：`synchronized`关键字可以保证被它`修饰`的`方法`或者`代码块`在任意时刻只能有`一个线程执行`。

为了提高悲观锁的性能，提出了锁升级的概念。

[为什么synchronized可以实现线程同步]: https://tech.meituan.com/2018/11/15/java-lock.html



#### synchronized的使用

由于同步是为了同步多线程共享的资源，例如类，对象，因此我们加锁的时候就是对类和对象进行加锁。

对静态方法进行加锁就是对`类`进行加锁

```java
synchronized static void method() {
    //业务代码
}
```

对实例方法进行加锁就是对`对象`进行加锁

```java
synchronized void method() {
    //业务代码
}
```

对代码块进行加锁，有两种可能，一是对类进行加锁，另外一种是对对象进行加锁。

```java
synchronized(this) {
    //业务代码
}
//锁住某个指定对象
synchronized(object) {
    //业务代码
}
//锁住类
synchronized(类.class) {
    //业务代码
}
```



#### 可以使用synchronized修饰构造方法吗？（待学习）

答：不能，但是为什么不能？构造方法既不属于类，也不属于对象，因此对构造方法使用`synchronized`没有任何意义。











[^1]: 编译型：一次性将所有源代码编译为机器码。
[^2]: 解释型：一句一句地将源代码翻译为机器码，即需要执行哪行代码，就解释哪行代码。
[^3]: 那不是可以把同一套C语言代码，使用不同平台的编译器编译不就行了，不也能跨平台吗？答案是不行，若C语言程序中调用了与windows操作系统密切相关的API，则无法在Linux平台上编译运行。
[^4]: 若是从A进程的某个线程切换到B进程的某个线程，这叫进程切换了。

[^5]: 又叫干扰函数，其作用是为了减少碰撞。
[^6]: 线程已经被操作系统创建，只要线程被分配了CPU，该线程就可以运行了。
[^7]: 线程被分配了CPU，正在运行。
[^8]: 计算机进行`%`运算的方式：`A % B = A - (A / B) * B`，在大部分机器上，整数乘法指令需要`10`个以上的时钟周期，整数除法需要`30个`或者以上的时钟周期但是`加法，减法，位级运算和移位`只需要`1个`时钟周期。`A & (B-1)(B是2的整数次幂)`只需要`2个`时钟周期。体现出背书之间的差距了。

[^9]: 什么时候线程需要进入到wait状态呢？比如：当线程需要消耗某一个同步资源的时候，由于此时资源的数量不够，因此需要等待，即释放该资源的锁，直到该资源的数量能够满足自己的需要的时候，就可以被notify(唤醒)，重新获得锁。
# 抽象类

1. 抽象类不能被实例化,因为抽象类没有意义
2. 抽象类不一定要包含 abstract 方法。也就是说，抽象类可以没有 abstract 方法
3. 一旦类包含了 abstract 方法，则这个类必须声明为 abstract
4. abstract 只能修饰类的方法，不能修饰其他属性
5. 抽象类的价值更多作用是在于设计，是设计者设计好后，让子类继承并实现抽象类（）
6. 用 abstract 关键字来修饰一个方法时，这个方法就是抽象方法访问修饰符 abstract 返回类型 方法名(参数列表);//没有方法体
7. 如果一个类继承了抽象类，则它必须实现抽象类的所有抽象方法，除非它自己也声明为 abstract 类。
8. 抽象方法不能使用 private、final 和 static 来修饰，因为这些关键字都是和重写相违背的。

# 内部类

## 介绍：

一个类的内部又完整的嵌套了另一个类结构。被嵌套的类称为内部类（inner class），嵌套其他类的类称为外部类（oter class）。是我们类的第五大成员【类的五大成员：属性、方法、构造器、代码块、内部类】，内部类最大的特点就是可以直接访问私有属性，并且可以体现类与类之间的包含关系。

## 基本语法

```java
class Outer{ //外部类
    class Inner{ //内部类

    }
}
class Other{ //其他外部类

}
```

## 内部类的分类

- 定义在外部类局部位置上（比如方法内）：
  - 局部内部类（有类名）
  - 匿名内部类（没有类名，重点！！！！）
- 定义在外部类的成员外置上：
  - 成员内部类（没用 static 修饰）
  - 静态内部类（使用 static 修饰）

## 局部内部类

![](../图片/局部内部类.png)

> 总结：
>
> 1.  局部内部类定义在方法中/代码块
> 2.  作用域在方法或者代码块中
> 3.  本质仍然是一个类
> 4.  外部其他类---不能访问---->局部内部类（因为 局部内部类相当于是一个局部变量）
> 5.  如果外部类和局部内部类的成员重名时，默认遵循就近原则，如果想访问外部类的成员，则可以使用（外部类名.this.成员）去访问【例如】 System.out.println("外部类名 n2=" + 外部类名.this.n2);

## 匿名内部类

![](../图片/匿名内部类的创建过程.png)

> 可以使用 对象名.getClass() 来查看对象的运行类型。

## 成员内部类

1. 成员内部类可以使用四种修饰符来修饰(默认,public,private,protected)
2. 其他类访问成员内部类的方法如下：

```java
class Outer
{
	private int x = 3;

	class Inner//内部类
	{
           int x = 4;//默认转换为final变量
		void function()
		{
                   int x = 6;
			System.out.println("innner :" + Outer.this.x);
                   //x = 6; this.x = 4; Outer.this.x = 3;
		}
	}

	void method()
	{
		Inner in = new Inner();
		in.function();
	}
}

class  InnerClassDemo
{
	public static void main(String[] args)
	{
           //访问内部类成员方法一
		Outer out = new Outer();
		out.method();//通过在外部内建立方法，在其中建立内部类对象。间接访问内部类中方法。
          //访问内部类成员方法二
		Outer.Inner in = new Outer().new Inner();
		in.function();//通过直接建立内部类的对象访问其方法
   }
}

```

`重要：`

# 单列集合框架：

![](../图片/单列集合.png)
2、双列集合框架：
![](../图片/双列集合.png)

# Collection 接口

    1. Iterator对象称为迭代器，主要用于遍历Collection集合中的元素
    2. 所有实现了Collection接口的集合类都有一个Iterator()方法，用以返回一个实现了Iterator接口的对象，即可以返回一个迭代器。
    3. Iterator仅用于遍历集合，Iterator本身并不存放对象。
    4. 增强for循环就是一个简化版的迭代器。

# List 接口

    1. List集合类中元素有序（即添加顺序和取出顺序一致）、且可重复
    2. List集合中的每个元素都有其对应的顺序索引，即支持索引
    3. List容器中的元素对应一个整数型的序号记载其在容器中的位置，可以根据序号存取容器中的元素。

## ArrayList 的注意事项

    1. permits all elements,including null,ArraysList 可以加入null，并且多个
    2. ArrayList 是由数组来实现数据存储的；
    3. ArrayList基本等同于Vector，除了ArraysList是线程不安全（执行效率高，适合单线程）看源码，在多线程的情况下不建议使用ArrayList

## ArrayList 底层结构和源码分析<font color="red">（重点、难点）</font>

    1. ArrayList 中维护了一个Object类型的数组elementData.(transient Object[] elementData;)
    2. 当创建对象时，如果使用的是无参构造器，则初始elementData容量为0(jdk7是10)
    3. 当添加元素时：先判断是否需要扩容，如果需要扩容，则调用grow方法，否则直接添加元素到合适的位置。
    4. 如果使用的是无参构造器，如果第一次添加，需要扩容的话，则扩容elementData为10，如果需要再次扩容的话，则扩容elementData为1.5倍。
    5. 如果使用的是指定容量capacity的构造器，则初始elementData容量为capacity
    6. 如果使用的是指定容量capacity的构造器,如果需要扩容，则直接扩容elementData为1.5倍

![](../图片/Vector跟ArrayList比较.png)

# ArrayList 和 LinkedList 的比较

![](../图片/ArrayLIst和LinkedList.png)

1. 如果我们改查操作多，选择用 ArrayList。
2. 如果我们增删操作多，选择用 LinkedList

# 接口（Interface）、implements(实施、实现)

- 介绍
  接口就是给出一些没有实现的方法，封装到一起，到某个类要使用的时候，在根据具体情况把这些方法写出来。
  - 在 jdk7.0 前 接口里的所有方法都没有方法体，即都是抽象方法。
  - jkd8.0 后接口可以有<mark>静态方法（static）</mark>，<mark>默认方法(default)</mark>，也就是说接口中可以有方法具体实现。

`入门案例代码`

```java
//接口
public interface Usb {
	public void start();
	public void stop();
    //静态方法
    public static void Info(){
        System.out.println("我是一个静态方法....");
    }
    //默认方法
    public default void def(){
        System.out.println("我是一个默认方法...");
    }
}
//相机类
public class Camera implements Usb{
	Camera(){
		start();
		stop();
	}
	public void start() {
		System.out.println("相机开始工作！！！");
	}
	public void stop() {
		System.out.println("相机停止工作！！！");
	}
}
//测试类
public class Test {

	public static void main(String[] args) {
		Camera camera = new Camera();
	}
}
```

输出：

> 相机开始工作！！！  
> 相机停止工作！！！

# 使用细节：

- 一个类可以同时实现多个接口，用逗号隔开
- 接口中的属性，只能是 final 的，而且是 public static final 修饰符。  
  例如：int a = 1;实际是 public static fianl int a = 1;
- 接口不能继承其他的类，但是可以继承多个别的接口
- 接口的修饰符，只能是 public 和默认

# 接口的多态性

- 接口的多态跟类的多态相似
- 多态的继承性，案例如下：

```java
interface Usb{}
//继承Usb
interface Usb2 extends Usb{}
//在Camera中需要实现 Usb跟Usb2 中的所有方法
class Camera implements Usb2{

}
```

# HashSet

    1. HashSet 底层是 HashMap的
    2. 添加一个元素时，先得到hash值然后再转换成索引值
    3. 找到存储数据表table，看这个索引位置是否已经存放的有元素
    4. 如果当前索引位置没有元素，则直接添加
    5. 如果当前索引位置有元素，调用equals比较，如果相同，就放弃添加，如果不相同，则添加在末尾。（链表形式）
    6. 在java8中，如果一条链表的元素个数大于或等于TREEIFY_THRESHOLD(默然是8)，并且table的大小>=MIN_TREEIFY_CAPACITY(默认64)，就会进行树化（红黑树）

## HashSet 自定义添加机制：

    1. 重写对象的HashCode和equals方法(HashCode方法也必须重写，因为默认HashCode计算是根据对象进行计算的)
    2. 将HashCode改写是为了让符合要求的对象得到的Hash值相同。
    3. 改写equals方法是为了将两个对象符合要求的对象定义为同一个对象。

# LinkedHashSet

    1. 在LinkedHashSet中维护了一个hash表和双向链表有head和tail
    2. 每一个节点有pre和next属性，这样可以形成双向链表
    3. 在添加一个元素时，先求出hash值，再求索引。确定该元素在hashtable的位置，然后将添加的元素加入到双向链表（如果已经存在，不添加[原则和hashset一样]）
    4. 所以我们在遍历LinkedHashSet也能确保插入顺序和遍历顺序一致

> `注意事项`  
> HashSet 的底层实现的是一个 HashMap,而 LinkedHashSet 的底层实现的是一个 LinkedHashMap,
> 他们实际上都是实现了 HashMap

# Map 接口(JDK8)

    1. Map与Collection并列存在。用于保存具有映射关系的数据：Key-Value
    2. Map中的key和value可以是任何引用类型的数据，会封装到HashMap$Node对象中
    3. Map中的key不允许重复，原因和HashSet（线程不安全）一样（当key相同，但value不相同时，会用后面那个元素替换先前的元素）
    4. Map中的value可以重复
    5. Map的key可以为null，value也可以为null，注意key为null，只能有一个，value为null，可以多个。
    6. 常用String类作为Map的Key
    7. key和value之间存在单向一对一关系，即通过指定的key总能找到对应的value

## Map 接口遍历方式：

    1. containsKey：查找键是否存在
    2. keySet：获取所有键
    3. entrySet：获取所有关系
    4. values：获取所有的值
    5. 增强for
    6. 迭代器

# HashTable(线程安全)

    1. 存放元素是键值对：即k-v
    2. hashtable的键和值都不能为null，否则会抛出NullPointerException
    3. hashTable使用方法基本上和HashMap一样
    4. hashTable是线程安全的（synchronized）,hahsMap是线程不安全的
    5. 默认大小为11，临界值为length*0.75,当长度大于或等于临界值时扩容( length << 2 )+1

![](../图片/HashMap和HashTable.png)

# Properties

    1. Properties类继承自Hashtable类并且实现了Map接口，也是使用一种键值对的形式来保存数据。
    2. Properties还可以用于从xxx.properties文件中，加载数据到Properties类对象，并进行读取和修改。
    3. xxx.properties 文件通常作为配置文件

![](../图片/开发中集合的选择.png)

# TreeSet 和 TreeMap

    1. TreeSet底层维护的是一个TreeMap。
    2. 默认情况添加元素是无序的。
    3. TreeSet和TreeMap可以在构造方法中添加一个匿名 Comparator 类 并重写 compare 方法来实现自定义添加元素顺序，如下：

```java
		Set treeset = new TreeSet(new Comparator() {
			public int compare(Object a,Object b) {
				return ((String)b).length() - (((String)a)).length();
			}
		});
```

> 个人猜想： TreeMap 底层是一个二叉树，在重写 compare 方法后添加元素时，小的在左节点，大的在右节点。输出时按照前序遍历输出。【红黑树是特殊的二叉树】

# Collections 工具类

    1. Collections 是一个操作Set、List和Map的集合的工具类。
    2. Collections中提供了一系列静态方法对集合元素进行排序、查询、修改等操作。

- 常用方法（均为 static）
  - reverse: 反转 List 中元素的顺序
  - shuffle：对 List 集合元素进行随机排序
  - sort：根据元素的自然顺序排序
  - sort(List,Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
  - swap(List,int,int)将指定 List 集合中的 i 处元素和 j 处元素进行交换。

# 泛型

## 为什么要用泛型

    1. 不能对加入到集合ArrayList中的数据类型进行约束（不安全）
    2. 遍历的时候，需要进行类型转换，如果集合中的数据量较大，对效率有影响。

## 什么是泛型

    1. 泛型又称参数化类型，是jdk5.0出现的新特性，解决数据类型的安全性问题。
    2. 在类声明或实例化时只要指定好需要的具体类型即可。
    3. java泛型可以保证如果程序在编译时没有发出警告，运行就不会产生ClassCastException(类型转换异常)异常.同时，代码更简洁、健壮
    4. 泛型的作用是：可以在类声明时通过一个标识类中某个属性的类型，或者是某个方法的返回值的类型，或者是参数类型。

## 约束

    1. 泛型只能是引用数据类型，不能是基本数据类型
    2. 在指定泛型具体类型后，可以传入该类型或其子类
    3. 若不指定类型，则默认是Object类型

## 基本语法

```java
class 类名<T,R...>{ //...表示可以有多个泛型
    成员
}
```

> 注意细节：

1. 普通成员可以使用泛型（属性、方法）
2. 使用泛型的数组，不能初始化
3. 静态方法中不能使用类的泛型
4. 泛型类的类型，是在创建对象时确定的（因为创建对象时，需要指定确定类型）
5. 如果在创建对象时，没有指定类型，默认为 Object

## 自定义泛型接口

### 基本语法

```java
interface 接口名<T,R,M...>{

}
```

注意细节：

1. 接口中，静态成员也不能使用泛型(这个和泛型规定一样)
2. 泛型接口的类型，在继承接口或者实现接口时确定
3. 没有指定类型，默认为 Object

### 问题：

    1. 为什么静态成员不能使用泛型呢？
       1. 因为在静态成员是在类加载是就创建好的，所以如果将静态成员指定为泛型那么在类加载的时候就需要指定相应的类型，故静态成员无法指定为泛型。

## 泛型方法

### 基本语法

```java
修饰符<T,R...>返回类型 方法名(参数列表){

}
```

> 注意事项

    1. 泛型方法，可以定义在普通类中，也可以定义在泛型类中
    2. 当泛型方法被调用时，类型会确定
    3. public void eat(E e){},修饰符后没有<T,R...>的方法不是泛型方法，而是使用了泛型，如下：

```java
public void eat<R,T>(R r,T t){

}
```

## 泛型的继承和通配符

    1. 泛型不具备继承性
        List<Object> list = new ArrayList<String>(); //因为泛型不具备继承，所以会报错
    2. <?> 支持任意泛型类型
    3. <? extends A>:支持A类以及A类的子类，规定了泛型的上限
    4. <? super A>: 支持A类以及A类的父类，不限于直接父类，规定了泛型的下限

# 文件流

## 基本介绍

输入流：数据从数据源（文件）到程序（内存）的路径  
输出流：数据从程序（内存）到数据源（文件）的路径

## 创建文件的三种方式

```Java
new File(String pathname) //根据路径构建一个File对象
new File(File parent,String child) //根据父目录文件+子路径构建
new File(String parent,String child) //根据父目录+子路径构建

File.creteNewFile //创建新文件
```

## File 的常用方法

1、 getName() 得到文件名字
2、 getAbsolutePath() 得到文件绝对路径
3、 getParent() 得到文件父级目录
4、 length() 得到文件大小（字节）
5、 exists() 文件是否存在
6、 isFile() 是不是一个文件
7、 isDirectory() 是不是一个目录
8、 mkdir()创建一级目录、mkdirs()创建多级目录、delete()删除空目录或文件

## IO 流原理

1. I/O 是 Input/Output 的缩写，I/O 技术是非常实用的技术，用于处理数据传输。如读/写文件，网络通讯等。
2. Java 程序中，对数据的输入/输出操作以“流(stream)”的方式进行。
3. java.io 包下提供了各种“流”类和接口，用以获取不同类的数据，并通过方法输入或输出数据。
4. 输入 input：读取外部数据（磁盘、光盘、网络等存储设备的数据）到程序（内存）中。
5. 输出 output：将程序（内存）数据输出到磁盘、光盘等存储设备中

### 流的分类

1. 按操作数据单位不同分为：字节流（8bit）二进制文件(声音、视频、doc、pdf 等等)，字符流（按字符）文本文件
2. 按数据流的流向不同分为：输入流，输出流
3. 按流的角色不同分为：节点流、处理流/包装流

| 抽象基类 | 字节流       | 字符流 |
| :------- | :----------- | :----- |
| 输入流   | InputStream  | Reader |
| 输出流   | OutputStream | Writer |

## FileReader 和 FileWriter

FileReader 和 FileWriter 是字符流，即按照字符来操作 IO

- FileReader 相关方法：
  1. new FileReader(File/String)
  2. read : 每次读取单个字符，返回该字符，如果到文件末尾返回-1
  3. read(char[]) 批量读取多个字符到数组，返回读取到的字符数，如果到文件末尾返回-1

> 相关 API
>
> 1.  new String()
> 2.  new String(char[],off,len) 将 char[]的指定的部分转换成 String

### 注意：

FileWriter 使用后，必须关闭(close)或刷新(flush)，否则写入不到指定的文件

## 节点流和包装流的区别

![](../图片/节点流和包装流区别.png)

- 节点流和处理流的区别和联系

1. 节点流是底层流/低级流，直接跟数据源相接
2. 处理流(包装流)包装节点流，既可以消除不同节点流的实现差异，也可以提供更方便的方法来完成输入输出。
3. 处理流(也叫包装流)对节点进行包装，使用了修饰器设计模式，不会直接与数据源相连[修饰器设计模式]

- 处理流的功能主要体现在以下两个方面：
  1. 性能的提高：主要以增加缓冲的方式来提高输入输出的效率。
  2. 操作的便捷：处理流可能提供了一系列便捷的方法来一次输入输出大批量的数据，使用更加灵活方便

> 注意事项：  
>  BufferedReader 和 BufferedWriter 是按字符操作的,所以不要去操作 二进制文件[声音、视频、doc、pdf 等等]，可能造成文件损害

## 节点流和处理流

- 区别  
   节点流只能存储基本数据而对象流可以将对象存储到文件中例如
  将 Dog dog = new Dog("小黄",3)这个 dog 对象保存到文件中，并且能够从文件恢复。

## 序列化和反序列化

1. 序列化就是在保存数据时，保存数据的值和数据类型
2. 反序列化就是在恢复数据时，恢复数据的值和数据类型
3. 需要让某个对象支持序列化机制，则必须让其类是可序列化的，为了让某个类是课序列化的，该类必须实现如下两个接口之一：
   > Serializable //标记接口(推荐使用,因为里面是空的没有方法)  
   > Externalizable

### 注意事项和使用细节

1. 读写顺序要求一致。
2. 要求序列化或反序列化对象，需要 实现 Serializable
3. 序列化的类中建议添加 SerialVersionUID,提高版本兼容性。(给类绑定一个 ID,在以后更新类的属性和方法时不会被认为是一个新的类)
4. 序列化对象时，默认将里面所有属性都进行序列化，但除了 static 或 transient(短暂的、不被保存的) 修饰的成员
   > 打个比方，如果一个用户有一些敏感信息（如密码，银行卡号等），为了安全起见，不希望在网络操作（主要涉及到序列化操作，本地序列化缓存也适用）中被传输，这些信息对应的变量就可以加上 transient 关键字。
5. 序列化对象时，要求里面属性的类型也需要实现序列化接口
6. 序列化具备课继承性，也就是如果某类已经实现了序列化，则它的所有子类也已经默认实现了序列化

## 节点流和处理流

介绍：

1. InputStreamReader(Reader 的子类),可以将 InputStream(字节流)包装成 Reader(字符流)
2. OutputStreamWriter(Writer 的子类)，实现将 OutputStream(字节流)包装成 Writer(字符流)
3. 当处理纯文本数据时，如果使用字符流效率更高，并且可以有效解决中文问题，所以建议将字节流转换成字符流
4. 可以在使用时指定编码格式(比如 utf-8、gbk、gb2312、ISO8859-1 等)

# Properties 类(配置文件)

1. 配置文件的格式：
   键=值  
   键=值
2. 注意：键值对不需要有空格，值不需要用引号括起来，默认类型是 utf8.使用 字符流(Writer)保存中文，字节流(Output)保存 unicode 码

## Properties 的常见方法

1. load 加载配置文件的键值对 Properties 对象
2. list 将数据显示到指定的设备
3. getProperties(Key) 根据键获取值
4. setProperties(Key,value) 设置键值对到 Properties 对象
5. store 将 Properties 中的键值对存储到配置问价，在 idea 中，保存信息到配置问价，如果有中文<mark>(使用 字符流(Writer)保存中文，字节流(Output)保存 unicode 码)</mark>

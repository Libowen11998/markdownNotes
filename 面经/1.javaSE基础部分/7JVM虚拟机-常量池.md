

```java
/**一段代码中，先看 s3和s4字符串。String s3 = new String("1") + new String("1");，这句代码中现在生成了2最终个对象，是字符串常量池中的“1” 和 JAVA Heap 中的 s3引用指向的对象。中间还有2个匿名的new String("1")我们不去讨论它们。此时s3引用对象内容是”11”，但此时常量池中是没有 “11”对象的。
接下来s3.intern();这一句代码，是将 s3中的“11”字符串放入 String 常量池中，因为此时常量池中不存在“11”字符串，因此常规做法是跟 jdk6 图中表示的那样，在常量池中生成一个 “11” 的对象，关键点是 jdk7 中常量池不在 Perm 区域了，这块做了调整。常量池中不需要再存储一份对象了，可以直接存储堆中的引用。这份引用指向 s3 引用的对象。 也就是说引用地址是相同的。
最后String s4 = "11"; 这句代码中”11”是显示声明的，因此会直接去常量池中创建，创建的时候发现已经有这个对象了，此时也就是指向 s3 引用对象的一个引用。所以 s4 引用就指向和 s3 一样了。因此最后的比较 s3 == s4 是 true。

再看 s 和 s2 对象。 String s = new String("1"); 第一句代码，生成了2个对象。常量池中的“1” 和 JAVA Heap 中的字符串对象。s.intern(); 这一句是 s 对象去常量池中寻找后发现 “1” 已经在常量池里了。
接下来String s2 = "1"; 这句代码是生成一个 s2的引用指向常量池中的“1”对象。 结果就是 s 和 s2 的引用地址明显不同。图中画的很清晰。*/

public static void main(String[] args) {
    String s = new String("1");	//生成了两个对象 一个对象s 一个是常量池中"1"
    s.intern();
    String s2 = "1";
    System.out.println(s == s2);  //false

    //String中的intern()方法。“如果常量池中存在当前字符串, 就会直接返回当前字符串. 如果常量池中没有此字符串, 会将此字符串放入常量池中后, 再返回”。
    
    String s3 = new String("1") + new String("1");
    s3.intern();			//将11”字符串放入 String 常量池中
    String s4 = "11";		//会直接去常量池中创建,发现有"11"这个对象,也就是指向了s3引用对象的一个引用,引用就相同了
   	System.out.println(s3 == s4); //true
}


//s 和 s2 代码中，s.intern();，这一句往后放也不会有什么影响了，因为对象池中在执行第一句代码String s = new String("1");的时候已经生成“1”对象了。下边的s2声明都是直接从常量池中取地址引用的。 s 和 s2 的引用地址是不会相等的
//首先执行String s4 = "11";声明 s4 的时候常量池中是不存在“11”对象的，执行完毕后，“11“对象是 s4 声明产生的新对象。然后再执行s3.intern();时，常量池中“11”对象已经存在了，因此 s3 和 s4 的引用是不同的。
public static void main(String[] args) {
    String s = new String("1");
    String s2 = "1";
    s.intern();
    System.out.println(s == s2);	//false

     //String中的intern()方法。“如果常量池中存在当前字符串, 就会直接返回当前字符串. 如果常量池中没有此字符串, 会将此字符串放入常量池中后, 再返回”。

    String s3 = new String("1") + new String("1");//此时只有"1"对象,没有"11"对象
    String s4 = "11";			//s4直接引用"11",但是此时常量池中没有此对象,
    s3.intern();				//把"11"放入到常量池中,但是s3和s4的引用是不同的,所以结果为false
    System.out.println(s3 == s4);	//false
}
```





## intern() 方法

### 一个字符串，内容与此字符串相同，但一定取自具有唯一字符串的池。

```java
public class Test {
    public static void main(String args[]) {
        String Str1 = new String("www.runoob.com");
        String Str2 = new String("WWW.RUNOOB.COM");

        System.out.print("规范表示:" );
        System.out.println(Str1.intern());//www.runoob.com

        System.out.print("规范表示:" );
        System.out.println(Str2.intern());//WWW.RUNOOB.COM
    }
}
规范表示:www.runoob.com
规范表示:WWW.RUNOOB.COM
```





```java
public static void main(String[] args) {
 
    String s = new String("1");
    s.intern();

    String s2 = "1";

    System.out.println(s == s2);// false

}
```



第一句：`String s = new String("1");`

![img](D:\javaUseTools\Typora\images\String01)

第二句：`s.intern();`发现字符串常量池中已经存在"1"字符串对象，直接**返回字符串常量池中对堆的引用(但没有接收)**-->此时s引用还是指向着堆中的对象

第三句：`String s2 = "1";`发现字符串常量池**已经保存了该对象的引用**了，直接返回字符串常量池对堆中字符串的引用





```java
    public static void main(String[] args) {

        String s3 = new String("1") + new String("1");
        s3.intern();

        String s4 = "11";
        System.out.println(s3 == s4); // true
    }
```

第一句：`String s3 = new String("1") + new String("1");`注意：此时**"11"对象并没有在字符串常量池中保存引用**。

第二句：`s3.intern();`发现"11"对象**没有在字符串常量池中**，于是将"11"对象在字符串常量池中**保存当前字符串的引用**，并**返回**当前字符串的引用(但没有接收)

第三句：`String s4 = "11";`发现字符串常量池已经存在引用了，直接返回(**拿到的也是与s3相同指向的引用**)

根据上述所说的：最后会返回true~~~

- **如果常量池中存在当前字符串，那么直接返回常量池中它的引用**。
- **如果常量池中没有此字符串, 会将此字符串引用保存到常量池中后, 再直接返回该字符串的引用**！



```java
    public static void main(String[] args) {

        String s = new String("1");
        String s2 = "1";
        s.intern();
        System.out.println(s == s2);//false

        String s3 = new String("1") + new String("1");
        String s4 = "11";
        s3.intern();
        System.out.println(s3 == s4);//false
    }
```

```java
    public static void main(String[] args) {
        String s1 = new String("he") + new String("llo");
        String s2 = new String("h") + new String("ello");
        String s3 = s1.intern();
        String s4 = s2.intern();
        System.out.println(s1 == s3);// true
        System.out.println(s1 == s4);// true
    }
```
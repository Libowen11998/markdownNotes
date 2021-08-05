# 二、堆溢出

堆（Heap）是Java存放对象实例的地方。

堆溢出可以分为以下两种情况，这两种情况都会抛出OutOfMemoryError:java heap space异常：

### 1、内存泄漏

内存泄漏是指对象实例在新建和使用完毕后，仍然被引用，没能被垃圾回收释放，一直积累，直到没有剩余

内存可用。

如果内存泄露，我们要找出泄露的对象是怎么被GC ROOT引用起来，然后通过引用链来具体分析泄露的原因。

分析内存泄漏的工具有：Jprofiler，visualvm等。


```java
import java.util.ArrayList;
import java.util.List;
import java.util.UUID;
 
/**
 * 内存泄漏
 * @author feizi
 */
public class OOMTest {
 
	public static void main(String[] args) {
		
		List<UUID> list = new ArrayList<UUID>();
		while(true){
			list.add(UUID.randomUUID());
		}
	}
 
}
```

## 2、内存溢出

内存溢出是指当我们新建一个实力对象时，实例对象所需占用的内存空间大于堆的可用空间。

如果出现了内存溢出问题，这往往是程序本生需要的内存大于了我们给虚拟机配置的内存，这种情况下，我们可以采用调大-Xmx来解决这种问题。

```java

import java.util.ArrayList;
import java.util.List;
 
/**
 * 内存溢出
 * @author feizi
 */
public class OOMTest_1 {
	public static void main(String args[]){
		List<byte[]> byteList = new ArrayList<byte[]>();
		byteList.add(new byte[1000 * 1024 * 1024]);
	}
}
```



# 三、栈溢出

栈（JVM Stack）存放主要是栈帧( 局部变量表, 操作数栈 , 动态链接 , 方法出口信息 )的地方。注意区分栈和栈帧：栈里包含栈帧。

与线程栈相关的内存异常有两个：

a）、StackOverflowError(方法调用层次太深，内存不够新建栈帧)

b）、OutOfMemoryError（线程太多，内存不够新建线程）

### 1.递归调用一个方法,就会新建一个栈,导致栈溢出

```java
package DemoJVM相关;

public class Demo栈溢出 {

    public void stackOverFlowMethod(){
        stackOverFlowMethod();
    }
    /**
     * 通过递归调用方法,不停的产生栈帧,一直把栈空间堆满,直到抛出异常 ：
     * @param args
     */
    public static void main(String[] args) {
        Demo栈溢出 sof = new Demo栈溢出();
        sof.stackOverFlowMethod();
    }
}

```

### 2,循环持有对象

```java
package DemoJVM相关;

public class Demo栈溢出2 {
        public static void main(String[] args) {
            A obj = new A();
            System.out.println(obj.toString());
        }
}
class A {
    private int aValue;
    private B bInstance = null;

    public A() {
        aValue = 0;
        bInstance = new B();
    }

    @Override
    public String toString() {
        return "<" + aValue + ", " + bInstance + ">";
    }
}
class B {
    private int bValue;
    private A aInstance = null;

    public B() {
        bValue = 10;
        aInstance = new A();
    }

    @Override
    public String toString() {
        return "<" + bValue + ", " + aInstance + ">";
    }
}

```


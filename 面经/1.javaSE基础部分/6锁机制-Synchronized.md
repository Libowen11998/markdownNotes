## 详情视频:https://www.bilibili.com/video/BV18Z4y1P7N4?from=search&seid=11508022327868162390

# synchronized锁啥

synchronized:目的是实现线程同步,让多个线程依次排队获取某个资源,保证数据不会出错

synchronized究竟锁住的是什么

- #### 修饰方法

  - 修饰普通方法:**锁住的就是方法的调用者**(即:创建的SynTest1的引用synTest1)
  - 修饰静态方法:锁定的是类本身(即:例子中的SynTest1类)

- #### 修饰代码块:传入谁,就锁定谁

### synchronized修饰普通方法

两个线程的run()方法中分别调用了SynTest 中的方法func1() 和func()2()

所以此时锁住的就是创建的SynTest对象--->synTest1

- func1() 和func2() 都被synchronized 修饰的情况:此时线程会进行竞争 fun1()运行之后,fun2()才运行
- func1() 被synchronized修饰   func2()没有被修饰的情况:此时线程不会竞争 func()2先运行,fun1()后运行

```java
public class Test1 {
    public static void main(String[] args) {
        SynTest1 synTest1=new SynTest1();

        new Thread(new Runnable() {
            @Override
            public void run() {
                synTest1.func1();
            }
        },"线程1").start();

        new Thread(new Runnable() {
            @Override
            public void run() {
                synTest1.func2();
            }
        },"线程2").start();
    }

}

class SynTest1{
    //此处synchronized修饰普通方法
    public synchronized void func1(){
        try {
            TimeUnit.MILLISECONDS.sleep(3000);//毫秒,使方法休眠3秒
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("运行方法1");
    }
     //此处synchronized修饰普通方法
    public synchronized void func2(){
        System.out.println("运行方法2");
    }
}
```



### synchronized修饰静态方法的情况

此时虽然申请了两个SynTest1 引用对象 synTest1  synTest2 但是synchronized修饰的是静态方法

所以实际上锁住的资源是SynTest1这个类  所以此时线程也会发生竞争,所以导致fun1()先输出  fun2()后输出

- func1() 和func2() 都被synchronized 修饰的情况:此时线程会进行竞争 fun1()运行之后,fun2()才运行
- func1() 被synchronized修饰   func2()没有被修饰的情况:此时线程不会竞争 func()2先运行,fun1()后运行

```java
package Demo线程锁.SynStudent;

import java.util.concurrent.TimeUnit;

public class Test1 {
    public static void main(String[] args) {
        SynTest1 synTest1=new SynTest1();
        SynTest1 synTest2=new SynTest1();

        new Thread(new Runnable() {
            @Override
            public void run() {
                synTest1.func1();
            }
        },"线程1").start();

        new Thread(new Runnable() {
            @Override
            public void run() {
                synTest2.func2();
            }
        },"线程2").start();
    }

}

class SynTest1{
    public synchronized static void func1(){
        try {
//            TimeUnit.SECONDS.sleep(3);//秒
            TimeUnit.MILLISECONDS.sleep(3000);//毫秒
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("运行方法1");
    }

    public synchronized static void func2(){
        System.out.println("运行方法2");
    }
}
```



### synchronized修饰代码块的情况

#### synchronized() 括号中是什么,那么锁住的就是什么主要看锁住的东西到底有几个,如果是多个,那么就不竞争,如果是一个,就会引发竞争

synchronized (this) {//当前锁住的其实是类的实例对象

synchronized (SynTest3.class) {//当前锁住的其实是类SynTest3

```java
package Demo线程锁.SynStudent;

import java.util.concurrent.TimeUnit;

public class Test2 {
    public static void main(String[] args) {
        SynTest3 synTest3 = new SynTest3();//这里是放在循环之外,,
        for (int i = 0; i < 5; i++) {
//            SynTest3 synTest3 = new SynTest3();如果放在循环之内,那么就相当于申请五个资源,不存在竞争,就不阻塞
            new Thread(new Runnable() {
                @Override
                public void run() {
                    synTest3.fun2();
                }
            }, "线程" + i).start();
        }
    }
}

class SynTest3 {

    public synchronized void fun2() {

        synchronized (this) {//当前锁住的其实是类的实例对象synTest3

            System.out.println("start=======");
            try {
//            TimeUnit.SECONDS.sleep(3);//秒
                TimeUnit.MILLISECONDS.sleep(1000);//毫秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            System.out.println("end=======");
        }
    }


    public synchronized void fun() {
        System.out.println("start=======");
        try {
//            TimeUnit.SECONDS.sleep(3);//秒
            TimeUnit.MILLISECONDS.sleep(1000);//毫秒
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("end=======");
    }
}
```


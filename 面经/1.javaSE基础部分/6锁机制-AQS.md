![image-20210314160915232](C:\Users\Administrator.MACHENI-KA32LTP\AppData\Roaming\Typora\typora-user-images\image-20210314160915232.png)

```java
volatile int status=0;

Queue parkQueue;/11t list

void lock()(

while( ! compareAndSet(0,1))(

park();

//lock

10/HPI

unlock()

void unlock()f

lock_ notify();

]

void park()(

118 "19111141915

parkQueue . add(currentThread);114491 ifilicpu

releaseCpu();

]

void lock. notify()(

Thread t=parkQueue . header();

unpark(t);

]
```


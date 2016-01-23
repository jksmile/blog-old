

## Synchronized关键字知多少？

*   [前言](#preface)

*   [分析](#analyzed)

*   [总结](#summary)




<h3 id="preface">前言</h3>

***

JAVA多线程的同步机制对资源进行加锁，使得在同一个时间，只有一个线程可以进行操作，同步用以解决多个线程同时访问时可能出现的问题。

synchronized关键字为了解决同步问题应运而生！synchronized关键字修饰方法或者代码块，实现加锁-执行-解锁机制（这与MySQL事务如出一辙）。

那么问题来了，synchronized加锁机制是对方法或者代码块区域加锁还是对所操作对象加锁？

带着这个问题，扩展出来的问题多多，总结以下：

1. synchronized对非static方法修饰，是方法级别的加锁？还是对象级别的加锁？
 
2. synchronized对非static方法中代码块修饰，是方法级的加锁？还是对象级别的加锁？

3. synchronized对static方法修饰，是所属类中方法级别的加锁？还是类级别加锁？

4. synchronized对static方法中代码块修饰，是类方法级别加锁？还是类级别的加锁？


<h3 id="analyzed">分析</h3>

***

**1.synchronized对非static方法修饰，是对方法区域加锁？还是对所属对象加锁？**


    public class SynchronizedTest extends Thread{
    
        public static void main(String[] args){
        
            SynchronizedTest  synchronizedTest = new SynchronizedTest();
            
            synchronizedTest.start();
            
            a.test3();
            
            a.test2();
        }
        
        
        @Override
        public void run(){
        
            test1();
        }
        
        public synchronized void test1(){
        
            try {
            
                Thread.sleep(5000);
    
                System.out.println("Test1 over!");
    
            } catch (InterruptedException e) {
                
                e.printStackTrace();
            }
        
        }
        
        
        public synchronized void test2(){
        
            System.out.println("test2 over!");
        
        }
        
        public void test3(){
        
            System.out.println("test3 over!");
        
        }
        
    }


    运行结果：
    
    test3 over!
    Test1 over!
    Test2 over!
    
    Process finished with exit code 0



**结论：**根据以上DEMO可知，synchronized对非static方法修饰，加锁机制是在对象synchronizedTest区域内对所有synchronized修饰的方法进行监视的，对于某一线程访问synchronizedTest对象中synchronized修饰的方法A时，另一线程访问synchronizedTest对象中synchronized修饰的方法B时，需要等待synchronizedTest对象释放锁才能进行，而对于访问非synchronized修饰的方法不受影响。


***

**2. synchronized对非static方法中代码块修饰，是方法级的加锁？还是对象级别的加锁？**

    public class SynchronizedTest extends Thread{

    
        public static void main(String[] args) {
    
            SynchronizedTest a = new SynchronizedTest();
    
            a.start();
    
            a.test3();
    
            a.test2();
    
        }
    
        @Override
        public void run() {
            test1();
        }

    
        public  void test1(){
    
            System.out.println("Test1 synchronized before!");
    
            synchronized(this) {
                try {
    
                    Thread.sleep(5000);
    
                    System.out.println("Test1 over!");
    
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
    
        }
    
    
        public  void test2(){
    
            System.out.println("Test2 synchronized before!");
    
            synchronized(this){
    
                System.out.println("Test2 over!");
            }
    
        }
    
    
        public void test3(){
    
            System.out.println("test3 over!");
        }
        
    }

    
    运行结果：

    Test1 synchronized before!
    test3 over!
    Test2 synchronized before!
    Test1 over!
    Test2 over!
    
    Process finished with exit code 0


**结论：** 根据DEMO可知，synchronized修饰代码块，其作用的范围是大括号{}括起来的代码，作用的对象是调用这个代码块的对象；某一线程X访问SynchronizedTest对象中包含synchronized修饰的代码块的方法A时，另一线程Y访问SynchronizedTest对象中包含synchronized修饰的代码块的方法B并执行到synchronized修饰的部分时，需要等待synchronized对象释放锁，线程Y才能继续进行,而对于非synchronized修饰的方法不影响执行。

***


**3. synchronized对static方法修饰，是所属类中方法级别的加锁？还是类级别加锁？**


    public class SynchronizedTest extends Thread{
    
    
        @Override
        public void run() {
    
            test1();
        }
    
        public static void main(String[] args) {
    
    
            SynchronizedTest a = new SynchronizedTest();
    
            a.start();
    
            test3();
    
            test2();
        }
    
    
        public synchronized static void test1(){
    
                try {
    
                    Thread.sleep(5000);
    
                    System.out.println("Test1 over!");
    
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
        }
    
    
        public synchronized static void test2(){
    
                System.out.println("Test2 over!");
        }
    
    
        public static void test3(){
    
            System.out.println("test3 over!");
        }
    }
    
    
    运行结果：
    
    test3 over!
    Test1 over!
    Test2 over!
    
    Process finished with exit code 0


**结论：** 根据DEMO可知，synchronized修饰的static方法，其作用的范围是整个静态方法，作用的对象是这个调用这个类的所有对象。因为这个synchronized修饰的static方法是属于类所有的，并非属于某一实例对象，类的某个static方法在堆中是唯一存在的，所以对于所有调用这个类的synchronized修饰的static方法都需要等待类释放锁。
    
***
    

    
    
    public class SynchronizedTest extends Thread{
    
        @Override
        public void run() {
    
            test1();
        }
    
        public static void main(String[] args) {
    
            SynchronizedTest a = new SynchronizedTest();
    
            a.start();
    
            test3();
    
            test2();
        }
    
    
        public  static void test1(){
    
            System.out.println("Static test1 synchronized before!");
    
            synchronized(SynchronizedTest.class){
    
                try {
    
                    Thread.sleep(5000);
    
                    System.out.println("Test1 over!");
    
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
    
            }
    
    
        }
    
    
        public  static void test2(){
    
            System.out.println("Static test2 synchronized before!");
    
            synchronized(SynchronizedTest.class){
    
                System.out.println("Test2 over!");
            }
    
        }
    
    
        public static void test3(){
    
            System.out.println("test3 over!");
        }
    }


    运行结果：

    Static test1 synchronized before!
    test3 over!
    Static test2 synchronized before!
    Test1 over!
    Test2 over!
    
    Process finished with exit code 0

**结论：**根据DEMO可知，synchronized修饰static方法中的代码块 其作用的范围是synchronized后面括号括起来的部分，作用主的对象是这个类的所有对象。

***


<h3 id="summary">总结</h3>

***

1. 无论synchronized关键字加在方法上还是对象上，如果它作用的对象是非静态的，则它取得的锁是对象；如果synchronized作用的对象是一个静态方法或一个类，则它取得的锁是对类，该类所有的对象同一把锁。 

2. 每个对象只有一个锁（lock）与之相关联，谁拿到这个锁谁就可以运行它所控制的那段代码。 
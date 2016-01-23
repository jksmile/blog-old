

## 【创建型】单例模式

*   [定义](#define)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：单例模式就是在应用程序中，一个类只有一个实例的存在。

    单例模式的要点有三个；
    
        1.某个类只能有一个实例；
        2.它必须自行创建这个实例；
        3.它必须自行向整个系统提供这个实例。
    
    
    有很多应用程序中都有单例模式的应用，比如数据库连接【稍后分析】。
    
    单例类既可以被状态化，也可以无状态化。同时单例模式有利于内存回收。
    
    在Spring框架中，单例类隐身可见。
    
    
    

<h3 id="code">代码</h3>


***懒汉类型的单例模式***

    
    
    public class Singleton{
    
        //私有化构造方法
    	private Singleton(){
    
    	}
    
        
    	private static Singleton instance = null;
    
        //synchronized 多线程同步
    	public synchronized static Singleton getInstance(){
    
    		if( instance == null ){
    
    			new Singleton();
    
    		}
    		
    		return instance;
    	}
    	
    }
    
在static方法加上synchronized修饰，保证线程同步，但缺点就是每次调用类下面的getInstance方法都要获取锁、释放锁，效率不高！

对于以上懒汉类型的单例模式完全可以改进，如下：

    public class Singleton{
        
        private Singleton(){}
        
        private static Singleton singleton = null;
        
        public static Singleton getInstance(){
            
            if( singleton == null ){
            
                synchronized(Singleton.class){
                
                    if( singleton == null ){
                    
                        singleton = new Singleton();
                    }
                }
            
            }
            
            return singleton;
        }
    }
    
这样通过Singleton类下getInstance方法，通过验证singleton是否为空，如果空则其中一线程获得锁，执行实例化，后面获得锁的线程再次通过是否为null的判断，避免再次实例化！这样以后获取单例对象，再也不需要获得锁、释放锁，大大提高了效率。



***饿汉类型的单例模式***


        public class Singleton{
        
            //私有化构造方法
        	private Singleton(){
        
        	}
        
        	private static final Singleton instance = new Singleton();
        
            
        	public static Singleton getInstance(){
        
        		return instance;
        	
        	}
        	
        }
        

以上两类型的单例模式，推荐饿汉类型，饿汉类型的单例模式既实现了线程安全，又避免了同步带来的性能影响，而且代码简洁。



<h3 id="app">应用</h3>





***

相关推荐：[设计模式原则](./Principle)


上一篇：

下一篇：[【创建型】简单工厂模式](./SimpleFactory)








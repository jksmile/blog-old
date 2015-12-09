

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
    	public static synchronized Singleton getInstance(){
    
    		if( instance == null ){
    
    			new Singleton();
    
    		}
    		
    		return instance;
    	}
    	
    }
    




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
        

以上两类型的单例模式，推荐饿汉类型，饿汉类型的单例模式既实现了线程安全，又避免了同步带来的性能影响。



<h3 id="app">应用</h3>





***

相关推荐：[设计模式原则](./Principle)


上一篇：

下一篇：[简单工厂模式](./SimpleFactory)








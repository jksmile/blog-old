

## 【行为型】模板方法模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：蕨类定义一个操作中的算法的骨架，而将步骤延迟到子类中。模板方法使得子类可以不改变一个算法的结构即可重定义算法的某些特定步骤。
    
    模板方法模式角色：
    1.抽象类：实现模板方法，定义算法骨架
    2.具体类：实现抽象类中的抽象方法

<h3 id="UML">UML图</h3>

               _ _ _ _ _ _ _ _ _ _ _ _
              |                       |
              | TemplateAbstractClass |
              |_ _ _ _ _ _ _ _ _ _ _ _|
                         ↑      
                         | 
             ┌--------------------------┐        
      _ _ _ _|_ _ _ _ _ _      _ _ _ _ _|_ _ _ _ _ 
     |                   |    |                   |
     |   ConcreteClassA  |    |   ConcreteClassB  |
     |_ _ _ _ _ _ _ _ _ _|    |_ _ _ _ _ _ _ _ _ _|

   

<h3 id="code">代码</h3>

    public abstract Swim{

        public abstract void warmUp();
        
        
        public void do(){
        
            warmUp();
            
            System.out.println("Swimming now...");
        }
    }


***

    public A extends Swim{
    
        @Override
        public void warmUp(){
        
            System.out.println("Run a few minutes...");
        }
    
    }

***

    public B extends Swim{
    
        @Override
        public void warmUp(){
        
            System.out.println("Ride bike...");
        }
    
    }
***

  
    public class Client{


        public static void main(String[] args){
            
           Swim a = new A();
           a.do();
           
           
           Swim b = new B();
           b.do();
        }

    }

    运行结果：

        Run a few minutes...
        Swimming now...

        Ride bike...
        Swimming now...
        



<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】策略模式](./Strategy)

下一篇：[【行为型】观察者模式](./Observer)








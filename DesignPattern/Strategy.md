

## 【行为型】策略模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)


<img src="/logo.jpg" width="0" height="0" />

<h3 id="define">定义</h3>

    定义：定义一系列的算法,把每一个算法封装起来, 并且使它们可相互替换。本模式使得算法可独立于使用它的客户而变化。
    
    策略模式优点：
    1.相关算法系列 Strategy类层次为Context定义了一系列的可供重用的算法或行为。 继承有助于析取出这些算法中的公共功能
    2.提供了可以替换继承关系的办法
    3.消除了一些if else条件语句 ：Strategy模式提供了用条件语句选择所需的行为以外的另一种选择。当不同的行为堆砌在一个类中时 
      很难避免使用条件语句来选择合适的行为。将行为封装在一个个独立的Strategy类中消除了这些条件语句。含有许多条件语句的代码通
      常意味着需要使用Strategy模式
    4.实现的选择 Strategy模式可以提供相同行为的不同实现。客户可以根据不同时间 /空间权衡取舍要求从不同策略中进行选择
    
    @link http://blog.csdn.net/hguisu/article/details/7558249
    
    策略模式缺点：
    1.客户端必须知道所有的策略类，并自行决定使用哪一个策略类
    2.Strategy和Context之间的通信开销
    3.策略模式将造成产生很多策略类

<h3 id="UML">UML图</h3>

      _ _ _ _ _ _
     |           |
     |   Client  |
     |_ _ _ _ _ _|
           |
           |
      _ _ _↓_ _ _           _ _ _ _ _ _ _ _ _ _
     |           |         |                   |
     |  Context  |←--------| StrategyInterface |
     |_ _ _ _ _ _|         |_ _ _ _ _ _ _ _ _ _|
                                     ↑      
                                     | 
                         ┌--------------------------┐        
                  _ _ _ _|_ _ _ _ _ _      _ _ _ _ _|_ _ _ _ _ 
                 |                   |    |                   |
                 | ConcreteStrategyA |    | ConcreteStrategyB |
                 |_ _ _ _ _ _ _ _ _ _|    |_ _ _ _ _ _ _ _ _ _|

   

<h3 id="code">代码</h3>

    public interface Travel{

        public void travelStyle();
    }


***

    public class TrainTravel implements Travel{
    
        @override
        public void travelStyle(){
            
            System.out.println("Travel by train to Lhasa...");
        }
    
    }


***

    public class PlanTravel implements Travel{
    
        @override
        public void travelStyle(){
        
            System.out.println("Travel by plain to Lhasa...");
        }
    }

***

    public class ContextFactory{
    
        private Travel travel;
        
        public ContextFactory(Travel travel){
        
            this.travel = travel;
        }
    
        public void setTravel(Travel travel){
        
            this.travel = travel;
        }
    
        public void run(){
        
            travel.travelStyle();
        }
    }

***

    public class Client{


        public static void main(String[] args){
            
            ContextFactory contextFactory = new ContextFactory(new TrainTravel());
            
            contextFactory.run();
            
            contextFactory.setTravel(new PlainTravel());
            
            contextFactory.run();

        }

    }

    运行结果：

        Travel by train to Lhasa...

        Travel by plain to Lhasa...

        



<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【结构型】享元模式](./Flyweight)

下一篇：[【行为型】模版方法模式](./TemplateMethod)








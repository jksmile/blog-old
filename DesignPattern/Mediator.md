

## 【行为型】中介者模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：用一个中介者对象来封装一系列的对象交互。
    
        

    中介者模式中角色：
        1.中介者接口(MediatorAbstract): 中介者接口。在里面定义了各个同事之间相互交互所需要的方法，可以是公共的方法，如Change方法，也可以是小范围的交互方法
        2.具体中介者(ConcreteMediator): 具体的中介者实现对象。它需要了解并为维护每个同事对象，并负责具体的协调各个同事对象的交互关系
        3.抽象同事类(Colleague): 同事类的定义，通常实现成为抽象类，主要负责约束同事对象的类型，并实现一些具体同事类之间的公共功能，比如，每个具体同事类都应该知道中介者对象，也就是每个同事对象都会持有中介者对象的引用，这个功能可定义在这个类中
        4.具体同事类(ConcreteColleague): 具体的同事类，实现自己的业务，需要与其他同事对象交互时，就通知中介对象，中介对象会负责后续的交互
        

    中介者模式优点：
        1.中介者使得各对象不需要显式地相互引用，从而使其松散耦合，而且可以独立地改变它们之间的交互。
    

<h3 id="UML">UML图</h3>

     _ _ _ _ _ _ _ _ _   _ _ _ _ _ _ _ _ _ _
    |                 | |                   |
    | MediatorAbstract| | ColleagueAbstract |
    |_ _ _ _ _ _ _ _ _| |_ _ _ _ _ _ _ _ _ _|
      ↑                          ↑
      |              ____________|________
      |             |                     |
      |             |                     |
      |      _ _ _ _|_ _ _ _ _ _   _ _ _ _|_ _ _ _ _
      |     |                   | |                 |
      |     | ConcreteColleagueA| | ConcreteVisitorB|
      |     |_ _ _ _ _ _ _ _ _ _| |_ _ _ _ _ _ _ _ _|
      |         ↑                          ↑                    
      |         |                          |
      |         |                          |
     _|_ _ _ _ _|_ _ _                     | 
    |                 |                    |
    | ObjectStructure |---------------------
    |_ _ _ _ _ _ _ _ _|    



<h3 id="code">代码</h3>
    
    public abstract class PostOffice{
    
        public abstract void send();
        
        public abstract void receive();
    }

    
***

    public class BjPost extends PostOffice{
        
        private Poster sender;
        
        private Poster receiver;
        
        //Getter and Setter
        ...
        
        @override
        public void send(){
            
            sender.sendMsg();            
        }
        
        @override
        public void receive(){
        
            receiver.receiveMsg();
        }
    
    }

***

    public abstract class Poster{
    
        private PostOffice postOffice;
        
        public abstract void sendMsg();
        
        public abstract void receiveMsg();
    }
    
***

    public PosterA extends Poster{
    
        public PosterA(PostOffice postOffice){
            
            this.postOffice = postOffice;
        }
        
        @override
        public void sendMsg(){
            
            System.out.println("I'm posterA and just send message for district of Haidian.");
        }
        
        @override
        public void receiveMsg(){
            
            System.out.println("I'm posterA and just receive message from district of Chaoyang.");
        }
    }

***

    public PosterB extends Poster{
        
        public PosterB(PostOffice postOffice){
        
            this.postOffice = postOffice;
        }
        
        @override
        public void sendMsg(){
        
            System.out.println("I'm posterB and just send msg for Chaoyang.");
        }
        
        @override
        public void receiveMsg(){
        
            System.out.println("I'm posterB and just receive msg from Haidian.");
        }
    
    }

***

    public class Client{
    
        public static void main(String[] args){
        
            BjPost bjPost = new BjPost();
        
            PosterA posterA = new PosterA(bjPost);
            
            PosterB posterB = new PosterB(bjPost);
            
            bjPost.setSender(posterA);
            
            bjPost.setReceiver(posterB);
            
            bjPost.send();
            
            bjPost.receive();
        }
        
    }

    运行结果：
    
        I'm posterA and just send message for district of Haidian.
        
        I'm posterB and just receive msg from Haidian.
       


<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】访问者模式](./Visitor)

下一篇：[【行为型】解释模式](./Interpreter)








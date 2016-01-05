
## 【行为型】命令模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)






<h3 id="define">定义</h3>

    定义：将一个请求封装成一个对象，从而让你使用不同的请求把客户端参数化，对请求排队或者记录请求日志，可以提供命令的撤销和恢复功能。

    命令模式中角色：
        1.抽象命令角色(AbstractCommand):将共同执行的命令方法进行抽象
        2.具体命令角色(ConcreteCommand):对抽象类中的方法进行实现
        3.处理事务角色(Receiver):负责接收命令，并执行命令
        4.调用命令角色(Invoker):负责调用命令


    命令模式优点：
        1.封装性很好：每个命令都被封装起来，对于客户端来说，需要什么功能就去调用相应的命令，而无需知道命令具体是怎么执行的。比如有一组文件操作的命令：新建文件、复制文件、删除文件。如果把这三个操作都封装成一个命令类，客户端只需要知道有这三个命令类即可，至于命令类中封装好的逻辑，客户端则无需知道。
        2.在命令模式中，在接收者类中一般会对操作进行最基本的封装，命令类则通过对这些基本的操作进行二次封装，当增加新命令的时候，对命令类的编写一般不是从零开始的，有大量的接收者类可供调用，也有大量的命令类可供调用，代码的复用性很好。比如，文件的操作中，我们需要增加一个剪切文件的命令，则只需要把复制文件和删除文件这两个命令组合一下就行了，非常方便。
   
    命令模式缺点：
        1.最后说一下命令模式的缺点，那就是命令如果很多，随之对应的类也会增加
    
    

<h3 id="UML">UML图</h3>

       _ _ __ _      _ _ _ _ _      _ _ _ _ _ _ _ _ _ 
      |        |    |         |    |                 |
      | client |    | Invoker |---→| AbstractCommand |
      |__ _ _ _|    |_ _ _ _ _|    |_ _ _ _ _ _ _ _ _|
          |                                ↑            
          |                                |
          |                                |
          |      _ _ _ _ _ _        _ _ _ _|_ _ _ _ _
          └----→|           |      |                 |
                | Receiver  |←-----| ConcreteCommand |
                |_ _ _ _ _ _|      |_ _ _ _ _ _ _ _ _|
                



<h3 id="code">代码</h3>

    //调用命令角色
    public class CEO{
    
        private Leader leader;
        
        public void setCoder(Leader leader){
            
            this.leader = leader;
        }
        
        public void do(){
            
            leader.execute();
        }
    
    }

    
***

    //抽象命令角色
    public abstract class Leader{
    
        public abstract void execute();
    
    }
    

***
    
    //具体命令角色
    public class Jack extends Leader{
    
        private Coder coder;
    
        public Jack(Coder coder){
        
            this.coder = coder;
        }
        
        @implement
        public void execute(){
        
            coder.work();
        }
    }


***

    public class Coder{
    
        public void work(){
        
            System.out.println("I'm coder and I will do my best!");
        }
  
    }   



***

    public class Client{
    
        public static void main(String[] args){
        
            Coder coder = new Coder();
            
            Leader jack = new Jack(coder);
            
            CEO ceo = new CEO();
            
            ceo.setLeader(jack);
            
            ceo.do();
          
        }
    
    
    } 

    运行结果：
        
        I'm coder and I will do my best!
        

<h3 id="app">应用</h3>

   既然是命令模式，当然是大懒拖小懒，最后苦命的只有码农了...




***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】责任链模式](./ResponsibilityChain)

下一篇：[【行为型】备忘录模式](./Memento)








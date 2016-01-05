
## 【行为型】责任链模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)






<h3 id="define">定义</h3>

    定义：避免请求发送者与接收者耦合在一起，让多个对象都有可能接收请求，将这些对象连接成一条链，并且沿着这条链传递请求，直到有对象处理它为止。




<h3 id="UML">UML图</h3>

       _ _ _ _ _ _      _ _ _ _ _ _  _ _ _
      |           |    |                  |
      | client    |---→| AbstractHandler  |←---┐
      |_ _ _ _ _ _|    | requestHandler() |    |
                       |_ _ _ _ _ _  _ _ _|    |
                          ↑        ↑    |      |
                          |        |    |______|
                          |        |
         _ _ _ _ _ _ _ _ _|_      _|_ _ _ _ _ _ _ _ _
        |                   |    |                   |
        | ConcreteHandlerA  |    | ConcreteHandlerB  |
        | requestHandler()  |    | requestHandler()  |
        |_ _ _ _ _ _ _ _ _ _|    |_ _ _ _ _ _ _ _ _ _| 



<h3 id="code">代码</h3>


    public abstract class Manager{
    
        
        private Manager manager;
        
        
        public Manager getManager(){
        
            return manager;
        }
        
        public void setHandler(Manager manager){
        
            this.manager = manager;
        }
    
        public abstract void handleRequest(String requestContent);
        
    }

    
***


    public class Leader extends Manager{
    
        @implement
        public void handleRequest(String requestContent){
        
            if( getHandler() == null ){
            
                System.out.println("Leader agree for request:"+requestContent);
            }else{
            
                System.out.println("Leader have no power to handle the request.");
            
                getHandler().handleRequest(requestContent);
            }
            
        }
    
    }
    

***

    public class CEO extends Manager{
    
        @implement
        public void handleRequest(String requestContent){
        
            if( getHandler() == null ){
                
                System.out.println("CEO agree for request:"+requestContent);
            }else{
            
                System.out.println("CEO have no power to handle the request.");
                
                getHandler().handleRequest(requestContent);
            }
        }
    
    }


***

    public class Client{
    
        public static void main(String[] args){
        
            Manager leader = new Leader();
            
            Manager ceo = new CEO();
            
            leader.setHandler( ceo );
            
            
            leader.handleRequest("I'm a leader... I want to increase wages!");
        
        }
    
    
    } 

    运行结果：
        
        Leader have no power to handle the request.
        
        CEO agree for request:I'm a leader... I want to increase wages!
        

<h3 id="app">应用</h3>

    只有想起加薪水的时候，才会想起责任链模式！ -_-#




***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】迭代器模式](./Iterator)

下一篇：[【行为型】命令模式](./Command)








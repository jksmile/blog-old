

## 【结构型】代理模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)

<img src="/logo.jpg" width="0" height="0" />


<h3 id="define">定义</h3>

    定义：为其他对象提供一种代理以控制对这个对象的访问。
    
    代理模式几个角色：
        1.主题接口：提取真正使用类与代理类的公共方法
        2.真正主题：真正处理请求的类
        3.代理类：真正主题的代理类
    


<h3 id="UML">UML图</h3>


                
                
                     _ _ _ _ _ _ _ _ _
                    |                 |
                    |     Interface   |
                    |_ _ _ _ _ _ _ _ _|
                              ↑
                              |
            ┌---------------------------------┐
      _ _ _ |_  _ _ _ _ _              _ _ _ _|_ _ _ _ _ _
     |                   |            |                   |
     |        Proxy      |-----------→|     RealSubject   |
     |_ _ _ _ _ _ _ _ _ _|            |_ _ _ _ _ _ _ _ _ _|
               ↑             
               |
      _ _ _ _ _ _ _ _ _ _       
     |                   | 
     |      Client       |
     |_ _ _ _ _ _ _ _ _ _|  
    


<h3 id="code">代码</h3>

    public interface Network{

        public  void innerNet();
    }


***

    public class BeijingNetwork implements Network{

        @override
        public void innerNet(){

            System.out.println("This is inner net");
        }
    }


***

    public ProxyNetWork implements Network{

        private BeijingNetwork bjNetwork;


    public ProxyNetWork(){

            this.bjNetwork = new BeijingNetwork();
        } 


        @override
        public void innerNet(){

            bjNetwork.innerNet();
        }

    }

***

 
***

    public class Client{


        public static void main(String[] args){

            ProxyNetWork proxy = new ProxyNetWork();

            proxy.innerNet();            

        }

    }




<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【结构型】装饰器模式](./Decorator)

下一篇：[【结构型】外观模式](./Facade)








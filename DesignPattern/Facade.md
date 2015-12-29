

## 【结构型】外观模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)

<img src="/logo.jpg" width="0" height="0" />


<h3 id="define">定义</h3>

    定义：为子系统中的一组接口提供一个一致的界面，此模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。
    
    代理模式几个角色：
        1.外观角色：外观角色被客户端调用，它知道各个子系统的功能，可以根据客户端请求定制不同子系统的功能组合
        2.子系统角色：实现子系统的任务，并处理由外观对象触发的任务


    外观模式优点：
        1.外观模式对客户端屏蔽子系统组件，减少客户端调用子系统对象数目，外观模式使客户端调用变得简单
        2.实现子系统组件与客户端松耦合，子系统组件的改变不影响客户端的调用，只需要调整外观类
        3.提供了一个访问子系统的统一入口，并不影响用户使用子系统组件
        4.降低了编译依赖性，简化系统在不同平台之间的移植过程


    外观模式缺点：
        1.很难把握客户端通过外观类使用子系统的限制
        2.在不引用抽象类的情况下，添加新的子系统组件，可能需要修改外观类或者客户端代码，违背开闭原则
    


<h3 id="UML">UML图</h3>


                
                
                     _ _ _ _ _ _ _ _ _
                    |                 |
                    |     SubSystemA  |
                    |_ _ _ _ _ _ _ _ _|
                              ↑
                              |
            ┌-----------------┘
      _ _ _ |_  _ _ _ _ _              _ _ _ _ _ _ _ _ _ _
     |                   |            |                   |
     |        Facade     |-----------→|     SubSystemB    |
     |_ _ _ _ _ _ _ _ _ _|            |_ _ _ _ _ _ _ _ _ _|
               ↑             
               |
      _ _ _ _ _ _ _ _ _ _       
     |                   | 
     |      Client       |
     |_ _ _ _ _ _ _ _ _ _|  
    


<h3 id="code">代码</h3>

    public class GitAction{

        public void pull(){

            System.out.println("Pull the new content from remote...");
        }

        public void push(){

            System.out.println("push the local content to remote...");
        }


    }


***

    public class MvnAction(){

        public void mvnImport(){

            System.out.println("Import the new dependency jar...");
        }

        public void mvnInstall(){

            System.out.println("Compile the project file for run...");
        }

    }


***

    public class Facade(){

        private GitAction git;

        private MvnAction mvn;

        public Facade(GitAction git, MvnAction mvn){

            this.git = git;

            this.mvn = mvn;
        }

        public void updateProject(){

            git.pull();

            mvn.Import();

            git.push();
        }

    }


***

    public class Client{


        public static void main(String[] args){

            GitAction git = new GitAction();

            MvnAction mvn = new MvnAction();

            Facade facade = new Facade(git,mvn);

            facade.updateProject();


        }

    }

    
    运行结果：

        Pull the new content from remote...

        Import the new dependency jar...

        push the local content to remote...




<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【结构型】代理模式](./Proxy)

下一篇：[【结构型】桥接模式](./Bridge)








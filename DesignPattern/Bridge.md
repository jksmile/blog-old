

## 【结构型】桥接模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：将抽象部分与它的实现部分分离，使它们都可以独立地变化。
    
    代理模式几个角色：
        1.变化因素接口类： 将可变的因素抽象成接口，各因素来实现接口
        2.变化因素实现类： 实现变化因素接口
        3.桥接抽象类：与变化因素接口
        4.扩展桥接类：实现具体的业务


    外观模式优点：
        1.能对不同的变化因素进行分类管理
        2.实现对不同变化实现类解耦



<h3 id="UML">UML图</h3>


                
                
     _ _ _ _ _ _ _ _ _
    |                 |
    |       Client    |
    |_ _ _ _ _ _ _ _ _|
              |
              |
              |
      _ _ _ _ ↓ _ _ _ _ _              _ _ _ _ _ _ _ _ _ _
     |                   |            |                   |
     |   AbstractBridge  |-----------→|     interface     |
     |_ _ _ _ _ _ _ _ _ _|            |_ _ _ _ _ _ _ _ _ _|
               ↑                                 ↑
               |                                 |
      _ _ _ _ _ _ _ _ _ _                        |
     |                   |       ┌------------------------------┐
     |      MyBridge     |       |                              |                
     |_ _ _ _ _ _ _ _ _ _|       |                              |
                                 |                              |
                         _ _ _ _ | _ _ _ _ _          _ _ _ _ _ | _ _ _ _         
                        |   implementA      |        |    implementB     |
                        |_ _ _ _ _ _ _ _ _ _|        |_ _ _ _ _ _ _ _ _ _|

<h3 id="code">代码</h3>

    public interface {

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








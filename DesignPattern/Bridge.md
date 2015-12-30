

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


                
                
      _ _ _ _ _ 
     |         |
     | Client  |
     |_ _ _ _ _|
          |
          |
          |
      _ _ ↓_ _ __        _ _ _ _ _ _
     |           |      |           |
     | AbBridge  |-----→| interface |
     |_ _ _ _ _ _|      |_ _ _ _ _ _|
          ↑                  ↑
          |                  |
      _ _ _ _ _ _            |
     |           |  ┌------------------┐
     | MyBridge  |  |                  |
     |_ _ _ _ _ _|  |                  |
                    |                  |
            _ _ _ _ |_ _          _ _ _| _ _ _
           | implementA |        | implementB |
           |_ _  _ _ _ _|        |_ __ _ _ _ _|

<h3 id="code">代码</h3>

    public interface Car{

        public void run();


    }


***

    public class Audi implement Car{

        public void run(){

            System.out.println("Audi:Max speed 200km/h");
        }

    }


***

    public class Landrover implement Car{

        public void run(){

            System.out.println("Max speed 240km/h");
        }

    }

***

    abstract class CarCompete{

        private Car car;

        public Bridge(Car car){

            this.car = car;
        }

        public void run(){

            car.run();
        }

        public abstract void prize();

    }


***


    public class F1 extends CarCompete{


        public F1(Car car){

            super(car);
        }


        @override
        public void prize(){

            System.out.println("Congratulations! Gold medal will be provided by F1.");
        }

    }

***

    public class Client{

        public static void main(String[] args){


            Car audi = new Audi();

            F1 f1 = new F1(audi);

            f1.run();

            f1.prize();

        }

    }


    运行结果：

        Audi:Max speed 200km/h

        Congratulations! Gold medal will be provided by F1.



<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【结构型】外观模式](./Facade)

下一篇：[【结构型】组合模式](./Composite)








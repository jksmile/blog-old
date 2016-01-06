


## 【行为型】状态模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：当一个对象的内在状态改变时允许改变其行为，这个对象看起来像是改变了其类。

    命令模式中角色：
        1.抽象状态类(AbstractState): 将具体状态类行为定义一个抽象方法
        2.具体状态类(ConcreteState): 继续抽象状态类，实现具体的行为
        3.容器类(Context): 存储具体状态类


<h3 id="UML">UML图</h3>

     _ _ _ _ _      _ _ _ _ _ _ _ _
    |         |    |               |
    | Context |---→| AbstractState |
    |_ _ _ _ _|    |_ _ _ _ _ _ _ _|
                           ↑
                ___________|__________
               |                      |
               |                      |
        _ _ _ _|_ _ _ _        _ _ _ _|_ _ _ _
       |               |      |               |
       | ConcreteStateA|      | ConcreteStateB|
       |_ _ _ _ _ _ _ _|      |_ _ _ _ _ _ _ _|



<h3 id="code">代码</h3>

    public abstract class TripState{

        public abstract void handle(Context context);
    }

***

    public class DriverArrive extends TripState{


        public void handle(Context context){

            System.out.println("The driver have arrived and notice the guest. Waiting...");

            context.setTripState( new StartTrip() );
        }
    }


***

    public class StartTrip extends TripState{

        public void handle(Context context){

            System.out.println("The guests are ready! Go with perfect day.");
        }
    }

***

    public class Context{

        private TripState tripState;

        public Context(TripState tripState){

            this.tripState = tripState;
        }

        //Getter And Setter
        ...

        public void request(){

            tripState.handle(this);
        }
    }

***

    public class Client{

        public static void main(String[] args){

            Context trip = new Context( new DriverArrive() );

            trip.request();

            trip.request();

        }
    }

    运行结果：

        The driver have arrived and notice the guest. Waiting...

        The guests are ready! Go with perfect day.



<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】备忘录模式](./Memento)

下一篇：[【行为型】访问者模式](./Visitor)








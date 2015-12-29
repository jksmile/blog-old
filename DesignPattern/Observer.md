

## 【行为型】观察者模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)

<img src="/logo.jpg" width="0" height="0" />


<h3 id="define">定义</h3>

    定义：定义一种一对多的依赖关系，让多个观察者对象同时监听某一对象。这个主题对象在状态发生变化时，会通知所有观察
         者对象，使它们能做出相应的动作。

    模板方法模式角色：



<h3 id="UML">UML图</h3>

       _ _ _ _ _ _ _ _ _ _      _ _ _ _ _ _  _ _ _
      |                   |    |                  |
      |  AbstractSubject  |---→| AbstractObserver |
      |_ _ _ _ _ _ _ _ _ _|    |_ _ _ _ _ _  _ _ _|
               ↑                         ↑
               |                         |
               |                         |
       _ _ _ _ |_ _  _ _ _      _ _ _ _ _|_ _ _ _ _
      |                   |    |                   |
      |  ConcreteSubject  |←---| ConcreteObserver  |
      |_ _ _ _ _ _ _ _ _ _|    |_ _ _ _ _ _ _ _ _ _|



<h3 id="code">代码</h3>

    public abstract Leader{

        private ArrayList<Observer> observerList = new ArrayList<Observer>();

        public void addObserver(Observer observer){

            observerList.add(observer);
        }

        public void delObserver(Observer observer){

            observerList.remove(observer);
        }

        public void notify(){

            for(Observer observer : observerList){

                observer.do();
            }
        }
    }


***

    public abstract Observer{

        public abstract void do();
    }

***

    public class Teacher extends Leader{

        private String message;

        public void setMessage(String message){

            this.message = message;
        }

        public String getMessage(){

            return this.message;
        }
    }
***

    public class Monitor extends Observer{

        private String name;

        private String observerMessage;

        private Teacher teacher;

        public Monitor(Teacher teacher, String name){

            this.name = name;

            this.teacher = teacher;
        }


        public void do(){

            this.observerMessage = teacher.getMessage();

            System.out.println("The monitor of "+this.name+" get message from teacher:"+this.observerMessage);
        }



    }


***

    public class Client{


        public static void main(String[] args){

            Teacher teacher = new teacher();

            teacher.addObserver( new Monitor(teacher,"Jack") );

            teacher.addObserver( new Monitor(teacher,"Bill") );

            teacher.setMessage("I will have a rest for a few days.");

            teacher.notify();

        }

    }

    运行结果：

        The monitor of Jack get message from teacher: I will have a rest for a few days.

        The monitor of Bill get message from teacher: I will have a rest form a few days.




<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】模板方法模式](./TemplateMethod)

下一篇：[【行为型】迭代子模式](./Iterator)








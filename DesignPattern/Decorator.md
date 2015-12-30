

## 【结构型】装饰器模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：动态地给一个对象添加一些额外的职责或者行为。就增加功能来说， Decorator模式相比生成子类更为灵活。

    装饰器模式的组成：

        1.抽象组件角色(Component):定义一个对象接口，以规范准备接受附加责任的对象，即可以给这些对象动态地添加职责
        2.具体组件角色(ConcreteComponent):被装饰者，定义一个将要被装饰增加功能的类可以给这个类的对象添加一些职责
        3.抽象装饰器(Decorator):维持一个指向构件Component对象的实例，并定义一个与抽象组件角色接口一致的接口
        4.具体装饰器角色（ConcreteDecorator):向组件添加职责

    装饰器模式的特点：

        1.装饰对象和真实对象有相同的接口。这样客户端对象就可以以和真实对象相同的方式和装饰对象交互。
        2.装饰对象包含一个真实对象的索引（reference）
        3.装饰对象接受所有的来自客户端的请求。它把这些请求转发给真实的对象。
        4.装饰对象可以在转发这些请求以前或以后增加一些附加功能。这样就确保了在运行时，不用修改给定对象的结构就可以
          在外部增加附加的功能。在面向对象的设计中，通常是通过继承来实现对给定类的功能扩展。


<h3 id="UML">UML图</h3>


                  _ _ _ _ _ _
                 |           |
                 | Component |------┐
                 |_ _ _ _ _ _|      |
                        ↑           |
                        |           |
            ┌------------------┐    |
      _ _ _ |_  _ _ _ _      _ | _ _↓_ _
     |                 |    |           |
     |ConcreteComponent|    | Decorator |
     |_ _ _ _ _ _ _ _ _|    |_ _ _ _ _ _|
                                ↑
                                |
            ┌---------------------------┐
      _ _ _ |_  _ _ _ _ _        _ _ _ _|_ _ _ _ _ _
     |                   |      |                   |
     |ConcreteComponentX |      |ConcreteComponentY |
     |_ _ _ _ _ _ _ _ _ _|      |_ _ _ _ _ _ _ _ _ _|




<h3 id="code">代码</h3>

    public abstract class Exam{

        public abstract void doAction();
    }


***

    public class ExamImp extends Exam{

        @override
        public void doAction(){

            System.out.println("Do my best!");
        }
    }


***

    public abstract class Student extends Exam{

        protected Exam exam;


        public Student(Exam exam){

            this.exam = exam;
        }


        @override
        public void doAction(){

            exam.doAction();
        }

    }

***

    public class StudentA extends Student{

        public StudentA(Exam exam){

            Super(exam);
        }


        private void doBefore(){

            System.out.println("Have a good rest!");
        }


        private void doAfter(){

            System.out.println("Waiting for result!");
        }


        @override
        public void doAction(){

            doBefore();

            super.doAction();

            doAfter();
        }
    }


***

    public class Client{


        public static void main(String[] args){

            Exam exam = new ExamImp();

            Student studentA = new StudentA(exam);

            studentA.doAction();

        }

    }




<h3 id="app">应用</h3>

    1.需要在不影响其他对象的情况下，以动态、透明的方式给对象添加职责;

    2.如果不适合使用子类来进行扩展的时候，可以考虑使用装饰器模式;


***

相关推荐：[设计模式原则](./Principle)


上一篇：[【结构型】适配器模式](./Prototype)

下一篇：[【结构型】代理模式](./Proxy)








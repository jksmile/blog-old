

## 【结构型】代理模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：


<h3 id="UML">UML图</h3>


                        _ _ _ _ _ _ _ _ _
                       |                 |
                       |     Component   |------------┐
                       |_ _ _ _ _ _ _ _ _|            |
                                ↑                     |
                                |                     |
                ┌--------------------------------┐    |
          _ _ _ |_  _ _ _ _              _ _ _ _ | _ _↓_ _
         |                 |            |                 |
         |ConcreteComponent|            |     Decorator   |
         |_ _ _ _ _ _ _ _ _|            |_ _ _ _ _ _ _ _ _|
                                                  ↑
                                                  |
                                ┌---------------------------------┐
                          _ _ _ |_  _ _ _ _ _              _ _ _ _|_ _ _ _ _ _
                         |                   |            |                   |
                         |ConcreteComponentX |            |ConcreteComponentY |
                         |_ _ _ _ _ _ _ _ _ _|            |_ _ _ _ _ _ _ _ _ _|




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


上一篇：[【结构型】装饰器模式](./Decorator)

下一篇：[【结构型】外观模式](./Facade)








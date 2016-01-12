



## 【行为型】访问者模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：表示一个作用于某对象结构中的各元素的操作。它使你可以在不改变各元素的类的前提下定义作用于这些元素的新操作。

    访问者模式中角色：
        1.抽象访问者类(VisitorAbstract): 为ConcreteElement的每一个类声明一个visit操作
        2.具体访问者(ConcreteVisitor): 实现抽象访问者类声明的操作
        3.抽象元素类(ElementAbstract): 声明一个接受的操作，参数为一个访问者
        4.具体元素类(ConcreteElement): 具体的元素类实现抽象类的声明操作
        5.对象结构类(ObjectStructure): 能枚举它的元素，可以提供一个高层的接口以允许访问者访问它的元素


<h3 id="UML">UML图</h3>

     _ _ _ _ _      _ _ _ _ _ _ _ _ _
    |         |    |                 |
    | Context |---→| VisitorAbstract |
    |_ _ _ _ _|    |_ _ _ _ _ _ _ _ _|
      |                     ↑
      |          ___________|____________
      |         |                        |
      |         |                        |
      |  _ _ _ _|_ _ _ _ _        _ _ _ _|_ _ _ _ _
      | |                 |      |                 |
      | | ConcreteVisitorA|      | ConcreteVisitorB|
      | |_ _ _ _ _ _ _ _ _|      |_ _ _ _ _ _ _ _ _|
      |
      |
      |
     _↓_ _ _ _ _ _ _ _      _ _ _ _ _
    |                 |    |         |
    | ObjectStructure |---→| Element |
    |_ _ _ _ _ _ _ _ _|    |_ _ _ _ _|
                                ↑
                      __________|______________
                     |                         |
           _ _ _ _ _ | _ _ _ _       _ _ _ _ _ | _ _ _
          |                   |     |                 |
          | ConcreteElementA  |     | ConcreteElementB|
          |_ _ _ _ _ _ _ _ _ _|     |_ _ _ _ _ _ _ _ _|





<h3 id="code">代码</h3>

    public abstract class Visitor{

        public abstract void visitDeathPrisoner(DeathPrisoner deathPrisoner);

        public abstract void visitGeneralPrisoner(GeneralPrisoner generalPrisoner);
    }

***

    public class Police extends Visitor{

        @override
        public void visitDeathPrisoner(DeathPrisoner deathPrisoner){

            System.out.println("Dangerous level:"+deathPrisoner.getLevel()+". Don't touch with yourself!");
        }

        @override
        public void visitGeneralPrisoner(GeneralPrisoner generalPrisoner){

            System.out.println("Dangerous level:"+generalPrisoner.getLevel()+". Keep vigilance!");
        }

    }

***

    public class Worker extends Visitor{

        @override
        public void visitDeathPrisoner(DeathPrisoner deathPrisoner){

            System.out.println("Dangerous level:"+deathPrisoner.getLevel()+". Have no power to contact!");
        }

        @override
        public void visitGeneralPrisoner(GeneralPrisoner generalPrisoner){

            System.out.println("Dangerous level:"+generalPrisoner.getLevel());
        }
    }

***

    public abstract class Prisoner{

        private int level;

        public abstract void visit(Visitor visitor);

    }

***

    public class DeathPrisoner extends Prisoner{

        public DeathPrisoner(int level){

            this.level = level;
        }

        @override
        public void visit(Visitor visitor){

            visitor.visitDeathPrisoner(this);
        }
    }


***

    public class GeneralPrisoner extends Prisoner{

        public GeneralPrisoner(int level){

            this.level = level;
        }

        @override
        public void visit(Visitor visitor){

            visitor.visitGeneralPrisoner(this);
        }
    }



***

    public class Register{

        private ArrayList<Prisoner> allowVisitList = new ArrayList<Prisoner>();


        public void addRegister(Prisoner prisoner){

            allowVisitList.add(prisoner);
        }

        public void cancelRegister(Prisoner prisoner){

            allowVisitList.remote(prisoner);
        }

        public void acceptVisit(Visitor visitor){

            foreach(Prisoner prisoner:allowVisitList){

                prisoner.visit(visitor);
            }
        }
    }

***

    public class Client{


        public static void main(String[] args){

            Register register = new Register();

            register.addRegister( new DeathPrisoner(5) );

            register.addRegister( new GeneralPrisoner(1) );

            Police police = new Police();

            Worker worker = new Worker();

            register.acceptVisit( police );

            register.acceptVisit( worker );
        }
    }


    运行结果：

        Dangerous level:5. Don't touch with yourself!

        Dangerous level:2. Keep vigilance!

        Dangerous level:5. Have no power to contact!

        Dangerous level:2.



<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】状态模式](./State)

下一篇：[【行为型】中介者模式](./Mediator)










## 【结构型】享元模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：利用共享技术有效地支持大量细粒度的对象。
    
    在了解享元模式之前我们先要了解两个概念：
    内部状态：在享元对象内部不随外界环境改变而改变的共享部分。
    外部状态：随着环境的改变而改变，不能够共享的状态就是外部状态。

    享元模式中的角色：
    抽象享元类：所有具体享元类的超类或者接口，通过这个接口，Flyweight可以作用于外部
    具体享元类：指定内部状态，为内部状态增加存储空间
    非共享具体享元类：指出不需要共享的Flyweight子类
    享元工厂类：用来创业并管理Flyweight对象，确保合理地共享Flyweight,当Client请求一个Flyweight时，工厂类就会提供一个Flyweight对象


<h3 id="UML">UML图</h3>

      _ _ _ _ _ _
     |           |
     |   Client  |
     |_ _ _ _ _ _|
           |
           |
      _ _ _↓_ _ _       _ _ _ _ _ _
     |           |     |           |
     |   Factory |----→| Component |
     |_ _ _ _ _ _|     |_ _ _ _ _ _|
                          ↑    ↑
                          |    |
                          |    |
              ┌-----------┚    ┖--┐
              |                   |
              |                   |
              |                   |
      _ _ _ _ | _ _ _ _ _   _ _ _ |_ _ _ __ _ _ _ _ _ _
     | ConcreteFlyweight | | UnsharedConcreteFlyweight |
     |_ _ _ _ _ _ _ _ _ _| |_ _ _ _ _ _ _ _ _ _ _ _ _ _|

<h3 id="code">代码</h3>

    public abstract class Shape{

        public abstract void draw();
    }


***

    public class Circle extends Shape{

        private String color;

        public Circle(String color){

            this.color = color;
        }

        public void draw(){

            System.out.println("Draw a "+color+" circle.");
        }

    }


***

    public class FlyweightFactory{

        static Map<String,Shape> shapes = new HashMap<String,Shape>();

        public static Shape getShape(String key){

            Shape shape = shapes.get(key);

            if(shape == null){

                shape = new Circle(key);

                shapes.put(key,shape);
            }

            return shape;
        }


        public static int getSum(){

            return shapes.size();
        }

    }


***

    public class Client{


        public static void main(String[] args){


            Shape shape1 = FlyweightFactory.getShape("Red");

            shape1.draw();

            Shape shape2 = FlyweightFactory.getShape("Blue");

            shape2.draw();

            System.out.println("We draw "+FlyweightFactory.getSum()+" kinds of circle.");
        }

    }

    运行结果：

        Draw a Red circle.

        Draw a Blue circle.

        We draw 2 kinds of circle.



<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】策略模式](./Composite)

下一篇：[【行为型】观察者模式](./Strategy)








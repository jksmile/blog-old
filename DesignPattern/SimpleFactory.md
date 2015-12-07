

## 简单工厂模式

*   [定义](#define)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    简单工厂类又称为表态工厂类

    简单工厂模式根据提供给的不同数据，返回不两只类的实例，但这些类有一个共同的父类。



    简单工厂模式的优点；
    
        1.工厂的作用是实例化类，调用方不需要知道调用的具体子类，降低耦合；

    简单工厂模式的缺点；

        1.新增加实例类型需要修改工厂，总之工厂需要知道要实例的类；
        2.当子类过多，不适合使用；

    
    

<h3 id="code">代码</h3>

    public interface Fruit{

        public void printName();

    }


---------


    class Apple implements Fruit{

        public void printName(){
            System.out.println( "My name's apple." );
        }
    }

    class Orange implements Fruit{

        public void printName(){
            System.out.println( "My name's orange." );
        }
    }


    public class Factory(){

        public static Fruit getFruitInstance(String fruitName){

            Fruit fruit = null;

            switch(fruitName){

                case "apple":

                        fruit = new Apple();

                        break;

                case "orange":

                        fruit = new Orange();

                        break;
            }

            return fruit;
        }

    }

------

    public class Client{

        public static void main(String[] args){

            Fruit apple = Factory.getFruitInstance("apple");

            apple.printName();

            Fruit orange = Factory.getFruitInstance("orange");

            orange.printName();

        }
    }


    运行结果：

        My name's apple.

        My name's orange.
        -----------------







        

<h3 id="app">应用</h3>





***

相关推荐：[设计模式原则](./Principle)


上一篇：[单例模式](./Singleton)

下一篇：[工厂方法模式](./FactoryMethod)








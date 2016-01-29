

## 【创建型】原型模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

***

    定义：用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。

    原型模式主要用于对象的复制，它的核心是就是原型类，原型类需要具备以下条件：

        1.实现Cloneable接口，否则会使用clone方法会抛出CloneNotSupportedException异常；
        2.重写clone方法，将接口中的protect类型改为public类型；


    原型模式的优点：

        1.使用原型模式创建对象比new一个对象在性能上要好很多，因为它直接操作内存中二进制流；
        2.使用起来更为方便便捷；


    注意事项：

        1.原型模式不会调用类的构造方法，因为是直接操作内存中复制数据；
        2.原型模式只会拷贝对象中的基本类型，对于数组、对象不会拷贝，只会拷贝引用地址【浅拷贝】
        3.若想实现深拷贝，必须在类引用对象类中同样实现Cloneable接口；
    

<h3 id="UML">UML图</h3>

***

     _ _ _ _ _ _       _ _ _ _ _ _ _ _ _ 
    |           |     |                 |  
    |  Client   |---->|    Prototype    |
    |_ _ _ _ _ _|     |    +clone()     |
                      |_ _ _ _ _ _ _ _ _|
                               ↑
                       _ _ _ _ | _ _ _ _ _
                      |                   |
                      | concretePrototype |
                      |_ _ _ _ _ _ _ _ _ _| 
                        
                        
<h3 id="code">代码</h3>

***

    public class Prototype implements Cloneable{


        @overwrite
        public Prototype clone(){

            Prototype prototype = null;

            try{

                prototype = (Prototype)super.clone();
            }catch(CloneNotSupportException e){

                e.printStackTrace();
            }

            return prototype;

        }

    }

***

    public class Client{


        public static void main(String[] args){

            Prototype prototype = new Prototype();

            Prototype prototypeNew = prototype.clone();

        }

    }


<h3 id="app">应用</h3>

***

**JDK中原型模式的的应用：**


java.lang.Object#clone()



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【创建型】建造者模式](./Builder)

下一篇：[【结构型】适配器模式](./Adapter)








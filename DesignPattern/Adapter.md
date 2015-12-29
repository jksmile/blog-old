

## 【结构型】适配器模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)

<img src="/logo.jpg" width="0" height="0" />


<h3 id="define">定义</h3>

    定义：将一个类的接口转换成需要的接口，使原本由于接口不兼容不能一起工作的类可以一起工作。

    适配器接口的几个角色：

        1.目标接口(TargetInterface)：Client端所期待的接口【可以是具体的类、抽象类、接口】；
        2.适配类(ServerInterface)：需要适配的类【Server端提供的原接口】；
        3.适配器(AdapterInterface)：将适配类包装成目标接口的类；


    引用《大话设计模式》言语：

        1.适配器模式有点亡羊补牢的意思；
        2.适配器模式在某个阶段可能是最经济的做法；



<h3 id="UML">UML图</h3>


     _ _ _ _ _ _ _ _ _              _ _ _ _ _ _ _ _ _
    |                 |            |                 |
    |      Client     |-----------→| TargetInterface |
    |_ _ _ _ _ _ _ _ _|            |_ _ _ _ _ _ _ _ _|
                                            ↑
                                            |
                                            |
                                      _ _ _ |_  _ _ _ _              _ _ _ _ _ _ _ _ _
                                     |                 |            |                 |
                                     |AdapterInterface |-----------→| ServerInterface |
                                     |_ _ _ _ _ _ _ _ _|            |_ _ _ _ _ _ _ _ _|






<h3 id="code">代码</h3>

    public class TargetInterface{

        public void method1(){

            System.out.println("Just an expected one");
        }

    }


***

    public class ServerInterface{

        public void echoData(){

            System.out.println("echo data for client");
        }

    }

***

    public class AdapterInterface extends TargetInterface{

        private ServerInterface serverInterface = new ServerInterface();

        @override
        public void method1(){

            serverInterface.echoData();
        }


    }


***

    public class Client{


        public static void main(String[] args){

            AdapterInterface adapterInterface = new AdapterInterface();

            adapterInterface.method1();

        }

    }




<h3 id="app">应用</h3>


    引用《大话设计模式》中例子：

        姚明刚去NBA打篮球的时候，最大的问题就是沟通问题，有三种方案：

        1.努力学习英文【要花费大量时间】
        2.与姚明沟通时，请讲中国话【这个工程量更大，除非全世界都说中国话】
        3.姚明请个实时翻译员

        以上三方案，很明显方案3才是最经济最能快速解决问题的方案，当然姚明也会慢慢适应的，学会用英文沟通

        然后自然水到渠成，也就是我们项目中所说的，慢慢改造，不能永远是临时方案。


***

相关推荐：[设计模式原则](./Principle)


上一篇：[【创建型】原型模式](./Prototype)

下一篇：[【结构型】装饰器模式](./Decorator)








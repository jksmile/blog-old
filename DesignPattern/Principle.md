
## 设计模式原则

*   [单一职责原则](#SRP)
*   [里氏替换原则](#LSP)
*   [依赖倒置原则](#DIP)
*   [接口隔离原则](#ISP)
*   [迪米特法则](#LoD)
*   [开闭原则](#OCP)


<h3 id="SRP">单一职责原则</h3>

    单一职责原则简称SRP【Single Responsibility Principle】,设计模式最基本原则。
    
    简单的说就是一个类只负责一件事，只有一个因素能引起类的变化。
    
    我们可以理解为类的专注吧，只有专注于解决某一件事才能专业。
    
    如果一个类负责多件事，这会千万类之间的耦合性高，不方便代码的扩展。




<h3 id="LSP">里氏替换原则</h3>
    
    里氏替换原则简称LSP【Liskov Substitution Principle】是个什么鬼？名字叫的这么洋气！
    
    先来看下里氏替换原则的定义：
    
    定义1：如果对第一个类型为T1的对象O1，都有类型为T2的对象O2，使得以T1定义的所有程序P在
          所有对象O1都替换成O2时，程序P的行为没有发生变化，那么类型T2是T1的子类型；
          
    定义2：所有引用基类的地方必须能透明地使用其子类的对象；
    
    定义往往总是官方绕口难懂的，换句话表达里氏替换原则说的就是在类的继承中，对于父类已经实
    现好的方法A，子类尽量不要重写A方法或者重载A方法。为什么？为什么要有这样的建议？
    
    比如说：有一个功能P1，是由类X来完成的，现在要升级功能P1到P，P功能是P1功能和P2功能的组
           合，升级的功能P是由 类X 和 子类Y 共同完成的，所以在 子类Y 完成功能P2时，有可
           能导致P1功能发生故障。【有可能重写了 类X 中的方法】
           
           所以为了避免此类情况的发生，子类Y 在继承 类X 时除添加新方法完成功能P2外，尽量
           不要重写或者重载 类X 中的方法。
           
           案例：
           
           1.我需要在类中实现两数相加
                
                class X{
                
                    public int func1( int a, int b ){
                        return a+b;
                    }
                
                }
                
                
                public class Client{
                
                    public static void main(String[] args){
                        
                        X x = new X();
                        
                        System.out.println( "100+50=" + x.func1(100,50) );
                        
                    }
                }
           
                
                运行结果：
                
                100+50= 150
                --------------------
           
           2.现在需要写一个类，不仅要实现两数相加，更要实现相数相减后再加上10
           
                class Y extends X{
                
                    public int func1( int a, int b ){
                        return a-b;
                    }
                
                    public int func2( int a, int b ){
                        return func1(a,b)+10;
                    }
                
                }
           
                
                public class Client{
                
                    public static void main(String[] args){
                    
                        Y y = new Y();
                        
                        System.out.println( "100+50=" + y.func1(100,50) );
                        
                        System.out.println( "100-50+10=" + y.func2(100,50) );
                        
                    }
                }
                
                
                运行结果：
                
                100+50= 50
                
                100-50+10= 60
                -------------
                
           结论：子类Y 重写了父类X中的方法func1, 导致的结果是子类Y失去两数相加的功能
           
           
    里氏替换原则包含以下含义：
        
        1.子类可以实现父类中的抽象方法，但不能覆盖父类中的非抽象方法；
        2.子类可以新增加特有的方法来扩展功能；
        3.当子类的方法重载父类方法时，方法的形参要比父类方法的形参宽松；
        4.当子类的方法实现父类的抽象方法时，方法的返回值要比父类更严格；
        
        
    PS: 此原则之所以被称为里氏替换原则，是因为它是由麻省理工学院的Barbara Liskov提出来的
        芭芭拉·里斯科夫（Barbara Liskov）是一位非常牛逼的女性程序员，可以度娘下。
           
           
    



<h3 id="DIP">依赖倒置原则【Dependency Inversion Principle】</h3>


<h3 id="ISP">接口隔离原则【Interface Segregation Principle】</h3>


<h3 id="LoD">迪米特法则【Law of Demeter】</h3>


<h3 id="OCP">开关原则【Open-Closed Principle】</h3>
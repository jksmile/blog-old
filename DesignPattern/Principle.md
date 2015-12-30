
## 设计模式原则

*   [1.单一职责原则](#SRP)
*   [2.里氏替换原则](#LSP)
*   [3.依赖倒置原则](#DIP)
*   [4.接口隔离原则](#ISP)
*   [5.迪米特法则](#LoD)
*   [6.开闭原则](#OCP)



<h3 id="SRP">1.单一职责原则</h3>

    单一职责原则简称SRP【Single Responsibility Principle】,设计模式最基本原则。
    
    简单的说就是一个类只负责一件事，只有一个因素能引起类的变化。
    
    我们可以理解为类的专注吧，只有专注于解决某一件事才能专业。
    
    如果一个类负责多件事，这会千万类之间的耦合性高，不方便代码的扩展。




<h3 id="LSP">2.里氏替换原则</h3>
    
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
        
        
    PS: 此原则之所以被称为里氏替换原则，是因为它是由麻省理工学院的Barbara Liskov提出
        来的芭芭拉·里斯科夫（Barbara Liskov）是一位非常牛逼的女性程序员，可以度娘下。
           
           
    



<h3 id="DIP">3.依赖倒置原则</h3>
    
    依赖倒置原则简称DIP【Dependency Inversion Principle】，其核心思想便是面向接口编程

    依赖倒置原则定义：    
    
    高层模块不应该依赖低层模块，二者都应该依赖其抽象；抽象不应该依赖细节；细节应该依赖抽象。
    
    啊.... 正如我所说，定义总是官方绕口难懂的...
    
    简单来说依赖倒置原则就是希望我们写的类A依赖其它类B时，类B最好是一个抽象的存在【接口】
    
    案例：
    
        1.需要写个小机器人，能说出苹果的味道
         
            class Apple{
            
                public String getTaste(){
                
                    return "Apple's taste may be sweet or sour.";
                
                }
                
            }
            
            class Robot{
            
                public void say(Apple apple){
                
                    System.out.println( "Start speaking: "+apple.getTaste() );
                }
            }

            public class Client{
            
                public static void main(String[] args){
                
                    Robot robot = new Robot();
                    
                    Apple apple = new Apple();
                    
                    Robot.say(apple);
                    
                }
                
            }
        
        输出结果：
            
            Start speaking: Apple's taste may be sweet.
            ---------------------------------------------------
        
        
        2.这时候我需要小机器人，告诉我葡萄是什么味道。我是新加一个方法？这显然不是好的办法...
            
            interface Fruit{
                public String getTaste();
            }
            
            class Apple implements Fruit{
                
                public String getTaste(){
                    return "Apple's taste may be sweet.";
                }
                
            }
            
            class Grape implements Fruit{
                
                public String getTaste(){
                    return "Grape's taste may be sour."
                }
            }
            
            class Robot{
                
                public void Say(Fruit fruit){
                    System.out.println( "Start speaking: "+fruit.getTaste() );
                }
            
            }
            
            public class Client{
            
                public static void main(String[] args){
                
                    Robot robot = new Robot();
                    
                    Apple apple = new Apple();
                    
                    Grape grape = new Grape();
                    
                    robot.say(apple);
                    
                    robot.say(grape);
                }
            }
        
            运行结果：
                
                Start speaking: Apple's taste may be sweet.
                
                Start speaking: Grape's taste may be sour.
                -------------------------------------------
         
         
    以上传递依赖关系使用了接口传递，使用接口传递极大的降低了类之间的耦合性
          
    依赖倒置原则告诉我们：
    
        1. 低层模块【非业务模块】尽量要有抽象类或者接口；
        2. 变量申明也尽量抽象；
         


<h3 id="ISP">4.接口隔离原则</h3>

    接口隔离原则简称ISP【Interface Segregation Principle】。
    
    接口隔离可以使接口最小专，单一化，有利于实现类的适用笥。
    
    定义：
        客户端不应该依赖它不需要的接口；一个类对另一个类的依赖应该建立在最小的接口上。
        
    
    换句话说，如果类A通过接口I依赖类B, 类X也通过接口I依赖类Y，接口I对于类B，类Y来说并非最小接口
    
    也就是说类B,类Y实现了接口I中多余的方法，这是不可取的，应该将接口I拆分为两接口I1、I2，让类B、
    
    类Y分别实现接口I1,I2,这样类A通过接口I1来依赖类B，类X通过接口I2来依赖类Y。
    
    
    
    接口隔离原则含义：
    
        1. 建立单一接口，避免庞大臃肿的接口，从而避免实现类实现无关的方法；
    
    


<h3 id="LoD">5.迪米特法则</h3>


    迪米特法则简称LoD【Law of Demeter】又是什么鬼？洋气的名字又出现鸟......
    
    迪米特法则定义：
    
        一个对象应该对其它对象保持最少的了解。
        
    
    这个定义好懂，官方都这样说简单明白的话就不那么烧脑了。迪米特法则宗旨是尽量降低类与类之间的耦合。
    
    类与类之间的关系越密切，耦合越大，当一个类改变时，对另一个类的影响就越大......
    
    程序设计中的原则是：低耦合，高内聚。这也体现了面对象的三大特性的目标。
    
    
    迪米特含义：
    
        1. 只与自己有直接关系的类进行耦合；
        
        

<h3 id="OCP">6.开闭原则</h3>

    开闭原则简称OCP【Open-Closed Principle】。

    开闭原则定义：
    
        一个软件的实体如类、模块和函数应该对扩展开放，对修改关闭。
        
        
    在软件的生命周期内，因为变化、升级和维护等因素需要对代码进行修改更新，这可能会带来一些新的BUG，
    
    日积月累下去，可能会导致项目不得不进行重构。
    
    如何才能遵循开闭原则？ 做好前5项原则，自然会做到开闭。
    
    
    开闭原则含义：
    
        1. 用抽象构建框架，用实现扩展细节；
        
        
    
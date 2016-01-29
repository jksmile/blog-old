

## 【创建型】抽象工厂模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：多个抽象产品类，派生出多个具体产品类；一个抽象工厂类，派生出多个具体工厂类；每个具体工厂类可创建多个具体产品类的实例。

    工厂方法模式是简单工厂模式的升级版

    抽象工厂模式有四个要素：

        1.一个系统不应当依赖于产品类实例如何被创建、组合和表达的细节，这对于所有形态的工厂模式都是重要的。
        2.这个系统有多于一个的产品族，而系统只消费其中某一产品族。
        3.同属于同一个产品族的产品是在一起使用的，这一约束必须在系统的设计中体现出来。
        4.系统提供一个产品类的库，所有的产品以同样的接口出现，从而使客户端不依赖于实现。


<h3 id="UML">UML图</h3>

***
        
              _ _ _ _ _ _
             |           |
             |   Client  |
             |_ _ _ _ _ _|
                   |
          ┌-----------------┐         
     _ _ _↓_ _ _       _ _ _↓_ _ _  
    |           |     |           | 
    | IFactory  |     | IProduct  | 
    |_ _ _ _ _ _|     |_ _ _ _ _ _|       
          ↑                 ↑
          |                 |
     _ _ _|_ _ _       _ _ _|_ _ _  
    |           |     |           | 
    |  Factory  |----→|  Product  | 
    |_ _ _ _ _ _|     |_ _ _ _ _ _| 
      
    
<h3 id="code">代码</h3>

    public interface CPU{

        public void createCPU();

    }

---

    public interface Monitor{

        public void createMonitor();
    }

---

    public class Intel implements CPU{

        public void createCPU(){

            System.out.println( "Intel company produce CPU of intel.");
        }
    }
---

    public class AMD implements CPU{

        public void createCPU(){

            System.out.println("AMD company produce CPU of AMD.");
        }
    }

---

    public class Dell implements Monitor{

        public void createMonitor(){

            System.out.println("Creating... Dell monitor!");
        }
    }
---

    public class Samsung implements Monitor{

        public void createMonitor(){

            System.out.println("Creating... Samsung monitor!");
        }
    }

---

    abstract class FactoryX{

        abstract CPU needIntelCPU();

        abstract Monitor needSamsungMonitor();

    }

---

    abstract class FactoryY{

        abstract CPU needAMDCPU();

        abstract Monitor needDellMonitor();

    }

---

    public class Lenovo extends FactoryX{

        public CPU needIntelCPU(){

            return new Intel();
        }


        public Monitor needSamsungMonitor(){

            return new Samsung();
        }

    }

---

    public class Apple extends FactoryY{

        public CPU needAMDCPU(){

            return new AMD();
        }

        public Monitor needDellMonitor(){

            return new Dell();
        }
    }



---

    public class Client{

        public static void main(String[] args){


            Lenovo  lenovoComputer = new Lenovo();

            lenovoComputer.needIntelCPU().createCPU();

            lenovoComputer.needSamsungMonitor().createMonitor();



            Apple  macComputer = new Apple();

            macComputer.needAMDCPU().createCPU();

            macComputer.needDellMonitor().createMonitor();


        }

    }

    运行结果：

    Intel company produce CPU of intel.

    Creating... Samsung monitor!


    AMD company produce CPU of AMD.

    Creating... Dell monitor!
    ------------------------------------


<h3 id="app">应用</h3>

***

**JDK中抽象工厂模式的的应用：**

• java.util.Calendar#getInstance()

• java.util.Arrays#asList()

• java.util.ResourceBundle#getBundle()

• java.net.URL#openConnection()

• java.sql.DriverManager#getConnection()

• java.sql.Connection#createStatement()

• java.sql.Statement#executeQuery()

• java.text.NumberFormat#getInstance()

• java.lang.management.ManagementFactory (所有getXXX()方法)

• java.nio.charset.Charset#forName()

• javax.xml.parsers.DocumentBuilderFactory#newInstance()

• javax.xml.transform.TransformerFactory#newInstance()

• javax.xml.xpath.XPathFactory#newInstance()




**Arrays#asList()**

    
    public class Arrays{
        
        .....
        
        public static <T> List<T> asList(T... a) {
            return new ArrayList<>(a);
        }

        ......
        
    }



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【创建型】工厂方法模式](./FactoryMethod)

下一篇：[【创建型】建造者模式](./Builder)








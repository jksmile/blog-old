

## 【创建型】工厂方法模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

***


    定义：一抽象产品类派生出多个具体产品类；一抽象工厂类派生出多个具体工厂类；每个具体工厂类只能创建一个具体产品类的实例。

    工厂方法模式是简单工厂模式的升级版

    工厂方法模式有四个要素：

        1.产品接口，产品接口里定义产品的相关动作，产品接口里的定义直接决定代码的稳定性;
        2.产品实现，产品实现决定了产品的具体的动作；
        3.工厂接口，工厂接口是工厂方法的核心，它与调用方直接耦合来调用产品实现；
        3.工厂实现，工厂实现负责如何实例化产品类，每个具体工厂实例化一具体产品类；



<h3 id="UML">UML图</h3>

***

     _ _ _ _ _ _       _ _ _ _ _ _  
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

***

    public interface Product{

        public void printName();

    }

---

    public interface Factory{

        public Product createProduct();
    }

---

    public class ProductA implements Product{

        public void printName(){

            System.out.println("I'm product of A.");
        }
    }
---

    public class ProductB implements Product{

        public void printName(){

            System.out.println("I'm product of B.");
        }
    }

---

    public class FactoryX implements Factory{

        public Product createProduct(){

            return  new ProductA();
        }
    }

---

    public class FactoryY implements Factory{

        public Product createProduct(){

            return new ProductB();
        }
    }


---

    public class Client{

        public static void main(String[] args){

            Factory xFactory = new FactoryX();

            xFactory.createProduct.printName();

            Factory yFactory = new FactoryY();

            yfactory.createProduct.printName();


        }

    }


    运行结果：

    I'm product of A.

    I'm product of B.
    -----------------


<h3 id="app">应用</h3>

***

**JDK中java.lang.String/Boolean/Long/Double/Float等类中valueOf()就是工厂方法模式的的应用：**

    package java.lang;
    
    import java.io.ObjectStreamField;
    import java.io.UnsupportedEncodingException;
    import java.nio.charset.Charset;
    import java.util.ArrayList;
    import java.util.Arrays;
    import java.util.Comparator;
    import java.util.Formatter;
    import java.util.Locale;
    import java.util.regex.Matcher;
    import java.util.regex.Pattern;
    import java.util.regex.PatternSyntaxException;
        
    public final class String
        implements java.io.Serializable, Comparable<String>, CharSequence {
        
        
        ......
        

        public static String valueOf(Object obj) {
            return (obj == null) ? "null" : obj.toString();
        }
    
        public static String valueOf(char data[]) {
            return new String(data);
        }
    
        public static String valueOf(char data[], int offset, int count) {
            return new String(data, offset, count);
        }

        ......
    }        




***

相关推荐：[设计模式原则](./Principle)


上一篇：[【创建型】简单工厂模式](./SimpleFactory)

下一篇：[【创建型】抽象工厂模式](./AbstractFactory)








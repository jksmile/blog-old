

## 【创建型】简单工厂模式

*   [定义](#define)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    简单工厂类又称为静态工厂类

    简单工厂模式根据提供给的不同数据，返回不两只类的实例，但这些类有一个共同的父类。

    简单工厂模式有三个要素：

        1.产品接口。产品接口里定义产品的相关动作，产品接口里的定义直接决定代码的稳定性;
        2.产品实现。产品实现决定了产品的具体的动作；
        3.工厂类。通过传入工厂类的表态方法来决定实现化相关的产品实现；


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

**JDK中java.lang.Integer类中valueOf()就是静态工厂模式的的应用：**

    package java.lang;
    import java.util.Properties;
    
    /**
     * The {@code Integer} class wraps a value of the primitive type
     * {@code int} in an object. An object of type {@code Integer}
     * contains a single field whose type is {@code int}.
     *
     * <p>In addition, this class provides several methods for converting
     * an {@code int} to a {@code String} and a {@code String} to an
     * {@code int}, as well as other constants and methods useful when
     * dealing with an {@code int}.
     *
     * <p>Implementation note: The implementations of the "bit twiddling"
     * methods (such as {@link #highestOneBit(int) highestOneBit} and
     * {@link #numberOfTrailingZeros(int) numberOfTrailingZeros}) are
     * based on material from Henry S. Warren, Jr.'s <i>Hacker's
     * Delight</i>, (Addison Wesley, 2002).
     *
     * @author  Lee Boynton
     * @author  Arthur van Hoff
     * @author  Josh Bloch
     * @author  Joseph D. Darcy
     * @since JDK1.0
     */
    public final class Integer extends Number implements Comparable<Integer> {
    
        ......
    
        private static class IntegerCache {
            static final int low = -128;
            static final int high;
            static final Integer cache[];
    
            static {
                // high value may be configured by property
                int h = 127;
                String integerCacheHighPropValue =
                    sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
                if (integerCacheHighPropValue != null) {
                    int i = parseInt(integerCacheHighPropValue);
                    i = Math.max(i, 127);
                    // Maximum array size is Integer.MAX_VALUE
                    h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
                }
                high = h;
    
                cache = new Integer[(high - low) + 1];
                int j = low;
                for(int k = 0; k < cache.length; k++)
                    cache[k] = new Integer(j++);
            }
    
            private IntegerCache() {}
        }
    
    
        public static Integer valueOf(int i) {
            assert IntegerCache.high >= 127;
            if (i >= IntegerCache.low && i <= IntegerCache.high)
                return IntegerCache.cache[i + (-IntegerCache.low)];
            return new Integer(i);
        }
        
        ......
        
    }


***

相关推荐：[设计模式原则](./Principle)


上一篇：[【创建型】单例模式](./Singleton)

下一篇：[【创建型】工厂方法模式](./FactoryMethod)








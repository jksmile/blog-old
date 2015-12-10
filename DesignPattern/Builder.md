

## 【创建型】建造者模式

*   [定义](#define)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。

    建造者模式的四个要点：

        1.产品类，产品类可以是具体的类，也可以是抽象类与其实现类组成；
        2.抽象建造者，可以是个抽象类或者接口，一般有创建产品方法和返回产品方法；
        3.建造者，实现抽象建造者；
        4.导演类，调用建造者来得到具体产品；

    建造者模式优点：
        1.建造者模式可以有效的封装变化，将业务逻辑封闭在导演类中，整体稳定性好；
        2.扩展性好，有新的需求，加入新的建造者即可；


<h3 id="code">代码</h3>

    public class ComputerProduct{

        private String cpu;

        private String monitor;

        public void setCpu(String cpu){
            this.cpu = cpu;
        }

        public void setMonitor(String monitor){
            this.monitor = monitor;
        }

        public void show(String computerName){

            System.out.println( "We use "+cpu+" and "+monitor+" produce a computer called: "+computerName );
        }

    }


****

    public interface Builder{

        public void createProduct();

        public ComputerProduct getProduct();

    }

****

    public class BuilderX implements Builder{

        private computerProduct = new ComputerProduct();

        public void createProduct(String cpu, String monitor){

            computerProduct.setCpu( cpu );
            computerProduct.setMonitor( monitor );

        }

        public ComputerProduct getProduct(){
            return computerProduct;
        }

    }


****

    public class Director{

        private builder = new BuilderX();

        public ComputerProduct getProductDell(){

                builder.createProduct("intel","Samsung");
                return builder.getProduct();
        }

        public ComputerProduct getProductMac(){

                builder.createProduct("AMD","HP");
                return builder.getProduct();
        }

    }


***

    public class Client{

        public static void main(String[] args){

            Director director = new Director();

            ComputerProduct Dell = director.getProductDell();

            Dell.show("Dell");


            ComputerProduct Mac = director.getProductMac();

            Mac.show("Mac");

        }
    }

    运行结果：

        We use intel and Samsung produce a computer called: Dell

        We use AMD and HP produce a computer called: Mac
        ---------------------------------------------------------



<h3 id="app">应用</h3>





***

相关推荐：[设计模式原则](./Principle)


上一篇：[【创建型】抽象工厂模式](./AbstractFactory)

下一篇：[【创建型】原型模式](./Prototype)








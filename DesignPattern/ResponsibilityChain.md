

## 【行为型】责任链模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)



<img src="/logo.jpg" width="0" height="0" />


<h3 id="define">定义</h3>

    定义：




<h3 id="UML">UML图</h3>

       _ _ _ _ _ _ _ _ _ _      _ _ _ _ _ _  _ _ _
      |                   |    |                  |
      | AggregateAbstract |---→| IteratorAbstract |
      |_ _ _ _ _ _ _ _ _ _|    |_ _ _ _ _ _  _ _ _|
               ↑                         ↑
               |                         |
               |                         |
       _ _ _ _ |_ _  _ _ _       _ _ _ _ _|_ _ _ _ _
      |                   |- - →|                   |
      | ConcreteAggregate |     | ConcreteIterator  |
      |_ _ _ _ _ _ _ _ _ _|←----|_ _ _ _ _ _ _ _ _ _|



<h3 id="code">代码</h3>

    public interface Aggregate{

        public Iterator iterator();

        public void add(Object obj);

        public void remove(Object obj);

    }


***

    public class ConcreteAggregate implements Aggregate{

        private List  list = new ArrayList();

        public void add(Object obj){

            list.add(obj);
        }

        public void remove(Object obj){

            list.remove(obj);
        }

        public Iterator iterator(){

            return new ConcreteIterator(list);
        }
    }

***

    public interface Iterator{

        public boolean hasNext();

        public Object next();

    }

***


    public class ConcreteIterator implements Iterator{

        private List list = new ArrayList();

        private int cursor = 0;

        public boolean hasNext(){

            if(cursor >= list.size()){

                return false;
            }

            return true;
        }

        public Object next(){

            Object obj = null;

            if(this.hasNext()){

                obj = this.list.get(cursor++);
            }

            return obj;
        }

    }



***

    public class Client{


        public static void main(String[] args){

            ConcreteAggregate aggregate = new ConcreteAggregate()

            aggregate.add("Lily");

            aggregate.add("Jack");

            aggregate.add("Json");

            Iterator iterator = aggregate.iterator();

            while(iterator.hasNext()){

                String str = (String) iterator.next();

                System.out.println(str);
            }
        }

    }

    运行结果：

        Lily

        Jack

        Json




<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】观察者模式](./Observer)

下一篇：[【行为型】责任链模式](./ResponsibilityChain)








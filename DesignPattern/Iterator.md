

## 【行为型】迭代器模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：提供一种方法有顺序的访问一个聚合对象中各个元素，而又不暴露该对象的内部表示。

    迭代器模式中的角色：
    1.抽象容器：一般是一个接口，提供一个iterator()方法，例如java中的Collection接口，List接口，Set接口等。
    2.具体容器：就是抽象容器的具体实现类，比如List接口的有序列表实现ArrayList，List接口的链表实现LinkList，Set
      接口的哈希列表的实现HashSet等。
    3.抽象迭代器：定义遍历元素所需要的方法，一般来说会有这么三个方法：取得第一个元素的方法first()，取得下一个元素
      的方法next()，判断是否遍历结束的方法isDone()（或者叫hasNext()），移出当前对象的方法remove(),
    4.迭代器实现：实现迭代器接口中定义的方法，完成集合的迭代。


    其实迭代器模式已经不再那么受重视，因为像JAVA，.NET等语言已经在自己语言内完整的实现了迭代器模式。

    For example:

        public class Demo{

            public static void print(Collection coll){

                Iterator it = coll.iterator();

                while(it.hasNext()){

                    String str = (String) it.next();

                    System.out.println(str);
                }
            }
        }



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










## 【行为型】责任链模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)






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




<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】观察者模式](./Observer)

下一篇：[【行为型】责任链模式](./ResponsibilityChain)








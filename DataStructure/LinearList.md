
## 线性表

*   [线性表定义](#define)

*   [单链表添加操作](#add)

*   [单链表删除操作](#delete)


<h3 id="define">线性表定义</h3>

线性表（亦作顺序表）是最基本、最简单、也是最常用的一种数据结构。线性表中数据元素之间的关系是一对一的关系，即除了第一个和最后一个数据元素之外，其它数据元素都是首尾相接的。线性表的逻辑结构简单，便于实现和操作。因此，线性表这种数据结构在实际应用中是广泛采用的一种数据结构。

根据在存储单元中方式，线性表可分为 **顺序线性表** 和 **链式线性表**

**顺序线性表** 指用一组地址连续的存储单元依次存储线性表的数据元素，即在逻辑关系上相邻的两元素在物理位置上也相邻。

**链式线性表（单链表）** 用一组任意的存储单元存储线性表的数据元素（这些单元可以是连接的，也可以是不连接的），因此为了表示每个元素之间的逻辑关系，存储单元不仅要存储本身的信息还要存储一个指示其直接后继者的信息。



<h3 id="add">单链表添加操作</h3>

节点表示

    public class Node{
    
        private int val;
        
        private Node next;
        
        public Node(int val){
        
            this.val = val;
        }
        
        //Getter And Setter
        ...
    }


    public class Action{
    
        private Node head;
        
        private int size;
    
        public static void main(String[] args){
            
            Node first = new Node(1);
            
            Node second = new Node(2);
        
            Node third = new Node(3);
            
            first.setNext(second);
            
            second.setNext(third);
            
            
            this.head = first;
            
            
            
            Node x = new Node(100);
            
            
            
        }
        
        public static void insert(int position,Node newNode){
        
            switch(position){
            
                case 0:
                    
                    newNode.setNext(head);

                    head = newNode;
                    
                    break;
                    
                case size:
                    
                    
            }
            
        }
    
    }





<h3 id="delete">单链表删除操作</h3>

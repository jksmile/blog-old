￼￼
## MySQL 事务


### 什么是事务？

定义：事务是由一组原子性的SQL组成的工作单元。

简单的来说，事务内的SQL要么全部执行成功，要么全部执行失败。

既然谈到事务，就必须说到保证事务的ACID原则：

A：atomicity(原子性)
    
    一个事务必须是一个不可分割的最小执行单元，不可能只执行成功其中一部分。

C：consistency(一致性)

    数据库总是从一个一致性状态切换到另一个一致性状态。
    
I：isolation(隔离性)

    在一个事务执行过程中，对其它事务是不可见的。
    
D：durability(持久性)

    事务一旦提交，其所做的修改将永远保存到数据库中。
    
    
要实现ACID原则，数据库需要做很多复杂的工作，同时会增加系统的开销，对机器的要求也会更高。


### 实操

MySQL并不是所有的引擎都支持事务，InnoDB引擎支持事务，MyISAM就不支持事务


InnoDB引擎默认是开启自动提交的，我们接下来看来：

**客户端A：**

    mysql>show variables like 'autocommit';
    +---------------+-------+
    | Variable_name | Value |
    +---------------+-------+
    | autocommit    | ON    |
    +---------------+-------+
    1 row in set (0.00 sec)
    
    mysql>set autocommit=0;
    Query OK, 0 rows affected (0.00 sec)
    
    mysql>show variables like 'autocommit';
    +---------------+-------+
    | Variable_name | Value |
    +---------------+-------+
    | autocommit    | OFF   |
    +---------------+-------+
    1 row in set (0.00 sec)
    
    mysql>use test;
    Database changed
    
    mysql>select * from test;
    +------+
    | id   |
    +------+
    |    1 |
    +------+
    1 row in set (0.00 sec)
    
    mysql>update test set id=100 where id=1;
    Query OK, 1 row affected (0.00 sec)
    Rows matched: 1  Changed: 1  Warnings: 0
    
    
    
**客户端B：**
    
    mysql>use test;
    Database changed
    
    mysql>select * from test;
    +------+
    | id   |
    +------+
    |    1 |
    +------+
    1 row in set (0.00 sec)
   

客户端A的进程一个事务还未提交，在客户端B看来，客户端A的的UPDATE操作是不可见的，只是客户端A自己进程内的操作；


我们切回客户端B:

**客户端B：**

    mysql>update test set id=800 where id=1;
    |
    

然后发现客户端B一直执行中，因为客户端A的事务还没有提交，导致id=1这一行的数据被锁，客户端B等级解锁；


**客户端A：**

    mysql>commit;
    Query OK, 0 rows affected (0.01 sec)


**客户端B：**

    mysql>update test set id=800 where id=1;
    Query OK, 0 rows affected (5.55 sec)
    Rows matched: 0  Changed: 0  Warnings: 0













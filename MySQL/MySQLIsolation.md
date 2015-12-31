
## MySQL 事务隔离级别


*   [读异常](#readException)
*   [隔离级别](#isolationLevel)
*   [实操](#actioin)
    *   [1.验证未提交读](#verifyReadUncommitted)
    *   [2.验证提交读](#verifyReadCommitted)
    *   [3.验证可重复读](#verifyRepeatableRead)

MySQL事务中的隔离性在SQL标准定义中定义了四种隔离级别

简单的理解就是不是每种业务需求都需要很高的隔离性，针对不同的场景使用不同的隔离


<h3 id="readException">读异常</h3>

**在介绍四种隔离级别前，我们来了解下关于读数据时容易发生的异常：**

    脏读【Dirty Read】 
        某个事务已更新一份数据，另一个事务在此时读取了同一份数据，由于某些原因，前一个RollBack了操作，则后一个事务所读取的数据就会是不正确的。
             
    不可重复读【Non-repeatable read】
        在一个事务的两次查询之中数据不一致，这可能是两次查询过程中间插入了一个事务更新的原有的数据。
             
    幻读【Phantom Read】
        在一个事务的两次查询中数据笔数不一致，例如有一个事务查询了几列(Row)数据，而另一个事务却在此时插入了新的几列数据，先前的事务在接下来的查询中，就会发现有几列数据是它先前所没有的。


<h3 id="isolatioinLevel">隔离级别</h3>

**下面介绍下MySQL的四种隔离级别【从低到高】：**

    1. READ UNCOMMITTED（未提交读）
        在此级别，事务A中的修改操作即使没有commit操作，对事务B一样是可见的。简单的说事务B可以读到事务A未提交的修改数据，对事务B来说就是脏读。
        
    2. READ COMMITTED（提交读）
        在此级别，事务A中的修改操作需要commit后，在事务B中才可见，在事务B未结束前，任何其它事务对数据的修改commit后，事务B读取的数据结果都不同。对事务B来说不可重复读，因为有可能读取的结果不一致。此级别是MySQL默认级别。
        
    3. REPEATABLE READ（可重复读）
        在此级别，在事务B开始后读取数据X，事务A修改某数据X然后commit，事务B再次读取数据X的结果仍与上一次一致，不受事务A修改的影响。但如果事务A在事务B读取数据的范围内插入了新的记录，事务B就会产生幻读。
        
    4. SERIALIZABLE（串行化）
        此级别是MySQL最高隔离级别，强行事务串行执行，避免幻读的发生。串行化级别在读取数据的每一行上都加锁，开销大，加锁会导致超时和竞争，避免并发，性能受影响。在非常需要数据一致性时才考虑使用。
        
    +-------------------------------------------
    |     隔离级别      | 脏读 | 不可重复读 | 幻读 |
    +-------------------------------------------    
    | READ UNCOMMITTED |  √  |     √     |  √  |
    +-------------------------------------------    
    | READ COMMITTED   |  ×  |     √     |  √  | 
    +-------------------------------------------
    | REPEATABLE READ  |  ×  |     ×     |  √  |
    +-------------------------------------------
    | SERIALIZABLE     |  ×  |     ×     |  ×  |
    +-------------------------------------------
        
        
<h3 id="action">实操</h3>

<h4 id="verifyReadUncommitted">1.验证未提交读</h4>

**客户端A：**

确认默认级别【可重复读】

    mysql> select @@global.tx_isolation,@@tx_isolation;
    +-----------------------+-----------------+
    | @@global.tx_isolation | @@tx_isolation  |
    +-----------------------+-----------------+
    | REPEATABLE-READ       | REPEATABLE-READ |
    +-----------------------+-----------------+
    1 row in set (0.00 sec)

设置成读未提交【READ UNCOMMITTED】级别

    mysql> set global tx_isolation = 'READ-UNCOMMITTED';
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> set session tx_isolation = 'READ-UNCOMMITTED';
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> select @@global.tx_isolation,@@tx_isolation;
    +-----------------------+------------------+
    | @@global.tx_isolation | @@tx_isolation   |
    +-----------------------+------------------+
    | READ-UNCOMMITTED      | READ-UNCOMMITTED |
    +-----------------------+------------------+
    1 row in set (0.00 sec)
    

**客户端B:**

打开一个新的连接，验证客户端A设置的级别
    
    mysql> select @@global.tx_isolation,@@tx_isolation;
    +-----------------------+------------------+
    | @@global.tx_isolation | @@tx_isolation   |
    +-----------------------+------------------+
    | READ-UNCOMMITTED      | READ-UNCOMMITTED |
    +-----------------------+------------------+
    1 row in set (0.00 sec)
       
**客户端A[验证未提交读]：**

开始事务A，查询数据

    mysql> use test;
    Database changed
    
    mysql> start transaction;
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> select * from test;
    +------+
    | id   |
    +------+
    |  888 |
    +------+
    1 row in set (0.09 sec)
    
    mysql>|     

**客户端B[验证未提交读]：**

开始事务B，更新数据，不提交

    mysql> use test;
    Database changed
    
    mysql> start transaction;
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> select * from test;
    +------+
    | id   |
    +------+
    |  888 |
    +------+
    1 row in set (0.09 sec)
    
    mysql> update test set id=1 where id=888;
    Query OK, 1 row affected (0.14 sec)
    Rows matched: 1  Changed: 1  Warnings: 0
       
    mysql>|

**客户端A[验证未提交读]：**

事务A，再次查询数据 

    mysql> select * from test;
    +------+
    | id   |
    +------+
    |  1   |
    +------+
    
    mysql>commit;
    Query OK, 0 rows affected (0.00 sec)
    
此时事务B未commit操作，但事务A中，前后两次查询结果不一致，脏读！

**客户端B[验证未提交读]：**

结束事务B
    
    mysql>commit;
    Query OK, 0 rows affected (0.00 sec)
    

    
<h4 id="verifyReadCommitted">2.验证提交读</h4>

**客户端A[验证提交读]：**

设置提交读【READ COMMITTED】级别

    mysql> set global tx_isolation = 'READ-COMMITTED';
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> set session tx_isolation = 'READ-COMMITTED';
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> select @@global.tx_isolation,@@tx_isolation;
    +-----------------------+------------------+
    | @@global.tx_isolation | @@tx_isolation   |
    +-----------------------+------------------+
    |   READ-COMMITTED      |   READ-COMMITTED |
    +-----------------------+------------------+
    1 row in set (0.00 sec)
    
    mysql>|

**客户端B[验证提交读]：**

设置提交读【READ COMMITTED】级别

    mysql> set session tx_isolation = 'READ-COMMITTED';
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> select @@global.tx_isolation,@@tx_isolation;
    +-----------------------+------------------+
    | @@global.tx_isolation | @@tx_isolation   |
    +-----------------------+------------------+
    |   READ-COMMITTED      | READ-COMMITTED   |
    +-----------------------+------------------+
    1 row in set (0.00 sec)    

    mysql>|
    

**客户端A[验证提交读]：**    
    
开始事务A，读取数据

    mysql> start transaction;
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> select * from test.test;
    +------+
    | id   |
    +------+
    |    1 |
    +------+
    1 row in set (0.01 sec)
    
    mysql>| 
    
**客户端B[验证提交读]：** 

开始事务B，修改数据，不提交

    mysql> start transaction;
    Query OK, 0 rows affected (0.01 sec)
    
    mysql> update test set id=999 where id=1;
    Query OK, 1 row affected (0.02 sec)
    Rows matched: 1  Changed: 1  Warnings: 0
    
    mysql>| 
    
**客户端A[验证提交读]：** 

事务A再次查询数据
    
    mysql> select * from test.test;
    +------+
    | id   |
    +------+
    |    1 |
    +------+
    1 row in set (0.00 sec)
    
与事务A前一次查询一致,事务B中未commit的修改数据不能读取，避免了脏读。

**客户端B[验证提交读]：**

完成事务B，commit操作

    mysql> commit;
    Query OK, 0 rows affected (0.04 sec)
    
    mysql>|
    
**客户端A[验证提交读]：** 

事务A再次查询数据后，完成事务
    
    mysql> select * from test.test;
    +------+
    | id   |
    +------+
    |  999 |
    +------+
    1 row in set (0.00 sec)
    
    mysql>commit;
    Query OK, 0 rows affected (0.04 sec)
    
与事务A前两次查询不一致,事务B已经commit修改操作，事务A中可以读取已经commit的修改数据。在事务A中，不可重复读。


    
<h4 id="verifyRepeatableRead">3.验证可重复读</h4>


**客户端A[验证可重复读]：**

设置可重复读【REPEATABLE READ】级别

    mysql> set global tx_isolation = 'REPEATABLE-READ';
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> set session tx_isolation = 'REPEATABLE-READ';
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> select @@global.tx_isolation,@@tx_isolation;
    +-----------------------+------------------+
    | @@global.tx_isolation | @@tx_isolation   |
    +-----------------------+------------------+
    | REPEATABLE-READ       | REPEATABLE-READ  |
    +-----------------------+------------------+
    1 row in set (0.00 sec)
    
    mysql>|

**客户端B[验证可重复读]：**

设置可重复读【REPEATABLE READ】级别

    mysql> set session tx_isolation = 'REPEATABLE-READ';
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> select @@global.tx_isolation,@@tx_isolation;
    +-----------------------+------------------+
    | @@global.tx_isolation | @@tx_isolation   |
    +-----------------------+------------------+
    | REPEATABLE-READ       | REPEATABLE-READ  |
    +-----------------------+------------------+
    1 row in set (0.00 sec)
    
    mysql>|
    

**客户端A[验证可重复读]：**

开始事务A，读取数据

    mysql> start transaction;
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> select * from test;
    +------+
    | id   |
    +------+
    |  999 |
    +------+
    1 row in set (0.00 sec)
    
    mysql> |
    
    
**客户端B[验证可重复读]：**

开始事务B，修改数据,不提交

    mysql> start transaction;
    Query OK, 0 rows affected (0.01 sec)
    
    mysql> update test set id=100 where id=999;
    Query OK, 1 row affected (0.01 sec)
    Rows matched: 1  Changed: 1  Warnings: 0
    
    mysql> |


**客户端A[验证可重复读]：**

事务A，再次读取数据

    mysql> select * from test;
    +------+
    | id   |
    +------+
    |  999 |
    +------+
    1 row in set (0.00 sec)
    
    mysql> |

读取数据与上一次一致，确认不会脏读。


**客户端B[验证可重复读]：**

事务B，对修改操作，提交

    mysql> commit;
    Query OK, 0 rows affected (0.01 sec)
    
    mysql> |
    
**客户端A[验证可重复读]：**

事务B已经commit修改操作，事务A，第三次读取数据

    mysql> select * from test;
    +------+
    | id   |
    +------+
    |  999 |
    +------+
    1 row in set (0.00 sec)
    
    mysql> |

读取数据与前两次一致，在事务A中，确认可以重复读。


**客户端B[验证可重复读]：**

在客户端B中，插入一条数据

    mysql> show variables like 'autocommit';
    +---------------+-------+
    | Variable_name | Value |
    +---------------+-------+
    | autocommit    | ON    |
    +---------------+-------+
    1 row in set (0.14 sec)
    
    mysql> insert into test(`id`) value(1000);
    Query OK, 1 row affected (0.02 sec)
    
    mysql> select * from test;
    +------+
    | id   |
    +------+
    |  100 |
    | 1000 |
    +------+

    
**客户端A[验证可重复读]：**

事务A中，继续查询数据，并未出现幻读现象

    mysql> select * from test;
    +------+
    | id   |
    +------+
    |  999 |
    +------+
    1 row in set (0.00 sec)
    
    mysql> show create table test;
    +-------+------------------------------------------------------------------------------------------+
    | Table | Create Table                                                                             |
    +-------+------------------------------------------------------------------------------------------+
    | test  | CREATE TABLE `test` (
      `id` int(11) DEFAULT NULL
    ) ENGINE=InnoDB DEFAULT CHARSET=latin1 |
    +-------+------------------------------------------------------------------------------------------+
    1 row in set (0.29 sec)
    
    mysql> show variables like '%version%';
    +-------------------------+---------------------+
    | Variable_name           | Value               |
    +-------------------------+---------------------+
    | innodb_version          | 5.6.28              |
    | protocol_version        | 10                  |
    | slave_type_conversions  |                     |
    | version                 | 5.6.28              |
    | version_comment         | Source distribution |
    | version_compile_machine | x86_64              |
    | version_compile_os      | Linux               |
    +-------------------------+---------------------+
    7 rows in set (0.04 sec)

mysql版本5.6，InnoDB引擎，看来在5.6版本中解决了这个问题。

结束事务A

    mysql> commit;
    Query OK, 0 rows affected (0.01 sec)
    
    mysql> select * from test;
    +------+
    | id   |
    +------+
    |  100 |
    | 1000 |
    +------+
    



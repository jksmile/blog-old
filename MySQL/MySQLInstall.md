

## MySQL 安装



### 前言
    
MySQL安装在其官网上说的已经非常详细

MySQL安装文档：[http://dev.mysql.com/doc/refman/5.7/en/installing.html](http://dev.mysql.com/doc/refman/5.7/en/installing.html)

对于不同版本编译安装上可能有些差异，请仔细阅读官方文档

接下来要安装的版本是5.6

### 从GIT源安装

MySQL Git Repository: [https://github.com/mysql/mysql-server](https://github.com/mysql/mysql-server)


####安装前准备：

1.添加一个不可登陆的系统账户 mysql
    
    1. groupadd mysql
    
    2. useradd -r -g msyql -s /bin/false mysql


2.确认安装了cmake，如若未安装，yum安装

    1. yum install -y cmake


####安装：


    1. git clone https://github.com/mysql/mysql-server.git
    
    2. cd mysql-server
    
    3. git checkout 5.6 【切换到你要编译安装的分支】
    
    4. cmake . -DCMAKE_INSTALL_PREFIX=/usr/local/mysql  【cmake安装参数：http://dev.mysql.com/doc/refman/5.7/en/source-configuration-options.html】
    
    5. make && make install
    
    6. cd /usr/local/mysql
       
    7. chown -R mysql.mysql .
    
    8. scripts/mysql_install_db --user=mysql    【mysql 5.7.6版本前的】 
       bin/mysqld --initialize --user=mysql 【mysql 5.7.6版本及以后的】
       bin/mysql_ssl_rsa_setup              【mysql 5.7.6版本及以后的】 
    
    9. chown -R root .
    
    10. chown -R mysql data
    
    11. bin/mysqld_safe --user=mysql &
    
    12. cp support-files/mysql.server /etc/init.d/mysqld 【作为系统服务命令】


### 安装中注意事项

1.如果在启动后，mysql本地登陆,无法找到mysql.sock文件，两种解决方案：
  
      方案A:请修改my.cnf里的socket路径
      
      方案B: mysql -u root -p -S /var/lib/mysql/mysql.sock  通过参数来指定
      

2.第一次无密码登陆，请务必给root设置密码

    SET PASSWORD 'root'@'localhost' = PASSWORD('passwordString');
  
  
3.删除mysql.user表中的无密码用户：
  
    DELETE FROM mysql.user where PASSWORD='';
  
  
    

 
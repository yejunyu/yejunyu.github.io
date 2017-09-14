---
title: mysql基础
date: 2017-06-16 10:23:23
tags: [数据库, mysql]
---
1. 安装:略(详见官网)

2. 修改root用户密码       
    5.5以前，rpm包安装完MySQL后，root用户密码为空
    
    5.6中，rpm包安装完MySQL后，会随机生成一个root密码，保存在/root/.mysql_secret
    
    5.7以后，使用mysqld --initialize初始化时，默认会自动生成随机密码，并且不创建除root@localhost 外的其他账号，也不创建test库；

3. > /etc/my.conf     
    
    [client]                    
    port = 3307
    
    [mysqld]                    
    port = 3307

4. 创建用户
    CREATE USER 'root'@'%' IDENTIFIED BY '123456'; 
 
5. 授权       
    ```m
    CREATE USER 'yy'@'%' IDENTIFIED BY '123456'; 
    GRANT ALL ON *.* TO 'root'@'%';
    FLUSH PRIVILEGES;
    ```

6. 开启数据库快速回滚    
    [mysqld]    
    server_id = 1    
    log-bin=mysql-bin  #开启 MYSQL 二进制日志      
    max_binlog_size = 1000M    
    expire-logs-days=7  #只保留 7 天的二进制日志，以防磁盘被日志填满 
      
    binlog_format = row   
    binlog_row_image = full  
    
    进入数据库 show master logs;     
    [详细用法](https://github.com/danfengcao/binlog2sql)

7. 增删改查:略

    


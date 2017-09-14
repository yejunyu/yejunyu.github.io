---
title: mongo基础
date: 2017-06-16 10:23:30
tags: [数据库, mongodb]
---
1. 安装:略(详见官网)

2. 安全设置和远程登录      
    mongo为了方便使用，安装完是没有安全验证和用户名和密码的，如果是公网ip很容易遭受攻击(本人在安装完第二天就遇到过，数据被清空，只留了个要求打钱的邮箱。。。)

    简单说下配置
    
    首先进入mongo   
    ```m
    > use admin
    switched to db admin
    > db.createUser(
    ...   {
    ...     user: "dba",
    ...     pwd: "dba",
    ...     roles: [ { role: "root", db: "admin" } ]
    ...   }
    ... )
    Successfully added user: {
        "user" : "dba",
        "roles" : [
            {
                "role" : "root",
                "db" : "admin"
            }
        ]
    }
    ```
    ```
    user：用户名

    pwd：密码

    roles：指定用户的角色，可以用一个空数组给新用户设定空角色；在roles字段,可以指定内置角色和用户定义的角色。role里的角色可以选：

    Built-In Roles（内置角色）：
    1. 数据库用户角色：read、readWrite;
    2. 数据库管理角色：dbAdmin、dbOwner、userAdmin；
    3. 集群管理角色：clusterAdmin、clusterManager、clusterMonitor、hostManager；
    4. 备份恢复角色：backup、restore；
    5. 所有数据库角色：readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase
    6. 超级用户角色：root  
    // 这里还有几个角色间接或直接提供了系统超级用户的访问（dbOwner 、userAdmin、userAdminAnyDatabase）
    7. 内部角色：__system
        具体角色： 

    Read：允许用户读取指定数据库
    readWrite：允许用户读写指定数据库
    dbAdmin：允许用户在指定数据库中执行管理函数，如索引创建、删除，查看统计或访问system.profile
    userAdmin：允许用户向system.users集合写入，可以找指定数据库里创建、删除和管理用户
    clusterAdmin：只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限。
    readAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读权限
    readWriteAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读写权限
    userAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的userAdmin权限
    dbAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限。
    root：只在admin数据库中可用。超级账号，超级权限

    ```
    > /etc/mongod.conf  
    
    ```m
    net:
      port: 27018
    #  bindIp: 127.0.0.1  # Listen to local interface only, comment to listen on all interfaces.
 
    security:
      authorization: enabled
    ```
    yaml 语法, security:后新行空两个空格，冒号后需要一个空格
    
    重启mongo
    > systemctl restart mongod.service
    
    现在进入mongo需要先认证了
    
    ```m
    > db.auth('用户','密码')  #用创建的readWrite帐号进行写入
    1 #代表认证成功
    ```

3. 增删改查:略

    


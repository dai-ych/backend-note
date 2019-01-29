

-  select host,user,authentication_string,plugin from user;  //查询用户信息
####  创建用户
-  create user '[用户名]'@'[localhost]'

#### 创建角色并授权
-  [mysql8.0以上密码策略限制必须要大小写加数字特殊符号]  
-  create role role_dev;   // 创建角色
-  GRANT ALL ON [数据库名].* TO 'role_dev';   // 给角色授权
-  flush privileges;    // 刷新
-  SHOW GRANTS FOR 'root'@'localhost';  // 检查角色/用户权限  
-  grant 'role_root' to 'root'@'%';   //将角色role_root 的权限赋予 root账户
-  REVOKE ALL ON [数据库名].* FROM 'role_dev';    取消角色授权
-  revoke 'role_dev' from 'vampire'@'%';       // 取消用户授权
-  select current_role()    // 查看授权角色是否激活
-  set default role all to 'root'/'root'@'%';         // 激活用户的角色权限

#### 修改密码
-  [mysql8.0以上密码策略限制必须要大小写加数字特殊符号]  
-  ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY'Root@123';


####  /etc/my.cnf
-  [mysqld]default_password_lifetime=0   // 密码永不过期


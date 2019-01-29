

#### 创建角色并授权
-  [mysql8.0以上密码策略限制必须要大小写加数字特殊符号]  
-  create role role_dev;   // 创建角色
-  GRANT ALL ON [数据库名].* TO 'role_dev';   // 授权

#### 修改密码
-  [mysql8.0以上密码策略限制必须要大小写加数字特殊符号]  
-  alter user'root'@'%' IDENTIFIED BY 'MyNewPass@123'; 

####  一、 卸载mariadb
-   Centos7下默认安装了mariadb，需要先卸载该数据库
-   通过 rpm -qa|grep mariadb 命令查看 mariadb 的安装包
-   通过 rpm -e  --nodeps [mariadb名称] 命令装卸 mariadb

####  二、下载mysql8
-   Centos7 属于Red Hat系统，选择相应版本下载 RPM Bundle

####  三、安装mysql依赖包（选做）
-   yum -y install libaio.so.1 libgcc_s.so.1 libstdc++.so.6
-   yum update libstdc++-4.4.7-4.el6.x86_64
-   yum search libaio # 检索相关信息
-   yum install libaio # 安装依赖包
-   yum install net-tools

####  四、解压MySQL-xx-xx-xx.tar 到/usr/local/下的mysql目录内（mkdir /usr/local/mysql）
-   tar -xvf mysql-8.0.14-1.el7.x86_64.rpm-bundle.tar -C /usr/local/mysql

####  五、安装mysql
-   在/usr/local/mysql下安装mysql,注意安装有先后，有依赖关系
-   rpm -ivh …common.rpm
-   rpm -ivh …libs.rpm
-   rpm -ivh …client.rpm
-   rpm -ivh …server.rpm
![图片异常](https://img-blog.csdn.net/20180531135622183?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dqeF9qYXNpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

####  六、初始化mysql
-   mysqld --initialize --user=mysql
-   初始化完成后,查看生成的随机密码: cat /var/log/mysqld.log
-   启动mysql：systemctl start mysqld.service

####  七、登陆mysql
-   mysql -u root -p
-   初次登陆必须修改密码：ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Root@123';
-   刷新：flush privileges;    
-   退出：exit;

####  八、修改mysql配置文件 /etc/my.cnf
-  [mysqld]default_password_lifetime=0   // 密码永不过期

####  创建用户
-   select host,user,authentication_string,plugin from user;  //查询用户信息
-   update user set authentication_string='*E32A671056805EBAD613F4090727279564EED370',plugin='mysql_native_password',host='%';  修改加密方式和远程登陆权限
-   create user '[用户名]'@'[localhost]'

#### 修改密码
-  [mysql8.0以上密码策略限制必须要大小写加数字特殊符号]  
-  ALTER USER '[用户名]'@'%' IDENTIFIED WITH mysql_native_password BY 'Root@123';
-  create database [数据库名]  // 创建数据库


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


####  开放端口
-   firewall-cmd --zone=public --add-port=3306/tcp --permanent
-   firewall-cmd --reload

####  windows 免密启动
-   mysqld --console --skip-grant-tables --shared-memory   管理员权限
-   update user set authentication_string='' where user='root';

####  bin目录下
-   mysqld --install
-   mysqld --initialize-insecure    初始化





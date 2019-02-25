#####   安装依赖软件
-   yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel asciidoc
-   yum install  gcc perl-ExtUtils-MakeMaker
-   yum remove git  //卸载git


#####  下载解压git后
-   wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.21.0.tar.gz
-   tar -xzvf git.tar.gz
-   cd git-2.20.1
-   make prefix=/usr/local/git all   // 指向目录编译
-   make prefix=/usr/local/git install  //指向目录安装

#####  如果是非root用户使用git，则需要配置下该用户下的环境变量
-   [git@uatjenkins01 ~]$ echo "export PATH=$PATH:/usr/local/git/bin" >> ~/.bashrc
-   [git@uatjenkins01 ~]$ source ~/.bashrc

-   groupadd git //创建用户组
-   useradd -g git git  //创建账号
-   passwd git   
-   git init --bare website.git    // 创建仓库
-   chown -R git:git website.git    // 授权

-   ln -s /usr/local/git/bin/git-upload-pack /usr/bin/git-upload-pack   //无法下载时建立软链接
####  分支    
-   git branch                      //查看当前所有分支
-   git checkout -b 分支名称        //创建一个分支并且使用它工作
-   git merge 分支名称              //快速合并到有新版本的另一个分支
-   git branch -d 名称              //删除分支
-   git branch 分支名称             //切换分支

####    查看进程
-   ps -ef|grep tomcat


-   ssh-keygen -t rsa
-   scp id_rsa.pub  git@144.202.23.231:/home/git/.ssh/authorized_keys     远程推送密钥
-   chmod 700 /home/git/.ssh                             权限必须为700 
-   chmod 600 /home/git/.ssh/authorized_keys             权限必须为600
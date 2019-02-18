####    linux登录后出现-bash-4.1$   以git用户为例
-   cp /etc/skel/.bash* /home/git/       原因是配置文件丢失，将/etc/skel/目录下的三个文件拷贝到git用户家目录即可
-   chown -R git:git /home/git           授权到git用户

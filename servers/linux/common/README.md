#### 
-   date -R    查看时间时区
-   timedatectl set-timezone Asia/Shanghai   设置时区

####    linux登录后出现-bash-4.1$   以git用户为例
-   cp /etc/skel/.bash* /home/git/       原因是配置文件丢失，将/etc/skel/目录下的三个文件拷贝到git用户家目录即可
-   chown -R git:git /home/git           授权到git用户

####   
-   /etc/sudoers    设置权限
-   du -h –max-depth=1 /    查看文件夹下文件大小


####    普通账号通过systemctl管理服务需要输入root密码
~~~text
进入/usr/share/polkit-1/actions/org.freedesktop.systemd1.policy，
将对应manae-units的defaults中的授权全部改为yes，然后执行systemctl restart polkit重启polkit
<defaults>
        <allow_any>yes</allow_any>
        <allow_inactive>yes</allow_inactive>
        <allow_active>yes</allow_active>
</defaults>
~~~ 



####    基本操作
-   mkdir 创建目录
-   touch 创建目录


####    基础工具包
-   dnf groupinfo "Development Tools"  查看工具包列表
-   dnf group install "Development Tools"  安装开发工具包
-   dnf group remove "Development Tools"  去除工具包
####    centos7   gitlab
~~~text
1. 安装依赖软件
yum -y install policycoreutils openssh-server openssh-clients postfix

2.设置postfix开机自启，并启动，postfix支持gitlab发信功能
systemctl enable postfix && systemctl start postfix

3.下载gitlab安装包，然后安装
centos 6系统的下载地址:https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el6
centos 7系统的下载地址:https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7
yum install policycoreutils-python
rpm -i soft/gitlab-ce-10.7.3-ce.0.el7.x86_64.rpm 

4.修改gitlab配置文件指定服务器ip和自定义端口：
vim  /etc/gitlab/gitlab.rb
external_url = "http://144.202.23.231"

vim /opt/gitlab/embedded/service/gitlab-rails/config/gitlab.yml
vim /var/opt/gitlab/gitlab-shell/config.yml
5.重置并启动GitLab
执行：
gitlab-ctl reconfigure
gitlab-ctl restart
~~~
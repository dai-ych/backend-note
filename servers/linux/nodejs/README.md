#####  下载解压
-   wget https://nodejs.org/dist/v12.18.2/node-v12.18.2-linux-x64.tar.xz
-   tar -xzvf https://nodejs.org/dist/v12.18.2/node-v12.18.2-linux-x64.tar.xz
-   mkdir -p /usr/local/node
-   mv /opt/node-v12.18.2-linux-x64/* /usr/local/node
-   ln -s /usr/local/node/bin/node /usr/bin/node  创建软链


-   echo "export PATH=$PATH:/usr/local/node/bin" >> /etc/profile
-   source /etc/profile

#####  安装yarn
~~~ text 
curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee 
/etc/yum.repos.d/yarn.repo
rpm --import https://dl.yarnpkg.com/rpm/pubkey.gpg
dnf install yarn

~~~ 

#####  jenkins 脚本
~~~ text

~~~ 
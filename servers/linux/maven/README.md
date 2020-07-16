#### 
-   wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz   

####    linux登录后出现-bash-4.1$   以git用户为例


####   
-   


####    
~~~text
进入/usr/share/polkit-1/actions/org.freedesktop.systemd1.policy，
将对应manae-units的defaults中的授权全部改为yes，然后执行systemctl restart polkit重启polkit
<defaults>
        <allow_any>yes</allow_any>
        <allow_inactive>yes</allow_inactive>
        <allow_active>yes</allow_active>
</defaults>
~~~ 



####    



####   

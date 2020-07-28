##  centOS8 JDK环境集成
-   last updateTime: 2020.7.6
####  yum 安装 jdk
-   yum list java-1.8*      检查 yum 中有没有 java1.8 包
-   yum install java-1.8.0-openjdk* -y      开始安装
-   java -version           版本验证
-   /usr/lib/jvm            JDK默认安装路径

-   ln -s /opt/jdk1.8.0_261/bin/java /usr/bin/java


-   /etc/profile

```text
export JAVA_HOME=/usr/lib/jvm/jdk1.8
export JRE_HOME=${JAVA_HOME}/jre
export CATALINA_HOME=/opt/tomcat8
export CATALINA_BASE=/opt/tomcat8
export TOMCAT_HOME=/opt/tomcat8
export M2_HOME=/opt/maven3.6
export GIT_HOME=/usr/local/git

export CLASSPATH=.:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar
export PATH=$PATH:${JAVA_HOME}/bin:${JRE_HOME}/bin:${CATALINA_HOME}/bin:${CATALINA_BASE}/bin:${TOMCAT_HOME}/bin:${M2_HOME}/bin:${GIT_HOME}/bin

```

-   source  /etc/profile       保存生效
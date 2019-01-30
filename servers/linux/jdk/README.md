##  linux JDK环境集成
        
####  一、下载jdk
https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

-   /etc/profile
```text
export JAVA_HOME=/opt/jdk1.8
export JRE_HOME=/opt/jdk1.8/jre
export CATALINA_HOME=/opt/tomcat8
export CATALINA_BASE=/opt/tomcat8
export TOMCAT_HOME=/opt/tomcat8
export M2_HOME=/opt/maven3.6
export GIT_HOME=/usr/local/git

export CLASSPATH=.:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar
export PATH=$PATH:${JAVA_HOME}/bin:${JRE_HOME}/bin:${CATALINA_HOME}/bin:${CATALINA_BASE}/bin:${TOMCAT_HOME}/bin:${M2_HOME}/bin:${GIT_HOME}/bin

```
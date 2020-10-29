####    必备插件
-   deploy to container
-   maven Integration
-   nodejs
-   github

~~~text
DATE=$(date +%Y%m%d)
JARDIR=/opt/tomcat8/webapps/jenkins/workspace/canopus-backend/target/
DIR=/home/tomcat/project/canopus-backend/
JARFILE=canopus-backend-1.0.0-SNAPSHOT.jar
 
if [ ! -d $DIR/backup ];then
   mkdir -p $DIR/backup
fi
cd $DIR

pid=`ps -ef | grep canopus-backend-1.0.0-SNAPSHOT.jar | grep -v grep | awk '{print $2}'`
if [ -n "$pid" ]
then
   kill -9 $pid
fi

mv -f $JARDIR$JARFILE $DIR$JARFILE

BUILD_ID=dontKillMe
nohup java -jar $JARFILE >out.log 2>&1 &

cp $DIR$JARFILE $DIR/backup/$JARFILE$DATE
cd backup/
ls -lt|awk 'NR>5{print $NF}'|xargs rm -rf

~~~

-   nohup java -jar canopus-backend-1.0.0-SNAPSHOT.jar >out.log 2>&1 &
-   ps aux|grep canopus-backend-1.0.0-SNAPSHOT.jar


~~~text
LOG=catalina$(date +%Y%m%d).log
JARDIR=/var/lib/jenkins/workspace/canopus/canopus-backend/target/
DIR=/opt/project/canopus/
JARFILE=canopus-1.0.0-SNAPSHOT.jar

cd $JARDIR

pid=`ps -ef | grep canopus-1.0.0-SNAPSHOT.jar | grep -v grep | awk '{print $2}'`
if [ -n "$pid" ]
then
   kill -9 $pid
fi

BUILD_ID=dontKillMe
nohup java -jar $JARFILE >$DIR$LOG 2>&1 &

cd $DIR
ls -lt|awk 'NR>5{print $NF}'|xargs rm -rf
~~~

-   clean install -Dmaven.test.skip=true -Ptest      排除测试的包内容，使用后缀为 test 的配置文件

####    rpm安装
-   wget https://pkg.jenkins.io/redhat-stable/jenkins-2.235.2-1.1.noarch.rpm 
-   rpm -ivh jenkins-2.235.2-1.1.noarch.rpm                 指定安装路径

~~~~text
默认安装路径
/usr/lib/jenkins/jenkins.war           war包
/etc/sysconfig/jenkins                 jenkins配置文件
/var/lib/jenkins/                      默认的JENKINS_HOME目录
/var/log/jenkins/jenkins.log           Jenkins日志文件
/var/cache/jenkins/war/WEB-INF/lib/    包地址
~~~~

~~~~text
cp -r /var/lib/jenkins/workspace/canopus-web /opt/project/    复制项目文件
  
~~~~
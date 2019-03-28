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
JARDIR=/usr/local/tomcat/webapps/jenkins/workspace/canopus/webapp-backend/target/
DIR=/usr/local/tomcat/project/canopus-backend/
JARFILE=webapp-backend-1.0.0-SNAPSHOT.jar

cd $JARDIR

pid=`ps -ef | grep webapp-backend-1.0.0-SNAPSHOT.jar | grep -v grep | awk '{print $2}'`
if [ -n "$pid" ]
then
   kill -9 $pid
fi

BUILD_ID=dontKillMe
nohup java -jar $JARFILE >$DIR$LOG 2>&1 &

cd $DIR
ls -lt|awk 'NR>5{print $NF}'|xargs rm -rf
~~~

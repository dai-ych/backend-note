####    必备插件
-   deploy to container

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

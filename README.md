# linux-autoshutdown-shellscript


```

#!/bin/sh

#tomcat connection off


export CATALINA_HOME=자바경로


Log=$CATALINA_HOME/logs/restart.log
DATE=`date +%Y년%m월%d일-%H:%M:%S`

echo "$DATE : TOMCAT을 종료합니다." >> $Log

#톰캣 종료 스크립트 실행
$CATALINA_HOME/bin/shutdown.sh


#20초 슬립
sleep 20


# 톰캣 프로세스 카운트
tomcatCnt=`ps -ef | grep tomcat | grep /usr/bin/java | grep -v grep | grep -v vi | wc -l`


if [ $tomcatCnt -gt 0 ]
then

        echo "$DATE : TOMCAT이 종료되지 않았습니다." >> $Log

        ps -ef | grep tomcat | grep /usr/bin/java | grep -v grep | grep -v vi | awk '{print $2}'|

        while read PID

        do

                kill -9 $PID

                echo "$DATE : 프로세스 킬 $PID" >> $Log

        done

else
    echo "$DATE : TOMCAT이 종료되었습니다." >> $Log
fi


```

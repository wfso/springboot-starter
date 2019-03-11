#!/bin/bash
#本脚本基本无需改动，注意要点均已用中文说明
# 1. 请将本脚本放到Linux系统的path路径下，最好是/bin目录下
# 2. 请给本脚本设备可执行权限
# 3. 启动示例         springboot-starter xxx.jar start
# 4. 重启示例         springboot-starter xxx.jar restart
# 5. 停止示例         springboot-starter xxx.jar stop
# 6. 查看状态示例     springboot-starter xxx.jar status

## 获取 java 命令的路径
JAVA_CMD=`which java`

if [ -z "${JAVA_CMD}" ];then
  echo "Please install the Java environment";
  exit 1;
fi

## 输出本命令的使用方法 并退出
usage() {
    echo "Usage: springboot-starter [app_name].jar [start|stop|restart|status]"
    exit 1
}

## 判断是否输入了两个参数
if [ $# -lt 2 ]; then
    usage
fi


## 脚本名称
APP_NAME=$1;

## 操作
OPERATION=$2;

## 运行模式
MODEL=$3

if [ -z "$MODEL" ]; then
    MODEL="production"
fi

## 其它参数处理
OTHER_ARGS=""
if [ $# -gt 3 ]; then
    shift 3
else
    shift $#
fi
for ARG in $*
do
  OTHER_ARGS="$OTHER_ARGS $ARG"
done


## 脚本所在目录，绝对路径表示
BASE_PATH=$(cd `dirname $APP_NAME`;pwd)

## 去掉所有目录后的脚本名
APP_NAME=${APP_NAME##*/}

## 脚本的路径，绝对路径表示
APP_PATH=$BASE_PATH"/"$APP_NAME


## 判断目标程序是否已经启动
is_running(){
  ## 尝试获取已经运行程序的PID
  PID=`ps -ef|grep ${APP_PATH}|grep -v grep|awk '{print $2}'`
  if [ -z "${PID}" ]; then
    return 0
  else
    return 1
  fi
}

## 启动程序
start(){
  is_running
  if [ $? -eq "1" ]; then
    echo "${APP_NAME} is already running. pid is ${PID} ."
  else
    ## 启动 jar 包
    echo "${APP_NAME} starting ...... "
    nohup ${JAVA_CMD} -jar ${OTHER_ARGS} -Dspring.profiles.active=${MODEL} ${APP_PATH} > /dev/null 2>&1 &
    echo "nohup ${JAVA_CMD} -jar ${OTHER_ARGS} -Dspring.profiles.active=${MODEL} ${APP_PATH} > /dev/null 2>&1 &"
    sleep 1
    echo "${APP_NAME} started  completed "
    echo ""
  fi
}

## 停止程序
stop(){
  is_running
  if [ $? -eq "1" ]; then
    echo "PID is ${PID}, ${APP_NAME} stopping ...... "
    kill ${PID}
    if [ $? -ne "0" ]; then
        echo "kill ${PID} failed，execute kill -9 ${PID}"
        kill -9 ${PID}
    fi
    sleep 1
    echo "${APP_NAME} stopped completed "
  else
    echo "${APP_NAME} is not running"
  fi
}

## 输出程序运行状态
status(){
  is_running
  if [ $? -eq "1" ]; then
    echo "${APP_NAME} is running. pid is ${PID}"
  else
    echo "${APP_NAME} is NOT running."
  fi
}

## 重启程序
restart(){
  stop
  start
}


case "$OPERATION" in
  "start")
    start ;;
  "stop")
    stop ;;
  "status")
    status ;;
  "restart")
    restart ;;
  *)
    usage ;;
esac
exit 0

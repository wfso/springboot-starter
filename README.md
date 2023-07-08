# springboot-starter
当 spring-boot 项目 部署到正式环境中的后，需要启动、停止、重启、查看状态等操作。 本项目仅包含一个shell脚本，安装Linux系统的/usr/bin 目录下，方便对 spring-boot 项目发布的 jar 程序包进行 启动、停止、重启、查看状态等操作。


本脚本基本无需改动，注意要点均已用中文说明
1. 请将本脚本放到Linux系统的path路径下，最好是/bin目录下
2. 请给本脚本设备可执行权限
3. 启动示例         springboot-starter xxx.jar start
4. 重启示例         springboot-starter xxx.jar restart
5. 停止示例         springboot-starter xxx.jar stop
6. 查看状态示例     springboot-starter xxx.jar status

如需要更多高级用法，请阅读源码

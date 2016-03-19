---
layout: post
title: "服务器Mysql备份脚本"
tags: ["Mysql"]
---
{% include JB/setup %}

生成备份目录:

    !/bin/bash
    backdir=/home/ubuntu/database_backup
    today=$(date +%Y%m%d%H%M)
    mkdir $backdir/$today

mysql备份：

	mysqldump -h127.0.0.1 -uroot -ppassword database > $backdir/$today/$today.sql

打包并删除目录：

	tar -czf $backdir/$today.tar.gz $backdir/$today/$today.sql
    rm -rf $backdir/$today

保留10天的备份记录，删除其他的备份：

	find $backdir -maxdepth 1 -name "*.tar.gz" -type f -mtime +10 -exec rm -f {} \; >/dev/null 2>&1

同步到七牛（要先安装七牛的同步程序qrsync）：

    /home/ubuntu/qiniu/qrsync /home/ubuntu/qiniu/conf.json
    
直接放到cron的daily里面就可以每天执行,也可以自己写定时任务执行：

    cd /etc/cron.daily/
    cp ~/database_backup/backup.sh mysql_backup

---
layout: post
title: "MySQL编码设置"
tags: ["MySQL"]
---
{% include JB/setup %}

查看MySQL支持的编码：

	mysql> SHOW CHARACTER SET;

查看当前MySQL服务器默认编码：
	
	mysql> SHOW VARIABLES LIKE 'character_set%'

创建数据库的时候指定编码：

	CREATE DATABASE linuxcast
		  DEFAULT CHARACTER SET utf8
		  DEFAULT COLLATE utf8_general_ci;

修改一个已有数据库的编码：

	ALTER DATABASE linuxcast CHARACTER SET utf8 COLLATE utf8_general_ci;

设置数据库默认编码：

修改MySQL配置文件my.cnf：
	
	[client]
	default-character-set=utf8
	[mysql]
	default-character-set=utf8
	[mysqld]
	default-character-set = utf8    
	collation-server = utf8_unicode_ci
	init-connect='SET NAMES utf8'
	character-set-server = utf8

修改之后重启MySQL生效

	

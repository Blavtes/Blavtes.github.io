---
layout: post
title: tomcat-初始化配置
category: tomcat
tags: tomcat
description: tomcat-服务器配置
---
### tomcat-服务器配置
记录一次服务器误删除故障，在服务器删除日志文件时不小心在tomcat主目录执行了 	``rm -rf ./*`` ,反应过来为时已晚。看着空荡荡的目录结构，有点慌了。因服务器使用的是青云，第一时间咨询客服得知，只有做了备份的数据才能恢复。可是这个服务器原本用做测试，临时拿过来做生产发布。既然这样只能想着重新部署一套tomcat环境了。

想到 tomcat 使用免安装的方式，那我就想办法从其他生产环境copy 一份过来。下面记录修改的配置文件
### 1、`redis` 修改：
	
`redis`服务器本地安装。执行启动脚本:
 
 在`src` 目录下执行：` ./redis-server ../redis.conf ` 
 启动监听服务`./redis-cli  -p 6379`
	
如提示找不到 `redis-server` 脚本，需在`src` 目录 执行`make` 编译命令。成功之后 生成以上脚本。
	
### 2、`apache-tomcat-8.5.29` 配置文件修改

删除``webapps 、work`` 目录下文件，``web``应用`war` 包拷贝到`webapps` 目录下 （如`pc.war`）

配置文件放在 `apache-tomcat-8.5.29/config/cfg.properties` 下
`war` 需读取该配置文件 则需修改 文件
``config/catalina.properties``

	shared.loader=${catalina.base}/config

让浏览器访问网站不带项目名称访问：
	
修改`config`下`server.xml `

```	
<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
      <Context path="" docBase="PC"  reloadable="true" />
```
   ssl证书配置，上传证书文件到`conf` 目录下
   
   修改server.xml:
  
``` 
<Connector
  protocol="org.apache.coyote.http11.Http11NioProtocol"
            port="443"
            maxThreads="150"
            SSLEnabled="true">
    <SSLHostConfig>
          <Certificate
              certificateKeystoreFile="/xxx/apache-tomcat-8.5.29/conf/xxx.jks"
              certificateKeystorePassword="password"
              type="RSA"
              SSLVerifyClient="false"  SSLProtocol="TLSv1+TLSv1.1+TLSv1.2"
              ciphers="TLS_RSA_WITH_AES_128_CBC_SHA,TLS_RSA_WITH_AES_256_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_256_CBC_SHA256"
              />
    </SSLHostConfig>
</Connector>
```
   
 启动时提示找不到`java_home` 环境变量
 须在`apache-tomcat-8.5.29/bin/` 目录下修改`setclasspath.sh` 脚本开头添加对应的jdk信息
 
 ```
export JAVA_HOME=/home/tomcat/jdk1.8.0_121
export JRE_HOME=/home/tomcat/jdk1.8.0_121/jre
 ```
 
 至此配置完成，即可启动 `tomcat `
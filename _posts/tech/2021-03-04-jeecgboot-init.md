---
layout: post
title:  jeecgBoot 工程初始化
category: 框架
tags: redis
description:  jeecgBoot 前后端工程如何启动
---

### jeecgBoot 后端工程启动

使用`idea `打开 `jeecgBoot` 主目录，包括前后端项目。

展开`jeecg-boot` 目录，找到`pom.xml` 文件。右击 选择`add maven `

展开子目录检查 所有的`pom.xml `文件是否已同步。

展开右边工具栏 `Maven Projects`等待同步完成。

### 配置文件修改：

本地开发修改`/jeecg-boot-module-system/src/main/resources/application-dev.yml`

#### 数据库配置

```
datasource:
        master:
          url: jdbc:mysql://127.0.0.1:3306/jeecg-boot?characterEncoding=UTF-8&useUnicode=true&useSSL=false&tinyInt1isBit=false&allowPublicKeyRetrieval=true&serverTimezone=Asia/Shanghai
          username: root
          password: root
          driver-class-name: com.mysql.cj.jdbc.Driver
          # 多数据源配置
          #multi-datasource1:
          #url: jdbc:mysql://localhost:3306/jeecg-boot2?useUnicode=true&characterEncoding=utf8&autoReconnect=true&zeroDateTimeBehavior=convertToNull&transformedBitIsBoolean=true&allowPublicKeyRetrieval=true&serverTimezone=Asia/Shanghai
          #username: root
          #password: root
          #driver-class-name: com.mysql.cj.jdbc.Driver
          
```

打开`idea`右边栏数据库工具、新建数据库，执行`./db/jeecgboot-mysql-5.7.sql`


####   redis配置

```
  #redis 配置
  redis:
    database: 0
    host: 127.0.0.1
    lettuce:
      pool:
        max-active: 8   #最大连接数据库连接数,设 0 为没有限制
        max-idle: 8     #最大等待连接中的数量,设 0 为没有限制
        max-wait: -1ms  #最大建立连接等待时间。如果超过此时间将接到异常。设为-1表示无限制。
        min-idle: 0     #最小等待连接中的数量,设 0 为没有限制
      shutdown-timeout: 100ms
    password: ''
    port: 6379
```

启动服务方式
1、Run `jeecg-boot-module-system/src/main/java/org.jeecg/jeecgSystemApplication`

```
	由于未知原因 执行无反应，无报错，无异常，无输出，采用第二方式启动
```

2、依次执行点击 

```
jeecg-boot-parent/Lifecycle/install 
jeecg-boot-module-system/Lifecycle/install 
```
无报错将生成jar文件
 ```
 $PWD/jeecg-boot/jeecg-boot-module-system/target/jeecg-boot-module-system-2.4.2.jar 
 ```
 
 启动后端服务执行
 ```
 java -jar jeecg-boot-module-system-2.4.2.jar 
 ```
 
 ```
 
   (_)                          | |               | |
    _  ___  ___  ___ __ _ ______| |__   ___   ___ | |_
   | |/ _ \/ _ \/ __/ _` |______| '_ \ / _ \ / _ \| __|
   | |  __/  __/ (_| (_| |      | |_) | (_) | (_) | |_
   | |\___|\___|\___\__, |      |_.__/ \___/ \___/ \__|
  _/ |               __/ |
 |__/               |___/



Jeecg  Boot Version: 2.4.2
Spring Boot Version: 2.3.5.RELEASE (v2.3.5.RELEASE)


2021-03-04 18:12:00.534 [background-preinit] INFO  org.hibernate.validator.internal.util.Version:21 - HV000001: Hibernate Validator 6.1.6.Final
2021-03-04 18:12:00.630 [main] INFO  org.jeecg.JeecgSystemApplication:55 - Starting JeecgSystemApplication v2.4.2 on MacBook-Pro.local with PID 72769 (/Users/yongyang/Documents/WorkPlace/myWork/jeecg-boot/jeecg-boot/jeecg-boot-module-system/target/jeecg-boot-module-system-2.4.2.jar started by yongyang in /Users/yongyang/Documents/WorkPlace/myWork/jeecg-boot/jeecg-boot/jeecg-boot-module-system/target)
2021-03-04 18:12:00.631 [main] INFO  org.jeecg.JeecgSystemApplication:655 - The following profiles are active: dev
2021-03-04 18:12:01.514 [background-preinit] WARN  o.s.h.converter.json.Jackson2ObjectMapperBuilder:127 - For Jackson Kotlin classes support please add "com.fasterxml.jackson.module:jackson-module-kotlin" to the classpath
2021-03-04 18:12:03.319 [main] INFO  o.s.d.r.config.RepositoryConfigurationDelegate:249 - Multiple Spring Data modules found, entering strict repository configuration mode!
2021-03-04 18:12:03.324 [main] INFO  o.s.d.r.config.RepositoryConfigurationDelegate:127 - Bootstrapping Spring Data Redis repositories in DEFAULT mode.
2021-03-04 18:12:03.481 [main] INFO  o.s.d.r.config.RepositoryConfigurationDelegate:187 - Finished Spring Data repository scanning in 124ms. Found 0 Redis repository interfaces.
2021-03-04 18:12:04.248 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'spring.redis-org.springframework.boot.autoconfigure.data.redis.RedisProperties' of type [org.springframework.boot.autoconfigure.data.redis.RedisProperties] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:04.253 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'org.springframework.boot.autoconfigure.data.redis.LettuceConnectionConfiguration' of type [org.springframework.boot.autoconfigure.data.redis.LettuceConnectionConfiguration] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:04.607 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'lettuceClientResources' of type [io.lettuce.core.resource.DefaultClientResources] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:04.849 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'redisConnectionFactory' of type [org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:04.852 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'shiroConfig' of type [org.jeecg.config.shiro.ShiroConfig$$EnhancerBySpringCGLIB$$91f34ee9] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:04.910 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'shiroRealm' of type [org.jeecg.config.shiro.ShiroRealm] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:05.157 [main] INFO  org.jeecg.config.shiro.ShiroConfig:208 - ===============(1)创建缓存管理器RedisCacheManager
2021-03-04 18:12:05.164 [main] INFO  org.jeecg.config.shiro.ShiroConfig:226 - ===============(2)创建RedisManager,连接Redis..
2021-03-04 18:12:05.170 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'redisManager' of type [org.crazycake.shiro.RedisManager] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:05.175 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'securityManager' of type [org.apache.shiro.web.mgt.DefaultWebSecurityManager] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:05.237 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'authorizationAttributeSourceAdvisor' of type [org.apache.shiro.spring.security.interceptor.AuthorizationAttributeSourceAdvisor] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:05.632 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'spring.datasource.dynamic-com.baomidou.dynamic.datasource.spring.boot.autoconfigure.DynamicDataSourceProperties' of type [com.baomidou.dynamic.datasource.spring.boot.autoconfigure.DynamicDataSourceProperties] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:05.640 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'com.baomidou.dynamic.datasource.spring.boot.autoconfigure.DynamicDataSourceAutoConfiguration' of type [com.baomidou.dynamic.datasource.spring.boot.autoconfigure.DynamicDataSourceAutoConfiguration$$EnhancerBySpringCGLIB$$9c4577c1] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:05.649 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'dsProcessor' of type [com.baomidou.dynamic.datasource.processor.DsHeaderProcessor] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:05.672 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'redisConfig' of type [org.jeecg.config.redis.RedisConfig$$EnhancerBySpringCGLIB$$8dc3dfd] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:05.736 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'org.apache.shiro.spring.boot.autoconfigure.ShiroBeanAutoConfiguration' of type [org.apache.shiro.spring.boot.autoconfigure.ShiroBeanAutoConfiguration$$EnhancerBySpringCGLIB$$45cfe4a0] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:05.744 [main] INFO  o.s.c.s.PostProcessorRegistrationDelegate$BeanPostProcessorChecker:335 - Bean 'eventBus' of type [org.apache.shiro.event.support.DefaultEventBus] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2021-03-04 18:12:06.211 [main] INFO  o.s.boot.web.embedded.tomcat.TomcatWebServer:108 - Tomcat initialized with port(s): 8080 (http)
2021-03-04 18:12:06.226 [main] INFO  org.apache.coyote.http11.Http11NioProtocol:173 - Initializing ProtocolHandler ["http-nio-8080"]
2021-03-04 18:12:06.227 [main] INFO  org.apache.catalina.core.StandardService:173 - Starting service [Tomcat]
2021-03-04 18:12:06.228 [main] INFO  org.apache.catalina.core.StandardEngine:173 - Starting Servlet engine: [Apache Tomcat/9.0.39]
2021-03-04 18:12:06.345 [main] INFO  o.a.c.c.C.[Tomcat].[localhost].[/jeecg-boot]:173 - Initializing Spring embedded WebApplicationContext
2021-03-04 18:12:06.346 [main] INFO  o.s.b.w.s.c.ServletWebServerApplicationContext:285 - Root WebApplicationContext: initialization completed in 5614 ms
2021-03-04 18:12:07.898 [main] INFO  com.alibaba.druid.pool.DruidDataSource:994 - {dataSource-1,master} inited
2021-03-04 18:12:07.900 [main] INFO  c.b.dynamic.datasource.DynamicRoutingDataSource:132 - dynamic-datasource - load a datasource named [master] success
2021-03-04 18:12:07.900 [main] INFO  c.b.dynamic.datasource.DynamicRoutingDataSource:237 - dynamic-datasource initial loaded [1] datasource,primary datasource named [master]
2021-03-04 18:12:10.209 [main] INFO  o.j.boot.starter.redis.config.RedisConfiguration:45 -  --- redis config init ---
2021-03-04 18:12:11.014 [main] INFO  org.jeecg.config.redis.RedisConfig:66 -  --- redis config init ---
2021-03-04 18:12:12.739 [main] INFO  org.quartz.impl.StdSchedulerFactory:1220 - Using default implementation for ThreadExecutor
2021-03-04 18:12:12.745 [main] INFO  org.quartz.simpl.SimpleThreadPool:268 - Job execution threads will use class loader of thread: main
2021-03-04 18:12:12.764 [main] INFO  org.quartz.core.SchedulerSignalerImpl:61 - Initialized Scheduler Signaller of type: class org.quartz.core.SchedulerSignalerImpl
2021-03-04 18:12:12.764 [main] INFO  org.quartz.core.QuartzScheduler:229 - Quartz Scheduler v.2.3.2 created.
2021-03-04 18:12:12.771 [main] INFO  o.s.scheduling.quartz.LocalDataSourceJobStore:672 - Using db table-based data access locking (synchronization).
2021-03-04 18:12:12.774 [main] INFO  o.s.scheduling.quartz.LocalDataSourceJobStore:145 - JobStoreCMT initialized.
2021-03-04 18:12:12.776 [main] INFO  org.quartz.core.QuartzScheduler:294 - Scheduler meta-data: Quartz Scheduler (v2.3.2) 'MyScheduler' with instanceId 'MacBook-Pro.local1614852732743'
  Scheduler class: 'org.quartz.core.QuartzScheduler' - running locally.
  NOT STARTED.
  Currently in standby mode.
 ```

服务启动成功


### jeecgBoot 前端工程启动

idea 中编辑配置文件 `Edite Configurations`
添加`npm `


	name：jbootNpm
	package.json：./jeect-boot/ant-design-vue-jeecg/	package.json
	Command:run
	Scripts:serve

`Run jbootNpm` 启动前端

```
	DONE  Compiled successfully in 36461ms                                                                                         下午4:12:17


  	App running at:
  	- Local:   http://localhost:3000/ 
 	- Network: http://10.100.155.185:3000/

  	Note that the development build is not optimized.
  	To create a production build, run yarn build.
```

或者使用`VSCode` 打开，命令后运行 `npm run serve`

至此前后端启动完成


---
layout: post
title: Jeecg-boot Mac 工具清单
category: 框架
tags: jeecg-boot
description: Jeecg-boot Mac 工具清单
---
### Jeecg Boot 介绍

`JeecgBoot` 是一款基于代码生成器的低代码开发平台，零代码开发！采用前后端分离架构：`SpringBoot2.x`，`Ant Design&Vue`，`Mybatis-plus`，`Shiro`，`JWT`。强大的代码生成器让前后端代码一键生成，无需写任何代码! `JeecgBoot`引领新的开发模式(`Online Coding`模式-> `代码生成器模式`-> `手工MERGE智能开发`)， 帮助解决`Java`项目70%的重复工作，让开发更多关注业务逻辑。既能快速提高开发效率，帮助公司节省成本，同时又不失灵活性！`JeecgBoot`还独创在线开发模式（No代码概念）：在线表单配置（表单设计器）、移动配置能力、工作流配置（在线设计流程）、报表配置能力、在线图表配置、插件能力（可插拔）等等！

`JeecgBoot`在提高UI能力的同时，降低了前后分离的开发成本，`JeecgBoot`还独创在线开发模式（No代码概念），一系列在线智能开发：在线配置表单、在线配置报表、在线图表设计、在线设计流程等等。

`JEECG`宗旨是:简单功能由`Online Coding`配置实现（在线配置表单、在线配置报表、在线图表设计、在线设计流程、在线设计表单），复杂功能由代码生成器生成进行手工`Merge`，既保证了智能又兼顾了灵活;
业务流程采用工作流来实现、扩展出任务接口，供开发编写业务逻辑，表单提供多种解决方案： 表单设计器、`online`配置表单、编码表单。同时实现了流程与表单的分离设计（松耦合）、并支持任务节点灵活配置，既保证了公司流程的保密性，又减少了开发人员的工作量。

```
官方网站： http://www.jeecg.com
源码下载： https://github.com/zhangdaiscott/jeecg-boot
QQ交流群：②769925425、①284271917、③816531124
在线演示： http://boot.jeecg.com
版本日志： http://www.jeecg.com/doc/log

```

###技术架构：

####后端技术： `SpringBoot_2.1.3.RELEASE + Mybatis-plus_3.1.2 + Shiro_1.4.0 + Jwt_3.7.0  + Swagger-ui + Redis `
####前端技术： `Ant-design-vue + Vue + Webpack`
####其他技术： `Druid（数据库连接池）、Logback（日志工具） 、poi（Excel工具）、Quartz（定时任务）、lombok（简化代码）`
####项目构建： `Maven、Jdk8`

###前端开发必读文档：

####前端UI组件： `Ant Design of Vue`
[https://www.antdv.com/docs/vue/introduce](https://www.antdv.com/docs/vue/introduce)
####报表UI组件：`viser-vue`
[https://viserjs.gitee.io/demo.html#/viser/bar/basic-bar](https://viserjs.gitee.io/demo.html#/viser/bar/basic-bar)
####`VUE`基础知识：
[https://cn.vuejs.org/v2/guide](https://cn.vuejs.org/v2/guide)
####`Ant Design Vue Pro`：
[https://pro.loacg.com/docs/getting-started
](https://pro.loacg.com/docs/getting-started
)
###JeecgBoot采用前后分离架构，官方推荐前后端都用IDEA

 前端开发： IDEA 或  Webstrom
 
 后端开发： IDEA 或 Eclipse
 
 
####前端环境安装（开发工具—帮助文档）

```
序号	工具	描述	参考
1	Nodejs/Npm安装/Cnpm安装	JavaScript运行环境，此处使用到它的包管理器npm	https://my.oschina.net/jeecg/blog/4277939
2	Yarn安装	下载包工具	https://my.oschina.net/jeecg/blog/4278012
3	WebStorm安装与使用（也可用IDEA）	WEB前端开发工具	https://blog.csdn.net/u011781521/article/details/53558979

```

####配置Nodejs镜像

```
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global

yarn config set registry https://registry.npm.taobao.org --global
yarn config set disturl https://npm.taobao.org/dist --global

```
####后端环境安装（开发工具—帮助文档）

后端开发建议采用IDEA，方便多Maven模块开发，热部署请集成JRebel。

```
序号	工具	参考
1	JDK8安装、Maven安装	此部分请百度
2	IDEA安装	https://jeecg.blog.csdn.net/article/details/103252484
3	IDEA中Lombok插件的安装与使用	https://www.cnblogs.com/iathanasy/p/9262689.html
4	IDEA热部署JRebel安装	https://blog.csdn.net/weixin_42831477/article/details/82229436
5	IDEA自动生成类注释和方法注释	https://my.oschina.net/jeecg/blog/3198358
5	Eclipse安装lombok插件	https://blog.csdn.net/qq_25646191/article/details/79639633
6	Eclipse自定义皮肤主题	https://blog.csdn.net/StillOnMyWay/article/details/79109741
7	Eclipse常用快捷键	https://blog.csdn.net/zhangdaiscott/article/details/52790087
```


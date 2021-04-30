---
layout: post
title:  jeecgBoot 工程初始化
category: 框架
tags: redis
description:  jeecgBoot 在线代码生成配置，
---

在线代码生成配置（使用jar方式运行），无法生成代码，无报错，代码目录为空


需要把文件夹 `jeecg-boot/jeecg-boot/jeecg-boot-module-system/src/main/resources/jeecg`拷贝到 `jeecg-boot-module-system-2.4.2.jar` 同级新建目录 `config` 下

结构如下

```
/target: ls target/config/jeecg 
code-template             jeecg_config.properties
code-template-online      jeecg_database.properties
➜  target
```

重新运行jar

`java -jar jeecg-boot-module-system-2.4.2.jar`

### 在线表单开发，不需要发布代码的开发

在在线表单开发中添加完表单之后，查看 更多中的 配置地址，复制配置地址到 新加菜单的 菜单路径中,具体配置如下

```
菜单类型： 可以选择“一级菜单”，也可以选择“子菜单”，但“一级菜单”的排序级别不建议低于首页。
菜单名称： 菜单显示名称
菜单路径 填写刚刚复制的路径
前端组件 固定为modules/online/desform/auto/AutoDesignDataForm
排序 排序数字越高，显示顺序越靠下
是否路由菜单 默认为“是”，这里一定要点成“否”
```

另外需要给菜单赋值权限。

如需要修改前端页面，需复制vue到前端目录下
新建菜单之后，复制vue文件到前端之后，访问新建的菜单提示  “资源没找到”。 需要后端项目 全部`run` 一遍。 `maven` 中 `jeecg-boot-parent/Lifecycle/install`  

重新启动jar 文件

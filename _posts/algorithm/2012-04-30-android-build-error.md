---
layout: post
title: Android 打包上架应用市场漏洞修复
category: Android
tags: 漏洞
description: Android 打包上架应用市场漏洞修复
---

### Android 未使用编译器堆栈保护技术解决方法

风险描述

为了检测栈中的溢出，引入了`Stack Canaries`漏洞缓解技术。在所有函数调用发生时，向栈帧内压入一个额外的被称作`canary`的随机数，当栈中发生溢出时，`canary`将被首先覆盖，之后才是`EBP`和返回地址。在函数返回之前，系统将执行一个额外的安全验证操作，将栈帧中原先存放的`canary`和`.data`中副本的值进行比较，如果两者不吻合，说明发生了栈溢出。

危害描述

不使用`Stack Canaries`栈保护技术，发生栈溢出时系统并不会对程序进行保护。

修复建议

使用`NDK`编译`so`时，在`Android.mk`文件中添加：`LOCAL_CFLAGS := -Wall -O2 -U_FORTIFY_SOURCE -fstack-protector-all`

```
ndk {
            //选择要添加的对应cpu类型的.so库。
        abiFilters 'armeabi', 'armeabi-v7a'
        cFlags "-Wall -O2 -U_FORTIFY_SOURCE -fstack-protector-all"

}
```

在项目	`app	`的`build.gradle` 中添加

### 日志数据泄露风险

删除`System.out.println` 输出

### WebView组件忽略SSL证书验证错误漏洞
所有`webview` 初始化的地方都需要调用

```
webview.removeJavascriptInterface("searchBoxJavaBridge_");
webview.removeJavascriptInterface("accessibility");
webview.removeJavascriptInterface("accessibilityTraversal");
		
```

### AndroidManifest.xml 中去掉不必要的权限

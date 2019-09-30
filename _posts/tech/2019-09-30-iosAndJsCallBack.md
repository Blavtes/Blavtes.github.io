---
layout: post
title: js和native交互
category: 算法
tags: iOS
description: js和native交互
--- 
### h5调用native

在开发过程中很难避免使用h5开发页面，难免出现需要h5和native界面做交互的地方。比如h5调用原生界面的分享、h5关闭原生界面等。
 	
下面介绍下，当h5使用react.js时如何设置相关代码。
	
以在h5中调用原生界面的返回函数 ``appBackClick()``为例：

```
//index.html
...
<head>
  <script type="text/javascript">
    function appBackClick() {
      //app 实现该函数功能
      app.appBackClick();
    }
  </script>
</head>
...

//react.js
....
backClick() {
	window.appBackClick();
}
....

//oc WebviewController.m

//添加定义协议代理方法 和h5中方法名一致
·#import <JavaScriptCore/JavaScriptCore.h>
@protocol JSDelegate <JSExport>
//- (void)openShare:(id)name1 :(id)url1 :(id)name2 :(id)url2 :(id)name3 :(id)url4 :(id)name4;
- (void)appBackClick;
@end

//添加代理
@interface WebViewController () <UIWebViewDelegate,JSDelegate> 
//实例化context
@property (nonatomic, strong) JSContext *jsContext;

- (void)webViewDidFinishLoad:(UIWebView *)webView {
	[self addJsContextInfo];
}

- (void)addJsContextInfo
{
//持有context
    self.jsContext = [self.webView valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
    //'app'. 和h5 index.html 中调用的类名一致
    self.jsContext[@"app"] = self;
    self.jsContext.exceptionHandler = ^(JSContext *context, JSValue *exceptionValue) {
        context.exception = exceptionValue;
        DLog(@"webview 异常信息：%@", exceptionValue);
    };
}

//实现代理方法
- (void)appBackClick
{
    DLog(@"---appBackClick");
    [self.navigationController popViewControllerAnimated:YES];
}
```

以上就是简单的一个js 调用原生的函数。
如果要添加参数或者返回值修改方法名：

```
//两个参数
function appBackClick() {
  //app 实现该函数功能
  app.appBackClick(a, b);
}
</script>


//添加定义协议代理方法 和h5中方法名一致
·#import <JavaScriptCore/JavaScriptCore.h>
@protocol JSDelegate <JSExport>

- (void)appBackClick:(id)a :(id)b;
@end

//实现
- (void)appBackClick:(id)a :(id)b {
}
```

也可以添加返回值：

```
//两个参数 返回a+b的值
function appBackClick() {
  //app 实现该函数功能
  return app.appBackClick(a, b);
}
</script>


//添加定义协议代理方法 和h5中方法名一致
·#import <JavaScriptCore/JavaScriptCore.h>
@protocol JSDelegate <JSExport>

- (int)appBackClick:(id)a :(id)b;
@end

//实现
- (int)appBackClick:(id)a :(id)b {
	return a + b;
}
```

### 原生调用JS

```
//index.html

//扫描结果回调方法    app->h5
function scanResult(result){
	document.getElementById("result").innerHTML = '扫描结果：' + result;  
}

//oc function
JSContext *context = [_mainWebView valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
NSString *alertJS= [NSString stringWithFormat:@"scanResult('%@')",我是结果信息];
[context evaluateScript:alertJS];


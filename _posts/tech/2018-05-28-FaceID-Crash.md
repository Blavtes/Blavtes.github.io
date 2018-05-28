---
layout: post
title: iOS 11.3 Crash 权限问题
category: 技术
tags: iOS
description: iOS Crash：TCCAccessRequest block invoke
--- 

### 问题

最近发现有用户iPhone X 升级到11.3 之后，app中使用FaceID 崩溃。

Crash 信息如下：

	0 libsystem_kernel.dylib	__abort_with_payload + 8
	1 libsystem_kernel.dylib	_abort_with_payload_wrapper_internal + 100
	2 libsystem_kernel.dylib	system_set_sfi_window + 0
	3 TCC	___TCCAccessRequest_block_invoke.85
	4 TCC	___CRASHING_DUE_TO_PRIVACY_VIOLATION__
	5 TCC	___tccd_send_block_invoke + 296
	6 libxpc.dylib	__xpc_connection_reply_callout + 60
	7 libxpc.dylib	__xpc_connection_call_reply_async + 88
	8 libdispatch.dylib	__dispatch_client_callout3 + 16
	9 libdispatch.dylib	__dispatch_mach_msg_async_reply_invoke$VARIANT$armv81 + 312
	10 libdispatch.dylib	__dispatch_queue_override_invoke$VARIANT$armv81 + 388
	11 libdispatch.dylib	__dispatch_root_queue_drain + 592
	12 libdispatch.dylib	__dispatch_worker_thread3 + 112
	13 libsystem_pthread.dylib	_pthread_wqthread + 1176

看堆栈信息问题出在这：
	
	3 TCC	___TCCAccessRequest_block_invoke.85
初步猜想是和权限申请有关系。
app UI适配iPhoneX 之后没发现有问题就没管了。突然就报这样的问题，可能系统11.3 加了权限校验。

### 权限添加NSFaceIDUsageDescription

使用FaceID需要在info.plist中增加NSFaceIDUsageDescription权限申请说明，这个跟定位、拍照等一样。

### 使用方法
目前发现使用TouchID验证FaceID，方法同样可行。

	//初始化上下文对象
	LAContext *context = [[LAContext alloc] init];
	//localizedFallbackTitle＝@“”,不会出现“输入密码”按钮
	context.localizedFallbackTitle = @"";
	//错误对象
	NSError *error = nil;
	NSString *result = @"验证信息";
	
	/**
	 *LAPolicyDeviceOwnerAuthentication 手机密码的验证方式
	 *LAPolicyDeviceOwnerAuthenticationWithBiometrics 指纹的验证方式
	 */
	if ([context canEvaluatePolicy:LAPolicyDeviceOwnerAuthenticationWithBiometrics error:&error]) {
	    [context evaluatePolicy:LAPolicyDeviceOwnerAuthenticationWithBiometrics localizedReason:result reply:^(BOOL success, NSError *error) {
	        if(error.code == LAErrorTouchIDLockout) {
	            
	            BOOL can = [context canEvaluatePolicy:LAPolicyDeviceOwnerAuthentication error:&error];
	            if (can) {
	                [context evaluatePolicy:LAPolicyDeviceOwnerAuthentication localizedReason:result reply:^(BOOL success, NSError * _Nullable error) {
	                    
	                }];
	                
	            }
	            else{
	                NSLog(@"调起账号密码页面失败!!!");
	            }
	        }
	    }];
	}

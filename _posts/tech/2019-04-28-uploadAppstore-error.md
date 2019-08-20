---
layout: post
title: 提交appstore 错误
category: 脚本
tags: sh
description: 提交appstore 错误
---

提交appstore 错误
	
	App Store Connect Operation Error
	Could not find version: latest of iTMSTransporter to download.
	
	App Store Connect Operation Error
	Could not retrieve remote configuration details.
	
	App Store Connect Operation Error
	An exception has occurred: Unable to tunnel through proxy. Proxy returns "HTTP/1.1 502 Bad Gateway"
	
	App Store Connect Operation Error
	Communication error. Please use diagnostic mode to check connectivity.
	
	
终端执行三条命令完美解决

	1、cd ~
	2、mv .itmstransporter/ .old_itmstransporter/
	
	3、"/Applications/Xcode.app/Contents/Applications/Application Loader.app/Contents/itms/bin/iTMSTransporter"
	
	
最后还不行就还工具上传 ```Application Loader```
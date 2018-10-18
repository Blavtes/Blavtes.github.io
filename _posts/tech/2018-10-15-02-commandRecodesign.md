---
layout: post
title: 命令行重签名
category: 技术
tags: ios
description: 命令行重签名
--- 

##一、重签名准备工作：

找到开发者证书和配置文件：
列出所有开发者证书文件：


	security find-identity -p codesigning -v



找一个开发环境配置文件生成entitlements.plist文件，后面签名要用到：

	security cms -D -i XX.mobileprovision  > profile.plist
	
	/usr/libexec/PlistBuddy -x -c 'Print :Entitlements' profile.plist > entitlements.plist
	
	cat entitlements.plist

把准备好的开发环境配置文件复制到XX.app文件夹下：

	cp XX.mobileprovision Payload/XX.app/embedded.mobileprovision

修改包Info.plist中的Bundle Identifier与配置文件中的Bundle Identifier保持一致：

	/usr/libexec/PlistBuddy -c "Set :CFBundleIdentifier com.XX.XX" Payload/XX.app/Info.plist


移除之前的签名文件夹：

	rm -rf Payload/XX.app/_CodeSignature

##二、iOS重签名：

重签名framework：

	
	/usr/bin/codesign --force --sign 84A4B9F1F902462CC33D01E9FF72C1BA04A97653 --entitlements entitlements.plist /Payload/XX.app/Frameworks/JSONModel.framework

重签名app执行文件：

	/usr/bin/codesign --force --sign 84A4B9F1F902462CC33D01E9FF72C1BA04A97653 --entitlements entitlements.plist Payload/XX.app/XX

查看app签名信息：

	codesign -vv -d Payload/XX.app

注意：重签名有顺序，先把framework和dylib签名，最后再签名：XX.app/XX，顺序弄错了，就算签名成功也可能会安装失败!

##三、调试和打包：

ios-deploy安装与调试：

	ios-deploy -d -b Payload/XX.app

出现如下success字样，就证明成功了！

	(lldb) connect
	(lldb) run
	success
	
过程中如果遇到错误提示：`“Error 0xe8000067: There was an internal API error. AMDeviceSecureInstallApplication(0, device, url, options, install_callback, 0)”`

错误原因：可能存在有framework或者dylib未签名的情况。

解决方案：把app文件夹下面的framework全部签名。

打包（package）：
	
	zip -qry ppdest.ipa Payload
	
	rm -rf Payload/

##四、iOS重签名工具介绍：

用[iOS App Signer](https://github.com/DanTheMan827/ios-app-signer)重签名：

用[iResign](https://github.com/maciekish/iReSign)重签名：


##五、参考资料地址：

[Patching and Re-Signing iOS Apps](http://www.vantagepoint.sg/blog/85-patching-and-re-signing-ios-apps)

[OS X Man Pages](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/codesign.1.html)
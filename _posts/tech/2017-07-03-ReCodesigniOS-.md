---
layout: post
title: 重签名ipa 
category: 技术
tags: 重签名
description: ipa 重签名
---

##重签名ipa 

###重签名ipa 有两种方式：
	
	1.通过Xcode重签名
	2.直接修改已签名的ipa文件

###通过Xcode重签名
	
	目的是在不同Mac上重新签名，即传播Xcode Archive.
	在Xcode中archive成功后，导出xcarchive文件。传递到第三方。双击打开之后，选择save for iOS App Store Deployment 或 Save fo人 Enterprise Deployment ，这样就可以达到重签名的目的

###直接修改已签名的ipa文件
	其实iPA文件就是zip文件，只是后缀不同而已。要重签名，我们需要准备证书与provision profile， 证书直接在Keychian里管理，provision profile与证书是对应关系。 真机调试或提交过App到App Store的朋友都应不会陌生。
	下面直接说步骤：
	a.解压iPA文件
	b.删掉旧的签名文件
	c.拷贝新的provision profile替换旧的embedded.mobileprovision
	d.用codesign命令重签名
	f.重新zip为iPA文件
	
####下面有一个脚本，它完成了上面5步骤：



	#!/bin/sh
	newLoad=Payload.zip
	
	ipaName=$1.ipa
	
	if !([ -f $ipaName ]); then
		echo \"${1}\"文件不存在
		exit
	fi

	cp $ipaName $newLoad
	
	## step 1, unzip ipa file
	unzip $ipaName
	
	## step 2, remove old codesign
	rm -rf Payload/*.app/_CodeSignature/
	
	## step 3, copy new provision profile
	cp new.mobileprovision Payload/*.app/embedded.mobileprovision
	
	## step 4, codesign with new certificate and provision
	(/usr/bin/codesign -f -s "iPhone Developer: XXXX (XXXX)" --resource-rules Payload/*.app/ResourceRules.plist Payload/*.app/) || {
	## if code sign error, will to here
		echo failed
		# rm -rf Payload/
		exit
	}
	
	## step 5, zip it
	zip -r ${ipaName}abc.ipa Payload/
	# rm -rf Payload/

*如果出现Warning: --resource-rules has been deprecated in Mac OS X >= 10.10!
	
	Click on your project > Targets > Select your target > Build Settings >
	
	Code Signing Resource Rules Path
	
	and add: $(SDKROOT)/ResourceRules.plist
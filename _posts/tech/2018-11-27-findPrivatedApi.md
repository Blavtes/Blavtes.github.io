---
layout: post
title: 查找私有api
category: 脚本
tags: sh
description: 查找私有api
---

提交app审核，旧版本被下架。下架原因:

	We are writing to let you know about new information regarding your app currently live on the App Store.
	
	Upon re-evaluation, we found that your app is not in compliance with the App Store Review Guidelines. Specifically, we found:
	
	Performance - 2.5.2
	Your app, extension, or linked framework appears to contain code designed explicitly with the capability to change your app’s behavior or functionality after App Review approval, which is not in compliance with App Store Review Guideline 2.5.2 and section 3.3.2 of the Apple Developer Program License Agreement.
	
	For this reason, your app will be removed from sale on the App Store at this time.
	
	Deliberate disregard of the App Store Review Guidelines and attempts to deceive users or undermine the review process are unacceptable and is a direct violation Section 3.2(f) of the Apple Developer Program License Agreement. Continuing to violate the Terms & Conditions of the Apple Developer Program will result in the termination of your account, as well as any related or linked accounts, and the removal of all your associated apps from the App Store.
	
	Future submissions of this app may require a longer review time, and this app will not be eligible for an expedited review.
	
	If you have any questions about this information, please reply to this message to let us know.

查找原因是因为第三方SDK 使用违反规定的api。
主要查找这几个api：

	dlopen|method_exchangeImplementations|performSelector|respondsToSelector|dlsym
	
制作脚本：
	
	#!/bin/bash
	
	# 定義用到的變量
	project_path=""
	
	# 定義讀取輸入字符的函數
	function getProjectPath() {
	 # 輸出換行，方便查看
	 echo "================================================"
	 # 監聽輸入並且賦值給變量
	 read -p " Enter project path: " project_path
	 # 如果為空值，從新監聽
	 if test -z "$project_path"; then
	  getProjectPath
	 else
	  read_dir ${project_path}
	 fi
	}
	
	function read_dir(){
	 for file in `ls $1`       #注意此處這是兩個反引號，表示運行系統命令
	 do
	  if [ -d $1"/"$file ]  #注意此處之間一定要加上空格，否則會報錯
	  then
	   read_dir $1"/"$file
	  else
	   #在此處處理文檔即可
	   file_path="$1/$file"
	   if `file ${file_path} | grep -q 'Mach-O'` ; then
	    find_world=$(echo `nm -u ${file_path} | grep -E 'dlopen|method_exchangeImplementations|performSelector|respondsToSelector|dlsym'`)
	    # -n 字符串 字符串的長度不為零則為真
	    if [ -n "$find_world" ] ; then
	     echo '-----------------------------\n'
	     echo ${file_path}
	     echo '包含字段：'
	     echo ${find_world}
	     echo '\n'
	    fi
	   fi
	  fi
	 done
	}   
	
	#讀取第一個參數
	getProjectPath
	
	echo "------- end processing -------"
	


#检测IPA包
1、首先你有个可以提交审核的ipa，就是打包的第一个，不是测试的release。

2、将ipa重命名为zip格式，解压。如果有两个文件夹Payload、Symbols，就OK。

3、cd到Payload里面的app

4、有两种方式可以检测打包文件是否包含字符串
	
	 #pinduoduo.app strings - -a -arch armv7 "pingduoduo" | grep dlsym
	
	（1） strings - -a -arch armv7 "pingduoduo" | grep dlsym
	
	（2）strings - -a -arch armv7 "pingduoduo" > test.txt

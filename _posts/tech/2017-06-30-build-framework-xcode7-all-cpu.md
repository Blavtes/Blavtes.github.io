---
layout: post
title: 打包Framework
category: 技术
tags: Framework
description: 脚本打包framework（Xcode7&OSX10.11）兼容各种cpu类型
---
## 打包framework（Xcode7&OSX10.11）兼容各种cpu类型

###第一步新建工程
	选择Framework & Library => Cocoa Touch Framework
	
![step1](http://oshs6ulbi.bkt.clouddn.com/framework-step1)

###第二步新建Framework项目，eg：TestFramework

![step1](http://oshs6ulbi.bkt.clouddn.com/framework-step2)

###第三步在已有target中新建一个target，eg：TesetBuild

	1.选择Cross-platform 分类

	2.选择 Aggregate 目标
![step1](http://oshs6ulbi.bkt.clouddn.com/framework-step3)

###设置TesetBuild编译条件

	1.BuildSettings的Mach-O Type=> static Library
	2.Build Phases，Run Script 
![step1](http://oshs6ulbi.bkt.clouddn.com/framework-step4)

###通用脚本 Script

```
# Sets the target folders and the final framework product.
# 如果工程名称和Framework的Target名称不一样的话，要自定义FMKNAME
# 例如: FMK_NAME = "MyFramework"

FMK_NAME=${PROJECT_NAME}

# Install dir will be the final output to the framework.
# The following line create it in the root folder of the current project.

INSTALL_DIR=${SRCROOT}/Products/${FMK_NAME}.framework

# Working dir will be deleted after the framework creation.

WRK_DIR=build

DEVICE_DIR=${WRK_DIR}/Release-iphoneos/${FMK_NAME}.framework

SIMULATOR_DIR=${WRK_DIR}/Release-iphonesimulator/${FMK_NAME}.framework

# -configuration ${CONFIGURATION}
# Clean and Building both architectures.

xcodebuild -configuration "Release" -target "${FMK_NAME}" -sdk iphoneos -arch armv7 -arch armv7s -arch arm64 clean build

xcodebuild -configuration "Release" -target "${FMK_NAME}" -sdk iphonesimulator -arch x86_64 -arch i386 clean build

# Cleaning the oldest.
if [ -d "${INSTALL_DIR}" ] then
	rm -rf "${INSTALL_DIR}"
fi

mkdir -p "${INSTALL_DIR}"

cp -R "${DEVICE_DIR}/" "${INSTALL_DIR}/"

# Uses the Lipo Tool to merge both binary files (i386 + armv6/armv7) into one Universal final product.

lipo -create "${DEVICE_DIR}/${FMK_NAME}" "${SIMULATOR_DIR}/${FMK_NAME}" -output "${INSTALL_DIR}/${FMK_NAME}"

rm -r "${WRK_DIR}"

#open "${SRCROOT}/Products/"

```

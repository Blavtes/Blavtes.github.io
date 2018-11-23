---
layout: post
title: AES-JavaScript加解密
category: 算法
tags: AES
description: AES-JavaScript加解密
---

AES 加密解密解析

概述

AES 即 高级加密标准（英语：Advanced Encryption Standard，缩写：AES），在密码学中又称Rijndael加密法，是美国联邦政府采用的一种区块加密标准。这个标准用来替代原先的DES，已经被多方分析且广为全世界所使用

原理

AES加密过程是在一个4×4的字节矩阵上运作，这个矩阵又称为“体（state）”，其初值就是一个明文区块（矩阵中一个元素大小就是明文区块中的一个Byte）。（Rijndael加密法因支持更大的区块，其矩阵行数可视情况增加）加密时， 各轮AES加密循环（除最后一轮外）均包含4个步骤：

AddRoundKey—矩阵中的每一个字节都与该次回合密钥（round key）做XOR运算；每个子密钥由密钥生成方案产生。 SubBytes—通过一个非线性的替换函数，用查找表的方式把每个字节替换成对应的字节。 ShiftRows—将矩阵中的每个横列进行循环式移位。 MixColumns—为了充分混合矩阵中各个直行的操作。这个步骤使用线性转换来混合每内联的四个字节。最后一个加密循环中省略MixColumns步骤，而以另一个AddRoundKey替换。

加密模式

AES有5种工作模式，分别为CBC、ECB、CTR、OCF、CFB

电码本模式（```Electronic Codebook Book (ECB)）```
密码分组链接模式（```Cipher Block Chaining (CBC)```）
计算器模式（```Counter (CTR)```）
密码反馈模式（```Cipher FeedBack (CFB)```）
输出反馈模式（```Output FeedBack (OFB)```）
填充方式

填充方式, 有``` Pkcs7, AnsiX923, Iso10126, Iso97971, ZeroPadding, NoPadding```

加密解密

在此介绍的AES加密解密方法用到基本库是
	
	 crypto-js ，JavaScript library of crypto standards.。

首先 按照 README文件中的 步骤导入 该库

（1）ECB ZEROPadding 加密 解密 加密：

	
	const cipher = CryptoJS.AES.encrypt(message, key, {
 	 mode: CryptoJS.mode.ECB,
 	 padding: CryptoJS.pad.ZeroPadding,
  	iv: '',
	});
// 将加密后的数据转换成 Base64
	
	const base64Cipher = cipher.ciphertext.toString(CryptoJS.enc.Base64);
解密：


	const decipher = CryptoJS.AES.decrypt(encrypted, key, { mode: CryptoJS.mode.ECB, padding: CryptoJS.pad.ZeroPadding, iv: '', });

// 将解密对象转换成 UTF8 的字符串 

	const resultDecipher = CryptoJS.enc.Utf8.stringify(decipher);

（2）ECB NOPadding 加密 解密 nopadding 的填充方式特别注意 因为涉及到加密字符串的长度 对齐问题，如果不处理 原字符串 解密会直接出错

加密前 首先将加密的字符串 处理一下： 如： 补齐字符 需要和后台协商 ，要前端和后台需一致 在此用 空格代替

	if(message.length%16!==0){ var numChar = 16-message.length%16; for(var i=0;i<numChar;i++){ message =message+' '; } }

处理后 对处理后的字符串进行加密：

处理后 对处理后的字符串进行加密：

	const cipher = CryptoJS.AES.encrypt(message, key, { mode: CryptoJS.mode.ECB, padding: CryptoJS.pad.NoPadding, iv: '', }); // 将加密后的数据转换成 Base64 const base64Cipher = cipher.ciphertext.toString(CryptoJS.enc.Base64);

解密：

	const decipher = CryptoJS.AES.decrypt(encrypted, key, { mode: CryptoJS.mode.ECB, padding: CryptoJS.pad.NoPadding, iv: '', });

// 将解密对象转换成 UTF8 的字符串
	
	 const resultDecipher = CryptoJS.enc.Utf8.stringify(decipher);

解密出的字符串是我们加长后的 需要去除后面 添加的字符
	
	 cont resultStr = resultDecipher.Rtrim() ;


react-js 和微信小程序使用aes加解密示例


	import React, { Component } from 'react'
	var CryptoJS = require('./aes.js')
	
	export default class UserAes extends Component {
	
	    componentWillMount() {
      // AES-CBC-

      var data = "{\"list\":[{\"finishTime\":\"2018-11-21 17:59:07.007\",\"lastPageId\":\"com.xxx.app.ui.fragments.RecommendFragment\",\"pageId\":\"com.xxx.app.ui.activities.MainActivity\",\"sessionId\":\"f61131fc903246f88af9a441eac0eea8\",\"startTime\":\"2018-11-21 17:59:07.007\",\"userId\":\"113730\"},{\"finishTime\":\"2018-11-21 17:59:07.007\",\"lastPageId\":\"com.xxx.app.ui.activities.MainActivity\",\"pageId\":\"com.xxx.app.ui.fragments.RecommendFragment\",\"sessionId\":\"f61131fc903246f88af9a441eac0eea8\",\"startTime\":\"2018-11-21 17:59:07.007\",\"userId\":\"113730\"}],\"total\":2,\"type\":0}";

      var key = CryptoJS.enc.Utf8.parse("69324D76887D5795");
      var iv = CryptoJS.enc.Utf8.parse("ujhfwe9ihv0as89w");

      var encrypted = CryptoJS.AES.encrypt(data,key,
        {iv:iv,
          mode:CryptoJS.mode.CBC,
          padding:CryptoJS.pad.Pkcs7,
          asBpytes: true
        });

      console.log(encrypted.toString());


      var encryptedBase64Str = "Ur81iOKPtqYw/iroz9XRBnf7awGh38yJtmrl64LVG7sfRCnm4bsBPzXG0oHDIvYTD5wpgs9lAfKm2nVPo0ruX1RTIeDLWLG+4FjmPoCNd7Kr2/CPLerOV+paNsFK4h3+oznW+rhbdNpqLoyAaLsogfsxu6iUSeRH25ubCf19obOf6G/sNwTdfjyQBuEQVuPiuee6/KhscXjBXmUIWdrngenpymcj/i0xpmgpP7wrAqciuauxyPdq5pt8cdXKgsvId/HzRJ9N0RhfssuT4lHxalXHwK0A4Xp9reOvhNzTBRLUGWZm8AHd6wILYTlbOodAilibmZgLIxI+eMxNbLg6V9fEoQ2/YYEmhZAZPuai4/VFcALrKPvnfy4etzBU0eAwMO09QKmbfLA7RGnqNC/MzrpSnmByD/5p48vPKM3aBUCiZ35BdAX7jSaJaOmyqUu5OLz1f08xvMMT4CnutCGJt1fbbfEC+HeMRNbL+yKNemjpk/Ni6jIFDTo00wIZbPNDoG1er4hzFdNneRSMPZ0cCGH3OCD/++OtsenfLWxv1twlbsDjb4EalqupTJFSC0T/14PSC5fk1zl0+Et5V9Akk8WbhPGNAyWlS0ZS/CJ2qoLKv4tigjAPI3DfAn1+4MPOUVRcfQvlTNE4LYPn+1xvNZO8JvG08p4dqYmJpsnm+JkmfX4f/c/Y4T8XwI0ls02ej1+60iPyuMOHMlpM55ZeAw==";

      var decrypted = CryptoJS.AES.decrypt(encryptedBase64Str, key, {
        iv: iv,
        mode: CryptoJS.mode.CBC,
        padding: CryptoJS.pad.Pkcs7,
        asBpytes: true
      });
      console.log(CryptoJS.enc.Utf8.stringify(decrypted).toString());

     }
	}
	



微信小程序

	
	var CryptoJS = require('./aes.js')
	var AppId = 'ujhfwe9ihv0as89w'
	var AppSecret = '69324D76887D5795'
	var Crypto = require('./cryptojs.js').Crypto;
	
	
	App({
	  onLaunch: function () {
	    console.log('App Launch')
	    this.testPromise()
	    var key = CryptoJS.enc.Utf8.parse("69324D76887D5795");
	    var iv = CryptoJS.enc.Utf8.parse("ujhfwe9ihv0as89w");
	    // var encryptedData = Crypto.util.base64ToBytes("2abcdef")
	    var mode = new Crypto.mode.CBC(Crypto.pad.pkcs7);
	    var eb = Crypto.charenc.UTF8.stringToBytes("abcdef");
	    var kb = Crypto.charenc.UTF8.stringToBytes("69324D76887D5795");//KEY
	    var vb = Crypto.charenc.UTF8.stringToBytes("ujhfwe9ihv0as89w");//IV
	    var ub = Crypto.AES.encrypt(eb, kb, { iv: vb, mode: mode, asBpytes: true });
	
	   
	    console.log(ub)
	
	    var mode1 = new Crypto.mode.CBC(Crypto.pad.pkcs7);
	    var encryptedBase64Str = "Ur81iOKPtqYw/iroz9XRBnf7awGh38yJtmrl64LVG7sfRCnm4bsBPzXG0oHDIvYTD5wpgs9lAfKm2nVPo0ruX1RTIeDLWLG+4FjmPoCNd7Kr2/CPLerOV+paNsFK4h3+oznW+rhbdNpqLoyAaLsogfsxu6iUSeRH25ubCf19obOf6G/sNwTdfjyQBuEQVuPiuee6/KhscXjBXmUIWdrngenpymcj/i0xpmgpP7wrAqciuauxyPdq5pt8cdXKgsvId/HzRJ9N0RhfssuT4lHxalXHwK0A4Xp9reOvhNzTBRLUGWZm8AHd6wILYTlbOodAilibmZgLIxI+eMxNbLg6V9fEoQ2/YYEmhZAZPuai4/VFcALrKPvnfy4etzBU0eAwMO09QKmbfLA7RGnqNC/MzrpSnmByD/5p48vPKM3aBUCiZ35BdAX7jSaJaOmyqUu5OLz1f08xvMMT4CnutCGJt1fbbfEC+HeMRNbL+yKNemjpk/Ni6jIFDTo00wIZbPNDoG1er4hzFdNneRSMPZ0cCGH3OCD/++OtsenfLWxv1twlbsDjb4EalqupTJFSC0T/14PSC5fk1zl0+Et5V9Akk8WbhPGNAyWlS0ZS/CJ2qoLKv4tigjAPI3DfAn1+4MPOUVRcfQvlTNE4LYPn+1xvNZO8JvG08p4dqYmJpsnm+JkmfX4f/c/Y4T8XwI0ls02ej1+60iPyuMOHMlpM55ZeAw==";

   		var eb1 = Crypto.util.base64ToBytes(encryptedBase64Str);
	
	    var ub1 = Crypto.AES.decrypt(eb1, kb, { asBpytes: true, mode: mode1, iv: vb });
	
	    console.log(ub1)
	   
	    }
	})
	
[github地址](https://github.com/Blavtes/CryptoJS)
---
layout: post
title: AES-JavaScript加解密
category: 算法
tags: AES
description: AES-JavaScript加解密
---

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
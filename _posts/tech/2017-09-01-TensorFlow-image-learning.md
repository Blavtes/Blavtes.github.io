---
layout: post
title: TensorFlow 图片识别 
category: 技术
tags: TensorFlow
description: TensorFlow 图片识别
--- 

#一、模型训练
###1、下载数据

	cd UserPath
	mkdir tf_files
	cd tf_files
	curl -O http://download.tensorflow.org/example_images/flower_photos.tgz
	tar xzf flower_photos.tgz
	open ./flower_photos

###2、训练模型
####1.下载[TensorFlow](https://github.com/tensorflow/tensorflow)
	
	git clone https://github.com/tensorflow/tensorflow
	cd tensorflow

模型训练
	
	cd  tf_files
	python /Users/Blavtes/Documents/WorkPlace/python/tensorflow/tensorflow/examples/image_retraining/retrain.py \
	--bottleneck_dir=./bottlenecks/ \
	--how_many_training_steps 100000 \
	--model_dir=./inception2 \
	--output_graph=./retrained_graph2.pb \
	--output_labels=./retrained_labels.txt \
	--image_dir ./flower_photos


脚本会下载inception v3模型，80多兆，可以提前下载好放到[tf_files](tf_files)的[inception](inception)目录下
模型路径:[XX_file](http://download.tensorflow.org/models/image/imagenet/inception-2015-12-05.tgz)
训练完成后，在[tf_files](tf_files)目录下看到模型文件[retrained_graph.pb](retrained_graph.pb)和标签[retrained_labels.txt](retrained_labels.txt)

训练完成：（训练1000次结果）

	INFO:tensorflow:Final test accuracy = 78.9% (N=369)
	INFO:tensorflow:Froze 2 variables.
	Converted 2 variables to const ops.


3、模型验证
	
使用TensorFlow自带测试
	
	cp /Users/Blavtes/Documents/WorkPlace/python/tensorflow/tensorflow/examples/image_retraining/label_image.py tf_files/
	#图片识别
	python label_image.py --graph=retrained_graph2.pb --labels=retrained_labels.txt --image=XXXX.jpg
	
```
	vailable on your machine and could speed up CPU computations.
	2017-09-01 16:16:23.320559: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
	2017-09-01 16:16:24.587380: W tensorflow/core/framework/op_def_util.cc:333] Op BatchNormWithGlobalNormalization is deprecated. It will cease to work in GraphDef version 9. Use tf.nn.batch_normalization().
	roses (score = 0.35852)
	tulips (score = 0.28178)
	sunflowers (score = 0.15517)
	dandelion (score = 0.10815)
	daisy (score = 0.09638)
```

编写简易脚本识别

	#-*- coding:utf-8 -*-
	import tensorflow as tf
	
	image_path = 'a.jpg'
	
	image_data = tf.gfile.FastGFile(image_path,'rb').read()
	
	lable_lines = [line.strip() for line in tf.gfile.GFile("retrained_labels.txt")]
	
	with tf.gfile.FastGFile('retrained_graph2.pb','rb') as f:
		graph_def = tf.GraphDef()
		graph_def.ParseFromString(f.read())
		_ = tf.import_graph_def(graph_def, name='')
	
	
	with tf.Session() as sess:
		softmax_tensor = sess.graph.get_tensor_by_name('final_result:0')
	
	
	preditions = sess.run(softmax_tensor,{'DecodeJpeg/contents:0':image_data})
	
	top_k = preditions[0].argsort()[-len(preditions[0]):][::-1]
	
	for node_id in top_k:
		human_string = lable_lines[node_id]
		score = preditions[0][node_id]
		print('%s (score = %.5f' % (human_string, score))

脚本执行	

```
python lable_image.py
```

测试结果：

	2017-09-01 16:48:42.133762: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
	2017-09-01 16:48:42.133802: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
	2017-09-01 16:48:42.133812: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
	2017-09-01 16:48:42.133820: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
	2017-09-01 16:48:43.497776: W tensorflow/core/framework/op_def_util.cc:333] Op BatchNormWithGlobalNormalization is deprecated. It will cease to work in GraphDef version 9. Use tf.nn.batch_normalization().
	roses (score = 0.35852
	tulips (score = 0.28178
	sunflowers (score = 0.15517
	dandelion (score = 0.10815
	daisy (score = 0.09638

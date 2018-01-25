---
layout: post
title:  "Tensorflow: how to evaluate performance at checkpoints"
date:   2018-01-13 20:50:00 +0800
categories: [post]
---


It is common that uses [tf.train.Saver()](https://www.tensorflow.org/api_docs/python/tf/train/Saver) to save model checkpoints and [tf.train.get_checkpoint_state()](https://www.tensorflow.org/api_docs/python/tf/train/get_checkpoint_state) to restore the saved states. Mostly We only care about the final performance but today if you would like to evaluate performances at **each** checkpoint, how would you do?


**all_model_checkpoint_paths**: return a list, which orders all checkpoints from the oldest to the latest

```python
with tf.Session() as sess:
	sess.run(tf.global_variables_initializer())
	ckpt = tf.train.get_checkpoint_state(save_dir)
	if ckpt and ckpt.model_checkpoint_path:
		saver = tf.train.Saver()
		for checkpoint in ckpt.all_model_checkpoint_paths:
			saver.restore(sess, checkpoint)
			sess.run(tf.global_variables())
			"""
			run your evaluation method here
			"""
```

**model_checkpoint_path**: return the latest checkpoints

```python
with tf.Session() as sess:
	sess.run(tf.global_variables_initializer())
	saver = tf.train.Saver()
	ckpt = tf.train.get_checkpoint_state(save_dir)
	if ckpt and ckpt.model_checkpoint_path:
		saver.restore(sess, ckpt.model_checkpoint_path)
		sess.run(tf.global_variables())
```

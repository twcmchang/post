---
layout: post
title:  "Tensorflow: how to evaluate performance at checkpoints"
date:   2018-01-13 20:50:00 +0800
categories: [post]
---

 
It is common that uses [tf.train.Saver()](https://www.tensorflow.org/api_docs/python/tf/train/Saver) to save model checkpoints and [tf.train.get_checkpoint_state()](https://www.tensorflow.org/api_docs/python/tf/train/get_checkpoint_state) to restore the saved states. Normally we only care about the final performance, but if you would like to evaluate performances at **each** checkpoint, how would you do?

Here we demonstrate how to do performance evaluation in TensorFlow: (1) evaluate at every checkpoint and (2) evaluate at the latest checkpoint.

- TensorFlow version: 1.4.0

=============

(1) **all_model_checkpoint_paths**: return a list, which orders all checkpoints from the oldest to the latest

```python
with tf.Session() as sess:
	sess.run(tf.global_variables_initializer())
	ckpt = tf.train.get_checkpoint_state(save_dir)
	if ckpt and ckpt.model_checkpoint_path:
		saver = tf.train.Saver()
		for checkpoint in ckpt.all_model_checkpoint_paths:
			saver.restore(sess, checkpoint)
			sess.run(tf.global_variables())

			# run your evaluation steps here, i.e.
			# sess.run([accuracy], feed_dict={model.x: Xtest, model.y: Ytest})
```

=============

The following is an example for most cases, evaluating model at the latest checkpoint.

(2) **model_checkpoint_path**: return the latest checkpoint

```python
with tf.Session() as sess:
	sess.run(tf.global_variables_initializer())
	saver = tf.train.Saver()
	ckpt = tf.train.get_checkpoint_state(save_dir)
	if ckpt and ckpt.model_checkpoint_path:
		saver.restore(sess, ckpt.model_checkpoint_path)
		sess.run(tf.global_variables())

		# run your evaluation steps here, i.e.
		# sess.run([accuracy], feed_dict={model.x: Xtest, model.y: Ytest})
```

It is trivial, right? But such information is difficult to find in either TensorFlow documentation or other forums due to the frequent updates of TensorFlow.

Hope this article is helpful for you!


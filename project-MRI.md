---
layout: post
title: "Detecting Early-stage Neurodegeneration using 3D Convolutional Neural Networks"
date:   2017-12-16 00:50:00 +0800
display: "../images/logo_mri.png"
categories: [post]
---

This work proposes a novel 3D convolutional neural network to help detect early-stage neurodegeneration from brain MRI raw images. By building a predictive model on healthy subjects, the brain-predicted age can be used to quantify the ageing of brain by subtracting chronological age from brain-predicted age.
- The 3D CNN model considers (1) the **deeper bottleneck architecture** like ResNet, and (2) **instance normalization** instead of batch normalization for better adaptation across subjects. 
- We demonstrate the effectiveness of predicting chronological age over a dataset of 558 healthy individuals with MAE = 4.29, Correlation = 0.95 and R squared = 0.91.
- Despite that our dataset is smaller (N = 558) and the image resolution is lower (96 x 96 x 66) but our 3D CNN model still outperforms the result of James et. al. (2016) which uses 2001 subjects and the image resolution is up to 182 x 182 x 218.

## Dataset
- Our dataset is provided by NTU Hospital
- Total number of subjects is 558 and the subjects' age range from 16 to 88

### Preprocessing
- Diffusion tensor images (DTI) is reconstructed by python package, "dipy"
	- DTI (Diffusion Tensor Image): FA, MD, AD, RD, color FA
	- DKI (Diffusion Kurtosis Image): FA, MD, AD, RD, color FA
- Two denoising techiques are used to reduce the noise effect, **gaussian denoising** and **non-local means (nlmeans)**
- After our extensive experiments, the model trained by **FA and MD DTI images** provides the best results

<img src="../images/mri_data_example.png" style="width:100%;">

## 3D Convolutional Neural Network
- Deeper bottleneck architecture in a convolutional block ([ref](https://arxiv.org/abs/1512.03385))

- Instance normalization ([ref](https://arxiv.org/pdf/1607.08022.pdf))
**Instance normalization (IN)** adopts single sample statistics to normalize values by taking z-score normalization **sample-wise**, unlike batch normalization which calculates batch statistics of each dimension and independently normalizes dimension-wise. Through IN, the distribution of **this sample** is normalized to be a Gaussian distribution with mean = 0 and std = 1. And thus, IN better adapt across individual subjects by reducing the difference among them and more suitable in this case.

## Performance Comparisons
We compare 3 models with different sets of features:
1. our 3D CNN
2. 3D CNN proposed by [James H Cole et. al.](https://arxiv.org/abs/1607.08022)
3. 2D CNN proposed by [Tzu-Wei Huang et. al.](http://www.cs.nthu.edu.tw/~htchen/aemri/aemri.pdf)

<img src="../images/mri_performance.png" style="width:100%;">

## Conclusions
- The proposed 3D convolutional neural network, which applies on diffusion tensor images, can accurately predict ages of healthy subjects (MAE=4.29)
	- 3D convolution + Instance normalization + Deeper bottleneck architecture
	- Denoise by nlmeans and augment data by [-5,5] pixels shift and [-40,40] degrees of rotation
- The trained model can be used to detect early-stage neurodegeneration, and the severity of neurodegeneration can be quantified as the difference between chronological age and brain-predicted age
- Two current limitations: (1) limited number of subjects and (2) relatively low image resolution

## Presentation Slides
<iframe src="//www.slideshare.net/slideshow/embed_code/key/k3K3FWj3gj2cCN" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/ssuser950871/detecting-earlystage-neurodegeneration-using-3d-convnet" title="Detecting early-stage neurodegeneration using 3D ConvNet " target="_blank">Detecting early-stage neurodegeneration using 3D ConvNet </a> </strong> from <strong><a href="//www.slideshare.net/ssuser950871" target="_blank">Chun-Ming Chang</a></strong> </div>

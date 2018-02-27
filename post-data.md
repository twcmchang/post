---
layout: post
title:  "Common questions in data analysis"
date:   2018-02-13 00:50:00 +0800
categories: [post]
---

1. What's the problem in interest?
	- Supervised: regression, classification (binary, multi-class)
	- Unsupervised: clustering

2. What kinds of data we have?
	- the meaning of rows, cols
	- check the distribution and response with output
		- categorical: box plot (maybe with entropy)
		- numerical: scatter plot (with correlation)
	- extreme values
		- aggregate into a dummy value, e.g. "age < 12"
		- aggregate several small groups together, e.g. "ASIAN", "ASIAN/TAILAND" => "OTHER"
	- missing values
		- completely random
		- not random

3. Feature extraction from data
	- feature transformation, e.g. take log transformation to have linear relationship with output
	- define granularity
		- time series data => in day, week, month
		- spatial data => a unit of area
	- interaction among features, e.g. addition, subtraction, multiplication, division
		- total expense/number of transaction = avg. expense
	- demographic data

4. When apply PCA or other dimension reduction techniques?
	- reduce correlation between variables (because components in PCA are indpendent)
	- reduce model complexities and variable redundacy
	- extract informative variables

5. Pros and Cons of PCA:
	- (O) transform the original variables to the linear combination of these variables (which are independent)
	- (X) lose the explaining ability of the original variables

6. Other dimension reduction method:
	- Lasso: L1 norm on variables to make sparse coefficients
	- T-sne: QQ i dont know the details

7. Why we need clustering?
	- Find out hidden similarity/patterns in data points
	- Discovering possible partition of data points
	- Clustering highly depends on how we define 
	- Usually a very first step to analyze your data if there is no labels

8. Things we should know before clustering
	- the range of each variable (in most case, we should normalize each feature independently)
	- the definition of distance function


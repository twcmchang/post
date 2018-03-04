---
layout: post
title:  "Google Machine Learning Crash Course (1)"
date:   2018-03-04 00:50:00 +0800
categories: [post]
---

# Machine Learning Crash Course

## What is a machine learning model?
- *ML systems* learn how to combine input to produce useful predictions on never-before-seen data

- *Models* defines the relationship between input (feature) and output (label)
	- *Training* means creating or learning the model. That is, you show the model labeled example and enable the model to gradually learn the relationship between features and labels
	- *Inference* means applying the trained model to unlabeled examples

- In supervised learning, a machine learning algorithm builds a model by examining many examples and attempting to find a model that minimizes loss; this process is called *empirical risk minimization*

## Optimization: gradient descent

- Iterative approach: a Machine Learning model is trained by starting with an initial guess for the weights and bias and iteratively adjusting those guesses until learning the weights and bias with the lowest possible loss

- The popular *gradient descent* algorithm takes a step in the direction of the negative gradient in order to reduce loss as quickly as possible, until edging ever close to the minimum

- Gradient descent algorithms multiply the gradient by a scalar known as the *learning rate* (also sometimes called *step size*) to determine the next point
	- A Goldilocks learning rate for every regression problem

### On the calculation of gradients
- Gradient descent: using entire dataset per iteration would result in the inefficiency of gradient descent, due to many redundant samples 

- *Stochastic gradient descent* (SGD): estimate gradients by only a single example (a batch size of 1) per iteration; **SGD works but is very noisy**

- Mini-batch stochastic gradient descent (mini-batch SGD): a compromise between full-batch iteration and SGD. A mini-batch is typically between 10 and 1,000 examples, chosen at random. Mini-batch SGD reduces the amount of noise in SGD but is still more efficient than full-batch


[LinearRegressor exercise in TensorFlow](https://colab.research.google.com/notebooks/mlcc/first_steps_with_tensor_flow.ipynb?hl=en-US)

## Is There a Standard Heuristic for Model Tuning?
- This is a commonly asked question. The short answer is that the effects of different hyperparameters are data dependent. So there are no hard-and-fast rules; you'll need to test on your data.
- That said, here are a few rules of thumb that may help guide you:
	- Training error should steadily decrease, steeply at first, and should eventually plateau as training converges.
	- If the training has not converged, try running it for longer.
	- If the training error decreases too slowly, increasing the learning rate may help it decrease faster.
	- But sometimes the exact opposite may happen if the learning rate is too high.
	- If the training error varies wildly, try decreasing the learning rate.
	- Lower learning rate plus larger number of steps or larger batch size is often a good combination.
	- Very small batch sizes can also cause instability. First try larger values like 100 or 1000, and decrease until you see degradation.
- Again, never go strictly by these rules of thumb, because the effects are data dependent. Always experiment and verify.

## Generalization

### Occam's razor
The less complex an ML model, the more likely that a good empirical result is not just due to the peculiarities of the sample.

- We've formalized Occam's razor into the fields of statistical learning theory and computational learning theory, developing generalization bounds--a statistical description of a model's ability to generalize to new data based on factors such as:
	- the complexity of the model
	- the model's performance on training data

- Overfitting is caused by making a model more complex than necessary. The fundamental tension of machine learning is between fitting our data well, but also fitting the data as simply as possible

### Three basic assumptions guide generalization:

- We draw examples *independently and identically (i.i.d)* at random from the distribution. In other words, examples don't influence each other.
- The distribution is *stationary*; that is the distribution doesn't change within the data set.

- We draw examples from partitions from the same distribution.

In practice, we sometimes violate these assumptions. For example:

- Consider a model that chooses ads to display. The i.i.d. assumption would be violated if the model bases its choice of ads, in part, on what ads the user has previously seen.
- Consider a data set that contains retail sales information for a year. User's purchases change seasonally, which would violate stationarity.

When we know that any of the preceding three basic assumptions are violated, we must pay careful attention to metrics.

#### Question:
We looked at a process of using a test set and a training set to drive iterations of model development. On each iteration, we'd train on the training data and evaluate on the test data, using the evaluation results on test data to guide choices of and changes to various model hyperparameters like learning rate and features. Is there anything wrong with this approach?

#### Answer:
Doing many rounds of this procedure might cause us to implicitly fit to the peculiarities of our specific test set.


### Validation set
Use the validation set to evaluate results from the training set. Then, use the test set to double-check your evaluation after the model has *passed* the validation set. The following figure shows this new workflow:

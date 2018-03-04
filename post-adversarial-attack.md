---
layout: post
title:  "Adversarial attacks in deep learning"
date:   2018-03-01 00:50:00 +0800
categories: [post]
---

# Adversarial attack
Designing an input in a specific way to get the wrong result from the model is called an adversarial attack.
- machine learning models consist of a series of specific transformations
- most of these transformations turn out to be very sensitive to the slight changes in the input

## Type
- Non-targeted adversarial attack: make the classifier give an incorrect result (the most general type of attack) 
- Targeted adversarial attack: aims to receive a particular class for designed input


## Attempted defenses against adversarial examples
Tranditional techniques, such as weight decay and dropout, generall do not provide a practical defense against adversarial examples. So for, two methods have provided a significant defense.

- Adversarial training: generate a lot of adversarial examples and explicitly train the model not to be fooled by them

- Defensive distillation: is a strategy where we train the model to output probabilities of different classes, rather than hard decisions about which class to output

## Failed defense:
- The attacker can train their own model, a smooth model that has a gradient, make adversarial examples for their model, and then deploy those adversarial examples against our non-smooth model
- Very often, our model will misclassify these examples too => Transferable adversarial examples
- Experiment reveals that hiding the gradient didn’t get us anywhere


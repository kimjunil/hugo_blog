---
title: "선형회귀분석 Linear Regression"
date: 2021-12-22T06:27:02+09:00
tags:
- Machine Learning
- Deep Learning
draft: true
math: true
---

> 모두의 연구소 Aiffel 과정에서 공부한 내용을 정리한 글입니다.

# 선형회귀란?
선형회귀는 종속변수 Y와 한 개 이상의 독립변수 X와의 선형 상관관계를 모델링하는 회귀분석 기법이다.  
머신러닝에서는 독립변수=Feature, 종속변수=Target Value로 표현할 수 있다.

# 선형회귀 모델의 표기법
머신러닝에서 선형회기 모델은 아래와 같이 표기한다  
$$
H=Wx+b
$$
H: 가정(Hypothesis)  
W:가중치(Weight)  
b:편향(bias)
머신러닝에서는 주어진 데이터를 이용하여 W와 b를 구한다. 대부분의 경우 W와 b는 스칼라 값이 아닌 행렬(Matrix) 형태를 띄고 이 파라미터의 갯수가 많을수록 모델의 크기가 커진다.

# 경사하강법 (Gradient Decent)



This post is from Coursera's Machine Learning Course (by Andrew Ng) from Stanford Univ.

# What is Machine Learning?


ML definition:

1. Arthur Samuel:(older def)Field of study that gives computers the ability to learn
  without being explicitly programmed

2. Tom Mitchell(Modern Def)Well-posed Learning problem:
  computer program is said to learn from experience E with respect to some task T
	and some performance measure P,
	if its performance on T , as measured by P,
	improves with experience E
  
  Let's see this in Playing checkers.
  
  E = the experience of playing many games of checkers  
  T = the task of playing checkers  
  P = the probability that the program will win the next game  
  
  so, computer program is learn from E to do T  
  and the program improves with performance measur P
	
# Machine learning algorithms:

there are two types of machine learning algorithms.
-> supervised learning
-> unsupervised learning

Others : Reinforcement learning, recommender systems


## 1. Supervised Learning

#### "right answers"given
we gave a data set of houses  
and told it what is the right price.  

the task: "just produce more of these right answers"  
(x라는 값이 주어지고, y라는 값을 내놓아야 하는게 supervised learning)  


### 1-1) Regression(Linear regression)

<img width="456" alt="housing2" src="https://user-images.githubusercontent.com/41497195/55059259-d84eff00-50b1-11e9-9efa-035d1a7f23d0.PNG">

x라는 값에 대해서 y라는 값을 어떤 연속적인 형태로 나타낼 수 있는 것을 Linear regression이라고 표현합니다. PRE

##### predict results within a continuous output.
##### so, we should map imput variables to some sort of continuous function.

### 1-2) Classification

<img width="588" alt="tumor" src="https://user-images.githubusercontent.com/41497195/55059268-dc7b1c80-50b1-11e9-8e60-5eb298ba6d09.PNG">
<img width="328" alt="classification2" src="https://user-images.githubusercontent.com/41497195/55059273-de44e000-50b1-11e9-9669-7603c8b7b8b9.PNG">

we should know that the tumor is malignant or not.
So it is the classification.
(there can be multiple types)

##### trying to predict results in a discrete output.
##### map input variables into discrete categories.

## 2.  Unsupervised Learning

just have data with no labels..anything

-> find something in the data
그냥 던져주고 자..cluster해봐
- allows us to approach problems with little or no idea what our results should look like.
-  we can derive structures from data where we don't know the effect of the variables.

- no feedback based on the prediction results.


### 2-1 ) Clustering
google news
### 2-1) 
cocktail party
(find structure in a chaotic environment)


# Model and cost Function

Machine Learning-Andrew Ng(2)


This post is from Coursera's Machine Learning Course (by Andrew Ng) from Stanford Univ.

## Model Representation

(i): index

x(i): input variables/features  
y(i): output variables/target - what we are trying to predict.  
(x(i),y(i)):training example(s) which consist training set.

![training](https://user-images.githubusercontent.com/41497195/55250216-0474a680-5291-11e9-8f29-7c6d4ef10dd4.png)

h:hypothesis

our goal is:  
training set is given -> 
learn a function h:X->Y so that h(x) is a good predictor for the corresponding value of y

Traing set을 Learning algorithm을 통해 train하여,
x를 통해 h(x)의 원하는 결괏값이 나오는 것이 목적입니다.

## Cost Function

모델을 설정하는 데 중요한 것은 무엇일까요?  
그 중에 하나는 parameter들을 잘 설정하는 것이라고 할 수 있습니다.

Hypothesis가 h(x) = a + bx 라면

a,b는 parameter들입니다. 이 parameter를 잘 설정해서 h(x)가 training examples(x,y)의 y에 가깝도록 하는 것이 목적입니다.

그러면 h(x)의 accuracy를 어떻게 measure하느냐?  

#### Cost Function을 통해 hypothesis function의 accuracy를 측정할 수 있습니다.  

가장 유명한 cost function중의 하나는 "Squared error function", or "Mean Squared error function"입니다.

<img width="250" alt="mse" src="https://user-images.githubusercontent.com/41497195/55253329-6684da00-5298-11e9-857b-c7236b002044.PNG">


이 function 은 h(x)와 y사이의 avg difference를 측정합니다.
여기서 두 개의 세타 값들이 minimize되어야 합니다.  
즉 difference가 최소화 되어야 하는 것이죠.

cost function을 통해 hypothesis function의 error를 최소화 하여 가장 적절한 모델을 찾는 것이 과제입니다.



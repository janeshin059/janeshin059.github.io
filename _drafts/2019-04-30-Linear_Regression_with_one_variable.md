# Linear regression with one variable - cost function intuition 1

지난 시간에는 cost function에 대해 알아 보았습니다.  
housing price의 traning set이  

x(size in feet) : 2104, 1323 , 555, 283  
y(price): 460, 232, 315, 178 ..  
이렇게 있다고 하면   
Hypothesis 는 h<sub/>θ<sub> = θ<sub/>0<sub> + θ<sub/>1<sub>x   
이러한 함수라고 할 수 있습니다.
  여기서 θ<sub/>0<sub> + θ<sub/>1<sub> 는  
  , h<sub/>θ<sub> 이 우리의 training examples (x,y)에서의 y와 최대한 같아지는 것을 목적으로 결정되어야 합니다.  
  
  그래서 이를 위해 cost function을 사용하는데 , 이는 error가 가장 적도록 만들어 줍니다. (가장 fit되도록)  
  가장 유명한 cost function중 하나는  다음과 같은 Squared Error Function입니다.
  
  
  우리의 goal은 J( θ<sub/>0<sub> , θ<sub/>1<sub> ) 를 최소화하는 것입니다.  
  
  ![CodeCogsEqn](https://user-images.githubusercontent.com/41497195/57367717-7ca18680-71c4-11e9-87c2-d9c313c02aa7.gif)  

# Linear regression with one variable - gradient descent

Have some function J(θ<sub/>0<sub> , θ<sub/>1<sub>)  
  want to minimize J(θ<sub/>0<sub> , θ<sub/>1<sub>)  
   
  이를 위해서는  
             - 어떠한 θ<sub/>0<sub> , θ<sub/>1<sub> 들을 갖고 시작한다( θ<sub/>0<sub> = 0 , θ<sub/>1<sub> = 0 가정 등)  
             - minimum 에 도달하기 위해 θ<sub/>0<sub> , θ<sub/>1<sub> 를 계속 바꿉니다.   
  이를 Gradient descent algorithm이라고  합니다. (cost function J가 최소에 도달하도록 계속 내려감) 
  
  repeat until convergence:  
  ![CodeCogsEqn (1)](https://user-images.githubusercontent.com/41497195/57368615-87f5b180-71c6-11e9-80d7-0f69df5593b6.gif)

( simultaneoulsy update j = 0 and j = 1)    
여기서 α를 learning rate라고 합니다 . 얼마나 step을 take하는지 결정하는 것이죠.  

α 가 너무 작으면, gradient descent가 slow하게 됩니다.  
α가 너무 크면 , gradient descent가 minimum을 overshoot할 수 있습니다. 수렴하지 않고 발산할 위험성이 커집니다.   
![gd](https://user-images.githubusercontent.com/41497195/57368824-12d6ac00-71c7-11e9-8f91-0ea82d9bc857.PNG)  

즉 적절한 learning rate를 선택하는 것이 중요합니다.  

# Linear regression with one variable - gradient descent for linear regression

앞에서 봤던 gradient descent와 linear regression을 연관시킬 수 있습니다.  

![gd2](https://user-images.githubusercontent.com/41497195/57369000-8082d800-71c7-11e9-9a3f-b6d75abffd34.PNG)  
h<sub/>0<sub>(x)를 대입하면 식을 계산할 수 있습니다.  
  
Batch Gradient descent: gradient descent의 각 step이 모든 traning example들을 사용하는 방법입니다.
위의 Σ부분이라고 생각하시면 됩니다.  





  
  
  
              

# 이진분류
Linear Regression을 통해 얻게되는 모델의 예측값은 연속적인 숫자값이 나옵니다.<br>
만약 연속적인 숫자를 예측하는 것이 아니라 분류를 예측하려면 어떻게 해야할까요? 기존의 linear regression이 아닌 다른 방식을 사용하여야 합니다.<br>
예를 들어 시험을 쳤을 경우 시험 결과로 Fail과 Pass로 분류될 수 있습니다.<br>
결과가 Fail또는 Pass가 나오기 때문에 이진 분류(binary classification)라고 합니다.<br>
이진 분류를 구현해보겠습니다.
```python
import numpy as np
from sklearn import linear_model
import mglearn
import matplotlib.pyplot as plt

# 데이터 셋을 가지고 옵니다.
(x, y) = mglearn.datasets.make_forge()

# print(type(x)) # <class 'numpy.ndarray'>
# print(x.shape) # (26, 2)
# print(x) # [[ 9.96346605  4.59676542], [11.0329545  -0.16816717], ... ]

# print(type(y)) # <class 'numpy.ndarray'>
# print(y.shape) # (26,)
# print(y) # [1 0 1 0 0 1 1 0 1 1 1 1 0 0 1 1 1 0 0 1 0 0 0 0 1 0]

# 1열을 x축으로, 2열을 y축으로 좌표를 찍겠습니다.
mglearn.discrete_scatter(x[:,0], x[:,1], y)

# 모델을 만들고 학습합니다.
model = linear_model.LinearRegression()
model.fit(x[:,0].reshape(-1,1), x[:,1].reshape(-1,1))

# 1차 직선을 그립니다.
plt.plot(x[:,0], x[:,0] * model.coef_.ravel() + model.intercept_, color='r')

plt.show()
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/f12f223c-6202-44a2-a616-475bae23a842)

이것을 구현하기 위해서는 linear regression을 변형하여 **logistic regression**으로 구현할 수 있습니다.<br>
logistic regression과 linear regression은 둘다 직선이 되는데 linear regression으로는 불가능할까요?<br>
불가능한 이유는 linear regression은 linear하게 값이 증가하는 모델인데 반해 이진분류는 True 또는 False로 표현되기 때문입니다.<br>
이진분류를 Linear Regression으로 구현해보겠습니다.
```python
import numpy as np
from sklearn import linear_model
import matplotlib.pyplot as plt

x_data = np.array([1, 2, 5 ,8 ,10, 30]) # 공부시간
t_data = np.array([0, 0, 0, 1, 1, 1]) # 합격여부(0: Fail, 1:Pass)

# 모델을 만들고 학습시킵니다.
model = linear_model.LinearRegression()
model.fit(x_data.reshape(-1,1), t_data.reshape(-1,1))
# 예측합니다.
print(model.predict([[7]])) # [[0.41831972]] => 불합격인건가요..

# 그래프를 그려봅니다.
plt.scatter(x_data, t_data)
plt.plot(x_data, x_data * model.coef_.ravel() + model.intercept_, color='r')
plt.show()
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/82f7b731-ad96-478b-8764-30fabe72ad37)
이진분류는 확률값이 나옵니다. 0.5미만이면 False, 0.5 이상이면 True 이런식으로 판단하기 때문입니다.<br>
하지만, 위의 그래프의 Linear Regression으로 모델을 만들면 0~1사이가 아닌 1.2의 확률값이 예측이 어려워집니다.<br>
이를 해결하는 방법은 S모양의 sigmoid 함수입니다.<br>
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/16a3ecb0-1409-4e95-82cd-47eaa3f6c454)

sigmoid 함수를 통해 구현된 모델이 생성되면 loss함수를 사용하여 오차를 구해야합니다.
이 또한 linear regression에서 사용했던 mse를 사용할 수는 없습니다. 
왜냐하면 logistic regression model은 꼬불꼬불한 그래프가 그려지기 때문입니다.
이를 해결하기 위해서는 MSE대신 Cross Entropy를 사용할 수 있습니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/6ce918a0-84db-4a41-b8d6-8746cdc052e2)
이것은 기존의 linear regression에서 activation 과정을 추가하면 됩니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/05ed02d9-8051-4e74-b64c-6936b770bdab)
```python
import numpy as np
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Flatten, Dense
from tensorflow.keras.optimizers import SGD
from sklearn import linear_model

x_data = np.arange(2,21,2).reshape(-1,1)
t_data = np.array([0,0,0,0,0,0,1,1,1,1]).reshape(-1,1)

# sklearn구현

sklearn_model = linear_model.LogisticRegression()
sklearn_model.fit(x_data, t_data.ravel())

# 13시간 공부하면 합격인가요 불합격인가요?
print(sklearn_model.predict([[13]]))  # => 0 불합격으로 판별해요!
print(sklearn_model.predict_proba([[13]]))  # [[0.50009391 0.49990609]]

# Tensorflow keras 구현
keras_model = Sequential()
keras_model.add(Flatten(input_shape=(1,)))
keras_model.add(Dense(units=1, activation='sigmoid'))
keras_model.compile(optimizer=SGD(learning_rate=1e-3), loss='binary_crossentropy')
keras_model.fit(x_data, t_data, epochs=500, verbose=1)
print(keras_model.predict([[13]])) # [[0.6098874]]
```
이제 저희는 모델을 만들어보았으니 평가(Evaluation)을 해보아야 합니다.
Linear Regression에서는 평가를 할때 skit-learn을 사용했었는데요. Logistic Regression에서는 다른 방법을 사용해야 합니다.
Logistic Regression 모델을 평가하기 위해서는 **평가 기준**이 필요하고 이 기준은 여러개가 있습니다.
Linear Regression과 같이 Training Data Set을 이용해서 평가를 진행하면 안됩니다.

데이터는 아래와 같이 Original Data Set을 Training Data, Validation Data, Test Data로 나눌 수 있습니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/f00866f8-a498-4119-9f6e-40cbc8ffe4d7)

# Evaluation 평가
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/c2f8bccf-1db6-43ea-ac01-41e4dcf69266)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9c3dc44f-4b8c-429b-b210-256c7e6317bb)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9853e683-a3f8-4c91-ba16-2c74fa903f7f)

# 추가로 알아두어야할 사항
1. Learning rate
   - learning rate가 필요이상으로 크게 설정되면 over shoooting 발생
   - learning rate가 필요이상으로 작게 설정되면 local minima 발생
2. 과적합
   - 과대적합(overfitting): training data가 너무 모델에 잘 들어맞는 경우
     - overfitting은 언제 발생하나요? **epoch이 너무 많거나 학습 데이터가 적을때**
   - 과소적합: model이 충분히 학습되지 않은 경우(epoch수가 부족할 경우)
3. OverSampling
   - 데이터의 불균형이 발생할 수 있습니다.(domain의 bias)

Overfitting을 피할 수 있는 방법은 무엇인가요?
1. Training Data가 많으면 overfitting이 줄어듭니다.
2. Feature의 개수를 가능한 줄입니다. → Feature이 많아지면 모델이 복잡해집니다.
3. Deep Learning → Dropout이라는 기법
4. Weight값이 크면 curve를 그리게 됩니다.
   - 계산되는 weight값을 인위적으로 줄입니다. L1, L2라는 규제공식이 있습니다.
5. 적절한 수의 epoch을 설정합니다. 

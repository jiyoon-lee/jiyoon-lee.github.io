# AI
AI(Aritificial Itelligence)는 **사람이 가지고 있는 사고능력을 컴퓨터 프로그램으로 표현**한 것입니다.<br>
AI는 Strong AI(강AI) Weak AI(약AI)로 나눌 수 있습니다.<br>
Strong AI는 사람과 구별이 되지 않는 수준의 AI로 최종 목표이죠.<br>
Weak AI는 특정 분야에 있어 사감과 거의 동등한 능력을 가지는 AI입니다. 예를 들면 자율주행과 알파고가 있습니다.

AI를 만들기 위한 전력으로는 인간과 같이 학습하는 방법을 사용합니다.<br>
인간의 학습을 통해 예측을 합니다. 그래서 기존에 우리가 해왔던 자바, 자바스크립트와 같은 프로그래밍과는 많이 다릅니다.<br>
기존의 프로그래밍은 Rule-based Programming이었습니다. 데이터를 입력하면 소스코드를 따라 진행되어 결과가 도출되죠.<br>
하지만 AI Programming은 대량의 데이터와 해답으로 학습을 시키고 규칙성을 찾아내어 Model(=>수학식)을 도출합니다.<br>
모델을 통해 새로운 것을 예측할 수 있습니다.<br>
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/658ad75c-9e02-4ff2-9aad-f438859cd3c9)

# Machine Learning
이런 AI를 구현하기 위해 즉 규칙성을 찾기위해서 Machine Learning기법을 사용합니다.<br>
Machine Learning 기법에는 다양한 알고리즘이 있는데요.

1. Regression(회귀)
2. SUM(Support Vector Machine)
3. Decision Tree(Random Forest)
4. Native Bayes
5. KNN(K-Nearest Neighbors)
6. ANN(Artificial Neural Network) => Deep Learning
7. K-MEANS, DBSCAN
8. 강화학습

위와 같이 다양하게 존재하는데요. 이중 2~5번은 라이브러리화가 되어있어 간편하게 만들 수 있습니다.<br>
저희는 Regression과 ANN을 학습해보겠습니다.

Machine Learning 기법은 정형 데이터에 적합하고 Deep Learning 기법은 비정형 데이터에 적합합니다.

# Machine Learning 분류
- 지도학습(supervised Learning)
  - 모델을 만들 때 데이터+해답을 입력으로 같이 들어가는 경우입니다.
- 비지도 학습(Unsupervised Learning)
  - 모델을 만들 때 데이터만 입력되어 모델이 학습되는 경우로 clustering이라고 합니다.
- 초지도 학습(semisupervised Learning)
  - 지도 학습과 비지도 학습을 섞은 것입니다.
- 강화 학습(Reinforcement LEarning)
  - 현재 상태에서 조금 더 나은 다음 상태를 찾아내는 기법입니다.
 
# Regression vs Classification
저희는 Machine Learning의 분류 중 지도 학습에 대해 학습하겠습니다.<br>
지도 학습에는 Regression과 Classfication이 있습니다.

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/d9a5dfc9-7444-4017-9b1b-f785302bcaa3)

# 새로운 용어
- Training Data Set
- 독립변수, Feature
- 종속변수, Target, Label

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9aac53d0-685a-4562-9c10-6920e389a4c1)


---
layout: single
title: "타이타닉으로 Logistic Regression 실습"
categories: coding
tag: [python, blog]
toc: true
author_profile: false
sidebar:
  nav: "counts"
---

1. 데이터셋 불러오기
2. 사용하지 않는 컬럼부터 제거
3. 문자값을 전부 숫자값으로 변경

<figure style="width: 800px">
  <img src="" alt="">
</figure>

### 1. 데이터셋 불러오기

- kaggle을 사용하겠습니다.(링크: https://www.kaggle.com/)
<figure style="width: 800px">
  <img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cd147bc9-09f3-40bc-ba6c-a4174f7b9ca9" alt="">
</figure>

- 검색창에 'titanic'을 입력합니다.
<figure style="width: 800px">
  <img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e682f832-8c95-4746-8369-1609c921cc7c" alt="">
</figure>

- 데이터를 다운받습니다.
<figure style="width: 800px">
  <img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/f31af99b-19fe-4728-a07c-092b4acb55d2" alt="">
</figure>

- Google 드라이브로 돌아옵니다.
- Google 드라이브에 다운받은 titanic csv파일을 저장합니다.
- 새로운 Colab을 생성합니다.
- 명령어를 통해 데이터셋을 불러옵니다.

  ```python
    import numpy as np
    import pandas as pd
    titanic = pd.read_csv('저장한 csv파일 경로/train.csv')
  ```

  데이터가 제대로 들어왔는지 확인합니다.

  <figure style="width: 800px">
    <img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e1e728c2-32e3-4657-804b-6f6051099fed" alt="">
  </figure>

### 2. 사용하지 않는 컬럼을 제거

컬럼 즉 독릭변수(feature)이 많아지면 모델이 복잡해지고 overfitting이 발생할 우려가 있습니다.

각 컬럼을 확인해보겠습니다.

<figure style="width: 500px">
  <img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/8875b91d-85cb-4f56-92ec-efcb947afeb2" alt="">
</figure>

'PassengerId', 'Name', 'Ticket', 'Fare', 'Cabin'은 종속변수인 생존여부에 영향을 미치지않는다고 간주하여 제거하도록 하겠습니다.

```python
titanic.drop(['PassengerId', 'Name', 'Ticket', 'Fare', 'Cabin'], axis=1, inplace=True)
```

잘 제거되었는지 확인합니다.

<figure style="width: 500px">
  <img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/a83dbf14-7bac-4b9b-9b94-79412b74f410" alt="">
</figure>

### 3. 문자값을 전부 숫자값으로 변경

결과적으로 하나의 확률값으로 나와야하기 때문에 데이터셋의 모든 문자를 숫자로 변경해주어야합니다.

먼저 Sex(성별)에서 Male을 0으로 Female을 1로 변경하겠습니다.

Male이 1이고 Female이 0이어도 상관없습니다.

```python
gender_dict = {'male': 0, 'female': 1}

titanic['Sex'] = titanic['Sex'].map(gender_dict)
```

잘 제거되었는지 확인합니다.

<figure style="width: 500px">
  <img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/f80585d5-331b-4983-ae29-69730c8daebb" alt="">
</figure>


### 결측치 제거
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/01c137a8-d766-41c7-99c8-995bda563f30)

- Embarked 결측치 채우기
Embarked 컬럼은 결측치가 2개이므로 'Q'로 대체해서 사용하겠습니다.
```
titanic['Embarked'] = titanic['Embarked'].fillna('Q')
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/c1373725-2469-4b85-81c8-3d41dad32f42)

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/a5f9f77f-68f4-4686-a01e-aa038e18adc3)

- Age으 결측치 채우기
  ```python
  titanic['Age'] = titanic['Age'].fillna(titanic['Age'].mean())
  ```

나이의 range가 너무 크다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/a54e840a-93ab-4145-bb21-ba0c89e2eb39)
구간(Binning) 처리를 합니다.
- 8세 미만 = 0
- 8세 이상 20살 미만 = 1
- 20세 이상 65세 미만 = 2
- 65세 이상 = 3
  ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/36b6dbb3-76fb-4aad-9f7f-5acc44c78d16)

### Training data set 준비
```python
x_data = titanic.drop('Survived', axis=1, inplace=False).values
t_data = titanic['Survived'].values.reshape(-1, 1)
```
training data와 test data로 분리해야 합니다.
training data는 다시 training과 validation용으로 나누어줍니다.
validation 데이터를 나눠서 중간평가 하는 것은 Keras가 대신 해줍니다.
따라서 특별한 경우가 아니라면 validation data는 Keras를 이용해서 처리하면 됩니다.



1. 데이터셋 불러오기
2. 사용하지 않는 컬럼부터 제거
3. 문자값을 전부 숫자값으로 변경

<img width='800px' src='' alt='' />

### 1. 데이터셋 불러오기
- kaggle을 사용하겠습니다.(링크: https://www.kaggle.com/)

  <img src='https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cd147bc9-09f3-40bc-ba6c-a4174f7b9ca9' alt='' width='800px' />

- 검색창에 'titanic'을 입력합니다.

  <img width='800px' src='https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e682f832-8c95-4746-8369-1609c921cc7c' alt='' />

- 데이터를 다운받습니다.

  <img width='800px' src='https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/f31af99b-19fe-4728-a07c-092b4acb55d2' alt='' />

- Google 드라이브로 돌아옵니다.
- Google 드라이브에 다운받은 titanic csv파일을 저장합니다.
- 새로운 Colab을 생성합니다.
- 명령어를 통해 데이터셋을 불러옵니다.
  ```
    import numpy as np
    import pandas as pd
    titanic = pd.read_csv('저장한 csv파일 경로/train.csv')
  ```
  데이터가 제대로 들어왔는지 확인합니다.
  
  <img width='800px' src='https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e1e728c2-32e3-4657-804b-6f6051099fed' alt='' />

### 2. 사용하지 않는 컬럼을 제거
컬럼 즉 독릭변수(feature)이 많아지면 모델이 복잡해지고 overfitting이 발생할 우려가 있습니다.

각 컬럼을 확인해보겠습니다.

<img width='500px' src='https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/8875b91d-85cb-4f56-92ec-efcb947afeb2' alt='' />

'PassengerId', 'Name', 'Ticket', 'Fare', 'Cabin'은 종속변수인 생존여부에 영향을 미치지않는다고 간주하여 제거하도록 하겠습니다.
```
titanic.drop(['PassengerId', 'Name', 'Ticket', 'Fare', 'Cabin'], axis=1, inplace=True)
```
잘 제거되었는지 확인합니다.

<img width='500px' src='https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/a83dbf14-7bac-4b9b-9b94-79412b74f410' alt='' />

### 3. 문자값을 전부 숫자값으로 변경
결과적으로 하나의 확률값으로 나와야하기 때문에 데이터셋의 모든 문자를 숫자로 변경해주어야합니다.

먼저 Sex(성별)에서 Male을 0으로 Female을 1로 변경하겠습니다.

Male이 1이고 Female이 0이어도 상관없습니다.

```
gender_dict = {'male': 0, 'female': 1}

titanic['Sex'] = titanic['Sex'].map(gender_dict)
```
잘 제거되었는지 확인합니다.
<img width='500px' src='https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/ad6428dc-baae-46d3-84ac-928245f1cd4b' alt='' />

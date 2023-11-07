---
layout: single
title: "Multinomial Classification - 다중 분류"
categories: AI
tag: [AI, 빅데이터]
toc: true
author_profile: false
# sidebar:
#   nav: "docs"
toc: true
---

다중분류(multinomial classification)는 이진분류(logistic regression)를 여러 개를 모아서 model로 구현한 것입니다.

## 1. 이미지 특징 알아보기

다중분류를 학습하기위한 예시로 이번에는 이미지를 사용해보겠습니다.<br>
먼저 이미지의 특징에 대해서 학습해보겠습니다.<br>
이미지는 기본적으로 3차원 데이터입니다.<br>
`img.shape`로 행렬 차원을 확인해보겠습니다.<br>
3차원(높이, 너비, 채널)으로 이루어져있습니다.<br>

```python
print(pixel.shape) # (426, 640, 3) = (높이, 너비, 채널(RGB))
```

이미지를 좌표계에서 표현하면 x축은 너비, y축은 높이, 각 셀은 채널로 RGB가 들어갑니다.<br>
픽셀안에는 세개의 칸으로 나누어져있는데요. RED, GREEN, BLUE를 가리킵니다.<br>
이것을 조합하여 컬러를 만들 수 있습니다. 그렇다면 흑백은 어떻게 표현할까요.<br>
RED, GREEN, BLUE의 평균을 구하면 흑백이 됩니다.

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/48ad29ce-b6cf-4207-a45d-7e2003b442e2" style="width: 600px" />

## 2. 이미지 불러오기

이제는 Google Colab에서 이미지를 가져와서 화면에 출력해보겠습니다.<br>
바로 `PIL`을 사용할 수 있습니다.<br>

```python
import numpy as np # 이미지 데이터를 우리가 사용할 수 있는 행렬로 변경하기 위해 사용합니다.
from PIL import Image # 이미지를 불러오기 위해 사용합니다.
import matplotlib.pyplot as plt # 좌표계를 그리기위해 사용합니다.

img = Image.open('/content/justice.jpg')

plt.imshow(img)
plt.show()
```

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/32689212-4d55-430f-80af-2f362df80c28)

이미지는 `<matplotlib.image.AxesImage at 0x7ca1a03b32b0>`의 타입을 가집니다.<br>
우리가 사용할 수 있는 nparray로 변경해보겠습니다.<br>
그러면 방금 배운대로 (높이, 너비, 채널)으로 표시됩니다.

```python
print(img) # <matplotlib.image.AxesImage at 0x7ca1a03b32b0>
pixel = np.array(img)
print(pixel.shape) # (426, 640, 3) = (높이, 너비, 채널(RGB))
```

## 3. 이미지 잘라내기

```python
crop_img = img.crop((30,100,150,330)) # 좌, 상, 우, 하 순서
plt.imshow(crop_img)
plt.show()
```

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e1ff2e09-20cb-40ac-a60a-059b17b94564" style="width: 525px" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/2a4aa1db-cd9b-4ddf-9c2f-7c378ea40908" style="width: 225px;" />

## 4.이미지 크기 변경

```python
# print(img.size) # (640, 426)
resize_img = img.resize((int(img.size[0]/2), int(img.size[1]/2))) # width, height 순서
plt.imshow(resize_img)
plt.show()
```

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/bfe77c83-de46-4dc6-9859-0768efd8c341)

## 5. 이미지 회전

```python
rotate_img = img.rotate(90) # 시계방향
plt.imshow(rotate_img)
plt.show()
```

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/0e3bb29d-d70e-4890-bd86-65a090f64182)

## 6. 컬러 이미지를 흑백 이미지로 변경하기

```python
# 필요한 라이브러리를 불러옵니다.
import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

# Image를 불러옵니다.
color_img = Image.open('/content/fruits.jpg')

# Image를 ndarray로 변환합니다.
color_pixel = np.array(color_img)

gray_pixel = color_pixel.copy()
# print(color_pixel.shape) # (426, 640, 3)

for y in range(color_pixel.shape[0]): # 높이 426
  for x in range(color_pixel.shape[1]): # 너비 640
    gray_pixel[y,x] = int(np.mean(gray_pixel[y,x])) # 각 채널(RGB)의 평균(scalar)을 gray_pixel에 추가합니다.

gray_2d_pixel = gray_pixel[:,:,0]
plt.imshow(gray_2d_pixel)
plt.show()
```

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/1463ac24-f6e8-438a-a427-a945c864542c)

색이 이상합니다. 아래와 같이 `cmap='gray'`를 추가하면 흑백으로 바뀝니다.

```python
...
plt.imshow(gray_2d_pixel, cmap='gray')
...
```

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/b0579dce-c314-4746-b1f4-b3b1a2ad896a)

## 7. DNN(Deep Neural Network)

DNN은 입력층(Input Layer)과 출력층(Outer Layer) 사이에 여러 개의 은닉층(Hidden Layer)들로 이뤄진 인공신경망입니다.

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9702ca71-c91c-4eb7-937d-e668757b7bf2)
<img src="" style="width: 600px" />

### 7-1. DNN 실습

#### [1] Fashion MNIST

실제 데이터를 통해 실습해보겠습니다.<br>
사용할 데이터는 kaggle의 'Fashion MNIST'를 사용하겠습니다.<br>

> https://www.kaggle.com/datasets/zalando-research/fashionmnist

```python
# 필요한 라이브러리 불러오기
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Flatten, Dense
from tensorflow.keras.optimizers import Adam

# csv파일로 부터 데이터를 불러옵니다.
df = pd.read_csv('[경로]/fashion-mnist_train.csv')

# 데이터 전처리
# 1. 결측값 제거(결측치가 존재하지 않습니다.)
# 2. 이상치 제거(이상치가 존재하지 않습니다.)
# 3. 정규화 처리
scaler = MinMaxScaler()
scaler.fit(df.drop('label', axis=1, inplace=False).values)
x_data_norm = scaler.transform(df.drop('label', axis=1, inplace=False).values)
t_data = df['label'].values.reshape(-1,1)

# training data와 test data로 분할
x_data_norm_train, x_data_norm_test, t_data_train, t_data_test = \
train_test_split(x_data_norm, t_data, test_size=0.3)

# 모델 생성
model = Sequential()
# 입력층(Input Layer) 추가
model.add(Flatten(input_shape=(784,)))

# 은닉층(hidden Layer) 추가
model.add(Dense(units=64, activation='relu'))
model.add(Dense(units=128, activation='relu'))
model.add(Dense(units=256, activation='relu'))

# 출력층(Output Layer) 추가
model.add(Dense(units=10, activation='softmax'))

# 모델 학습
model.compile(optimizer=Adam(learning_rate=1e-4),
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

# 모델 학습
model.fit(x_data_norm_train,
          t_data_train,
          epochs=100,
          verbose=1,
          validation_split=0.3) # 전체 데이터의 30%가 검증 데이터로 사용

# 평가
print(model.evaluate(x_data_norm_test, t_data_test)) # [0.5319429039955139, 0.8774999976158142]
```

정확도는 0.8774999976158142이 됩니다. 정확도가 굉장히 낮다는 것을 알 수 있습니다.

#### [2] XOR

이번에는 단순한 데이터로 실습을 진행해보겠습니다.

```python
import numpy as np
import pandas as pd
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Flatten, Dense
from tensorflow.keras.optimizers import Adam

x_data = np.array([[0,0], [0,1], [1,0], [1,1]])
t_data = np.array([0, 1, 1, 0]).reshape(-1,1)

model = Sequential()

# input layer
model.add(Flatten(input_shape=(2,)))

# hidden layer
model.add(Dense(units=256, activation='relu'))
model.add(Dense(units=64, activation='relu'))
model.add(Dense(units=128, activation='relu'))

# outer layer
model.add(Dense(units=1, activation='sigmoid'))
model.compile(optimizer=Adam(learning_rate=1e-2), loss='binary_crossentropy', metrics=['accuracy'])
model.fit(x_data, t_data, epochs=1000, verbose=1)
```

```python
model.summary()
```

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9b108b02-8f0d-401d-8d4f-e1b37b1eb4b1)

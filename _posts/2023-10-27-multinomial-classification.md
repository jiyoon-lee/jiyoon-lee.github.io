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

multinomial classification 다중 분류
다중분류(multinomial classification)은 이진분류(logistic regression)를 여러 개를 모아서 model로 구현한 것입니다.<br>

이번에는 이미지를 다루어 보겠습니다.<br>
이미지는 기본적으로 3차원 데이터입니다. (높이, 너비, 채널)로 이루어져있습니다.<br>
이미지를 좌표계에서 표현하면 x축은 너비, y축은 높이, 각 셀은 RGB가 들어가는 채널이 됩니다.<br>
픽셀안에는 세개의 칸으로 나누어져있는데요. RED, GREEN, BLUE를 가리킵니다.<br>
이것을 조합하여 컬러르 만들 수 있습니다. 그렇다면 흑백은 어떻게 표현할까요.<br>
RED, GREEN, BLUE의 평균을 구하면 흑백이 됩니다.

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/48ad29ce-b6cf-4207-a45d-7e2003b442e2" style="width: 600px" />

이번에는 Google Colab에서 이미지를 가져와서 화면에 출력해보겠습니다.

```python
import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

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

## 2. 이미지 잘라내기

```python
crop_img = img.crop((30,100,150,330))
plt.imshow(crop_img)
plt.show()
```

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e1ff2e09-20cb-40ac-a60a-059b17b94564" style="width: 500px" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/2a4aa1db-cd9b-4ddf-9c2f-7c378ea40908" style="width: 200px;" />

## 3.이미지 크기 변경

```python
# print(img.size) # (640, 426)
resize_img = img.resize((int(img.size[0]/2), int(img.size[1]/2)))
plt.imshow(resize_img)
plt.show()
```

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/bfe77c83-de46-4dc6-9859-0768efd8c341" style="width: 600px" />

## 4. 이미지 회전

```python
rotate_img = img.rotate(90)
plt.imshow(rotate_img)
plt.show()
```

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/0e3bb29d-d70e-4890-bd86-65a090f64182" style="width: 600px" />

## 5. 컬러 이미지를 흑백 이미지로 변경하기

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
# print(type(color_pixel)) # <class 'numpy.ndarray'>

for y in range(color_pixel.shape[0]):
  for x in range(color_pixel.shape[1]):
    gray_pixel[y,x] = int(np.mean(gray_pixel[y,x])) # scalar

gray_2d_pixel = gray_pixel[:,:,0]
plt.imshow(gray_2d_pixel)
plt.show()
```

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/1463ac24-f6e8-438a-a427-a945c864542c" style="width: 600px" />

색이 이상합니다. 아래와 같이 `cmap='gray'`를 추가하면 흑백으로 바뀝니다.

```python
...
plt.imshow(gray_2d_pixel, cmap='gray')
...
```

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/b0579dce-c314-4746-b1f4-b3b1a2ad896a" style="width: 600px" />

## 6. DNN

입력층과 출력층 사이에 여러 개의 은닉층들로 이뤄진 인공신경망입니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9702ca71-c91c-4eb7-937d-e668757b7bf2)
<img src="" style="width: 600px" />

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Flatten, Dense
from tensorflow.keras.optimizers import Adam

df = pd.read_csv('/content/drive/MyDrive/AI 융합 서비스 개발자 양성과정제목없는 폴더/빅데이터 과정/data/fashion-mnist/fashion-mnist_train.csv')

# 1. 결측값 제거
# 2. 이상치 제거
# 3. 정규화 처리
scaler = MinMaxScaler()
scaler.fit(df.drop('label', axis=1, inplace=False).values)
x_data_norm = scaler.transform(df.drop('label', axis=1, inplace=False).values)
t_data = df['label'].values.reshape(-1,1)

# training, test data 분할
x_data_norm_train, x_data_norm_test, t_data_train, t_data_test = \
train_test_split(x_data_norm, t_data, test_size=0.3)

# 모델 생성
model = Sequential()
model.add(Flatten(input_shape=(784,)))

# hidden layer
model.add(Dense(units=64, activation='relu'))
model.add(Dense(units=128, activation='relu'))
model.add(Dense(units=256, activation='relu'))

model.add(Dense(units=10, activation='softmax'))

model.compile(optimizer=Adam(learning_rate=1e-4),
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

# 모델 학습
model.fit(x_data_norm_train,
          t_data_train,
          epochs=100,
          verbose=1,
          validation_split=0.3) # 전체 데이터의 30%가 검증 데이터로 사용됩니다.

# 평가
print(model.evaluate(x_data_norm_test, t_data_test)) # [0.5319429039955139, 0.8774999976158142]
```

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

model.summary()
```

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9b108b02-8f0d-401d-8d4f-e1b37b1eb4b1)
<img src="" style="width: 600px" />

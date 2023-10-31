Linear Regression은 독립변수가 1개 종속변수가 1개였는데 Multiple Linear Regression은 독립변수가 여러개 종속변수가 1개가 됩니다.<br>
scikit-learn으로 Multiple Linear Regression을 구현하겠습니다.
```python
import numpy as np
import pandas as pd
from sklearn import linear_model

original = pd.read_csv('경로')

# 독립변수: Solar.R, Wind, Temp
# 종속변수: Ozone
# 위의 필요한 컬럼만 남깁니다.
df1 = original[['Solar.R', 'Wind', 'Temp', 'Ozone']]

# 결측치 제거
df2 = df1.dropna(how='any')
# 이상치 제거 필요

# scikit-learn 구현은 정규화 처리를 하지 않아도 됩니다.
x_data = df2.drop('Ozone', axis=1, inplace=False).values
t_data = df2['Ozone'].values.reshape(-1,1)

# Model 만들고 학습을 진
sklearn_model = linear_model.LinearRegression()
sklearn_model.fit(x_data, t_data)
sklearn_model.predict([[130, 10, 70]]) # array([[25.74518848]])
```
Keras로 Multiple Linear Regression을 구현해보겠습니다.
```python
import numpy as np
import pandas as pd
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Flatten, Dense
from tensorflow.keras.optimizers import SGD
from sklearn.preprocessing import MinMaxScaler

original = pd.read_csv('/content/drive/MyDrive/AI 융합 서비스 개발자 양성과정제목없는 폴더/빅데이터 과정/data/ozone/ozone.csv')

df1 = original[['Solar.R', 'Wind', 'Temp', 'Ozone']]

# 결측치 제거
df2 = df1.dropna(how='any')

# 정규화 처리
scaler_x = MinMaxScaler()
scaler_t = MinMaxScaler()

scaler_x.fit(df2.drop('Ozone',axis=1, inplace=False))
scaler_t.fit(df2['Ozone'].values.reshape(-1,1))

x_data = scaler_x.transform(df2.drop('Ozone',axis=1, inplace=False))
t_data = scaler_t.transform(df2['Ozone'].values.reshape(-1,1))

# 모델 만들고 학습
keras_model = Sequential()
keras_model.add(Flatten(input_shape=(3,)))
output_layer = Dense(units=1, activation='linear')
keras_model.add(output_layer)
keras_model.compile(optimizer=SGD(learning_rate=1e-2), loss='mse')
keras_model.fit(x_data, t_data, epochs=1000)

# 검증
my_data = np.array([[130, 10, 70]])
my_data_norm = scaler_x.transform(my_data)
result = keras_model.predict(my_data_norm)

real_result = scaler_t.inverse_transform(result)

print(real_result) # [[26.754656]]
```

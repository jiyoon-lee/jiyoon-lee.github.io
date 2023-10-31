데이터 분석을 하기 전에 데이터를 정제처리해주어야 합니다.
결측값, 이상치, 정규화를 처리해주지 않으면 

데이터 전처리 과정을 배워봅시다.
# 결치값
데이터 값이 존재하지 않는 것을 의미합니다.
1. df.info()를 출력하여 결치값이 있는지 확인합니다.
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/43b26fb4-9c15-48e4-a7c8-78e72cc14b81)
2. 결치값이 있다면 일단 삭제처리 하겠습니다.
   ```python
   drop_df = df.dropna(how='any')
   ```

# 이상치
- 일반적인 값과 편차가 큰 값을 지칭합니다.
- 이런 이상치는 **평균, 표준편차에 영향을 크게 미칩니다.**
- 이상치의 분류
  - 독립변수의 이상치(지대점)
  - 종속변수의 이상치(outlier)
    - 일반적으로 이상치라고 하면 종속변수의 이상치를 가리킵니다.

### 이상치 찾는 방법
```python
# 라이브러리 불러오기
import numpy as np
import matplotlib.pyplot as plt

# 사용할 데이터셋
data = np.array([1,2,3,4,5,6,7,8,9,10,11,12,13,14,22.1])
```

1. Tukey's Fences(사분위 기반)
   위의 데이터셋의 그래프를 그려보겠습니다.
   ```python
   fig = plt.figure() # 도화지를 준비합니다.

   fig_1 = fig.add_subplot(1,2,1) # 1행 2열의 첫번째 위치에 subplot을 배치
   fig_2 = fig.add_subplot(1,2,2) # 1행 2열의 두번째 위치에 subplot을 배치

   fig_1.set_title('Original Data Boxplot')
   fig_1.boxplot(data)
   ```
  ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/21fda35e-8da6-4f80-81ad-6c2f08b73267)

   ```
   print(np.median(data) # 8.0 2사분위, 중위값
   print(np.percentile(data, 25)) # 25%의 값, 1사분위값 → 4.5
   print(np.percentile(data, 75)) # 75%의 값, 3사분위값 → 11.5
   print(np.percentile(data, 100)) # 100%의 값, 4분위값 → 22.1

   iqr_value = np.percentile(data,75) - np.percentile(data,25) # 7.0
   upper_fence = np.percentile(data,75) + (iqr_value * 1.5) # 11.5+10.5 = 22.0
   lower_fence = np.percentile(data,25) - (iqr_value * 1.5) # 4.5-10.5 = -6.0

   result_data = data[(data <= upper_fence) & (data >= lower_fence)] # 22.1 제거

   fig_2.set_title('Remove Outlier Data Boxplot')
   fig_2.boxplot(result_data)

   fig.tight_layout()
   plt.show()
   ```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/4d28aa16-6cc3-49ff-8b5f-3ec71f68ef1b)

3. Z-Score(정규분포)
   Z-Score은 아래와 같이 정규분포를 그립니다.
  ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cca8611b-7837-4139-9cf6-f20b86986837)
  ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/0e0d71c0-3571-4b16-ac6b-50234f11108a)

# 정규화
데이터의 값 중 혼자만 너무 크고 혼자만 너무 작은 값이 섞여있다면 모델의 정확도가 떨어집니다.<br>
예를 들어, 우리나라 아파트 가격을 구하는 모델을 도출할 때 방 개수를 데이터셋으로 사용한다고 가정해봅시다.<br>
대부분의 아파트의 방의 개수는 일의 자리수일겁니다. 그런데 어떤 한 집만 방의 개수가 100개라고 한다면 갑자기 평균이 확 올라가고 모델의 정확도가 떨어질 우려가 발생합니다.<br>
데이터는 -1에서 1사이의 범위를 유지하는 것이 모델의 정확도를 높일 수 있는 방법입니다.<br>
정규화 방식 중 유명한 두가지 방식에 대해 학습해보겠습니다.
- MinMaxScaling(최대, 최소 0~1)
- Standardization(표준화, 정규분포)

## MinMaxScaling
```python
from sklearn.preprocessing import MinMaxScaler

scaler_x = MinMaxScaler()
scaler_y = MinMaxScaler()

# Scaler에게 최대값과 최소값을 알려줍니다.
scaler_x.fit(data['Temp'].values.reshape(-1,1)) # n행 1열 ndarray
scaler_t.fit(data['Ozone'].values.reshape(-1,1)) # n행 1열 ndarray

# Training Data Set을 만듭니다.
x_data = scaler_x.transform(data['Temp'].values.reshape(-1,1))
t_data = scaler_t.transform(data['Ozone'].values.reshape(-1,1))
```

데이터셋이 만들어졌습니다. 이제 이것을 활용하여 모델을 구현해봅시다.

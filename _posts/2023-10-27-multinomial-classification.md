multinomial classification 다중 분류
logistic regression 여러 개를 모아서 model로 구현
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/48ad29ce-b6cf-4207-a45d-7e2003b442e2)

```python
import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

img = Image.open('/content/justice.jpg')

plt.imshow(img)
plt.show()
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/32689212-4d55-430f-80af-2f362df80c28)
```python
pixel = np.array(img)
print(pixel.shape) # (426, 640, 3) = (높이, 너비, 채널(RGB))
```
이미지 잘라내기
```python
crop_img = img.crop((30,100,150,330))
plt.imshow(crop_img)
plt.show()
```

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e1ff2e09-20cb-40ac-a60a-059b17b94564)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/2a4aa1db-cd9b-4ddf-9c2f-7c378ea40908)

이미지 크기 변경
```python
# print(img.size) # (640, 426)
resize_img = img.resize((int(img.size[0]/2), int(img.size[1]/2)))
plt.imshow(resize_img)
plt.show()
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/bfe77c83-de46-4dc6-9859-0768efd8c341)


이미지 회전
```python
rotate_img = img.rotate(90)
plt.imshow(rotate_img)
plt.show()
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/0e3bb29d-d70e-4890-bd86-65a090f64182)

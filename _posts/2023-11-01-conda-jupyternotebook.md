---
layout: single
title: "Anaconda 환경에서 Jupyter Notebook 사용하기"
categories: AI
tag: [AI, 빅데이터]
toc: true
author_profile: false
# sidebar:
#   nav: "docs"
toc: true
---

Deep Learning은 학습데이터량이 많아야 합니다.<br>
많다는 기준은 10만개 이상을 가리킵니다.<br>
일반적으로 현실에서 얻을 수 있는 데이터의 양에는 한계가 있습니다.<br>
특히 vision 쪽은 더욱이 데이터를 얻기가 어렵습니다.<br>
그러므로 적은 양의 Data를 이용해서 학습할 수 있는 방법을 모색해야 합니다.

그 방법은 [개와 고양이 판별 예제]를 통해 배워보겠습니다.<br>
실사 이미지로 고양이와 강아지의 사진이 제공되는데요.<br>
이것을 이진분류 해봅시다.<br>
→ 이 작업을 위해 Anaconda를 설치합니다.

Anaconda는 가상환경으로 구성되어 있습니다.<br>
하나하나의 가상환경은 독립적인 공간입니다.<br>
기본적으로 Anaconda를 설치하면 `BASE`라는 가상환경이 이미 생성되어 있습니다.<br>
이 `BASE`가상환경에서 `data_env`라는 새로운 가상환경을 생성합니다.

Anaconda 홈페이지에서 Anaconda를 설치합니다.<br>
설치가 완료되었다면 Anaconda Prompt를 실행합니다.<br>

```python
# 가상공간 생성
conda create -n data_env python=3.8 openssl

# 가상공간 진입
conda activate data_env
```

<figure style="width: 300px" class="image">
    <img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/227d911d-311b-4e75-ad2a-42084ca8a7e2" />
</figure>
이제 필요한 모듈을 설치합니다.
설치 방법에는 두가지가 있습니다.

- pip: 기본이며 필요한 모듈을 그냥 설치합니다.
- conda: dependency를 맞춰줍니다.

```python
conda install numpy pandas matplotlib # 버전을 명시하지 않으면 가장 최신버전을 설치합니다.
conda install scikit-learn
conda install tensorflow
conda install nb_conda # Jupyter notebook 설치
```

Jupyter notbook의 Home 폴더를 만듭니다.
코드 작성하는 Home 폴더로 사용할 겁니다.

```python
C:\jupyter_home # 폴더를 생성합니다.
```

Jupyter notebook을 실행합니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/0ab881eb-39a6-4a41-8163-eb7a3b7cb822)
자동으로 아래의 페이지가 열리는데요.<br>
이 페이지의 'new'에서 방금 생성한 'dev-env' 가상환경이 보인다면 가상환경이 잘만들어진겁니다.<br>
프롬프트에서 `ctrl+c`를 실행해 jupyter notebook을 끕니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/2d1bf62e-9688-45c9-8c43-d44d572a0011)
프롬프트에 `jupyter notebook --generate-config`를 입력하면 아래의 입력된 주소에 config 파일이 생성됩니다.
아래의 경로로 들어가보겠습니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/aed745a0-640b-40a9-8abd-a9366bb5b3db)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cc869438-aac7-4f4a-8a0a-65093debebec)
파일의 450번째줄에 `c.NotebookApp.notebook_dir`에 방금 생성한 Home 폴더의 경로를 입력합니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/4c0db30c-67db-4ab7-b592-3e6365882a67)
다시 프롬프트로 돌아와 `jupyter notebook`을 입력해 실행시키면 아까와 같이 `new`폴더에 `dev-env`가상화면이 보입니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/590f7261-3cd3-4a82-8be1-931124a47fbe)
`dev-env`를 클릭하면 colab과 같은 화면이 보입니다!!!
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cc32a5b2-d9cf-4b83-a76c-672fd31cd939)
이렇게 환경구축은 끝났습니다!

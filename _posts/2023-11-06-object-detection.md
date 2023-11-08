---
layout: single
title: "39장 DOM"
categories: javascript
tag: [python, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
toc: true
---

1. Bounding Box 찾는 알고리즘(무언가를 먼저 찾아야 합니다)
2. CNN

그러므로 학습과정과 예측과정의 속도가 굉장히 느려서 Real-Time application은 구현하기 어려웠습니다.<br>
YOLO(You Only Look One) model로 해결할 수 있습니다. 이것은 속도가 빠릅니다.<br>
저희는 Darknet System을 이용하여 실습해볼 것입니다.<br>
Darknet System은 머신러닝, 딥러닝을 위한 open source framework입니다. 이 안에 YOLO model이 들어있습니다.

## 실습

1. 환경변수부터 설정합니다.
   ```python
   import os
   os.environ['ROOT_FOLDER'] = '/content/YOLO_Object_Detection'
   ROOT_FOLDER = '/content/YOLO_Object_Detection'
   ```
2. 폴더를 만듭니다.
   ```python
   !mkdir "$ROOT_FOLDER"
   ```
3. 폴더가 생성되었으면 해당 폴더로 working directory를 변경합니다.
   ```python
   cd "$ROOT_FOLDER"
   ```
4. 해당 폴더에 git 명령을 이용해 특정 repository를 clone합니다.
   ```python
   !git clone https://github.com/AlexeyAB/darknet.git
   ```
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/a2143770-b53b-4244-855d-a31027f4a745)
5. working directory 를 darknet으로 변경
6. 받은 darknet은 python코드가 아니라 c코드이므로 우리 시스템에 맞게 컴파일이 필요합니다.<br>
   컴파일하기 위해서 설정파일인 Makefile을 수정합니다.<br>
   아래의 항목대로 수정을 완료합니다.<br>
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e4b7222b-ad9b-49f9-8cdc-acedbeb20017)
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/1c03c715-23d1-4d7c-9d88-95d685acd408)
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/87f2ea13-86a4-4c36-9d56-154b1f9cbc9f)
   수정을 완료했다면 아래의 코드를 실행합니다.
   ```python
   !make
   ```
   이제 YOLO의 모델을 사용할 수 있게 되었습니다.
7. weight(가중치)파일을 다운로드 합니다.
   이미 학습이 끝난 Pretrained Network릐 가중치 파일을 가져와서 YOLO모델에 얹어서 사용합니다.
   ```python
   !wget https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.weights
   ```
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/6b52c4c5-585b-4ef5-a791-5579a03f6e4a)
   <<<<<<< HEAD
8. # 이미지 1장을 이용해서 직접 Object Detection을 수행합시다.
9. 이미지 1장을 이용해서 Object Detection을 수행합시다.

   > > > > > > > 003c7e0ffe790be42aa223b0227d6df91e78fed4
   > > > > > > > ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/acbe7590-2096-4cae-ae08-14e7a7846e0a)

   ```python
   !./darknet detector test cfg/coco.data cfg/yolov4.cfg yolov4.weights data/dog.jpg
   ```

   <<<<<<< HEAD

   /content/YOLO_Object_Detection/darknet/src/image.c
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/20cae6bf-bac9-45e2-81c0-410f2100ebbc)
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/8b617cb4-f6c7-445e-8766-71664f1f1503)

   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/f857babc-c923-4bf0-8a41-26fdaa5dfe5a)

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/92adb52f-0d0e-497b-ba90-a431e491fa20)
width, heigtㅅ cnn에 들어갈 이미지의 가로, 세로 길이
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/06f203fd-1279-43d5-acbd-628fcf5a960a)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/1e53d6f1-5000-43dc-a358-8643ebcba0d4)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cdb38030-f279-4940-858c-244383e5c3bf)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/8fbb71ae-b262-49d7-8a60-0dec8b3c2a2b)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/973f4ac4-d923-4448-8226-cf87389e58af)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/acbc87e6-a461-435c-a6b0-90d9975df9f9)

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/c6901d87-f49d-4e5f-a378-eb1478bbed47)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/5331a35a-7525-4b44-b87d-7ea4fb745ced)
======= 11. 예측결과출력
위의 명령어 입력 이후 `/content/YOLO_Object_Detection/darknet/predictions.jpg`에 `predictions.jpg`파일이 생성됩니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/89d59a7d-7edd-4ced-806a-265cb5bb1085)

> > > > > > > 003c7e0ffe790be42aa223b0227d6df91e78fed4

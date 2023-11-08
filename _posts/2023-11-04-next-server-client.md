---
layout: single
title: "Server Component vs Client Component"
categories: FrontEnd
tag: [Next.js]
toc: true
author_profile: false
sidebar:
  nav: "docs"
toc: true
---

# v12

- 페이지 단위로 렌더링 방식을 규정합니다.
- SSR은 `getSeverSideProps()`를 사용합니다.
- SSG은 `getStaticProps()`를 사용합니다.

# v13

- 컴포넌트 단위로 렌더링 방식을 규정합니다.
- 별도로 설정하지 않으면 기본적으로 서버 컴포넌트가 됩니다.

  ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/583d76ea-3413-42da-89ba-edfe40d484d5)

## 서버 컴포넌트의 특징

1. 서버 컴포넌트는 서버에서 실행됩니다.
2. 클라이언트는 HTML형태로 서버에서 받아옵니다.
3. 서버 컴포넌트는 브라우저에서 제공하는 API는 사용할 수 없고 Node api를 사용할 수 있습니다.
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/609d162a-6985-4d32-a9a6-0f0f18f1a4ed)
4. 아무 설정을 하지않을 경우 기본적으로 서버 컴포넌트입니다.

## 클라이언트 컴포넌트의 특징
1. 페이지 안에서 상태를 처리하는 useState나 useEffect, 브라우저 api를 사용할 수 있습니다.
2. 꼭 필요한 부분만 작은 단위의 클라이언트 컴포넌트로 만드는 것이 좋습니다.
3. 실습
   'use client'를 표기합니다!<br>
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/00b07bca-72eb-4063-b917-8b2c13c0afda)
   ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/c00138ef-e6fa-4e62-b0b7-6edc62e4837d)

## 동작 이해하기
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9b826c85-4fa0-46ef-b4d8-5cacca54942b)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/7a923b55-5e51-43dc-995b-605e70fee113)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/dd6c7d34-79e1-49ba-b4af-0456b2df9202)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/f00a8321-3aba-48a5-9e14-923392fc5d76)
위에서 확인 할 수 있듯이 서버 컴포넌트와 클라이언트 컴포넌트에 똑같이 `console.log`를 입력하면
서버 콘솔에도 '안녕! 클라이언트'와 '안녕! 서버'이 표시됩니다. 왜 '안녕! 클라이언트'도 출력되는지 의아해 하실 겁니다.
그 이유는 Next에서 서버 컴포넌트이던 클라이언트 컴포넌트이던 상관하지 않고 정적 HTML을 일단 만듭니다.
그이후에 js, react와 같은 부분적인 소스코드를 클라이언트에게 보내주어 hydration이 발생하고 나서야 이벤트 처리가 가능하게 됩니다.


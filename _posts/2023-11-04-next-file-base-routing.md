---
layout: single
title: "Next.js의 File Base Routing"
categories: React
tag: [React]
toc: true
author_profile: false
sidebar:
  nav: "docs"
toc: true
---

## Next.js v12

### File Base Routing

기본적으로 `npx create-next-app`를 실행하면 `pages`라는 폴더가 있습니다.<br>
이 폴더안에 `about.tsx`라는 새로운 파일을 생성하고 'About'이라는 리액트 컴포넌트를 만듭니다.<br>
이제 다시 `npm run dev`를 통해 실행시키고 `localhost:3000/about`으로 들어가면 페이지로 표기되는 것을 확인할 수 있습니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/b8032eec-8642-4e38-8aec-d21bf648d52a)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/4917abea-8981-42f2-b18f-d6ba4b8ac46c)

**File Base Routing**이라는 것은 `pages` 폴더 아래 파일만 만들어 주면 리액트 컴포넌트가 페이지처럼 라우팅 되는것을 말합니다.<br>
Next.js는 File Base Routing을 지원하므로 간편하게 라우팅 처리를 가능하게 합니다.

### 중첩경로

만약 `localhost:3000/products/pants`와 같이 경로를 만들고싶다면 `pages`폴더 아래에 `products`폴더를 추가하면 됩니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/1c3163e8-1a68-4536-8bbe-ffa16075b2a6)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/7192f7e5-b7d7-4e41-a024-935b69744fda)

## Next.js v13

13버전에는 `pages`폴더가 사라지고 `app`이라는 새로운 폴더가 추가되었습니다.<br>
`app`폴더 아래이 `about`폴더를 추가하고 아래에 `page.tsx`파일을 추가하여 리액트 컴포넌트를 생성합니다<br>
Next를 다시 실행시키면 페이지 라우팅이 되는 것을 확인할 수 있습니다.<br>
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/2fb3bfea-ec53-479d-a760-af52c78482cc)

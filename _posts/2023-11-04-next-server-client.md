---
layout: single
title: "Server Component vs Client Component"
categories: React
tag: [python, blog]
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


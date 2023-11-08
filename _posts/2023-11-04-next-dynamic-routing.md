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

`app`폴더 아래에 `[slug]`라는 폴더를 생성합니다.<br>
`[slug]`폴더 아래에 `page.tsx`폴더를 생성합니다.<br>
통상적으로는 `page.tsx` 폴더의 제일 아래에 `export function generateStaticParams() {}`를 사용해서 Next.js에게 알립니다.<br>
다이나믹 라우팅 페이지에서 특정한 경로에 한해서는 페이지를 미리 만들어 달라고 요청합니다. 그리고 그 경로를 알려주면 됩니다.<br>
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/1f66b9d6-3bef-4c62-a155-dc79916686f6)

그 다음 build를 시켜보면 꽉찬 동그라미 아이콘과 빈 동그라미 아이콘 두개가 나옵니다.<br>
둘 다 서버에서 SSG형태로 페이지가 만들어졌다는 것은 동일합니다.<br>
이미 서버에는 HTML 페이지가 만들져있습니다.<br>
하지만 빈 동그라미는 요청시에 HTML 페이지에 다시 데이터를 채워서 HTML 페이지를 생성하고,
꽉찬 동그라미는 Props로 전달된 데이터로 빌드할 때 미리 HTML 페이지를 만들어둡니다.<br>
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/dc90ad9f-fc79-4e86-8274-f10abcb3155c)

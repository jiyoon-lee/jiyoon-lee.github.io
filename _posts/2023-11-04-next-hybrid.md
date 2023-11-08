---
layout: single
title: "Next.js의 Hydration"
categories: React
tag: [React]
toc: true
author_profile: false
sidebar:
  nav: "docs"
toc: true
---

# 렌더링의 종류

## CSR(Client Side Rendering)

- **렌더링하는 주체가 클라이언트-브라우저**입니다.
- 장점
  - 한번 로딩되면 빠른 UX 제공합니다. - SPA(Single Page Application)
  - 서버의 부하가 적습니다.
- 문제점
  - 페이지 로딩 시간(TTV-Time To View), FCP(First Contentful Paint)이 오래 걸립니다.
  - SEO 최적화가 힘듭니다.
  - 보안에 취약합니다.
  - CDN에 캐시가 안됩니다.

## SSG(Static Site Generation)

- **렌더링하는 주체가 서버이며, 빌드할때 렌더링** 됩니다.
- 장점
  - 페이지 로딩 시간(TTV)이 빠릅니다.
  - 자바스크립트가 필요 없습니다.
  - SEO 최적화가 좋습니다.
  - 보안이 뛰어납니다.
  - CDN에 캐시가 됩니다.
- 문제점
  - 데이터가 정적입니다.
  - 사용자별 정보 제공이 어렵습니다.

## ISR(Incremental Static Regeneration)

- **렌더링하는 주체가 서버이며 주기적으로 렌더링** 합니다.
- SSG와 동일한 원리이지만, 정해진 주기에 따라 페이지를 다시 생성합니다.
- 장점
  - 페이지 로딩 시간(TTV)이 빠릅니다.
  - 자바스크립트가 필요없습니다.
  - SEO 최적화가 좋습니다.
  - 보안이 뛰어납니다.
  - CDN에 캐쉬가 됩니다.
  - 데이터가 주기적으로 업데이트 됩니다.
- 문제점
  - 실시간 데이터가 아닙니다.
  - 사용자별 정보 제공이 어렵습니다.

## SSR(Server Side Rendering)

- **렌더링 하는 주체가 서버이며, 요청시마다 렌더링** 합니다.
- 장점
  - 페이지 로딩 시간(TTV)이 빠릅니다.
  - 자바스크립트가 필요 없습니다.
  - SEO 최적화가 좋습니다.
  - 보안이 뛰어납니다.
  - 실시간 데이터를 사용합니다.
  - 사용자별 필요한 데이터를 사용합니다.
- 문제점
  - 비교적 느릴 수 있습니다.(overhead)
  - 서버의 과부하가 걸릴 수 있습니다.
  - CDN에 캐시가 안됩니다.

## 하이브리드

하이브리드의 뜻은 혼합인데요.<br>
특정 목적(성능 좋은 강력한 Web Application)을 달성하기 위해 두개 이상(CSR, SSG, ISR, SSR)의 기능이나 요소를 결합하는 것을 말합니다.<br>
Nextjs에서 하이브리드를 가능하게 하기 위해서 하이드레이션이라는 기능을 사용합니다.
Hydration이란 '수화시키다'라는 뜻을 가집니다. '물로 가득 채우다'라는 의미입니다.
'물'을 리액트라고 생각하면 됩니다. Hydration은 React로 가득채우는건데요.

클라이언트가 서버에게 HTML파일을 요청하면 서버는 클라언트가 볼수있는 의미있는 정적인 HTML파일을 먼저 보내줍니다.
그럼 사용자는 페이지를 볼 수는 있지만 아직 자바스크립트 코드를 다운받지 않은 상태이기 때문에 클릭을 해도 처리할 코드가 없기때문에
클릭을 해도 아무런 것도 일어나지 않습니다.
이후에 서버에서 리액트와 자바스크립트 파일들을 클라이언트에게 보내줍니다. 그럼 클라이언트가 정적 HTML파일에 리액트와 자바스크립트로 가득 채웁니다.
이것이 하이드레이션입니다.

## 상황에 따른 렌더링 방식

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/6928bf88-ed14-43df-bfcb-af375916920b)

## 빌드를 통한 Next.js의 렌더링 방식

next.js 프로젝트에서 `npm run build` 명령어로 빌드해보겠습니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e56918b2-9d20-4891-9d16-0051613148ae)

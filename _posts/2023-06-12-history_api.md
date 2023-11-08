---
layout: single
title: "History API"
categories: javascript
tag: [python, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
toc: true
---

# OVERVIEW

- back(), forward(), go() : '뒤로가기', '앞으로 가기'와 같은 **히스토리 스택 조작**
- pushState(), replaceState() : 주소창 **URL을 직접 조작**하기 위한 함수
- window.onpopstate : 콜백 함수를 넣어주면 되는데 '뒤로 가기'와 같은 pop 이벤트 발생시에 불리게 됩니다.
- state, length : 히스토리 객체가 가지고 있는 변수

# History instance methods: 히스토리 스택 조작을 위한 API

- history.back() : 뒤로 가기
- history.forward() : 앞으로 가기
- histofy.go()
  - '뒤로 가기'와 '앞으로 가기' 모두 가능
  - 매개변수로 정수값을 받는데, 음수값을 넣으면 뒤로(history.go(-1) == history.back())
  - 양수 값을 넣으면 앞으로 가기 동작(history.go(1) == history.forward())
  - 다른 숫자를 넣으면 그 숫자만큼 히스토리 스택을 한 번에 이동

# History instance methods: 주소창 URL 변경을 위한 함수

- history.pushState
- history.replaceState

매개 변수를 3개 받습니다.

```js
history.pushState(
  stateObj,
  title, → 모든 브라우저에서 지원하는건 아니라서 그냥 빈 문자열을 넣어주어도 되고 아무거나 넣어주어도 상관없음
  URL → 주소창에 보여주고 싶은 주소값을 넣어준다.
)

history.pushState(
  stateObj,
  title,
  URL
)
```

- pushState와 replaceState 함수를 부르게 되면 필수적으로 히스토리 스택이 변경
- 스택 안에 들어가는 아이템에 stateObj가 담긴다.
- URL 정보 뿐만 아니라 더 많은 정보를 넣고 싶을 때 이 stateObj에 추가 데이터를 넣어서 사용할 수 있다. 그러면 이 state 정보를 나중에 원할 때 적절하게 꺼내서 확인할 수 있다.
- pushState와 replaceState의 차이
  - pushState는 새로 넣는 역할(push)
  - replaceState는 현재 state를 그대로 대체하는 역할, pop을 한번 하고 그 다음 push

# Event: onpopstate 콜백

- history stack이 바뀔 때 발생
- onpopstate 콜백 함수가 불리게 되면 매개변수로 이벤트 객체가 전달됩니다.
- 여기서, pushState와 replaceState의 stateObj를 사용가능
- onpopstate를 통해 SPA 구성 가능

```
window.onpopstate = (
  function (event) {
    const { state } = event;
  }
);
```

# History Instance properties

- history.state: 현재 열려있는 페이지, history의 stateObj 정보 반환
- history.length : history stack의 크기

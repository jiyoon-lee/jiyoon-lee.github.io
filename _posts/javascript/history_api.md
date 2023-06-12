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
- pushState(), replaceState() : 주소창 URL을 직접 조작하기 위한 함수
- window.onpopstate : 콜백 함수를 넣어주면 되는데 '뒤로 가기'와 같은 pop 이벤트 발생시에 불리게 됩니다.
- state, length : 히스토리 객체가 가지고 있는 변수


# 히스토리 스택 조작을 위한 API
- history.back() : 뒤로 가기
- history.forward() : 앞으로 가기
- histofy.go()
  - '뒤로 가기'와 '앞으로 가기' 모두 가능
  - 매개변수로 정수값을 받는데, 음수값을 넣으면 뒤로(history.go(-1) == history.back())
  - 양수 값을 넣으면 앞으로 가기 동작(history.go(1) == history.forward())
  - 다른 숫자를 넣으면 그 숫자만큼 히스토리 스택을 한 번에 이동

# 주소창 URL 변경을 위한 함수
- history.pushState
- history.replaceState

매개 변수를 3개 받습니다.
```js
history.pushState(
  stateObj, →
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
- 스택 안에 들어가는 아이템에는 어떤 정보가 있을까. 바로 stateObj이다.
- URL 정보 뿐만 아니라 더 많은 정보를 넣고 싶을 때 이 stateObj에 추가 데이터를 넣어서 사용할 수 있다. 그러면 이 state 정보를 나중에 원할 때 적절하게 꺼내서 확인할 수 있다. 
곧 다룰 history의 state 변수와 onpopstate 콜백이 그런 용도로 사용된다.
그러면 pushState와 replaceState 함수는 뭐가 다른걸까요?
받는 매개변수는 동일하고 URL 변경하고 state 변경하는 것도 동일한데 딱 한가지가 다릅니다.
pushState는 스택에 말그대로 push 새로 넣는 역할을 하는데요.
replaceState는 현재 state를 그대로 대체하는 역할을 합니다.
스택 데이터 구조에 비유를 하자면 pushState는 push
replaceState는 일단 pop을 한 번 하고 그 다음에 push를 하는건데 조금 다른 점은
pop을 했다는 사실을 외부에 알리지 않고 몰래한다. 그래서 함수 이름이 popAndPushState가 아니라 replaceState라고 부르는 거죠 

# onpopstate 콜백
- history.onpopstate
히스토리 api는 아니라고도 할 수 있겠습니다. 왜냐하면 히스토리 객체 안에 있는 함수는 아니니까요.
하지만 이걸 빼놓고 히스토리 api를 이야기할 수 없기 때문에 포함시켰습니다.
같은 웹 사이트 안에 있다는 가정 하에 기본적으로 웹 브라우저에서 뒤로 가기 버튼을 누르면 이 콜백 함수가 불리게 됩니다.
다른 페이지로 이동을 하게 되면, 그 때는 부를 방법이 없겠죠?
그리고 또 중요한 건 아까 이야기했던 히스토리 API의 back이나 forward, go 함수죠
이런 히스토리 스택 조작 함수를 부르고 실제 히스토리 스택에 변경이 된다면 
그때도 onpopstate 콜백이 불리게됩니다. 하지만, 이건 어디까지나 히스토리 스택이 실제로 변경이 되어야 합니다.
예를 들어, 마지막 페이지에서 forward 함수를 부른다고 생각해보시죠. 이미 마지막 페이지이니까요.
그럼 onpopstate 콜백도 당연히 불리지 않게 됩니다. 이렇게 onpopstate 콜백 함수가 불리게 되면 매개변수로 이벤트 객체가 전달됩니다.
여기서, 아까 pushState나 replaceState 할 때 넣어주었던 stateObj를 꺼내서 사용할 수 있습니다.
그동안 stateObj에 뭔가 넣었던 건 바로 지금을 위한 큰 그림이었던 겁니다.
한 가지 더 이야기 하면, 이 함수는 여러분이 SPA 구성을 하신다면 페이지 이동 처리를 위해서 정말 필수적으로 사용하셔야 하는 함수입니다.
실제 웹사이트 자체가 바뀌지 않는데 페이지를 변경해주려면 해당 히스토리 이벤트를 프로그래머가 알 수 있어야 하겠죠?
그걸 onpopstate 콜백이 있으면 알수 있게 되겠습니다.
```
window.onpopstate = (
  function (event) {
    const { state } = event;
  }
);
```

- history.state: 현재 열려있는 페이지, history의 stateObj 정보 반환
- history.length : history stack의 크기




# 디렉티브 태그
- JSP 페이지를 어떻게 처리할 것인지를 설정하는 태그
- JSP 페이지가 서블릿 프로그램에서 서블릿 클래스로 변환할 때 **JSP 페이지와 관련된 정보를 JSP 컨테이너에 지시하는 메시지**
- 디렉티브 태그는 JSP 페이지를 수정하여 다시 컴파일 하는 경우에만 역할을 수행
```
<%@ page 속성1="값1" [속성2="값2" ...] %>
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9266f2e5-dfcf-47d8-a341-a588d99aba81)


## page 디렉티브 태그의 기능과 사용법
- JSP 페이지에 대한 정보를 설정하는 태그
- JSP 페이지의 최상단에 선언하는 것을 권장
- 하나의 page 디렉티브 태그에 하나 또는 여러 개의 속성을 설정할 수 있음
- 여러 개의 속성마다 개별적으로 page 디렉티브 태그를 선언할 수 있음
- import 속성을 제외한 속성은 JSP페이지에 한 번씩만 설정할 수 있음

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/435a8a5e-cfd7-4f54-a5eb-4c9ff700c584)

### language
- JSP 페이지에서 사용할 프로그래밍 언어를 설정하는데 사용
- 기본 값은 java
```
<%@ page language="java" %>
```

### contentType
- 현재 JSP 페이지의 콘텐츠 유형(MIME-type)을 설정하는 데 사용
- 콘텐츠 유형은 주로 `text/html`, `text/xml`, `text/pain`등이 있으며, 기본 값은 `text/html`
- 문자열 세트(charset)을 설정
```
<%@ contentType="text/html" %>
<%@ page contentType="text/html;charset=utf-8" %>
```

### pageEncoding
- 현재 JSP 페이지의 문자 인코딩 유형을 설정하는데 사용
- 기본 값은 `ISO-8859-1`
```
<%@ page pageEncoding="ISO-8859-1" %>
// 아래와 동일
<%@ page contentType="text/html; charset="iso-8859-1" %>
```

### import


## include 디렉티브 태그의 기능과 사용법


## taglib 디렉티브의 기능과 사용법

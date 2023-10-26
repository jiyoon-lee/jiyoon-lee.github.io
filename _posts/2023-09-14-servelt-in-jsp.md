---
layout: single
title: "서블릿이란"
categories: network
tag: [python, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
toc: true
---

서브릿은 웹 서버에서 작동하는 작은 자바 프로그램이다.
서브렛은 일반적으로 HTTP나 HTML 프로토콜로 웹 클라이언트로 부터 요청과 응답을 받는다.
이 인터페이스를 구현하기 위해 `javax.servlet.GenericServlet`이나 `javax.servlet.http.HttpServlet`을 사용해야한다.
이 인터페이스는 servlet을 초기화하거나 요청을 받거나 서버로 부터 서브릿을 지우는 메소드를 정의한다.
1. 서브릿이 생성되면 init메소드로 초기화한다.
2. 클라이언트로 부터 어떤 요청이 온다면 `service()` 메소드가 호출된다.
3. 서브릿 서비스가 중된되면 `destroy()` 메소드가 호출되어 제거된다.
추가적인 라이프사이클 메소드로 서블릿이 시작 정보를 가져오는데 사용할 수 있는`getServletConfig()`메소드과 서블릿이 작성자, 버전, 저작권과 같은 자체 기본 정보를 반환할 수 있도록 하는 `getServletInfo()`메소드가 있다.


## 서블릿 라이프 사이클
1. Sevlet 클래스 로드
  - 첫 요청을 받으면 웹 컨테이너는 서블릿을 로드한다.
  - 이 동작은 처음 한번만 실행된다.
2. 서블릿 인스턴스 생성
  - 서블릿 클래스를 로딩한 후에 웹 컨테이너는 서블릿 인스턴스를 만든다.
  - 한개의 인스턴스만 한개의 서블릿을 위해 생성된다.
  - 이후 동시에 들어온 모든 요청은 같은 서블릿 인스턴스에서 실행한다.
3. `init()` 메소드 호출
  - 웹 컨테이너가 서블릿 인스턴스를 만든 후에 서블릿의 `init()`메소드를 호출한다.
  - 이 메소드는 첫 요청 수행 전에 서블릿을 초기화하는데 사용된다.
  - 웹 컨테이너에 의해 한번만 호출된다.
4. `server()` 메소드 호출
  - 웹 컨티이너가 초기화를 한 이후에 `service()`메소드를 호출한다.
  - 서비스 메소드는 모든 요청에 의해 불려진다.
  - 모든 요청에 대해 개별의 스레드를 생성한다.
5. `destroy()` 메소드 호출
  - 이 메소드는 웹 컨테이너에 의해 서블릿 인스턴스가 지워지기 전에 호출된다.
  - `destroy()`메소드는 서블릿에게 이와 연관된 모든 리소스를 해제하라고 요청한다.
  - 서블릿의 모든 스레드가 종료되거나 시간 초과가 발생한 경우 웹 컨테이너에 의해 한 번만 호출됩니다.

## 서블릿 인터페이스

## GenericService class

## HttpServlet class

## web.xml file

## welcome-file-list

## load-on-startup in web.xml

## RequestDispatcher interface

## sen




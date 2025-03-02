---
layout: single
title: "[SQLD]데이터 모델링의 이해"
categories: javascript
tag: [python, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
toc: true
---
# OVERVIEW
### 모델링
- 복잡한 현실 세계를 추상화, 단순화, 명확화하기 위해 일정한 표기법으로 모델을 표현하는 기법

### 모델링의 특징
- 추상화: 복잡한 현실 세계를 **일정한 형식**에 맞게 표현한다
- 단순화: 복잡한 현실 세계를 서로가 **약속한 규약을 준수**하는 표기법이나 언어로 표현
- 명확화: 복잡한 현실 세계를 명확하게 기술

### 모델링의 3가지 관점
- 데이터 관점(What)
    - 비즈니스와 관련된 데이터는 무엇인지 또는 데이터 간의 관계
- 프로세스 관점(How)
    - 해당 비즈니스로 인해 일어나는 일은 어떠한 일인지
- 상관 관점(Data vs Process)
    - 데이터 관점과 프로세스 관점 간 서로 어떠한 영향을 받는지

---

### 데이터 모델링의 정의
- 현실 세계의 비즈니스를 IT 시스템으로 구현하기 위해 **데이터 관점**으로 업무를 분석하는 기법
- 현실 세계의 비즈니스를 **약속된 표기법**으로 표현하는 과정이다.
- IT 시스템의 근간이 되는 데이터베이스를 구축하기 위한 분석 및 설계의 과정이다.

### 데이터 모델링의 3단계 진행
- 개념적 데이터 모델링
    - IT 시스템에서 구현하고자 하는 대상에 대해 **포괄적** 수준의 데이터 모델링을 진행한다.
    - 전사적 데이터 모델링 시 많이 사용하는 단계이다.
- 논리적 데이터 모델링
    - IT 시스템에서 구현하고자 하는 비즈니스를 만족하기 위한 **기본키, 속성, 관계, 외래키 등**을 정확하게 표현하는 단계
- 물리적 데이터모델링
    - 논리 데이터 모델을 기반으로 실제 물리 DB구축을 위해 성능, 저장공간 등의 **물리적인 특성을 고려**하여 설계하는 단계

### 프로젝트 생명 주기에서 데이터 모델링
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9874f0b5-93bc-4846-95d3-734f965f67f6" width="550" height="auto" />

### 데이터 모델링의 필요성
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/3e041f31-09a7-41c3-bcf0-461e33e580f8" width="550" height="auto" />

### 데이터베이스의 3단계 구조
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/6bf63c08-10da-4de7-9bec-0c269f1a55ac" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/ec51f21c-ed97-41b0-a684-bd9e7401be08" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/17663f62-fc90-4490-9ad9-e78489aa81c4" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/d268d109-dd7d-4fe9-9ab9-24f4ef7e37dc" width="550" height="auto" />

---

### 데이터 모델링의 3가지 요소
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/c7bc3fdd-123d-46ba-82f9-20c81e27f0e1" width="550" height="auto" />

### ERD를 그리는 작업 순서
1. 비즈니스에 필요한 엔터티를 그린다.
2. 1번에서 그린 엔터티르 적절하게 배치한다.
3. 각 엔터티 간의 관계를 설정한다.
4. 설정한 관계의 관계명을 기술한다.
5. 설정한 관계의 참여도를 기술한다.
6. 설정한 관계의 필수 여부를 기술한다.

### 좋은 데이터 모델의 요소
- 완전성: 업무에 필요한 데이터가 모두 정의되어 있어야 함
- 중복배제
- 업무 규칙: 데이터 모델 분석만으로도 비즈니스 로직이 이해되어야 한다.
- 데이터 재사용: 데이터 통합성과 독립성을 고려하여 재사용이 가능해야 함
- 의사소통: 데이터 모델을 보고 이해 당사자들끼리 의사소통이 이루어질 수 있어야 함
- 통합성: 동일한 데이터는 유일하게 정의해서 다른 영역에서 참조해야 한다.

---

### 엔터티
- 엔터티는 사람, 사물, 사건, 개념 등의 명사에 해당한다.
- 엔터티는 비즈니스 관점에서 IT 시스템을 통해 관리가 필요한 관심사에 해당한다.
- 엔터티는 결국 비즈니스를 구현하기 위해 저장해야 하는 어떤 것(Thing)이라고 할 수 있다.

### 엔터티의 표기법
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/a2a37520-1fcf-442d-a2d8-55df5bd121b1" width="550" height="auto" />

### 엔터티의 특징
- 비즈니스 요구 조건 만족을 위해 반드시 필요하고, 저장 및 관리하고자 하는 정보여야 한다.
- 유일한 식별자에 의해 식별이 가능해야 한다. 즉 집합 내에서 단 1건을 콕 짚어낼 수 있어야 한다.
- 영속적으로 존재하는 인스턴스(2개 이상)의 집합이어야 한다.
- 엔터티는 비즈니스 프로스세에 의해 반드시 이용되어야 한다.
- 엔터티는 반드시 속성을 가지고 있어야 한다.
- 엔터티는 다른 엔터티와 최소 1개 이상의 관계가 있어야 한다.

### 엔터티의 분류
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/6c44288a-59b5-4a8d-99fc-37e665d0c14f" width="550" height="auto" />

### 엔터티의 명명규칙
- 가능한한 업무 담당자들이 사용하는 용어를 사용한다.
- 가능하면 약어를 사용하지 않는다.
- 엔터티는 단수명사여야 한다.
- 엔터티의 이름은 해다 ㅇ모델 내에서 유일한 이름이어야 한다.
- 엔터티의 생성 의미에 맞게 이름을 부여해야한다.

---

### 속성
- 브즈니스에서 필요로 한다.
- 엔터티에 대한 설명이며 인스턴스의 구성요소가 된다.
- 의미상 더 이상 분리되지 않는 데이터 단위이다.

### 엔터티, 인스턴스, 속성, 속성값의 관계
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/3a4870f9-a7a3-458b-9e2e-58a3139d2413" width="550" height="auto" />

- 1개의 엔터티는 2개 이상의 인스턴스의 집합이어야 한다.
- 1개 인스턴스는 여러 개의 속성을 갖는다.
- 1개의 엔터티는 2개 이상의 속성을 갖는다.
- 1개의 속성은 1개의 속성값을 갖는다.

### 속성의 표기법
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/69ee6894-a9d3-4db1-918c-55358dbbff95" width="550" height="auto" />

### 속성의 특징
- 엔터티와 마찬가지로 반드시 비즈니스에서 필요로 하고 IT시스템에서 저장 및 관리하고자 하는 정보여야 한다.
- 정규화 이론에 따라 속성이 속해 있는 엔터티의 주식별자에 함수 종속성을 가져야 한다.
- 하나의 속성에는 1개의 값만을 가진다. 하나의 속성에 여러 개의 값이 있는 다중 값일 경우 별도의 엔터티를 이용하여 분리한다.

### 속성의 분류
- 특성에 따른 분류
- 엔터티 구성 방식에 따른 분류
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/c57a8f04-160f-485c-ac72-89aea2ea22be" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/a93cf8ad-d723-468a-97a4-c9c49772cc61" width="550" height="auto" />

### 도메인
- 속성이 가질 수 있는 값의 범위
- 학생 엔터티의 학점 속성의 도메인은 0.0 ~ 4.5의 범위를 갖는 실수 값으로 정의할 수 있다.
- 각 속성의 속성값은 정의된 도메인 이외의 값을 가질 수 없다.

### 속성의 명명
- 비즈니스에 사용하는 이름을 부여한다.
- 속성명을 서술식으로 명명하지 않는다.
- 속성 명명 시 약어 사용은 가급적 하지 않는다.
- 전체 데이터 모델 내에서 유일한ㄷ 이름의 속성명으로 명명하는 것이 좋다.

---

### 관계
- 엔터티끼리 상호 연관서이 있는 상태를 의미
- 데이터 모델 내에 존재하는 엔터티 간 논리적인 연관성을 의미

### 관계의 페어링
- (관계) 페어링: 엔터티 안에 인스턴스가 개별적으로 관계를 가지는 것
- 관계: 이러한 관계 페어링을 논리적으로 표현한 페어링의 집합
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/38676313-a47a-4f12-8b62-3bdcb1cdd4d7" width="550" height="auto" />

### 관계의 표기법
- 관계의 표기 시에는 관계 차수 및 관계 선택사양을 명확하게 해야 합니다.
- 관계 차수: 2개의 엔터티 간 관계에서 참여자 수를 표현하는 것
- 1:M, 1:1, M:M이 있다.

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/61369701-57fd-410b-a5a5-7f055d91ace1" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/019c6ebe-1765-4d8d-a51b-ef5420007a17" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/4535be9f-4940-4d6b-8a0b-8c8822d586b3" width="550" height="auto" />


### 관계 선택사양
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/525673f2-e090-4419-ade5-80cab8edc4da" width="550" height="auto" />

- 지하철역승하차는 지하철역을 필수적으로 알아야 한다.

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/3e3e143f-4564-4bba-a8c1-0436e8584f34" width="550" height="auto" />

- 지하철역은 여러 개의 지하철역승하차 정보를 가질 수 있다(까치발).
- 단 1개의 지하철역승하차 정보도 갖지 않을 수 있다(점선).

---

### 식별자
- 엔터티의 각 인스턴스를 개별적으로 식별하기 위해 사용되는 하나의 속성 혹은 속성들의 집합

### 식별자의 특징
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/d86a71e7-2983-49f8-93b1-f577acaef0c7" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/0e89824a-7669-47c0-97a1-2c3e0cbab7c8" width="550" height="auto" />

### 식별자 도출 기준
- 비즈니스에서 자주 이용되는 속성을 주식별자로 지정한다.
- 명칭, 장소와 같이 이름으로 기술되는 속성은 가능하면 주식별자로 하지 않는.
- 주식별자를 복합식별자로 할 경우 지나치게 많은 속성을 포함되지 않도록 한다.

### 식별자 관계와 비식별자 관계의 결정
- 식별자 관계: 자식 엔터티에서 부모 엔터티로부터 받은 외부식별자를 자신의 주식별자로 이용
- 비식별자 관계: 부모와 연결이 되는 속성으로서만 이용

<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/c557a015-279e-4d3e-8080-77a96070ab4c" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/05f8a68b-3423-4008-9452-d98cf1a59259" width="550" height="auto" />

비식별자 관계를 갖는 경우
- 자식 엔터티에서 받은 속성이 반드시 필수가 아니어도 무방하기 때문에 부모 없는 자식이 생성될 수 있는 경우가 비식별자 관계이다.
- 부모 엔터티의 주식별자를 자식 엔터티의 주식별자 속성으로 사용해도 되지만, 자식 엔터티에서 별도의 주식별자를 생성하는 것이 더 유리하다고 판단될 때, 비식별자 관계에 의한 외부 식별자로 표현한다.

### 식별자 관계로만 설정할 경우의 문제점
식별자 관계로만 관계를 맺을 경우에 SQL문의 복잡성이 올라가고, 조인 조건이 누락되는 실수가 발생할 확률이 높아집니다.

### 식별자 관계 VS 비식별자 관계
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/e4e0a9b6-1e2a-4220-ba0b-68ea3462119c" width="550" height="auto" />

---

### 문제풀이
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/4ade8b91-7077-422d-a66d-73f4498fab4c" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/17cf56e9-e043-40be-93cc-6b14f0ee34fe" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/882b0e9a-6401-42f8-9682-0cd5ede846a0" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/b9c7efb4-f436-469a-991a-e73cf02bd450" width="550" height="auto" />
<img src="https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/d834ed34-f57f-48cd-aecc-0dfa4ddd5d87" width="550" height="auto" />

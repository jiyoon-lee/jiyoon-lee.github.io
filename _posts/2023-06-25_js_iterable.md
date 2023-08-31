---
layout: single
title: "33장 Symbol"
categories: javascript
tag: [python, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
toc: true
---

# 34. 이터러블
## 34.1 이터레이션 프로토콜
- ES6에서 도입된 이터레이션 프로토콜은 순회 가능한 데이터 컬렉션(자료구조)를 문달기 위해 ECMAScript 사양에 정의하여 미리 약속한 규칙이다.
- ES6에서 순회 가능한 데이터 컬렉션을 이터레이션 프로토콜을 준수하는 이터러블로 통일하여 for...of문, 스프레드 문법, 배열 디스트럭처링 할당의 대상으로 사용할 수 있도록 일원화
- 이터레이션 프로토콜에는 이터러블 프로토콜과 이터레이터 프로토콜이 있다.
  - 이터러블 프로토콜
    - Well-known Symbol인 Symbol.iterator를 프로퍼티 키로 사용한 메서드를 직접 구현하거나 프로토타입 체인을 통해 상속받은 Symbol.iterator 메서드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터를 반환한다.
    - 이러한 규약을 이터러블 프로토콜이라 하면, 이터러블 프로토콜을 준수한 객체를 이터러블이라 한다.
    - 이터러블은 for...of 문으로 순회할 수 있으며 스프레드 문법과 배열 디스트럭처링 할당의 대상으로 사용할 수 있다.
  - 이터레이터 프로토콜
    - 이터러블의 Symbol.iterator 메서드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터를 반환한다.
    - 이터레이터는 next 메서드를 소유하며 next 메서드를 호출하면 이터러블을 순히하며 value와 done 프로퍼티를 갖는 이터레이터 리절트 객체르 반환
    - 이러한 규약을 이터레이터 프로토콜이라 하며, 이터레이터 프로토콜을 준수한 객체를 이터레이터라 한다.
    - 이터레이터는 이터러블의 요소를 탐색하기 위한 포인터 역할을 한다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/26e36e54-cf78-432e-b3fd-9d5b029df941)<br>

### 34.1.1 이터러블
- 이터러블 프로토콜을 준수한 객체를 이터러블이라 한다.
- 이터러블은 Symbol.iterator를 프로퍼티 키로 사용한 메서드를 직접 구현하거나 프로토타입 체인을 통해 상속받은 객체를 말한다.
- 이터러블인지 확인하는 함수는 다음과 같이 구현할 수 있다.
```
const isIterable = v => v !== null && typeof v[Symbol.iterator] === 'function';

isIterable([]); // true
isIterable(''); // true
isIterable(new Map()); // true
isIterable(new Set()); // true
isIterable({}); // false
```
배열은 Array.prototype의 Symbol.iterator 메서드를 상속받는 이터러블이다.
이터러블은 for...of문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링 할당의 대상으로 사용할 수 있다.
```
const array = [1, 2, 3];

// 배열은 Array.prototype의 Symbol.iterator 메서드를 상속받는 이터러블이다.
console.log(Symbol.iterator in array); // true

// 이터러블인 배열은 for...of 문으로 순회 가능하다.
for (const item of array) {
  console.log(item);
}

// 이터러블인 배열은 스프레드 문법의 대상으로 사용할 수 있다.
console.log([...array]); // [1, 2, 3]

const [a, ...rest] = array;
console.log(a, rest); // 1, [2, 3]
```
Symbol.iterator 메서드를 직접 구현하지 않거나 상속받지 않는 일반 객체는 이터러블 프로토콜을 준수한 이터러블이 아니다.
따라서 일반 객체는 for...of 문으로 순회할 수 없으며 스프레드 문법과 배열 디스트럭처링 할당의 대상으로 사용할 수 없다.
```
const obj = { a: 1, b: 2 };

// 일반 객체는 Symbol.iterator 메서드를 구현하거나 상속받지 않는다.
// 따라서 일반 객체는 이터러블 프로토콜을 준수한 이터러블이 아니다
console.log(Symbol.iterator in obj); // false

// 이터러블이 아닌 일반 객체는 for...of 문으로 순회할 수 없다.
for( const item of obj) {
  console.log(item); // typeError: obj is not iterable
}

// 이터러블이 아닌 일반 객체는 배열 디스터럭처링 할당의 대상으로 사용할 수 없다.
const [a, b] = obj; // TypeError: obj is not iterable
```
단, 2021년 1월 현재, TC39 프로세스으 stage4(Finished) 단계에 제안되어 있는 스프레드 프로퍼티 제안은 일반 객체에 스프레드 문법의 사용을 허용한다.
```
const obj = { a: 1, b: 2 };

// 스프레드 프로퍼티 제안(Stage 4)은 객체 리터럴 내부의 스프레드 문법의 사용을 허용한다.
console.log({ ...obj }); // { a: 1, b: 2 }
```
하지만, 일반 객체도 이터러블 프로토콜을 준수하도록 구현하면 이터러블이 된다.

### 34.1.2 이터레이터
- 이터러블의 Symbol.iterator 메서드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터를 반환한다.
- 이터러블의 Symbol.iterator 메서드가 반환한 이터레이터는 next메서드를 갖는다.<br>
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/02e5d7e9-6aa5-43e8-a50d-2e7c9b1144b0)
- 이터레이터의 next 메서드는 이터러블의 각 요소를 순회하기 위한 포인터 역할을 한다.
- 즉, next 메서드를 호출하면 이터러블을 순차적으로 한 단계씩 순회하며 순회 결과를 나타내는 이터레이터 리절트 객체를 반환한다.<br>
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/0ddcfcae-b83b-4ea6-bfd6-f2931b7a94ad)<br>
- 이터레이터의 next 메서드가 반환하는 이터레이터 리절트 객체의 value 프로퍼티는 현재 순회 중인 이터러블의 값을 나타내며 done 프로퍼티는 이터러블의 순회 완료 여부를 나타낸다.

## 34.2 빌트인 이터러블
- 자바스크립트는 이터레이션 프로토콜을 준수한 객체인 빌트인 이터러블을 제공한다.<br>
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/b8e45a67-4c2d-4949-8c3b-79af769412c2)<br>
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/05790279-e480-4ff5-9cc3-fe2b39b16d2d)

## 34.3 for...of문
- for...of 문은 이터러블을 순회하면서 이터러블의 요소를 변수에 할당한다. for...of 문의 문법은 다음과 같다.
```
for (변수선언문 of 이터러블) { ... }
```
- for...of 문은 for...in 문의 형식과 매우 유사하다
- for...in문은 객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로퍼티 중에서 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 true인 프로퍼티를 순회하며 열거한다.
- 이때 프로퍼티 키가 심벌인 프로퍼티는 열거하지 않는다.
- for...of 문은 내부적ㅇ로 이터러블의 next메서드를 호출하여 이터러블을 순회하며 next 메서드가 반환한 이터레이터 리절트 객체의 value 프로퍼티 값을 for...of 문의 변수에 할당
- 그리고 이터레이터 리절트 객체의 done 프로퍼티 값이 false이면 이터러블의 순회를 계속하고 true이면 이터러블의 순회를 중단한다.<br>
- ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cac29fe1-e070-4776-802a-c038895903e2)

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/ce981fa8-b6a9-49c2-a3c7-668e16646170)

## 34.4 이터러블과 유사 배열 객체
유사 배열 객체는 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체를 말한다.
유사배열 객체는 length 프로퍼티를 갖기 때문에 for문으로 순회할 수 있고, 인덱스를 나타내는 숫자 형식의 문자열을 프로퍼티 키로 가지므로 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있다.
유사 배열 객체는 이터러블이 아닌 일반 객체다. 따라서 유사 배열 객체에는 Symbol.iterator 메서드가 없기 때문에 for...of 문으로 순회할 수 없다.
ES6에서 이터러블이 도입되면서 유사 배열 객체인 arguments, NodeList, HTMLCollection 객체에 Symbol.iterator 메서드를 구현하여 이터러블이 되었다.
하지만 모든 유사 배열 객체가 이터러블인 것은 아니다. 다만 ES6에서 도입된 Array.from 메서드를 사용하여 배열로 간단히 변환할 수 있다.

## 34.5 이터레이션 프로토콜의 필요성
- 데이터 소비자: for...of 문, 스프레드 문법, 배열 디스트럭처링 할당
- 데이터 공급자: Array, String, Map, Set,,,
이터러블을 지원하는 데이터 소비자는 내부에서 Symbol.iterator 메서드를 호출해 이터레이터를 생성하고 이터레이터의 next 메서드를 호출하여 이터러블을 순회하며 이터레이터 리절트 객체를 바놘 그리고 이터레이터 리절트 객체의 value/done 프로퍼티 값을 취득

## 34.6 사용자 정의 이터러블
### 34.6.1 사용자 정의 이터러블 구현
- 이터레이션 프로토콜을 준수하지 않는 일반 객체도 이터레이션 프로토콜을 준수하도록 구현하면 사용자 정의 이터러블이 된다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/5f772511-1c54-4d96-9549-cb093d171944)
- 사용자 정의 이터러블은 이터레이션 프로토콜을 준수하도록 Symbol.iterator 메서드를 구현
- Symbol.iterator 메서드가 next 메서드를 갖는 이터레이터를 반환
- 이터레이터의 next 메서드는 done과 value 프로퍼티를 가지는 이터레이터 리절트 객체를 반환
- for...of문은 done 프로퍼티가 true가 될 때까지 반복하며 done프로퍼티가 true가 되면 반복을 중지

### 34.6.2 이터러블을 생성하는 함수
앞에서 살펴본 fibonacci 이터러블은 내부에 수열의 최대값 max를 가지고 있다.
이 수열의 최대값은 고정된 값으로 외부에서 전달한 값으로 변경할 방법이 없다는 아쉬움이 있다.
수열의 최대값을 외부에서 전달할 수 있도록 수정해 보자.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/12967bde-46e1-41a5-98d0-6d31454b4f1c)

### 34.6.3 이터러블이면서 이터레이터인 객체를 생성하는 함수
fibonacciFunc 함수는 이터러블을 반환한다. 만약 이터레이터를 생성하려면 이터러블의 Symbol.iterator 메서드를 호출해야 한다. 
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/9bb9d568-5e9b-48ca-bce6-67acd0a077d3)
이터러블이면서 이터레이터인 객체를 생성하려면 Symbo.iterator 메서드를 호출하지 않아도 된다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/d8279026-89a3-4187-ad18-73af5dd18890)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/8ab9cc08-3f5a-41ba-a90c-5d3b35761492)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/a420c125-4a64-43c1-9bc5-3c22526fe78a)

### 34.6.4 무한 이터러블과 지연 평가
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/fcce0f3e-5d0d-43d1-b630-aaa04fa9437d)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/05944275-eafb-4536-aac6-555f40f9a8bd)

- 배열이나 문자열 등은 모든 데이터를 메모리에 미리 확보한 다음 데이터를 공급한다. 하지만 위 예제의 이터러블은 지연 평가를 통해 데이터를 생성한다. 지연 평가는 데이터가 필요한 시점 이전까지는 미리 데이터를 생성하지 않다가 데이터가 필요한 시점이 되면 그때야 비로소 데이터를 생성하는 기법이다.




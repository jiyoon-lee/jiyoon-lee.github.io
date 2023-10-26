
태그의 종류
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/728b63d9-7882-4b56-9f77-0649e42e6640)

스크립트 태그는 HTML 코드에 자바 코드를 넣습니다.
JSP 페이지가 서블릿 프로그램에서 서블릿 클래스로 변환할 때 JSP 컨테이너가 자바 코드가 삽입되어 있는 스크립트 태그를 처리하고 나머지 HTML 코드나 일반 텍스트로 간주합니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/7014b49f-a227-407a-ab3a-ff270e7b857d)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/6bca7a60-e4bf-45a3-8527-e06718ea367e)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/23d30994-e81c-4d7f-8d8c-8f16bc656635)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/05812980-d723-4d8d-9331-0ab019f88b3f)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/08f17381-85bb-4b0f-a7e1-6c106b570288)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/a1953fec-1c7a-4457-9f5a-069814cd23a0)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/8194a0e9-d652-4864-b3fe-03fcc20e0713)


### 선언문 태그의 기능과 사용법
선언문 태그로 선언된 변수는 서블릿 프로그램으로 번역될 때 클래스 수준의 멤버 변수가 되므로 전역 변수로 사용됩니다.
반면 스클립틀릿 태그에서 변수를 선언하면 `_jspService()` 메소드 내부에 들어갑니다.

### 스크립틀릿 태그의 기능과 사용법
- 스크립틀릿 태그는 자바 코드로 이루어진 로직 부분을 표현합니다.
- 스크립틀릿 태그에 작성된 자바 코드는 서블릿 프로그램으로 변환될 때 `_jspService()`메소드 내부에 복사됩니다.
- 각 클라이언트의 요청에 대해 `_jspService()` 메소드가 호출되므로 이 메소드의 내부 코드가 클라이언트의 요청마다 실행되어야 하기 때문입니다.

### 표현문 태그의 기능과 사용법
- 선언문 태그 또는 스크립틀릿 태그에서 선언된 변수나 메소드의 반환 값을 외부로 출력할 수 있습니다.
- 표현문 태그에 작성된 모든 자바 코드의 값은 문자열로 변환되어 웹 브라우저에 출력됩니다.
  - 기본 데이터 타입은 `toString()`을 통해 출력
  - 자바 객체 타입은 `java.lang.Object` 클래스의 `toString()` 메소드를 사용하거나 자체에서 선언한 `toString()`을 사용하여 출력
    ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/98227c4c-a4a1-4b5b-9c87-38d4b13e3485)


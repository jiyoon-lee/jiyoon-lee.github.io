- SQL(← SEQUEL) (← Structured Query Language)
  - 관계형 데이터베이스에서 데이터 정의, 조작, 제어를 위해 사용하는 언어
  - 표준 SQL: ISO의 표준 규격을 따르는 SQL
  - SQL 기본 작성 규칙
    - 문장 마지막은 세미콜론(;)으로 끝남
    - 명령어, 객체명, 변수명은 대/소문자 구분이 없음
      - 데이터 값은 대/소문자를 구분함
    - 날짜와 문자열은 작은 따옴표를 사용
    - 단어와 단어 사이는 공백 또는 중바꿈으로 구분
    - 주석문
      - -- 이것은 주석입니다.
      - /* 여기서부터
        여기까지 주석입니다. */

## SQL 구문 유형
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/2b048e95-c36d-48c5-bd43-963bd0266403)


- 테이블에 대한 구조 확인
DESCRIBE [테이블명];
DESC [테이블명];

- SELECT
  - SELECT [ALL/DISTINCT] 칼럼1, 칼럼2, ... FROM [테이블명]
  - ALL: 중복 데이터 모두 출력 (default)
  - DISTINCT: 중복 데이터를 1건으로 출력
    - SELECT DISTINCT TEAM_ID, POSITION FROM PLYER; → TEAM_ID, POSITION의 조합에 대한 중복을 제거
  - 별칭 사용
    - 칼럼명과 별칭 사이의 AS 키워드를 사용(optional)
    - 별칭이 공백, 특수문자 등을 포함하는 경우 큰 따옴표 사용
  - ORDER BY
    - 출력시 정렬 기준 설정
    - SQL 문장의 맨 마지막에 위치
    - 오름차순: ASC(생략가능), 내림차순(DESC)
  - WHERE 절
    - 특정 조건을 만족하는 데이터를 한정하기 위해 사용
    ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/77ae4c46-71df-40e6-ae79-92d5e4463ac7)
    ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/6124884a-bae7-4a0d-bfed-17cc16da81f1)
    ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/986edec3-c0bc-498e-a711-e80e91152a4e)
  - 산술 연산자
    - NUMBER와 DATE 자료형에 대해 적용
    - *, /, +, -
    - 연산자는 SELECT 문에서도 사용 가능
  - 비교 연산자
    - =, <>, >=, >, <=, <
    - 모든 자료형에 대해 적용
    - 문자열의 크기 비교는 사전 순으로 수행됨
    - 예: '01' < '02' < '1' < '11' < '2'
    - NULL에는 비교 연산자는 사용 불가
  - 논리 연산자
    - 모든 자료형에 대해 적용
    - NOT, AND, OR(우선순위: NOT > AND > OR)
    ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/55184b8a-4b77-4d6a-b7d8-cb6b0862b392)
  - SQL 연산자
    - 합성(연결) 연산자 - 문자열과 문자열을 연결함
    - 방법1: CONCAT(str1, str2)
    - 방법2: str1 || str2
    - BETWEEN, NOT BETWEEN
    - LIKE
      - 문자열 비교 연산
      - 와일드카드 사용 가능
        - '%': 임의의 문자 N개/ '_': 임의의 문자 1개 

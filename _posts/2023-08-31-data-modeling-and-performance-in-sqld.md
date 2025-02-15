![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/f3f13750-c661-4f8e-8c21-bb2615481c2b)![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/bea7530e-e55e-41e8-9094-83047b9df9f8)# 4. 데이터 모델과 성능

## 4.1 성능 데이터 모델링의 개요
### 4.1.1 성능 데이터 모델링의 정의
- 데이터베이스 성능을 고려하여 데이터 모델링을 수행하는 것
  - 정규화, 반정규화, 테이블 통합 및 분할, 조인 구조, PK/FK 설정 등
- 수행 시점
  - 빠를 수록 좋음
    - 분석/설계 단계에서 성능 모델링 수행 -> 재업무 비용 최소화
  - 일반적인 경우
    - 대충 설계 -> 성능 저화 -> 해당 부분만 SQL 튜닝

- 성능 데이터 모델링의 순서
  - 정규화를 정확하게 수행
    - 주요 관심사별로 테이블을 분산시킴
  - 데이터베이스 용량산정 수행
    - 각 엔터티에 어느 정도의 트랜잭선이 들어오는지 파악
  - 데이터베이스에 발생되는 트랜잭션의 유형 파악
    - CRUD 매트릭스 활용
  - 용량과 트랜잭션의 유형에 따라 반정규화 수행
    - 테이블, 속성, 관계 변경
  - 이력모델의 조정, 인덱스를 고려한 PK/FK의 순서 조정, 수퍼타입/서브타입 조정 등 수행
    - 성능 관점에서 데이터 모델 최종 검증
   
- 관계형 모델 제약
  - 도메인 제약
    - 속성 값은 원자성을 가지며, 도메인에서 정의된 값이어야 함
  - 키 제약
    - 릴레이션의 모든 튜플은 서로 식별 가능해야 함
  - 개체 무결성 제약
    - 기본키는 NOT NULL & UNIQUE 이어야 함  
  - 참조 무결성 제약
    - FK는 NULL이거나 NULL이 아닌 경우 실제로 존재하는 값을 구성해야 

 - 정규화와 성능
   - 이상현상
     - 삭제 이상
     - 삽입 이상
     - 갱신 이상
   - 정규화
     - 목적: 삽입/삭제/갱신 이상현상 방지
     - 함수적 종속성(FD, Functional Dependency)에 기반
     - 종류
       - 1NF: 모든 값이 원자값을 가짐
       - 2NF: 부분함수종속 제거
       - 3NF: 이행함수종속 제거
     - 효과
       - 데이터 중복 감소 → 성능 향상
       - 데이터가 관심사별로 묶임 → 성능 향상
       - 조회 질의에서 조인이 많이 발생 → 성능 저하
       → 정규화를 통해 일반적으로 성능이 향상되나, 조회의 경우 처리 조건에 따라 성능이 향상되거나 저하됨  

- 반정규화의 정의
  - 반정규화(=역정규화 = Denormalization)
  - 정규화된 엔터티, 속성, 관계에 대해 성능 향상을 목적으로 중복, 통합, 분리를 수행하는 데이터 모델링 기법
    - cf) 비정규화: 정규화를 아예 수행하지 않음
  - 특징
    - 테이블, 칼럼, 관계의 반정규화를 종합적으로 고려해야 함
      - 일반적으로 속성(칼럼)의 중복을 시도함
    - 과도한 반정규화 → 데이터 무결성을 침해하게     
  - 반정규화의 사전 절차
  ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/5dff6da7-b503-43f0-bbf3-fcb99ef0ad16)
    - 다른 방법 유도
      - 뷰(View) 생성: 뷰 자체가 성능 향상을 가져오지 않음, 신중하게 설계뙨 뷰를 재사용할 때 성능 향상
      - 클러스터링: 자주 사용되는 테이블의 데이터를 디스크와 같은 블록에 저장
      - 인덱스의 조정: 인덱스 추가, 삭제 및 순서 조정
      - 응용 애플리케이션: 데이터 처리를 위한 로직 변경
  - 반정규화 기법 - 칼럼 반정규화
    - 중복칼럼 추가
      - 조인 횟수를 감소시키기 위해, 다른 테이블의 칼럼을 중복으로 저장함
    - 파생칼럼 추가
      - 값의 계산으로 인한 시간 지연을 줄이기 위해, 예상되는 값을 미리 계산하여 중복을 저장함(Derived Attribute)
    - 이력테이블칼럼 추가
      - 대량 이력 데이터 처리의 성능 향상을 위해 종료 여부, 최근값 여부 등의 칼럼을 추가로 저장
    - PK의 의미적 분리를 위한 칼럼 추가
      - PK가 복합 의미를 갖고 있는 경우 구성 요소 값의 조회 성능 향상을 위해 일반 속성을 추가함
      - 예) 차량번호가 '지역' + '일련번호로 구성된 경우 '지역' 일반속성 추가
    - 데이터 복구를 위한 칼럼 추가
      - 사용자의 실수 또는 응용프로그램 오류로 인해 데이터가 잘못 처리된 경우, 원래 값으로의 복구를 위해 이전 데이터를 임시적으로 중복 저장
  - 반정규화 기법 - 테이블 반정규화
    - 테이블 병합
      - 관계 병합
        - 1:1 또는 1:M 관계를 병합함 (두 테이블의 동시 조회가 많은 경우)
      - 슈퍼/서브타입 병합
        - 슈퍼/서브타입 관계를 병합함(one to on type → single type / plus type)
        ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/3942ef06-9daf-4633-8e6a-cb68582e26ba)
    - 테이블 분할
      - 수직 분할
        - 디스크 I/O의 분산을 위해 테이블을 칼럼 단위로 분리함
      - 수평 분할
        - 디스크 I/O의 분산을 위해 테이블을 로우 단위로 분리함
        - 테이블이 많은 양의 데이터를 가질 것으로 예상되는 경우 → Partitioning
          - Range Partition: 범위로 분할 (고객번호: 1 ~ 1000)
          - List Partition: 값으로 분할 (지역: 서울, 대구 등)
          - Hash Partition: 해쉬 함수로 분할
    - 테이블 추가
      - 중복 테이블 추가
        - 원격 조인(다른 업무 또는 다른 서버 간 조인)을 제거하기 위해 동일한 테이블 구조를 중복시킴(분산 DB 참고)
      - 통계 테이블 추가
        - SUM, AVG 등읠 통계깞을 미리 졔산하여 저장 (분산 DB 참고)
      - 이력 테이블 추가
        - 이력 테이블 중 일부 레코드를 마스크 테이블에서 중복 관리
      -  부분 테이블 추가
        - 하나의 테이블에서 집중적으로 이용되는 칼럼들만을 추출하여 별도의 테이블 생성 (테이블 수직분할과 유사하지만, 원본 테이블을 유지하면서 추가함)
    - 관계 반정규화
      - 중복관계 추가: 조인을 통해 정보 조회가 가능하지만, 조인 경로 단축을 위해 중복관계를 추가함
    - 인덱스
      - 검색 속도의 향상을 위해 기술 → 실제 테이블을 Full Scan하지 않고 인덱스 테이블을 검색
      - 지나치게 많은 인덱스 생성시 시간 및 공간 낭비
      - 인덱스된 필드의 업데이트시 시간 증가
      - 자동 생성(PK 또는 Unique 조건) / 수동 생성(Create Index 구문)
      - PK의 속성 순서대로 인덱스가 정렬됨
      - FK 인덱스 설정을 통한 성능 향

- 분산 데이터베이스의 개념
  - 물리적으로 분산된 데이터베이스를 하나의 논리적 시스템으로 사용
  - 분산 데이터베이스의 장단점
    ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/de9ec420-139f-460a-aac8-601fb99e50c3)
  - 분산 데이터베이스의 적용 기법
    1. 테이블 위치 분산: 테이블을 각각 다른 장소에 위치시킴
    2. 테이블 분할(Fragmentation) 분산: 각 테이블을 분할하여 분산함
    3. 테이블 복제(Replication) 분산
      - 동일 테이블의 복사본을 여러 서버에서 동시에 관리함
      - 부분 복제(Segment Replication)
        - 지사에서 먼저 데이터 발생 → 본사에서 전체 통
      - 광역 복제(Broadcast Replication)
        - 본사에서 데이터의 입력, 수정, 삭제 발생 → 지사에서 이를 반
    4. 테이블 요약 (Summarization) 분산
      - 유사한 내용의 데이터를 서로 다른 관점/수준에서 요약하여 분산 관리
      - 분석 요약(Rollup Replication)
        - 각 지사별 동일한 주제의 정보를 본사에서 통합하여 전체 요약 정보 산출
      - 통합 요약(Consolidation Replication)
        - 각 지사별 상이한 주제의 정보를 본사에서 단순 취합하여 제
  - 분산 설계 고려사항
    - 성능이 중요한 사이트에 적용해야 함
    - 공통코드, 기준정보, 마스터 데이터(핵심 데이터, 여러곳에서 사용하는 데이터) 등에 대해 분산 구성시 성능 향상
    - 실시간 동기화가요구되지 않을 때 바람직
      - Near Real Time(거의 실시간) 업무의 경우도 분산 환경 구성 가능
    - 특정 서버에 집중된 부하(네트워크 트레픽)를 분산시키기 위한 목적으로도 가능
    - 백업 사이트(Disaster Recovery Site) 구성 시 분산 설계의 개념을 적용할 수 있다.
      




## 4.1 성능 데이터 모델링의 개요
### 4.1.1 성능 데이터 모델링의 정의
데이터의 성능 향상을 목적으로, 데이터 모델 설계 시점부터 정규화, 반정규화, 테이블 통합, 테이블 분할, 조인 구조, PK, FK 등 여러 가지 성능과 관련된 사항들이 데이터 모델링 작업에 반영될 수 있도록 하는 것

### 4.1.2 성능 데이터 모델링 수행 시점
분석/설계 단계에서부터 데이터베이스의 처리 성능을 향상시킬 수 있는 방법을 주도면밀하게 고려해야 함.

### 4.1.3 성능 데이터 모델링 고려사항
- 데이터 모델링 시 정규화 작업을 수행한다.
- 데이터베이스의 용량을 산정한다.
- 데이터베이스에서 발생되는 트랜잭션의 유형을 파악한다.
- 데이터베이스 용량 및 트랜잭션의 유형에 따라 반정규화를 수행한다.
- 이력 데이터 모델의 조정, PK/FK 조정, 슈퍼/서브 타입 변환 조정 등을 수행한다.
- 성능 관점에서 데이터 모델을 검증한다.

## 4.2 정규화와 성능
### 4.2.1 정규화를 통한 성능 향상 전략
- 데이터를 결정하는 결정자에 의해 함수적 종속을 가지고 있는 일반 속성을 의존자로 하여 이력/수정/삭제 이상현상을 제거하는 것
- 중복 속성을 제거하고, 결정자에 의해 동일한 의미의 일반 속성이 하나의 테이블로 집약되도록 한 테이블의 데이터 용량을 최소화한다.

### 4.2.2 정규화 용어
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/83a48c5a-4db2-4eb8-b6e5-a13e909488d1)


### 4.2.3 정규화 효과 및 장점
- 상호 종속성이 강한 데이터 요소들을 분리, 독립된 개념(엔터티, 테이블)으로 정의하게 됨에 따라 높은 응집도 & 낮은 결합도 원칙에 충실, 유연성 극대화
- 재활용 가능성이 높아진다.
- 식별자가 아닌 속성이 한 번만 표현됨에 따라 중복이 최소화
- 데이터 품질이 확보 저장공간 절약, DML 처리 시 성능 향상

### 4.2.4 정규화 이론
1차, 2차, 3차, 보이스-코드 정규화는 함수 종속성에 근거하여 정규화를 수행하고, 4차 정규화는 속성의 값이 여러 개 발생하는 다치 종속, 5차 정규화는 조인에 의해 발생하는 이상현상 제거로 정규화를 수행
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cdbb2d93-5bbd-41ac-99df-381b90e63099)

### 4.2.5 제 1정규화
한 속성에 여러 개의 속성값을 갖거나 같은 유형의 속성이 여러 개인 경우 해당 속성을 분리시켜야 함.

### 4.2.6 제 2정규형
PK에 종속적이지 않거나 PK 중 일부 칼럼(들)에만 종속적인 칼럼은 분리되야 한다.

### 4.2.7 제 3정규화
일반 속섣을 간 종속 관계까 존재하는 것들은 분리되어야 한다.

### 4.2.8 정규화의 성능
- 정규화를 수행한 후, 전에 없었던 조인이 발생하게 되더라도 효율적인 인덱스 사용을 통해 조인 연산을 수행하면 성능상의 단점은 거의 없다.
- 정규화를 수행한 후, 적은 용량의 테이블이 생성된다면 조인 연산 시 적은 용량의 테이블을 먼저 읽어 조인을 수행하면 되므로 성능사 유리하다.
- 정규화가 제대로 되지 않으면 비슷한 종류의 속성이 여러 개가 되어 과도하게 많은 인덱스가 만들어질 수 있다. 정규화를 한다면 하나의 인덱스만 만들어도 된다.

## 4.3 반정규화와 성능
### 4.3.1 반정규화의 정의
시스템의 성능 향상 및 개발과 유지보수의 단순화를 위해 반정규화는 정규화된 데이터 모델을 분석하여 엔터티/속성/관계를 **중복, 통합, 분리** 등의 작업을 수행하는 모델링 기법
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/4367065b-3efb-4316-a72a-3edeedfc97c8)

### 4.3.3 반정규화 기법
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/79a71558-79e5-4959-a88c-bae26dd457f2)


![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/46d17350-fdfb-4afe-b1c5-2692b8e011bb)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/d527a39f-49b8-491b-8407-f12ea94b09f4)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/f1cf8c5a-cb42-44f6-8f17-af13c78ecce9)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cd842b47-dd40-43a9-8792-110444a10477)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cd4f5f09-35c2-49f5-8929-f41470ef1a3b)



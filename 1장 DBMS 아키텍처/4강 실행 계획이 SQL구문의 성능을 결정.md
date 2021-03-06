# 1장 DBMS 아키텍처
## 4강 실행 계획이 SQL구문의 성능을 결정

- 데이터양이 많은 테이블에 접근하거나 복잡한 SQL구문을 실행하면 반응 지연이 발생하는 경우가 꽤 있다.

1. 실행 계획 확인 방법
  - 테이블 풀 스캔의 실핼 계획
  - 인덱스 스캔의 실행 계획
  - 간단한 테이블 결합의 실행 계획
  
2. 테이블 풀 스캔의 실핼 계획
  - 조작 대상 객체
    - PostgreSQL은 on이라는 글자 뒤에, Oracle은 Name 필드에 출력
    - 여러개의 테이블을 사용하는 SQL 구문에서는 어떤 객체를 조작하는지 혼동하지 않게 주의가 필요하다.
    - 테이블 뿐만아니라 인덱스, 파티션, 시퀀스처럼 SQL구문으로 조작할 수 있는 객체라면 무엇이든 올 수 있다.
  - 객체에 대한 조작의 종류
    - 객체에 대한 조작의 종류는 실행 계획에서 가장 중요한 부분이다.
    - PostgreSQL : Seq scan 순차적으로 접근해서 해당 테이블의 데이터 전체를 읽어낸다.
    - Oracle : TABLE ACCESS FULL 테이블의 데이터를 전부 읽어드린다.
    - PostgreSQL의 출력이 조금더 물리적 차원에 가깝다.
    - Oracle도 내부적으로는 시퀀셜 스캔을 수행하므로 같다고 생각해도 무방하다.
  - 조작 대상이 되는 레코드 수
    - 각 조작에서 얼마만큼의 레코드가 처리되는지가 SQL 구문 전체의 실행 비용을 파악하는 데 중요한 지표가 된다.
3. 인덱스 스캔의 실행 계획
  - 접근 대상 객체와 조작
    - PostgreSQL : index Scan
    - Oracle : INDEX UNIQUE SCAN
    - 일반적으로 스캔하는 모집합 레코드 수에서 선택되는 레코드 수가 적다면 테이블 풀 스캔보다 빠르게 접근을 수행한다.
    - 풀 스캔이 모집합의 데이터양에 비례해서 처리 비용이 늘어나는 것에 비해
    - 인덱스를 사용할 때 활용되는 B-tree가 모집합의 데이터양에 따라 대수 함수적으로 처리 비용이 늘어가기 때문이다.
    - 풀 스캔 보다 효율적이다.
4. 간단한 테이블 결합의 실행 계획
  - Nested Loops : 한쪽 테이블을 읽으면서 레코드 하나마다 결합 조건에 맞는 레코드를 다른 쪽 테이블에서 찾는 방식이다.
  - 만약 절차지향적 언어로 구현한다면 이중 반복으로 구현되기 때문에 중첩 반복이라고 이름이 붙여졌다.
  - Sort Merge : 결합 키를 레코드를 정렬하고, 순차적으로 두 개의 테이블을 결합하는 방법
  - Hash : 결합 키값을 해시값으로 매핑하는 방법이다.
    

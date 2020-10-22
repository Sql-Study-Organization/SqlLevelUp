
# 2장 SQL 기초

## 6강 SELECT 구문

데이터베이스를 이용하는 때 핵심이 되는 처리가 `검색`이다.  질의(query), 추출(retrieve) 라고도 부름

- Select 구문에는 데이터를 `어떤 방법으로` 선택할지 일절 쓰여있지 않다
- `방법`은 DBMS에게 맡긴다

### WHERE 구

엑셀의 `필터 조건`과 같다. WHERE은 어디?의 뜻이 아닌 `~라는 경우` 관계부사


|연산자|의미|
|------|---|
|=|~ 와 같음|
|<>|~ 와 같지 않음|
|>=|~ 이상|
|>|~ 보다 큼|
|<=|~ 이하|
|<|~ 보다 작음|
  
</BR>

- IN
- OR
- NULL : 데이터가 없다는 의미로, 데이터값이 아니기 때문에 = 연산자를 사용할 수 없다.
    - IS NULL : NULL인지 확인하는 키워드
    - IS NOT NULL : NULL이 아닌지 확인하는 키워드
  
### GROUP BY 구

합계 또는 평균 등의 집계 연산을 SQL 구문으로 할 수 있음

- COUNT
- SUM
- AVG
- MAX
- MIN

### HAVING 구

WHERE 구가 `레코드` 에 조건을 지정한다면, HAVING 구는 `집합` 에 조건을 지정하는 기능

### ORDER BY 구

- DESC (Descending Order)
- ASC (Ascending Order)

## 조건분기, 집합 연산, 윈도우 함수, 갱신

### CASE 식

절차 지향형 프로그래밍 언어의 `SWITCH` 조건문과 거의 비슷

- UNION : 합집합
- INTERSECT : 교집합
- EXCEPT : 차집합

### 윈도우 함수

집약 기능이 없는 GROUP BY 구

GROUP BY : 자르기 + 집약

윈도우 함수는 `자르기` 에 해당

윈도우 함수의 기본적인 구문은 집약 함수 뒤에 OVER 구를 작성하고, 내부에 자를 키를 지정하는 PARTITION BY 또는 ORDER BY를 입력
Problem Domain

1. 소비자가 상품을 선택하여 구매하는 시스템을 만들고 싶다.



USDP - 보편적인 방법론

수집

분석

설계

| 후보명 | 제거이유 |          |
| ------ | -------- | -------- |
| 소비자 |          | 소비자   |
| 상품   |          | 상품     |
| 온라인 | 용어     |          |
| 구매   |          | 구매     |
| 시스템 |          | 이름     |
| ...    |          | 주소     |
|        |          | 전화번호 |

- 기준
  - 영속성: 반복해서 이전 상황을 지속해야하는 것
- 설계: 상관관계를 도출해 내는 것
- CRUD 조작기술을 배운다고하여 DB(MySQL)의 조작능력을 얻는 것은 아니다!
  (DB 조작능력은 별개의 능력 - SQL 언어)
- 설계 중 변경이 필요하여 수집, 분석 단계로 돌아가게되면.. 30~60% 시간이 더 소비된다.

구현

테스트



**SQL: Structure Query Language**



### DBMS(DataBase Management System)

모델링 - 설계 - 구현



* 모델링은 수집단계에서 시작해야한다.
* 

관계형 DB (Relation DBMS)

1. Oracle
2. MySQL
3. MSSQL
4. PostgreSQL
5. DB2
6. ...

* 전통적인(오래지속된) DB들은 대부분이 R-DB이다.





NoSQL 시대 (Not only SQL)

* 데이터의 형식이 변하면서 저장하는 방식 또한 변경되어야 한다.
* UCC같은 영상 데이터들.. Web의 특성을 가지고 있는 데이터들 등...
* Relation 외의 DB ( DB Rank: https://db-engines.com/en/ranking )
  * Document
  * Search Engine
  * Wide column
  * Graph
  * Key Value
  * ...

MongoDB - 집어넣는대로 시작.. 쌓이게되면 정보관리가 어려워 진다.
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



####Tips 

DB기능 설계: 방법론 없이. 애자일 방식 (Fair or Single에 적합)



데이터를 만들어가면서 수정하는 일이 많아 질 수 있다.

그래서.

* NULL을 우선 허용한다.
* 제약은 주지 않는다.



### auto_increment 초기화

alter table [table name] auto_increment=[값];

- **단! 값은 auto_increment가 적용되어 생성된 최종 값보다 작을 수 없다.**



### Join

![img](http://rapapa.net/wp/wp-content/uploads/2012/06/Visual_SQL_JOINS_V2.png)

참조 사이트: http://rapapa.net/?p=311

* 동일한 컬럼 값을 가진 Select 표시

  ```
  SELECT Orders.OrderID, Customers.CustomerName
  FROM Orders
  INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
  ```

  



### MySQL View Table

1. #####Create View

   ```
   CREATE VIEW [테이블명] AS SELECT
   D1.[D1의 컬럼명] AS '[새로 지정할 컬럼이름]',
   D1.nMoney AS 'Money',
   D2.strJukyo AS 'Jukyo',
   FROM_UNIXTIME(D1.nDate) AS 'Date'
   FROM [테이블명1] AS D1 INNER JOIN
   [테이블명2] AS D2
   ON (D2.idx = D1.idx);
   ```

   **출처: https://jepi.tistory.com/129 [jepi free programming]**

2. ##### Alter View

   ```
   ALTER VIEW 뷰_이름 AS SELECT 칼럼_이름 FROM 테이블_이름;
   ```

   출처: https://recoveryman.tistory.com/181 [회복맨 블로그]
   사용해 보았지만.. view 테이블 망가짐. (정확한 사용법 숙지 필요)

3. 









### Sequelize View

참고 사이트
**http://webframeworks.kr/tutorials/expressjs/expressjs_orm_one/**



#### Sequelize View Table

* 어렵다… 사용 못함… 누가 알려줬으면...

**출처: https://github.com/abelosorio/sequelize-views-support**







create view patientsview as

select t1.email_id as 'email',

t1.name as 'name',

t1.gender as 'gender',

t2.tel as 'telnumber',

t2.disease as 'disease',

t2.createdAt as 'treatdate',

from users as t1 inner join patientsinfos as t2

 on (t1.tel = t2.tel);
# 사혼의구슬조각마냥 흩어진 개념들을 

# 빠르게 그리고 정확히 다시 모으자..! 

# 취직해야지..! 더이상 미루는건 없다! 벼랑끝이다.



## 20220521_TIL

#### **데이터베이스와 데이터베이스 관리 시스템**

-   Q> 데이터베이스와 데이터베이스 관리 시스템을 어린이도 알 수 있을 정도로 설명해주세요.
-   A> 도서관에 있는 책들이 데이터베이스라고 한다면, 도서관 사서분들이나 도서 정보를 찾아주는 컴퓨터를 DBMS라고 볼 수 있습니다.



#### **데이터베이스의 기본개념 (정의)**

-   데이터의 집합 (a Set of Data)
-   여러 응용 시스템(프로그램)들의 통합된 정보들을 저장하여 운영할 수 있는 공용(share) 데이터의 집합
-   효율적으로 저장, 검색, 갱신할 수 있도록 데이터 집합들끼리 연관시키고 조직화되어야 한다.



#### **데이터베이스의 특성**

-   실시간 접근성(Real-time Accessability)
    \- 사용자의 요구를 즉시 처리할 수 있다.

-   계속적인 변화(Continuous Evolution)
    \- 정확한 값을 유지하려고 삽입·삭제·수정 작업 등을 이용해 데이터를 지속적으로 갱신할 수 있다.

-   동시 공유성(Concurrent Sharing)
    \- 사용자마다 서로 다른 목적으로 사용하므로 동시에 여러 사람이 동일한 데이터에 접근하고 이용할 수 있다.

-   내용 참조(Content Reference)
    \- 저장한 데이터 레코드의 위치나 주소가 아닌 사용자가 요구하는 데이터의 내용, 즉 데이터 값에 따라 참조할 수 있어야 한다.



#### **데이터베이스 관리 시스템 (Database Management System = DBMS)**

-   데이터베이스를 관리하는 소프트웨어
-   여러 응용 소프트웨어(프로그램) 또는 시스템이 동시에 데이터베이스에 접근하여 사용할 수 있게 한다
-   필수 3기능
    \- 정의기능 :  데이터 베이스의 논리적, 물리적 구조를 정의
    \- 조작기능 : 데이터를 검색, 삭제, 갱신, 삽입, 삭제하는 기능
    \- 제어기능 :  데이터베이스의 내용 정확성과 안전성을 유지하도록 제어하는 기능
-   Oracle, SQL Server, MySQL, DB2 등의 상용 또는 공개 DBMS가 있다.

  

#### **데이터베이스 관리 시스템의 장/단점**

-   장점
    \- 데이터 중복이 최소화
    \- 데이터의 일관성 및 무결성 유지 
    \- 데이터 보안 보장
-   단점
    \- 운영비가 비싸다
    \- 백업 및 복구에 대한 관리가 복잡
    \- 부분적 데이터베이스 손실이 전체 시스템을 정지

***

#### **MySQL_MAC_OS** >>>> [MySQL DOC](https://dev.mysql.com/doc/refman/5.7/en/create-database.html)

1.   설치

`brew install mysql`

2.   실행

`mysql.server start`

3.   종료

`mysql.server stop`

#### **운영체제의 백그라운드로 MySQL이 계속 실행되도록 하고싶다면?**

*   `brew services start mysql` 데몬형태로 실행
*   `brew services restart mysql` 서비스 재시작
*   `brew services stop mysql`서비스 종료
*   `brew services list`데몬으로 실행되고 있는 프로그램 리스트 

#### **SQL(Structured Query Language)**

-   SQL은 데이터를 보다 쉽게 검색하고 추가, 삭제, 수정 같은 조작을 할 수 있도록 고안된 컴퓨터 언어입니다.
-   관계형 데이터베이스에서 데이터를 조작하고 쿼리하는 표준 수단입니다.
-   DML (Data Manipulation Language): 데이터를 조작하기 위해 사용합니다.
    INSERT, UPDATE, DELETE, SELECT 등이 여기에 해당합니다.
-   DDL (Data Definition Language): 데이터베이스의 스키마를 정의하거나 조작하기 위해 사용합니다.
    CREATE, DROP, ALTER 등이 여기에 해당합니다.
-   DCL (Data Control Language) : 데이터를 제어하는 언어입니다.
    권한을 관리하고, 테이터의 보안, 무결성 등을 정의합니다.
    GRANT, REVOKE 등이 여기에 해당합니다.

#### **MySQL 관리자 계정인 root로 데이터베이스 관리 시스템에 접속**

`mysql -u root -p`

#### **DATABASE 생성하기**

`create database "DB이름"`

#### **DATABASE CREATE USER**

`CREATE USER connectuser@localhost IDENTIFIED BY 'connect123!@#';`

#### **GIVE PRIVILEGES TO USER**

`GRANT ALL PRIVILEGES ON connectdb.* TO 'connectuser'@'localhost';`

#### **MAKING DBMS ACCEPTION**

`FLUSH PRIVILEGES;`

#### **ACCESS TO DB WITH USER**

`mysql -h 127.0.01 -u "USER NAME" -p "DB NAME";` then type password.

If U R using UR laptop -h will be 127.0.0.1

#### **GET MySQL VERSION AND CURRENT DATE**

`SELECT VERSION(), CURRENT_DATE;`

#### **IMPORT sql file to DB at specific user**

`mysql -u "USERNAME" -p "DBNAME" < "FILENAME.sql";` then type password.

#### **CHECKING TABLE'S STRUCTURE**

`desc "TABLENAME";`

#### **데이터 조작어 DML**

*   SELECT

    *   CONCAT - 컬럼을 설정한 문자열로 이어붙여 나오게 해준다.

    `SELECT CONCAT(name, '-', job, '*', salary, 'TEST', boss) 테스트중 from employee;`

    *   LIKE - '%'는 0에서부터 여러 개의 문자열을 나타냄, '_'는 단 하나의 문자를 나타내는 와일드 카드
    *   UPPER(), LOWER()

    `SELECT UPPER(NAME)FROM TABLE`, `SELECT LOWER(NAME) FROM TABLE`

    *   SUBSTRING(문자열, 시작인덱스, 몇글자까지)
    *   LPAD, RPAD

    `SELECT LPAD('HI',5,'?'), RPAD('DAN',10,'K')`

    -   FLOOR(x) : x보다 크지 않은 가장 큰 정수를 반환합니다. BIGINT로 자동 변환합니다.
    -   CEILING(x) : x보다 작지 않은 가장 작은 정수를 반환합니다.
    -   ROUND(x) : x에 가장 근접한 정수를 반환합니다.
    -   POW(x,y) POWER(x,y) : x의 y 제곱 승을 반환합니다.
    -   GREATEST(x,y,...) : 가장 큰 값을 반환합니다.
    -   LEAST(x,y,...) : 가장 작은 값을 반환합니다.
    -   CURDATE(),CURRENT_DATE : 오늘 날짜를 YYYY-MM-DD나 YYYYMMDD 형식으로 반환합니다.
    -   CURTIME(), CURRENT_TIME : 현재 시각을 HH:MM:SS나 HHMMSS 형식으로 반환합니다.
    -   NOW(), SYSDATE() , CURRENT_TIMESTAMP : 오늘 현시각을 YYYY-MM-DD HH:MM:SS나 YYYYMMDDHHMMSS 형식으로 반환합니다. 
    -   DATE_FORMAT(date,format) : 입력된 date를 format 형식으로 반환합니다.
    -   PERIOD_DIFF(p1,p2) : YYMM이나 YYYYMM으로 표기되는 p1과 p2의 차이 개월을 반환합니다.

*   INSERT

*   UPDATE

    `UPDATE 테이블명 SET 필드1=필드1의값, 필드2=필드2의값... WHERE 조건식`

*   DELETE

​	`DELETE FROM 테이블명 WHERE 조건식`

#### **데이터 정의어 DDL**

*   컬럼추가

    `alter table 테이블명 add  필드명 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT];`

*   컬럼삭제

​	`alter table 테이블명 drop 필드명`

*   테이블 이름 변경

​	`alter table  테이블명 rename 변경이름`

***

### Maven

애플리케이션을 개발하기 위해 반복적으로 진행해왔떤 작업들을 지원하기 위하여 등장한 도구이다. 이것으로 빌드, 패키징, 문서화, 테스트, 의존성관리 등 형상관리서버와 연동, 배포등의 작업을 손쉽게 할 수 있다.

Maven 전에 CoC를 알아야하는데, 이것을 예를 들자면 프로그램의 소스파일은 어떤 위치에 있어야 하고, 소스가 컴파일된 파일들은 어떤 위치에 있어야하는지를 미리 정해놨다는 것이다.

Maven을 사용함으로써 설정 파일에 몇 줄 적어서, 직접 다운로드 받거나 하지 않아도 라이브러리를 사용할 수 있다.

또한 Maven에 설정한 대로 모든 개발자가 일관된 방식으로 빌드를 수행할 수 있다. 

***

### JDBC - Java Database Connectivity

*   자바를 이용한 데이터베이스 접속과 SQL 문장의 실행, 그리고 실행 결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 관한 규악

#### **JDBC를 이용한 프로그래밍 방법**

1.  import java.sql.*;
2.  드라이버를 로드 한다.
3.  Connection 객체를 생성한다.
4.  Statement 객체를 생성 및 질의 수행
5.  SQL문에 결과물이 있다면 ResultSet 객체를 생성한다.
6.  모든 객체를 닫는다.

![](https://cphinf.pstatic.net/mooc/20180201_49/1517475141729UGWfv_PNG/2_11_1_JDBC_.PNG)
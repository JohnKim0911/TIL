# SQLD 이론교재 - Keyword 요약

## 📌 1과목 : `데이터모델링의 이해`

### ✅ Part 1.데이터 모델링의 이해

#### ✔️ 1-1. 데이터 모델의 이해

##### 🔵 모델링의 개념

##### 🔵 모델링의 특징
- 단순화
- 추상화
- 명확화

##### 🔵 데이터 모델링 3가지 관점
- 데이터 관점
- 프로세스 관점
- 데이터와 프로세스 관점

##### 🔵 데이터 모델링 유의점
- 중복
- 비유연성
- 비일관성

##### 🔵 데이터 모델링 3가지 요소
- 대상
- 속성
- 관계

##### 🔵 데이터 모델링의 3단계
- 개념적 모델링
- 논리적 모델링
- 물리적 모델링

##### 🔵 스키마의 3단계 구조
- 외부 스키마
- 개념 스키마
- 내부 스키마
- 3단계 스키마의 독립성
  - 논리적 독립성
  - 물리적 독립성

##### 🔵 데이터 모델의 표기법 (ERD)

##### 🔵 ERD 작성 절차 (6단계)

#### ✔️ 1-2. 엔터티(Entity)

##### 🔵 엔터티의 개념
- 엔터티
- 속성
- 식별자
- 인스턴스

##### 🔵 엔터티의 특징
- 유일한 식별자에 의해 식별 가능
- 해당 업무에 필요하고 관리하고자 하는 정보
- 인스턴스의 집합
- 엔터티는 반드시 속성을 가짐
- 엔터티는 업무 프로세스에 의해 이용
- 다른 엔터티와 최소 1개 이상의 관계 성립

##### 🔵 엔터티의 분류
- 유형과 무형에 따른 분류
  - 유형 엔티티
  - 개념 엔티티
  - 사건 엔티티
- 발생 시점에 따른 분류
  - 기본 엔티티
  - 중심 엔티티
  - 행위 엔티티

##### 🔵 엔터티의 명명

##### 🔵 엔터티와 인스턴스 표기법
- 엔터티와 인스턴스
- 엔터티 표기법
  - IE 표기법
  - Baker 표기법

#### ✔️ 1-3. 속성

##### 🔵 속성의 개념

##### 🔵 엔터티, 인스턴스, 속성, 속성값의 관계

##### 🔵 속성의 특징

##### 🔵 함수적 종속성
- 완전 함수적 종속
- 부분 함수적 종속

##### 🔵 속성의 분류
- 속성의 특성에 따른 분류
  - 기본 속성
  - 설계 속성
  - 파생 속성
- 엔터티 구성방식에 따른 분류
  - PK
  - FK
  - 일반 속성
- 분해 여부에 따른 속성
  - 단일 속성
  - 복합 속성
  - 다중값 속성

##### 🔵 속성의 명명규칙

##### 🔵 도메인(Domain)

#### ✔️ 1-4. 관계

##### 🔵 관계의 개념

##### 🔵 관계의 종류
- 존재적 관계
- 행위적 관계

##### 🔵 관계의 구성
- 관계명
- 차수 (Cardinality)
- 선택성 (Optionality)

##### 🔵 관계의 차수
- 1 대 1 관계
  - 완전 1 대 1 관계
  - 선택적 1 대 1 관계
- 1 대 N 관계
- N 대 N 관계

##### 🔵 관계의 페어링
- 관계의 차수, 페어링 차이

#### ✔️ 1-5. 식별자

##### 🔵 식별자의 개념

##### 🔵 주식별자 특징
- 유일성
- 최소성
- 불변성
- 존재성

##### 🔵 식별자 분류
- `대표성 여부`에 따른 식별자의 종류
  - 주 식별자
  - 보조 식별자
- `생성 여부`
  - 내부 식별자
  - 외부 식별자
- `속성 수`
  - 단일 식별자
  - 복합 식별자
- `대체 여부`
  - 본질 식별자 (원조 식별자)
  - 인조 식별자

##### 🔵 식별자 표기법
- IE 표기법
- Barker 표기법

##### 🔵 주식별자 도출기준
- 해당 업무에서 자주 이용되는 속성을 주식별자로 지정
- 명칭이나 내역 등과 같은 이름은 피함
- 속성의 수를 최대한 적게 구성

##### 🔵 관계간 엔터티 구분
- 강한 개체
- 약한 개체

##### 🔵 식별관계와 비식별관계
- 식별관계
- 비식별관계

##### 🔵 Key의 종류
- 기본키
- 후보키
- 슈퍼키
- 대체키
- 외래키

### ✅ Part 2. 데이터 모델과 SQL

#### ✔️ 1-6. 정규화

##### 🔵 정규화의 개념

##### 🔵 이상현상 (Abnormality)

##### 🔵 정규화 단계
- 제 1 정규화
- 제 2 정규화
- 제 3 정규화
- BCNF(Boyce-Codd Normal Form) 정규화
- 제 4 정규화
- 제 5 정규화

##### 🔵 반정규화(역정규화)의 개념

##### 🔵 반정규화 수행 케이스

#### ✔️ 1-7. 관계와 조인의 이해

##### 🔵 관계의 개념

##### 🔵 관계의 분류

##### 🔵 조인의 의미

##### 🔵 계층형 데이터 모델

##### 🔵 상호배타적 관계

#### ✔️ 1-8. 모델이 표현하는 트랜잭션의 이해

##### 🔵 트랜젝션이란

##### 🔵 필수적, 선택적 관계와 ERD
- IE 표기법
- Barker 표기법

#### ✔️ 1-9. Null 속성의 이해

##### 🔵 NULL이란

##### 🔵 NULL의 특성
- NULL을 포함한 연산 결과는 항상 NULL
- 그룹 함수는 NULL을 제외하고 연산을 수행한다.

##### 🔵 NULL의 ERD 표기법
- IE 표기법: Null 허용여부 알 수 없음
- Barker 표기법: 동그라미로 Null 허용 속성 나타냄

#### ✔️ 1-10. 본질식별자 vs 인조식별자

##### 🔵 식별자 구분
- 본질 식별자
- 인조 식별자


## 📌 2과목 : SQL 기본 및 활용

### ✅ Part 1. `SQL 기본`

#### ✔️ 2-1. 관계형 데이터베이스 개요

##### 🔵 데이터베이스와 DBMS
- 데이터베이스
- DBMS

##### 🔵 관계형 데이터베이스 구성 요소
- 계정
- 테이블
- 스키마

##### 🔵 테이블
- 정의
- 특징

##### 🔵 SQL

##### 🔵 관계형 데이터베이스 특징

##### 🔵 테이터 무결성

##### 🔵 테이터 무결성 종류
- 개체 무결성
- 참조 무결성
- 도메인 무결성
- NULL 무결성
- 고유 무결성
- 키 무결성

##### 🔵 ERD

#### ✔️ 2-2. SELECT 문

##### 🔵 SQL 종류

| 구분  | 종류                            |
|-----|-------------------------------|
| DDL | CREATE, ALTER, DROP, TRUNCATE |
| DML | INSERT, DELETE, UPDATE, MERGE |
| DCL | GRANT, REVOKE                 |
| TCL | COMMIT, ROLLBACK              |
| DQL | SELECT                        |

##### 🔵 SELECT 문 구조

##### 🔵 SELECT 절

##### 🔵 컬럼 Alias (별칭)

##### 🔵 특징 및 주의사항

##### 🔵 FROM 절

#### ✔️ 2-3. 함수

##### 🔵 함수 정의

##### 🔵 함수기능

##### 🔵 함수의 종류

##### 🔵 입/출력값의 타입에 따른 함수 분류

- 문자형 함수
  - `LOWER(대상)`
  - `UPPER(대상)`
  - `SUBSTR(대상, m, n)`
  - `INSTR(대상, 찾을 문자열, m, n)`
  - `LTRIM(대상, 삭제문자열)`
  - `RTRIM(대상, 삭제문자열)`
  - `TRIM(대상)`
  - `LPAD(대상, n, 문자열)`
  - `RPAD(대상, n, 문자열)`
  - `CONCAT(대상1, 대상2)`
  - `LENGTH(대상)`
  - `REPLACE(대상, 찾을문자열, 바꿀문자열)`
  - `TRANSLATE(대상, 찾을문자열, 바꿀문자열)`

- 숫자형 함수
  - `ABS(숫자)`
  - `ROUND(숫자, 자리수)`
  - `TRUNC(숫자, 자리수)`
  - `SIGN(숫자)`
  - `FLOOR(숫자)`
  - `CEIL(숫자)`
  - `MOD(숫자1, 숫자2)`
  - `POWER(m, n)`
  - `SQRT(숫자)`

- 날짜형 함수
  - `SYSDATE`
  - `CURRENT_DATE`
  - `CURRENT_TIMESTAMP`
  - `ADD_MONTHS(날짜, n)`
  - `MONTHS_BETWEEN(날짜1, 날짜2)`
  - `LAST_DAY(날짜)`
  - `NEXT_DAY(날짜, n)`
  - `ROUND(날짜, 자리수)`
  - `TRUNC(날짜, 자리수)`

- 변환함수
  - `TO_NUMBER(문자)`
  - `TO_CHAR(대상, 포맷)`
  - `TO_DATE(문자, 포맷)`
  - `FORMAT(날짜, 포맷)`
  - `CAST(대상 AS 데이터타입)`

- 그룹함수
  - `COUNT(대상)`
  - `SUM(대상)`
  - `AVG(대상)`
  - `MIN(대상)`
  - `MAX(대상)`
  - `VARIANCE(대상)`
  - `STDDEV(대상)`

- 일반함수
  - `decode(대상, 값1, 리턴1, 값2, 리턴2, ..., 그외리턴)`
  - `NVL(대상, 치환값)`
  - `NVL2(대상, 치환값1, 치환값2)`
  - `COALESCE(대상1, 대상2, ..., 그외리턴)`
  - `ISNULL(대상, 치환값)`
  - `NULLIF(대상1, 대상2)`
  - `CASE문`

#### ✔️ 2-4. WHERE 절

##### 🔵 WHERE 절

##### 🔵 IN 연산자

##### 🔵 BETWEEN A AND B 연산자

##### 🔵 LIKE 연산자

##### 🔵 NOT 연산자

#### ✔️ 2-5. GROUP BY, HAVING 절

##### 🔵 GROUP BY 절

##### 🔵 HAVING 절

#### ✔️ 2-6. ORDER BY 절

##### 🔵 ORDER BY 절

##### 🔵 정렬 순서 (오름차순)

##### 🔵 복합 정렬

##### 🔵 NULL 의 정렬

#### ✔️ 2-7. 조인

##### 🔵 JOIN(조인)

##### 🔵조인 종류
- 조건의 형태에 따라
  - `EQUI JOIN(등가 JOIN)`
  - `NON EQUI JOIN`
- 조인 결과에 따라
  - `INNER JOIN`
  - `OUTER JOIN`
- `NATURAL JOIN`
- `CROSS JOIN`
- `SELF JOIN`

##### 🔵 EQUI JOIN(등가 JOIN)

##### 🔵 NON-EQUI JOIN

##### 🔵 세 테이블 이상의 조인

##### 🔵 SELF JOIN

#### ✔️ 2-8. 표준 조인

##### 🔵 표준조인
- ANSI 표준
  - `INNER JOIN`
  - `CROSS JOIN`
  - `NATURAL JOIN`
  - `OUTER JOIN`

##### 🔵 INNER JOIN

##### 🔵 ON 절

##### 🔵 USING 조건절

##### 🔵 NATURAL JOIN

##### 🔵 CROSS JOIN

##### 🔵 OUTER JOIN
- OUTER JOIN 종류
  - LEFT OUTER JOIN
  - RIGHT OUTER JOIN
  - FULL OUTER JOIN
- ORACLE 표준
- ANSI 표준
### ✅ Part 2. `SQL 활용`

#### ✔️ 2-9. 서브 쿼리

##### 🔵 서브쿼리

##### 🔵 서브쿼리 사용 가능한 위치

##### 🔵 서브쿼리 종류
- 동작하는 방식에 따라
  - 비연관 서브쿼리
  - 연관 서브쿼리
- 위치에 따라
  - 스칼라 서브쿼리
  - 인라인뷰
  - WHERE 절 서브쿼리

##### 🔵 WHERE 절 서브쿼리 종류
- 단일행 서브쿼리
  - 연산자
    - `=`, `>`, `>=`, `<`, `<=`
    - `<>`: 같지 않다
- 다중행 서브쿼리
  - 다중행 서브쿼리 연산자
    - `IN`
    - `ANY`
    - `ALL`
    - `EXISTS`
    - `NOT EXISTS`

- 다중컬럼 서브쿼리
- 상호연관 서브쿼리

##### 🔵 ALL과 ANY 비교

##### 🔵 EXISTS / NOT EXISTS 연산자

##### 🔵 인라인뷰(Inline View)

##### 🔵 스칼라 서브쿼리

##### 🔵 서브쿼리 주의사항

#### ✔️ 2-10. 집합 연산자

##### 🔵 집합 연산자

##### 🔵 합집합
- `UNION`
- `UNION ALL`

##### 🔵 교집합

##### 🔵 차집합

##### 🔵 집합 연산자 사용시 주의 사항

#### ✔️ 2-11. 그룹 함수

##### 🔵 그룹함수

##### 🔵 COUNT

##### 🔵 SUM

##### 🔵 AVG

##### 🔵 MIN / MAX

##### 🔵 VARIANCE / STDDEV

##### 🔵 GROUP BY FUNCTION
- `GROUPING SET(A, B, ...)`
- `ROLLUP(A, B)`
- `CUBE(A, B)`

#### ✔️ 2-12. 윈도우 함수

##### 🔵 WINDOW FUNCTION

##### 🔵 윈도우 함수의 형태
- `SUM OVER()`
- `AVG OVER()`
- `MIN/MAX OVER()`
- `COUNT`

##### 🔵 윈도우 함수 연산 대상 및 범위
- `ROWS|RANGE BETWEEN A AND B`
- 연산 대상
  - `ROWS`
  - `RANGE`(DEFAULT)
- 범위
  - A: 시작점
    - `CURRENT ROW`
    - `UNBOUNDED PRECEDING`
    - `N PRECEDING`
  - B: 마지막 지점 정의
    - `CURRENT ROW`
    - `UNBOUNDED FOLLOWING`
    - `N FOLLOWING`

##### 🔵 순위 관련 함수
- RANK (순위)
  - `RANK() WITHIN GROUP()`
  - `RANK() OVER()`
  - `DENSE_RANK()`
  - `ROW_NUMBER()`

##### 🔵 LAG, LEAD

##### 🔵 FIRST_VALUE, LAST_VALUE

##### 🔵 NTILE

##### 🔵 비율관련 함수
- `RATIO_TO_REPORT`
- `CUME_DIST`
- `PERCENT_RANK`

#### ✔️ 2-13. Top N 쿼리

##### 🔵 TOP N QUERY

##### 🔵 TOP-N 행 추출방법
- `ROWNUM`
- `RANK`
- `FETCH`
- `TOP N` (SQL Server)

##### 🔵 ROWNUM

##### 🔵 FETCH 절

##### 🔵 TOP N 쿼리

#### ✔️ 2-14. 계층형 질의와 셀프 조인

##### 🔵 계층형 질의

##### 🔵 계층형 질의 조건
- CONNECT BY 절 조건
- WHERE 절 조건
- 계층형 질의 가상 함수
  - `CONNECT_BY_ROOT 컬럼명`
  - `SYS_CONNECT_BY_PATH(컬럼, 구분자)`
  - `ORDER SIBLINGS BY 컬럼`
  - `CONNECT_BY_ISCYCLE`
- NOCYCLE 옵션

#### ✔️ 2-15. PIVOT 절과 UNPIVOT절

##### 🔵 테이터의 구조
- LONG DATA (Tidy data)
- WIDE DATA (Cross table)

##### 🔵 데이터 구조 변경
- PIVOT: LONG ➡️ WIDE
- UNPIVOT: WIDE ➡️ LONG

##### 🔵 PIVOT
##### 🔵 UNPIVOT

#### ✔️ 2-16. 정규 표현식

##### 🔵 정규 표현식

- 정규 표현식 종류

|      |             |             |
|------|-------------|-------------|
| `\d` | `[ab]`      | `\n`        |
| `\D` | `[^ab]`     | `[:alnum:]` |
| `\s` | `[0-9]`     | (생략)        |
| `\S` | `[A-Z]`     | (생략)        |
| `\w` | `[a-z]`     | (생략)        |
| `\W` | `[A-z]`     | (생략)        |
| `\t` | `i+`        | (생략)        |
| `\n` | `i*`        | (생략)        |
| `^`  | `i?`        | (생략)        |
| `$`  | `i{n}`      | (생략)        |
| `\`  | `i{n1, n2}` | (생략)        |
| `\|` | `i{n,}`     | (생략)        |
| `.`  | `()`        | (생략)        |

##### 🔵 REGEXP_REPLACE

##### 🔵 REGEXP_SUBSTR

##### 🔵 REGEXP_INSTR

##### 🔵 REGEXP_LIKE

##### 🔵 REGEXP_COUNT

### ✅ Part 3. `SQL 관리구문`

#### ✔️ 2-17. DML

##### 🔵 DML

##### 🔵 INSERT

##### 🔵 UPDATE

##### 🔵 DELETE

##### 🔵 MERGE

#### ✔️ 2-18. TCL

##### 🔵 TCL

##### 🔵 트랜잭션
- 트랜잭션의 특징
  - 원자성
  - 일관성
  - 고립성
  - 지속성

##### 🔵 COMMIT

##### 🔵 ROLLBACK

#### ✔️ 2-19. DDL

##### 🔵 DDL

##### 🔵 CREATE

##### 🔵 데이터타입
- `CHAR(n)`
- `VARCHAR2(n)`
- `NUMBER(p, s)`
- `DATE`

##### 🔵 ALTER
- 컬럼 추가
- 컬럼(속성) 변경
  - 컬럼 사이즈 변경
  - 데이터 타입 변경
  - DEFAULT 값 변경
- 컬럼 이름 변경
- 컬럼 삭제

##### 🔵 DROP

##### 🔵 TRUNCATE

##### 🔵 DELETE / DROP / TRUNCATE 차이

##### 🔵 제약조건
- `PRIMARY KEY`
- `UNIQUE`
- `NOT NULL`
- `FOREIGN KEY`
- `CHECK`

##### 🔵 FOREIGN KEY 옵션
- `ON DELETE CASCADE`
- `ON DELETE SET NULL`

##### 🔵 기타 오브젝트
- 뷰 (VIEW)
- 시퀀스 (SEQUENCE)
- 시노님 (SYNONYM)

#### ✔️ 2-20. DCL

##### 🔵 DCL

##### 🔵 권한
- 권한 종류
  - 오브젝트 권한
  - 시스템 권한

##### 🔵 GRANT

##### 🔵 REVOKE

##### 🔵 롤(ROLE)

##### 🔵 권한부여 옵션 (중간관리자의 권한)
- `WITH GRANT OPTION`
- `WITH ADMIN OPTION`
